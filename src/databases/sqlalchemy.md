# SQLAlchemy
### Table of content

- [ORM Defenition/Configuration](#def)
    - [Imperative Way](#idef)
        - [Defenition](#idef)
        - [Raw Usage](#rawusage)
        - [Mapping with object](#imapping)
    - [Declarative way](#ddef)
      - Many to Many, One to Many
- [ORM Usage](#orm)
    - [Session basics](#session)
    - [Query](#query)
      - [Select](#select)
        - [Filter](#filter)
        - [Order By & limit](#ordblimit)
        - [Join](#join)
        - [Group By](#groupby)
      - [Add](#add)
      - [Update](#update)
      - [Delete](#delete)
    - [Raw SQL](#rawsql)

-------------------------------------------------
# <a name='def'></a> Defenition
## <a name='idef'></a> Classic way
#### Defenition
```py
# "postgresql+psycopg2://user:@localhost:5432/dbname"
# "sqlite:///dbname.db"
engine = create_engine(SQLALCHEMY_DATABASE_URI, echo=True)
meta = MetaData()


authors = Table(
    "authors",
    meta,
    Column("id", Integer, primary_key=True),
    Column("name", String(250), nullable=False),
)
books = Table(
    "books",
    meta,
    Column("id", Integer, primary_key=True),
    Column("title", String(250), nullable=False),
    Column("author_id", Integer, ForeignKey("authors.id")),
    Column("genre", String(250)),
    Column("price", Integer),
)

meta.create_all(engine)
```

#### <a name='rawusage'></a> Raw Usage
```py
engine = create_engine(SQLALCHEMY_DATABASE_URI)
meta = MetaData(engine)

table = Table("authors", meta, autoload=True)

conn = engine.connect()

# add
query = table.insert().values(
    field="value", fk_id=1, field3="value", field4=1288
)
conn.execute(query)

# select
query = table.select().where(condition)
result = conn.execute(query)

# update
query = table.update().where(condition).values(field="new value")
conn.execute(query)

# delete
query = table.delete().where(table.c.id == 1)
query = sa.delete(table).where(condition)
conn.execute(query)
```
#### <a name='imapping'></a> Mapping
```py
from sqlalchemy.orm import registry

engine = create_engine(SQLALCHEMY_DATABASE_URI)
meta = MetaData(engine)

mapper_registry = registry()

posts = Table("authors", meta, autoload=True)

class Post:
    def __init__(self, title):
        self.title = title

    def __repr__(self):
        return f"<Post: {self.title}>"

mapper_registry.map_imperatively(Post, posts)
```
then create session and work with [default mode](#orm)


-------------------------------------------------
## <a name='ddef'></a> Declarative way
```py
from sqlalchemy import Column, Integer, String, create_engine
from sqlalchemy.orm import declarative_base, relationship

engine = create_engine(SQLALCHEMY_DATABASE_URI)

Base = declarative_base()


class User(Base):
    __tablename__ = "users"

    id = Column(Integer, primary_key=True)
    posts = relationship("Post", backref="user")


post_tags = Table(
    "post_tags",
    Base.metadata,
    Column(
        "post_id",
        ForeignKey("posts.id"),
        primary_key=True,
        ondelete="delete",
    ),
    Column(
        "tag_name",
        ForeignKey("tags.name"),
        primary_key=True,
        ondelete="delete",
    ),
)


class Post(Base):
    __tablename__ = "posts"

    id = Column(Integer, primary_key=True)
    title = Column(String)
    body = Column(Text)
    user_id = Column(Integer, ForeignKey("users.id", ondelete="SET NULL"))
    tags = relationship("Tag", secondary=post_tags, backref="posts")


class Tag(Base):
    __tablename__ = "tags"

    name = Column(String, primary_key=True)
    slug = Column(String, unique=True)


Base.metadata.create_all(engine)
```
More about:
- [Mapping styles](https://docs.sqlalchemy.org/en/14/orm/mapping_styles.html#orm-mapping-styles)
- [Relationships](https://docs.sqlalchemy.org/en/14/orm/basic_relationships.html)
- [Cascades](https://docs.sqlalchemy.org/en/14/orm/cascades.html)

-------------------------------------------------
# <a name='orm'></a> ORM Usage
## <a name='session'></a> Session basic
- Create:
  ```py
  from sqlalchemy import create_engine
  from sqlalchemy.orm.session import sessionmaker

  engine = create_engine("postgresql://scott:tiger@localhost/")

  Session = sessionmaker(bind=engine)

  with Session.begin() as session:
      session.add(some_object)
      session.add(some_other_object)
  ```
  or
  ```py
  from sqlalchemy import create_engine
  from sqlalchemy.orm import Session

  engine = create_engine("postgresql://scott:tiger@localhost/")

  with Session(engine) as session:
      session.add(some_object)
      session.add(some_other_object)
      session.commit()
  ```

- session as object of work
  ```py
  # see uncomitted new entries
  session.new
  # see uncomitted mutated entries
  session.dirty
  # see uncomitted deleted entries
  session.deleted
  ```
- `session.rollback()`:
  ```py
  # verbose version of what a context manager will do
  with Session(engine) as session:
      session.begin()
      try:
          session.add(some_object)
          session.add(some_other_object)
      except:
          session.rollback()
          raise
      else:
          session.commit()
  ```
  or More succinctly
  ```py
  # create session and add objects
  with Session(engine) as session, session.begin():
      session.add(some_object)
      session.add(some_other_object)
  # inner context calls session.commit(), if there were no exceptions
  # outer context calls session.close()
  ```
- [More about session](https://docs.sqlalchemy.org/en/14/orm/session_basics.html)

-------------------------------------------------
## <a name='query'></a> Query
- [More about Query Api](https://docs.sqlalchemy.org/en/14/orm/query.html#the-query-object)
### <a name='select'></a> Select
#### <a name='filter'></a> Filter
- Common syntax
  ```py
  results = session.query(Class).filter(statement).all()
  results = session.query(Class).filter(Class.field == "value").all()
  results = session.query(Class).filter_by(field > 10).all()
  results = session.query(Class.field, Class.field2).all()
  ```
- `like` and `ilike`
  ```py
  results = session.query(Class).filter(Class.field.ilike("%An%"))
  results = session.query(Class).filter(Class.field.like("%An%"))
  ```
- Value in the list
  ```py
  results = session.query(Person).filter(Person.firstname.in_(["valu1", "value2"]))
  ```
- [More about statements for filter](https://docs.sqlalchemy.org/en/14/core/metadata.html#column-table-metadata-api)

#### <a name='ordblimit'></a> Order By & Limit
```py
# order by
q = session.query(Object).order_by(Object.title)

# limit
q = session.query(Object).limit(2)

# union
q = session.query(Object).order_by(Object.title).limit(2)
```

#### <a name='join'></a> Join
```py 
query = session.query(Book, Author).join(Book.author)
```
- [More about Join](https://docs.sqlalchemy.org/en/14/orm/query.html#sqlalchemy.orm.Query.join)

#### <a name='groupby'></a> Group By/Having
```py
q = (
    session.query(Book, Author)
    .filter(Book.author_id == Author.id)
    .filter(Book.price > 1000)
    .group_by(Author.name)
)
```
- [More about Group by](https://docs.sqlalchemy.org/en/14/orm/query.html#sqlalchemy.orm.Query.group_by)

-------------------------------------------------
### <a name='add'></a> Add
```py
user1 = User(name="user1")
user2 = User(name="user2")

session.add(user1)
session.add(user2)
# or session.add_all([user1, user2])

session.commit()  # write changes to the database
```

-------------------------------------------------
### <a name='update'></a> Update
```py
obj = session.query(Obj).filter_by(id=3).one()
if obj:
    obj.column = "new value"
    session.add(obj)
    session.commit()
```

-------------------------------------------------
### <a name='delete'></a> Delete
```py
# mark two objects to be deleted
session.delete(obj1)
session.delete(obj2)

# commit (or flush)
session.commit()
```

-------------------------------------------------
### <a name='rawsql'></a> sql-usage
```py
s = session.execute("SELECT * FROM tablename")
```
