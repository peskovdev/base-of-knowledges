# Flask-Security

Check or Create admin:
```py
from app import app, db, user_datastore
from models import User, Role
app.app_context().push()

is_object_exists = db.session.query(
    db.exists().where(User.email == 'admin@test.com')
).scalar()
print(f'Is admin exists? - {is_object_exists}')
if not is_object_exists:
    user_datastore.create_user(email='admin@test.com', password='admin')
    user_datastore.create_role(name='admin', description='administrator')
    db.session.commit()
    user = User.query.first()
    role = Role.query.first()
    user_datastore.add_role_to_user(user, role)
    db.session.commit()
    print(f'Admin is created!')
```
