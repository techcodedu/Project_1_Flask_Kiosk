```markdown
## Implementing Layout Inheritance in Flask with Bootstrap

Flask uses the Jinja2 templating engine which allows for template inheritance. We can create a base template called `layout.html` with elements common to all pages, such as the navigation bar and footer. Individual pages will extend this layout to include page-specific content.

### Creating the Base Template: layout.html

First, we set up `layout.html` to define the common structure of your web pages.

```html
<!doctype html>
<html lang="en">
<head>
  <!-- Required meta tags -->
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">

  <!-- Bootstrap CSS -->
  <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css">

  <title>{% block title %}Palenke Market{% endblock %}</title>
</head>
<body>
<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <a class="navbar-brand" href="#">Palenke Market</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>
  <div class="collapse navbar-collapse" id="navbarNav">
    <ul class="navbar-nav">
      <li class="nav-item active">
        <a class="nav-link" href="/">Home</a>
      </li>
      <!-- Additional nav items here -->
    </ul>
  </div>
</nav>

<div class="container">
  {% block content %}
  <!-- Content overridden by child templates -->
  {% endblock %}
</div>

<!-- Optional JavaScript; choose one of the two! -->
<!-- Option 1: jQuery and Bootstrap Bundle (includes Popper) -->
<script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/popper.js@1.7.12/dist/umd/popper.min.js"></script>
<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js"></script>

</body>
</html>
```

### Extending the Base Template in index.html

Next, we create `index.html` which extends `layout.html` and adds its own content.

```html
{% extends 'layout.html' %}

{% block title %}Home - Palenke Market{% endblock %}

{% block content %}
<!-- Your homepage content goes here -->
<h1>Welcome to Palenke Market!</h1>
<!-- Product grid/cards, additional content -->
{% endblock %}
```

### Rendering index.html in Flask

In the `routes.py` file within your Flask application, set up a route to render `index.html`.

```python
from flask import render_template
from app import app

@app.route('/')
def index():
    return render_template('index.html')
```

When the user visits the homepage, Flask will render `index.html`, which in turn extends `layout.html`. This means your navigation and other shared layout elements will be present on the homepage, along with any homepage-specific content.

