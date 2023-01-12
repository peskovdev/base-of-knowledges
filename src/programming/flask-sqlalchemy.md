# Flask, SQLAlchemy

```
db = SQLAlchemy(Flask(__name__))


class Name(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    title = db.Column(db.String(140))
    body = db.Column(db.Text)
    created = db.Column(db.DateTime, default=datetime.now())

    def __init__(self, *args, **kwargs):
        super(Post, self).__init__(*args, **kwargs)

    def __repr__(self):
        return f"<Post id: {self.id}, title: {self.title}>"

initialize all tables
>>> python:
from app import app, db
app.app_context().push()
db.create_all()


```


Get info from database:
```
# Find all
Model.query.all()

# Find by params
Model.query.filter(Model.title.contains('some_argument')).all()
Model.query.filter(Model.title=='some_argument').all()

```

Add objects to db:
```
>>> app.app_context().push()

db.session.add(Model)
db.session.add_all([Models])

db.session.commit()
```


# Flask-Security
create first admin:
```
from app import app, db, user_datastore
from models import User, Role
app.app_context().push()

user_datastore.create_user(email='admin@test.com, password='admin')
user_datastore.create_role(name='admin', description='administrator')
db.session.commit()
user = User.query.first()
role = Role.query.first()
user_datastore.add_role_to_user(user, role)
db.session.commit()
```
