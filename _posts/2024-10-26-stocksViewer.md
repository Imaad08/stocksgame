---
layout: none
permalink: /stocks/viewer
---

<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Apple Stocks UI with Navbar</title>
  <style>
    /* CSS Styles */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
      background-color: #f0f2f5;
      color: #333;
    }

    /* Navigation Bar */
    .navbar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 10px 20px;
      background-color: #001f3f; /* Dark blue background */
      color: #fff;
    }
    .navbar .logo {
      font-size: 24px;
      font-weight: bold;
      letter-spacing: 2px;
    }
    .navbar .nav-buttons {
      display: flex;
      gap: 20px;
    }
    .navbar .nav-buttons a {
      color: #fff;
      text-decoration: none;
      font-size: 16px;
      padding: 8px 16px;
      border-radius: 4px;
      transition: background-color 0.3s;
    }
    .navbar .nav-buttons a:hover {
      background-color: #ff8c00; /* Orange hover effect */
    }

    .container {
      display: flex;
      height: 92vh; /* Adjusted height for navbar */
    }

    .sidebar {
      width: 20%;
      background-color: #ffffff;
      border-right: 1px solid #ddd;
      padding: 20px;
    }

    .sidebar h2 {
      font-size: 1.2em;
      margin-bottom: 20px;
    }

    .stock-list {
      display: flex;
      flex-direction: column;
    }

    .stock-item {
      display: flex;
      justify-content: space-between;
      padding: 10px;
      margin-bottom: 10px;
      border-radius: 4px;
      cursor: pointer;
    }

    .stock-item.selected {
      background-color: #e0f7fa;
    }

    .price {
      font-weight: bold;
    }

    .change {
      color: #388e3c; /* Green for positive change */
    }

    .change.negative {
      color: #d32f2f; /* Red for negative change */
    }

    .main-content {
      width: 80%;
      padding: 20px;
    }

    .header h1 {
      font-size: 2em;
      font-weight: bold;
    }

    .header p {
      color: #777;
      margin-bottom: 20px;
    }

    .price-info h2 {
      font-size: 2.5em;
      font-weight: bold;
    }

    .change.positive {
      color: #388e3c;
    }

    .change.negative {
      color: #d32f2f;
    }

    .metrics {
      display: flex;
      gap: 15px;
      margin: 20px 0;
    }

    .metric {
      background-color: #ffffff;
      border: 1px solid #ddd;
      padding: 15px;
      border-radius: 4px;
      text-align: center;
      flex: 1;
    }

    .chart {
      background-color: #ffffff;
      padding: 15px;
      border-radius: 8px;
      margin-top: 20px;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 200px;
    }
  </style>
</head>
<body>

  <!-- Navigation Bar -->
  <nav class="navbar">
    <div class="logo">NITD</div>
    <div class="nav-buttons">
      <a href="{{site.baseurl}}/stocks/home">Home</a>
      <a href="{{site.baseurl}}/stocks/viewer">Stocks</a>
      <a href="#">Portfolio</a>
      <a href="#">Upgrades</a> <!-- Added "Upgrades" button -->
      <a href="#">Profile</a>
    </div>
  </nav>

  <!-- Stock Dashboard -->
  <div class="container">
    <!-- Sidebar -->
    <div class="sidebar">
      <h2>Stocks</h2>
      <div class="stock-list">
        <div class="stock-item selected" onclick="selectStock('AAPL', 174.30, '+1.2%')">
          <span>AAPL</span>
          <span class="price">$174.30</span>
          <span class="change">+1.2%</span>
        </div>
        <div class="stock-item" onclick="selectStock('GOOGL', 2812.50, '-0.3%')">
          <span>GOOGL</span>
          <span class="price">$2812.50</span>
          <span class="change negative">-0.3%</span>
        </div>
        <div class="stock-item" onclick="selectStock('AMZN', 3475.00, '+0.9%')">
          <span>AMZN</span>
          <span class="price">$3475.00</span>
          <span class="change">+0.9%</span>
        </div>
        <div class="stock-item" onclick="selectStock('AMZN', 3475.00, '+0.9%')">
          <span>AMZN</span>
          <span class="price">$3475.00</span>
          <span class="change">+0.9%</span>
        </div>
        <div class="stock-item" onclick="selectStock('AMZN', 3475.00, '+0.9%')">
          <span>AMZN</span>
          <span class="price">$3475.00</span>
          <span class="change">+0.9%</span>
        </div>
        <div class="stock-item" onclick="selectStock('AMZN', 3475.00, '+0.9%')">
          <span>AMZN</span>
          <span class="price">$3475.00</span>
          <span class="change">+0.9%</span>
        </div>
        <div class="stock-item" onclick="selectStock('AMZN', 3475.00, '+0.9%')">
          <span>AMZN</span>
          <span class="price">$3475.00</span>
          <span class="change">+0.9%</span>
        </div>
        <div class="stock-item" onclick="selectStock('AMZN', 3475.00, '+0.9%')">
          <span>AMZN</span>
          <span class="price">$3475.00</span>
          <span class="change">+0.9%</span>
        </div>
        <div class="stock-item" onclick="selectStock('AMZN', 3475.00, '+0.9%')">
          <span>AMZN</span>
          <span class="price">$3475.00</span>
          <span class="change">+0.9%</span>
        </div>
        <div class="stock-item" onclick="selectStock('AMZN', 3475.00, '+0.9%')">
          <span>AMZN</span>
          <span class="price">$3475.00</span>
          <span class="change">+0.9%</span>
        </div>
        <div class="stock-item" onclick="selectStock('AMZN', 3475.00, '+0.9%')">
          <span>AMZN</span>
          <span class="price">$3475.00</span>
          <span class="change">+0.9%</span>
        </div>
        <div class="stock-item" onclick="selectStock('AMZN', 3475.00, '+0.9%')">
          <span>AMZN</span>
          <span class="price">$3475.00</span>
          <span class="change">+0.9%</span>
        </div>
        <div class="stock-item" onclick="selectStock('AMZN', 3475.00, '+0.9%')">
          <span>AMZN</span>
          <span class="price">$3475.00</span>
          <span class="change">+0.9%</span>
        </div>
        <div class="stock-item" onclick="selectStock('AMZN', 3475.00, '+0.9%')">
          <span>AMZN</span>
          <span class="price">$3475.00</span>
          <span class="change">+0.9%</span>
        </div>
        <div class="stock-item" onclick="selectStock('AMZN', 3475.00, '+0.9%')">
          <span>AMZN</span>
          <span class="price">$3475.00</span>
          <span class="change">+0.9%</span>
        </div>
      </div>
    </div>

    <!-- Main Content -->
    <div class="main-content">
      <!-- Header -->
      <div class="header">
        <h1 id="stock-name">Apple Inc. (AAPL)</h1>
        <p id="stock-symbol">NASDAQ: AAPL</p>
      </div>

      <!-- Price Info -->
      <div class="price-info">
        <h2 id="stock-price">$174.30</h2>
        <p id="stock-change" class="change positive">+1.2%</p>
      </div>

      <!-- Key Metrics -->
      <div class="metrics">
        <div class="metric">
          <span>Market Cap</span>
          <span>$2.8 Trillion</span>
        </div>
        <div class="metric">
          <span>P/E Ratio</span>
          <span>30.5</span>
        </div>
        <div class="metric">
          <span>Dividend Yield</span>
          <span>0.60%</span>
        </div>
        <div class="metric">
          <span>52-Week High</span>
          <span>$198.23</span>
        </div>
        <div class="metric">
          <span>52-Week Low</span>
          <span>$124.17</span>
        </div>
      </div>

      <!-- Stock Chart -->
      <div class="chart">
        <span>[Graph Placeholder]</span>
      </div>
    </div>
  </div>

  <script>
    // JavaScript for interactivity
    function selectStock(name, price, change) {
      document.querySelectorAll('.stock-item').forEach(item => {
        item.classList.remove('selected');
      });
      event.currentTarget.classList.add('selected');
      
      document.getElementById('stock-name').textContent = `${name} Inc. (${name})`;
      document.getElementById('stock-symbol').textContent = `NASDAQ: ${name}`;
      document.getElementById('stock-price').textContent = `$${price}`;
      document.getElementById('stock-change').textContent = change;

      const changeElement = document.getElementById('stock-change');
      if (change.startsWith('+')) {
        changeElement.classList.add('positive');
        changeElement.classList.remove('negative');
      } else {
        changeElement.classList.add('negative');
        changeElement.classList.remove('positive');
      }
    }
  </script>
</body>
</html>
