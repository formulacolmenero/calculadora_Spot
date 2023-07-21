<!DOCTYPE html>
<html>
<head>
  <title>Product Calculator</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 20px;
    }

    h1 {
      text-align: center;
    }

    div {
      margin-bottom: 10px;
    }

    label {
      display: block;
      margin-bottom: 5px;
    }

    select,
    input[type="number"],
    button {
      padding: 5px;
      font-size: 16px;
    }

    select {
      width: 100%;
    }

    button {
      background-color: #4CAF60;
      color: white;
      cursor: pointer;
    }

    button:hover {
      background-color: #45a049;
    }

    h2 {
      margin-top: 20px;
      text-align: center;
    }

    #total {
      font-size: 24px;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <h1>Product Calculator</h1>

  <div>
    <label for="product">Select Product:</label>
    <select id="product">
      <option value="">-- Select Product --</option>
    </select>
  </div>

  <div>
    <label for="quantity">Quantity:</label>
    <input type="number" id="quantity" min="1" value="1">
  </div>

  <div>
    <button onclick="calculateTotal()">Calculate Total</button>
  </div>

  <div>
    <h2>Total: <span id="total">0</span></h2>
  </div>

  <script>
    var productsData = [
      { code: "P1", name: "Product 1", price: 10.99 },
      { code: "P2", name: "Product 2", price: 19.99 },
      { code: "P3", name: "Product 3", price: 7.99 },
      { code: "P4", name: "Pelon Peloneta", price: 5.99 },
      { code: "P5", name: "Pelon Mini", price: 4.49 },
      { code: "P6", name: "Bubbaloo", price: 2.29 },
      { code: "P7", name: "Winis", price: 3.99 },
      { code: "P8", name: "Diablitos", price: 6.49 },
      { code: "P9", name: "Banderillas", price: 7.99 },
      { code: "P10", name: "Lucas", price: 3.49 },
      { code: "P11", name: "Vero Mix", price: 4.99 },
      { code: "P12", name: "Maruchans", price: 1.99 },
      { code: "P13", name: "frosh dulce", price: 2.99 },
      { code: "P14", name: "Rockaleta Bola", price: 2.79 },
      { code: "P15", name: "Gudupop", price: 3.49 },
      { code: "P16", name: "Rockaleta paleta jr", price: 1.99 },
      { code: "P17", name: "Bombiux mini", price: 1.49 },
      { code: "P18", name: "Gudu Cubo", price: 2.99 },
      { code: "P19", name: "Tix Tix paleta", price: 1.79 },
      { code: "P20", name: "Arizona", price: 2.49 }
      // Add more products to the array as needed
    ];

    function init() {
      fetchProducts();
    }

    function fetchProducts() {
      var productDropdown = document.getElementById('product');

      productsData.forEach(function(product) {
        var option = document.createElement('option');
        option.value = product.code;
        option.textContent = product.name + ' - $' + product.price.toFixed(2);
        productDropdown.appendChild(option);
      });
    }

    function calculateTotal() {
      var product = document.getElementById("product").value;
      var quantity = document.getElementById("quantity").value;

      var price = getProductPrice(product);

      var total = price * quantity;
      document.getElementById("total").textContent = total.toFixed(2);
    }

    function getProductPrice(productCode) {
      var product = productsData.find(function(item) {
        return item.code === productCode;
      });

      if (product) {
        return product.price;
      }

      return 0;
    }
  </script>
</body>
</html>
