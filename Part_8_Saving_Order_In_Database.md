# Saving Orders and Implementing Flash Messages in Flask

This document outlines the process of saving user orders to the database, providing user feedback via flash messages, and the importance of setting a secret key in Flask applications.

## Saving the Order

When a user submits an order through the order form, the `submit_order` route in Flask processes and saves this order to the database.

### Flask Route for Order Submission

```python
@app.route('/submit_order', methods=['POST'])
def submit_order():
    try:
        product_id = request.form['productId']
        customer_mobile_number = request.form['customerMobileNumber']
        quantity = request.form['quantity']
        total_cost = request.form['totalPrice']

        order_id = insert_order_into_database(customer_mobile_number, total_cost, product_id, quantity)

        flash('Order submitted successfully!', 'success')
        return redirect(url_for('index'))
    except Exception as e:
        flash(f'Error processing your order: {str(e)}', 'error')
        return redirect(url_for('index'))
```

### Process

1. **Form Data Retrieval**: The route retrieves data from the submitted form.
2. **Database Insertion**: It calls `insert_order_into_database` function to save the order and order details.
3. **Success Feedback**: On successful insertion, a success message is flashed.
4. **Error Handling**: In case of an error, an error message is flashed.

### `insert_order_into_database` Function

```python
def insert_order_into_database(customer_mobile_number, total_cost, product_id, quantity):
    cursor = mysql.connection.cursor()
    cursor.execute("INSERT INTO `order` (CustomerMobileNumber, TotalCost) VALUES (%s, %s)", (customer_mobile_number, total_cost))
    order_id = cursor.lastrowid
    cursor.execute("INSERT INTO orderdetails (OrderID, ProductID, Quantity) VALUES (%s, %s, %s)", (order_id, product_id, quantity))
    mysql.connection.commit()
    cursor.close()
    return order_id
```

- This function inserts the order into the `order` table and then inserts the order details into the `orderdetails` table.
- It uses transaction handling with commit to ensure data integrity.

## Implementing Flash Messages

Flash messages provide feedback to the user about the outcome of their actions. In this application, they're used to inform the user whether the order submission was successful or if there was an error.

### Displaying Flash Messages

To display these messages, update your HTML templates where you want the messages to appear:

```html
{% with messages = get_flashed_messages(with_categories=true) %}
  {% if messages %}
    {% for category, message in messages %}
      <div class="alert alert-{{ category }}">{{ message }}</div>
    {% endfor %}
  {% endif %}
{% endwith %}
```

- This snippet iterates over all flashed messages and displays them with an appropriate alert class based on their category ('success' or 'error').

## Setting a Secret Key in `__init__.py`

A secret key in Flask is used to securely sign session data. It is essential for flash message functionality and other session-based features.

### `__init__.py` Setup

```python
from flask import Flask
from flask_mysqldb import MySQL

app = Flask(__name__)
app.secret_key = 'yousecretkey'  # Set a secure and unique secret key

# Database connection
app.config['MYSQL_HOST'] = 'localhost'
app.config['MYSQL_USER'] = 'root'
app.config['MYSQL_PASSWORD'] = ''
app.config['MYSQL_DB'] = 'kiosk_app'

# Initialize MySQL
mysql = MySQL(app)

from application import routes
```

- The `secret_key` is set to a unique and secure value. This key should be kept secret, especially in production environments.

## Conclusion

This implementation covers the order saving process in a Flask application, utilizes flash messages for user feedback, and emphasizes the importance of setting a secret key for session security. These components together enhance the user experience and ensure the application's functionality and security.
