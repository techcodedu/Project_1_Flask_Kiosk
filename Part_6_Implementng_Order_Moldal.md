# Modal Order Implementation

This document describes the implementation of the order modal in the Flask application, detailing how the modal is structured in `modal_order.html` and how it's integrated with the `products.html` page.

## `modal_order.html`

The `modal_order.html` file contains the HTML structure for the order modal. This modal is used to display the product details and capture the user's order information.

### Structure

```html
<!-- Order Modal -->
<div class="modal fade" id="orderModal" tabindex="-1" aria-labelledby="orderModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="orderModalLabel">Place Your Order</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
        <form id="orderForm" action="/submit_order" method="post">
          <!-- Hidden Product ID -->
          <input type="hidden" id="productId" name="productId" />
          
          <!-- Product Details -->
          <div class="mb-3">
            <label class="form-label">Product</label>
            <img id="productImage" src="" alt="Product Image" style="width: 100%; max-width: 300px; height: auto" />
            <input type="text" class="form-control mt-2" id="productName" name="productName" readonly />
          </div>

          <!-- Customer Mobile Number -->
          <div class="mb-3">
            <label for="customerMobileNumber" class="form-label">Mobile Number</label>
            <input type="text" class="form-control" id="customerMobileNumber" name="customerMobileNumber" required />
          </div>

          <!-- Quantity Input -->
          <div class="mb-3">
            <label for="quantity" class="form-label">Quantity</label>
            <input type="number" class="form-control" id="quantity" name="quantity" oninput="updateTotalPrice()" min="1" required />
          </div>

          <!-- Total Price Display -->
          <div class="mb-3">
            <label class="form-label">Total Price</label>
            <p id="displayTotalPrice"></p>
            <input type="hidden" id="totalPrice" name="totalPrice" />
          </div>

          <button type="submit" class="btn btn-primary">Submit Order</button>
        </form>
      </div>
    </div>
  </div>
</div>
```

### Explanation

- **Hidden Product ID**: This hidden field stores the `productId` of the selected product, which is essential for order processing.
- **Product Image and Name**: These fields display the selected product's image and name to the user.
- **Customer Mobile Number**: Captures the mobile number of the customer placing the order.
- **Quantity Input**: Allows the user to specify the quantity of the product they wish to order.
- **Total Price**: This section shows the total price of the order. The `displayTotalPrice` paragraph displays the price, while the hidden `totalPrice` input holds the value for form submission.

### Location

The `modal_order.html` is located in the `templates/partials/modal_order.html` directory, allowing for easy inclusion in other templates.

## Integration with `products.html`

In `products.html`, the "Order Now" buttons are updated to pass the product data to the modal.

### Button Data Attributes

```html
<div class="mx-3 mb-3">
  <button
    class="btn btn-primary w-100"
    data-bs-toggle="modal"
    data-bs-target="#orderModal"
    data-product-id="{{ product[0] }}"
    data-product-name="{{ product[1] }}"
    data-product-price="{{ product[2] }}"
    data-product-image="{{ url_for('static', filename=product[4]) }}"
  >
    Order Now
  </button>
</div>
```

### Explanation

- **Data Attributes**: Each button is equipped with data attributes that store the product's ID, name, price, and image URL.
- **Modal Trigger**: Clicking the button triggers the modal and passes this product data to it, ensuring that the modal displays information relevant to the selected product.

## Conclusion

The implementation of `modal_order.html` provides a dynamic and user-friendly way to handle product orders. It allows users to view product details and place orders directly from the `products.html` page, enhancing the overall user experience.
