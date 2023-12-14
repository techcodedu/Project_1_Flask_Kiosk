# Interactive Image Display with Modals in Flask

This guide demonstrates how to create an interactive feature in a Flask application where clicking on product images displays them in a Bootstrap modal. We'll use a separate partial template for the modal to keep our code organized.

## Prerequisites

- A Flask application with a configured products page.
- Bootstrap integrated into the application for modal functionality.

## Step 1: Create the Modal Partial

Create a separate HTML file for the modal in a `partials` folder within the `templates` directory.

### Example: Modal Partial in `partials/image_modal.html`

```html
<!-- templates/partials/image_modal.html -->

<!-- Bootstrap Modal -->
<div class="modal fade" id="productModal" tabindex="-1" aria-labelledby="productModalLabel" aria-hidden="true">
  <div class="modal-dialog modal-lg">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="productModalLabel">Product Image</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
        <img id="modalImg" src="" class="img-fluid" alt="Product">
      </div>
    </div>
  </div>
</div>
```

## Step 2: Include the Modal in `product.html`

Use Jinja2's `{% include %}` directive in `product.html` to include the modal partial.

### Example: Including Modal in `product.html`

```html
<!-- product.html -->

{% extends 'layout.html' %}

{% block content %}
<!-- Product cards and other content -->

<!-- Include the image modal from the partials folder -->
{% include 'partials/image_modal.html' %}
{% endblock %}
```

## Step 3: Set Up Product Images to Trigger the Modal

In the product display loop within `product.html`, configure each image to trigger the modal on click.

### Example: Product Images in `product.html`

```html
<div class="row">
    {% for product in products %}
    <div class="col-md-3 col-sm-6 mb-4">
        <div class="card">
            <img src="{{ url_for('static', filename='images/' + product.PhotoURL) }}" 
                 class="card-img-top img-fluid" 
                 alt="{{ product.ProductName }}" 
                 data-bs-toggle="modal" 
                 data-bs-target="#productModal" 
                 onclick="updateModalImage(this.src)">
        </div>
    </div>
    {% endfor %}
</div>
```

## Step 4: Add JavaScript for Updating Modal Image

Include a JavaScript function in `product.html` that updates the modal's image source when an image is clicked.

### Example: JavaScript Function in `product.html`

```html
<script>
function updateModalImage(imageSrc) {
    document.getElementById('modalImg').src = imageSrc;
}
</script>
```

## Step 5: Test the Functionality

Run your Flask application and navigate to the products page. Clicking on an image should open the modal displaying the clicked image.

## Conclusion

This implementation provides an interactive way for users to view larger versions of product images using a modal. The use of a separate partial for the modal helps keep the templates organized and promotes reusability.

