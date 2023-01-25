# Flask-SQLAlchemy, Flask-migrate

#### Official Documentation:
- [Flask-SQLAlchemy](https://flask-sqlalchemy.palletsprojects.com/en/3.0.x/quickstart/)
- [Flask-Migrate](https://flask-migrate.readthedocs.io/en/latest/)
-----------------------------------------------------

#### Table of contents:
- [Setup](#setup)
  - [Configure](#configure)
    - [`app.py`](#app)
    - [`models.py`](#models)
  - [Initialize Tables](#init)
    - [With migrations](#withm)
    - [Without migrations](#withoutm)
- [Usage](#usage)
-----------------------------------------------------

# <a name='setup'></a> Setup
## <a name='configure'></a> Flask-SQLAlchemy & Flask-Migrate

- <a name='app'></a> configure the Extensions in `app.py`:
  ```py
  from flask import Flask
  from flask_sqlalchemy import SQLAlchemy
  from flask_migrate import Migrate

  app = Flask(__name__)
  # configure the SQLite database, relative to the app instance folder
  app.config["SQLALCHEMY_DATABASE_URI"] = "sqlite:///project.db"

  db = SQLAlchemy(app)
  migrate = Migrate(app, db)
  ```

- <a name='models'></a> Define Models in `models.py`:
  ```py
  from app import db

  class Name(db.Model):
      id = db.Column(db.Integer, primary_key=True)
      title = db.Column(db.String(140))
      body = db.Column(db.Text)
      created = db.Column(db.DateTime, default=datetime.now())

      def __init__(self, *args, **kwargs):
          super(Post, self).__init__(*args, **kwargs)

      def __repr__(self):
          return f"<Post id: {self.id}, title: {self.title}>"


  # ... and other
  ```

## <a name='init'></a> Initialize tables:
### <a name='withm'></a> With migrations
1) `flask db init`
2) Uncomment & Change folowing content in `env.py`:
  ```py
  # add your model's MetaData object here
  # for 'autogenerate' support
  from models import *
  # target_metadata = mymodel.Base.metadata
  ```
3) `flask db migrate -m "Create user model"`
4) `flask db upgrade`

### <a name='withoutm'></a> Without migrations
```py
>>> python:
from app import app, db

app.app_context().push()
db.create_all()

# or
# with app.app_context():
#     db.create_all()
```

## <a name='usage'></a> Usage
Apart from pagination or get_or_404(), use as in normal SQLAlchemy

- Get info from database
  ```py
  # find all
  Model.query.all()

  # Find by params
  Model.query.filter(Model.title.contains("some_argument")).all()
  Model.query.filter(Model.body.ilike("%search query%")).all()
  Model.query.filter(Model.title=="Name of blabla").all()
  ```

- Add objects to db:
  ```py
  >>> app.app_context().push()

  db.session.add(Model)
  db.session.add_all([Models])

  db.session.commit()
  ```
