# Testing Database Connection in Flask

This guide provides steps to test the database connection in a Flask application using Flask-MySQLdb, assuming Flask-MySQLdb is already installed and configured.

## Configuration

Before testing, ensure that your database configuration is correctly set in your Flask application's `__init__.py` file.

### Example Database Configuration in `__init__.py`

```python
# __init__.py

from flask import Flask
from flask_mysqldb import MySQL

app = Flask(__name__)

# Configure database
app.config['MYSQL_HOST'] = 'localhost'
app.config['MYSQL_USER'] = 'root'
app.config['MYSQL_PASSWORD'] = ''
app.config['MYSQL_DB'] = 'db_kiosk'

# Initialize MySQL
mysql = MySQL(app)

from app import routes
```

## Creating a Test Route

Add a simple route in your `routes.py` to test the database connection. This route will attempt to connect to the database and, if successful, print a confirmation message to the terminal.

### Test Route in `routes.py`

```python
# routes.py

from app import app, mysql
from flask import jsonify

@app.route('/test_db')
def test_db():
    try:
        cursor = mysql.connection.cursor()
        cursor.close()
        print("Database connection successful.")
        return jsonify({'message': 'Database connection successful.'})
    except Exception as e:
        print("Error connecting to the database:", str(e))
        return jsonify({'error': str(e)})
```

## Testing the Connection

To test the database connection:

1. **Run the Flask Application**:
    - Execute `python run.py` to start your Flask application.

2. **Visit the Test Route**:
    - Open a web browser and go to `http://127.0.0.1:5000/test_db`.
    - This should trigger the database connection test.

3. **Check the Terminal Output**:
    - Look at the terminal where your Flask app is running.
    - A successful connection will print "Database connection successful."
    - In case of an error, the error message will be printed.
