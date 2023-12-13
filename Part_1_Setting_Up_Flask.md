## Setting Up Flask

```markdown
## Step 2: Set Up Flask Application

Now that you have your virtual environment and project structure ready, it's time to set up the Flask application. Follow these detailed steps to get your Flask app up and running:

### Initialize the Flask App

Inside the `app` directory, you will find the `__init__.py` file. This is where we will initialize our Flask application.

1. Open the `__init__.py` file in your code editor.

2. Write the following Python code to initialize the Flask app:

```python
from flask import Flask

app = Flask(__name__)

# If you have additional configurations, you can set them here
# For example, to enable debug mode, you can add:
# app.config['DEBUG'] = True

from app import routes
```
### Create Routes

The `routes.py` file is where you will define the routes for your application. These are the URLs that the app will respond to.

1. Open the `routes.py` file.

2. Start with a simple route for the home page:

```python
from app import app
from flask import render_template

@app.route('/')
def index():
    return render_template('index.html')
```

This code defines a route for the root URL (`'/'`). When this URL is visited, the `index()` function will be called, which will render and return the `index.html` template.

### Start the Flask Development Server

To see if your application is set up correctly, you can start the Flask development server.

1. Open the `run.py` file at the root of your project.

2. Add the following code to `run.py`:

```python
from app import app

if __name__ == '__main__':
    app.run(debug=True)
```

3. Save the file.

4. Go back to your command prompt or terminal.

5. Make sure your virtual environment is activated.

6. Start the server with the following command:

```bash
python run.py
```

7. Open a web browser and navigate to `http://127.0.0.1:5000/`. You should see your `index.html` page rendered.

