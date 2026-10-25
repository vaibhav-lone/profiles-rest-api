# Profiles REST API

A beginner-friendly Django REST Framework project that demonstrates how to build a custom user authentication model, create REST API endpoints, and use Django REST Framework views and viewsets.

## Overview

This project is a simple API application built as part of a Django REST Framework learning exercise. It focuses on the core concepts of creating a custom `UserProfile` model, configuring Django authentication, and exposing example API endpoints that return greeting messages.

The project includes:
- a custom user model using `AbstractBaseUser`
- password hashing and user creation logic
- DRF `APIView` example
- DRF `ViewSet` example
- router-based URL configuration
- SQLite database configuration for local development
- a Vagrant setup for a reproducible Ubuntu development environment

## Tech Stack

- Python 3
- Django 2.2
- Django REST Framework 3.9.2
- SQLite
- Vagrant

## Project Structure

```text
profiles-rest-api/
├── LICENSE
├── README.md
├── Vagrantfile
├── hello_world.py
├── manage.py
├── requirements.txt
├── profiles_api/
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── migrations/
│   │   ├── __init__.py
│   │   └── 0001_initial.py
│   ├── models.py
│   ├── serializers.py
│   ├── tests.py
│   ├── urls.py
│   └── views.py
├── profiles_project/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
└── db.sqlite3   # created after migrations
```

## Features

### Custom User Model

The app defines a custom `UserProfile` model in `profiles_api/models.py`.

This model includes:
- email address as the unique login identifier
- name field
- `is_active` and `is_staff` flags
- custom manager logic for creating normal users and superusers

The project configures Django to use this custom model via:

```python
AUTH_USER_MODEL = 'profiles_api.UserProfile'
```

### Serializer Example

A serializer is defined in `profiles_api/serializers.py`:

```python
class HelloSerializers(serializers.Serializer):
    name = serializers.CharField(max_length=10)
```

This validates a `name` field used by the example API endpoints.

### APIView Example

The `HelloApiView` class in `profiles_api/views.py` demonstrates a typical DRF API class.

It supports:
- `GET`
- `POST`
- `PUT`
- `PATCH`
- `DELETE`

The `GET` method returns a list of features describing `APIView`, and the `POST` method accepts a `name` value and returns a message like `Hello Vaibhav!`.

### ViewSet Example

A second example uses `HelloViewSet`, which is based on `viewsets.ViewSet`.

This demonstrates:
- router registration
- automatically mapped routes
- standard REST-style actions such as `list`, `create`, `retrieve`, and `update`

## API Routes

The project routes are included in `profiles_project/urls.py` and `profiles_api/urls.py`.

### Available endpoints

```text
/api/hello-view/
/api/hello-viewset/
/admin/
```

## Running the Project

### 1. Create a virtual environment

```bash
python -m venv venv
```

Activate it:

Windows:
```bash
venv\Scripts\activate
```

macOS/Linux:
```bash
source venv/bin/activate
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Apply database migrations

```bash
python manage.py migrate
```

### 4. Start the development server

```bash
python manage.py runserver
```

Then open:

```text
http://127.0.0.1:8000/
```

## Example API Calls

### Get hello APIView data

```bash
curl http://127.0.0.1:8000/api/hello-view/
```

### Post a greeting

```bash
curl -X POST http://127.0.0.1:8000/api/hello-view/ \
  -H "Content-Type: application/json" \
  -d '{"name": "Vaibhav"}'
```

Example response:

```json
{
  "message": "Hello Vaibhav!"
}
```

### Get hello ViewSet data

```bash
curl http://127.0.0.1:8000/api/hello-viewset/
```

## Django Admin

The app registers the custom user model for admin access in `profiles_api/admin.py`:

```python
admin.site.register(models.UserProfile)
```

Create a superuser with:

```bash
python manage.py createsuperuser
```

Then access:

```text
http://127.0.0.1:8000/admin/
```

## Database Configuration

The app uses SQLite by default:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}
```

This is suitable for local learning and development.

## Vagrant Environment

A `Vagrantfile` is included to support a reproducible development setup using Ubuntu. It forwards port 8000 from the VM to the host machine and installs Python virtual environment utilities.

This is useful when working in a controlled local environment or when replicating setup steps on a VM.

## Notes

This project is intentionally simple and educational. It is designed to show how Django and Django REST Framework work together in a practical example without introducing extra complexity. It is a good starting point for learning how to build APIs, register routes, and work with custom user models.

## License

This project is distributed under the MIT-style open-source license included in the repository. See the `LICENSE` file for full details.
