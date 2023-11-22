# Restaurant-billing-system-using-javascript
# Html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="styles.css">
    <title>Restaurant Billing System</title>
</head>
<body>
    <div class="container">
        <h1>Restaurant Billing System</h1>
        <div id="menu">
            <div class="menu-item" data-name="Burger" data-price="10.99">
                <h2>Burger</h2>
                <p>$10.99</p>
                <button onclick="addItem('Burger', 10.99)">Add to Order</button>
            </div>

            <div class="menu-item" data-name="Pizza" data-price="12.99">
                <h2>Pizza</h2>
                <p>$12.99</p>
                <button onclick="addItem('Pizza', 12.99)">Add to Order</button>
            </div>

            <!-- Add more menu items as needed -->
        </div>

        <div id="order">
            <h2>Order Summary</h2>
            <ul id="orderItems"></ul>
            <p>Total: $<span id="totalAmount">0.00</span></p>
            <button onclick="generateBill()">Generate Bill</button>
        </div>
    </div>

    <script src="script.js"></script>
</body>
</html>

#style.css
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    background-color: #f0f0f0;
}

.container {
    max-width: 800px;
    margin: 50px auto;
    background-color: #fff;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

#menu {
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;
}

.menu-item {
    border: 1px solid #ddd;
    border-radius: 4px;
    padding: 15px;
    margin: 10px;
    text-align: center;
}

button {
    background-color: #4caf50;
    color: #fff;
    padding: 10px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}
#button:hover {
    background-color: #45a049;
}

#order {
    margin-top: 20px;
}

#orderItems {
    list-style-type: none;
    padding: 0;
}

li {
    margin-bottom: 5px;
}
#totalAmount {
    font-weight: bold;
}

# Script.js
let orderItems = [];

function addItem(name, price) {
    const item = { name, price };
    orderItems.push(item);
    updateOrder();
}

function updateOrder() {
    const orderItemsList = document.getElementById('orderItems');
    const totalAmountElement = document.getElementById('totalAmount');

    // Clear existing order items
    orderItemsList.innerHTML = '';

    // Populate the order items
    orderItems.forEach(item => {
        const listItem = document.createElement('li');
        listItem.textContent = `${item.name} - $${item.price.toFixed(2)}`;
        orderItemsList.appendChild(listItem);
    });

    // Calculate and display the total amount
    const totalAmount = orderItems.reduce((total, item) => total + item.price, 0);
    totalAmountElement.textContent = totalAmount.toFixed(2);
}

function generateBill() {
    // In a real-world scenario, you would likely process the bill on the server.
    alert('Bill generated! Total amount: $' + getTotalAmount());
    resetOrder();
}

function getTotalAmount() {
    return orderItems.reduce((total, item) => total + item.price, 0).toFixed(2);
}

function resetOrder() {
    orderItems = [];
    updateOrder();
}
