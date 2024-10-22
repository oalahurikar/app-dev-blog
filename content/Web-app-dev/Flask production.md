#inprogress

## Productionise the code

>In production, Flask’s built-in server (app.run()) should typically not be used. Instead, you should use a production-ready server like Gunicorn or uWSGI. Here’s how you can change it:

`pip install gunicorn`

 Add wsgi.py file at root level
 
```wsgi.py
from app import create_app
app = create_app() # Create the Flask application instance
```
 
## How to simulate production environment locally

### Option 1:

1. Set FLASK_ENV=production in .env file

When deploying your Flask application with Gunicorn, you should reference the app object exposed in your wsgi.py file.

2. Run the app `gunicorn --bind 0.0.0.0:8080 wsgi:app` => visit http://127.0.0.1:8080

Explanation:

• wsgi:app: This tells Gunicorn to look for the app variable inside the wsgi.py module.

• --bind 0.0.0.0:8080: Binds the server to all interfaces on port 8080.

```
flask run
```

Or

```
gunicorn wsgi:app
```

or

```
gunicorn -c gunicorn.conf.py wsgi:app
```