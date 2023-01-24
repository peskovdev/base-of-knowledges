# Migrations with alembic & SQLAlchemy
## Setup
1) Add packages:
  ```sh
  poetry add sqlalchemy alembic
  ```
2) Set SQLAlchemy models
  ```py
  from datetime import datetime

  import sqlalchemy as sa
  from sqlalchemy.orm import declarative_base

  Base = declarative_base()


  class User(Base):
      __tablename__ = 'user'

      id = sa.Column(sa.Integer, primary_key=True)
      nick = sa.Column(sa.String, nullable=False, unique=True)
  ```
3) Init alembic files
  ```sh
  alembic init migrations
  ```
4) Edit `alembic.ini`:
```ini
# database uri for connection
sqlalchemy.url = sqlite:///models.db
```

5) Uncomment & change folowing content in `env.py`:
```py
# add your model's MetaData object here
# for 'autogenerate' support
from models import Base
target_metadata = Base.metadata
```

## Usage
1) Create migrations
```sh
alembic rebision --autogenerate -m "Create User model"
```
2) Upgrade
```sh
alembic upgrade heads
```
