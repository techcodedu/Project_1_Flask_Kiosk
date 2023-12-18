# JavaScript Implementation for Modal Order Form

This document outlines the JavaScript implementation for handling the order modal in the Flask application. The script is divided into three main parts: initializing the modal with product data, updating the total price, and resetting the modal.

## 1. Initializing the Modal with Product Data

When a user clicks the "Order Now" button, the modal is initialized with the corresponding product's data. This is handled by an event listener attached to the modal.

### Code

```javascript
let orderModal = document.getElementById("orderModal");
orderModal.addEventListener("show.bs.modal", function (event) {
  resetModal(); // Reset the modal's content to default values

  let button = event.relatedTarget; // Button that triggered the modal

  // Extract info from data-* attributes
  let productId = button.getAttribute("data-product-id");
  let productName = button.getAttribute("data-product-name");
  let productPrice = button.getAttribute("data-product-price");
  let productImage = button.getAttribute("data-product-image");

  // Update the modal's content with product information
  document.getElementById("productId").value = productId;
  document.getElementById("productName").value = productName;
  document.getElementById("productImage").src = productImage;
  currentProductPrice = parseFloat(productPrice);

  updateTotalPrice(); // Update total price based on default quantity
});
```

### Explanation

- The event listener listens for the `show.bs.modal` event, which is triggered when the modal is about to be shown.
- `event.relatedTarget` is used to get the button that triggered the modal.
- The product's details (ID, name, price, image) are extracted from the button's data attributes.
- These details are then used to update the corresponding fields in the modal.

## 2. Function to Update the Total Price

The total price is dynamically calculated based on the quantity entered by the user. This calculation is handled by the `updateTotalPrice` function.

### Code

```javascript
function updateTotalPrice() {
  let quantity = parseFloat(document.getElementById("quantity").value) || 0;
  let totalPrice = currentProductPrice * quantity;
  document.getElementById("displayTotalPrice").textContent = totalPrice.toFixed(2);
  document.getElementById("totalPrice").value = totalPrice.toFixed(2);
}
```

### Explanation

- This function is triggered whenever the quantity input changes.
- It calculates the total price based on the `currentProductPrice` (set when the modal is initialized) and the entered quantity.
- The calculated total price is displayed to the user and also stored in a hidden input for form submission.

## 3. Function to Reset the Modal

The `resetModal` function is used to reset the modal's fields to their default values. This ensures that each time the modal is opened, it starts in a clean state.

### Code

```javascript
function resetModal() {
  document.getElementById("productId").value = "";
  document.getElementById("productName").value = "";
  document.getElementById("productImage").src = "";
  document.getElementById("quantity").value = "";
  document.getElementById("displayTotalPrice").textContent = "0.00";
  document.getElementById("totalPrice").value = "0.00";
}
```

### Explanation

- Resets all the modal inputs and image to their default state.
- Ensures that when the modal is reopened, no residual data from the previous usage remains.

## Conclusion

This JavaScript implementation effectively manages the product order modal in the application, providing dynamic interaction for calculating and displaying total prices and ensuring a consistent user experience with modal resets.
