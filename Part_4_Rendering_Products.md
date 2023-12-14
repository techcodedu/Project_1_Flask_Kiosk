# Rendering Products on the Products Page in Flask

This guide outlines the steps to display products from a MySQL database on the products page in a Flask application.

## Prerequisites

- Flask application set up with Flask-MySQLdb for database access.
- A MySQL database with a `product` table.

## Step 1: Create a Route for the Products Page

In `routes.py`, define a route `/products` to fetch product data from the database and render it using a template.

### Example: Fetching Products from Database

```python
# routes.py

from app import app, mysql
from flask import render_template

@app.route('/products')
def products():
    cursor = mysql.connection.cursor()
    cursor.execute("SELECT * FROM product")  # Replace 'product' with your actual table name
    product_data = cursor.fetchall()
    cursor.close()
    return render_template('product.html', products=product_data)
```

## Step 2: Design the Products Template

Create a `product.html` template that extends from your base layout and displays the products using Bootstrap's grid system.

### Example: Displaying Products in `product.html`

```html
<!-- product.html -->

{% extends 'layout.html' %}

{% block title %}Product Page{% endblock %}

{% block content %}
<!-- Your homepage content goes here -->
<h1>Products</h1>
    <div class="row">
        {% for product in products %}
        <div class="col-4">
            <div class="card">
                <img src="{{ url_for('static', filename= product[4]) }}" class="card-img-top img-fluid">
                <div class="card-body">
                    <h5 class="card-title">{{ product[1] }}</h5>
                    <p class="card-text">{{ product[2] }}</p>
                    <!-- Additional product details here -->
                </div>
            </div>
        </div>
        {% endfor %}
    </div>

<!-- Here you can add more HTML elements such as cards, buttons, etc. -->
{% endblock %}
```

## Step 3: Run and Test the Application

Run your Flask application and navigate to `http://127.0.0.1:5000/products` to view the products page.

```bash
python run.py
```

## Conclusion

This setup allows your Flask application to display products from the database on a responsive products page. The use of Bootstrap's grid system and `img-fluid` class ensures that the product images are responsive and the layout adjusts for different screen sizes.

