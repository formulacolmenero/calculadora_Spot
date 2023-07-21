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
      background-color: #4CAF50;
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
      <!-- Product options will be dynamically added here -->
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

  <script src="https://apis.google.com/js/api.js"></script>
  <script>
    function init() {
      gapi.load('client', loadClient);
    }

    function loadClient() {
      gapi.client.init({
        apiKey: 'AIzaSyA137zKreKkC5DFoOxuvUgUs5w3lds9_yo',
        discoveryDocs: ['https://sheets.googleapis.com/$discovery/rest?version=v4'],
      }).then(function() {
        fetchProducts();
      });
    }

    function fetchProducts() {
      gapi.client.sheets.spreadsheets.values.get({
        spreadsheetId: 1o0OzxTuS5ikx7nu9IjcXFRVSPt2HyEB3j305giy1BNE,
        range: 'Products!b3:f',
      }).then(function(response) {
        var products = response.result.values;
        var productDropdown = document.getElementById('product');

        products.forEach(function(product) {
          var productCode = product[0];
          var productName = product[1];
          var price = parseFloat(product[2]);

          var option = document.createElement('option');
          option.value = productCode;
          option.textContent = productName + ' - $' + price.toFixed(2);
          productDropdown.appendChild(option);
        });
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
      switch (productCode) {
        case "P1":
          return 10.99;
        case "P2":
          return 19.99;
        case "P3":
          return 7.99;
        default:
          return 0;
      }
    }
  </script>
</body>
</html>
