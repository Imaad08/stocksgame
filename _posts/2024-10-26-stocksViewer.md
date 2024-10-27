---
layout: none
permalink: /stocks/viewer
---

<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Stock Viewer</title>
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

    canvas {
      width: 100% !important; /* Ensures the chart takes full width */
      height: 300px !important; /* Sets the height for the chart */
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
      <a href="#">Upgrades</a>
      <a href="#">Profile</a>
    </div>
  </nav>

  <!-- Stock Dashboard -->
  <div class="container">
    <!-- Sidebar -->
    <div class="sidebar">
      <h2>Stocks</h2>
      <div class="stock-list">
        <div class="stock-item selected" onclick="fetchStockData('AAPL')">
          <span>AAPL</span>
          <span class="price">$${data.prices}</span>
          <span class="change">+1.2%</span>
        </div>
        <div class="stock-item" onclick="selectStock('GOOGL')">
          <span>GOOGL</span>
          <span class="price">$2812.50</span>
          <span class="change negative">-0.3%</span>
        </div>
        <div class="stock-item" onclick="selectStock('AMZN')">
          <span>AMZN</span>
          <span class="price">$3475.00</span>
          <span class="change">+0.9%</span>
        </div>
        <div class="stock-item" onclick="selectStock('MSFT')">
          <span>MSFT</span>
          <span class="price">$295.60</span>
          <span class="change">+0.5%</span>
        </div>
        <div class="stock-item" onclick="selectStock('TSLA')">
          <span>TSLA</span>
          <span class="price">$890.30</span>
          <span class="change negative">-1.1%</span>
        </div>
        <div class="stock-item" onclick="selectStock('NFLX')">
          <span>NFLX</span>
          <span class="price">$520.80</span>
          <span class="change">+1.8%</span>
        </div>
        <div class="stock-item" onclick="selectStock('FB')">
          <span>FB</span>
          <span class="price">$339.80</span>
          <span class="change negative">-0.2%</span>
        </div>
        <div class="stock-item" onclick="selectStock('NVDA')">
          <span>NVDA</span>
          <span class="price">$230.45</span>
          <span class="change">+2.0%</span>
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
        <canvas id="stockChart"></canvas>
      </div>
    </div>
  </div>

  <!-- Chart.js Library -->
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

  <script>
    // JavaScript for interactivity
    async function fetchStockData(ticker) {
      const apiKey = '4LVWWBWLNGL62D5G'; // Replace with your Alpha Vantage API key
      const url = `https://www.alphavantage.co/query?function=TIME_SERIES_DAILY&symbol=${ticker}&apikey=${apiKey}`;
      const response = await fetch(url);
      const data = await response.json();

      if (data['Time Series (Daily)']) {
        const stockData = data['Time Series (Daily)'];
        const labels = Object.keys(stockData).reverse(); // Get dates
        const prices = Object.values(stockData).map(day => day['4. close']).reverse(); // Get closing prices
        console.log(prices);
      } else {
        console.error("Error fetching stock data:", data);
      }
    }

    function selectStock(ticker) {
      const stockName = {
        'AAPL': { name: 'Apple Inc.', price: '$174.30', change: '+1.2%', metrics: { marketCap: '$2.8 Trillion', peRatio: '30.5', dividendYield: '0.60%', weekHigh: '$198.23', weekLow: '$124.17' } },
        'GOOGL': { name: 'Alphabet Inc.', price: '$2812.50', change: '-0.3%', metrics: { marketCap: '$1.9 Trillion', peRatio: '28.4', dividendYield: '0%', weekHigh: '$2950.00', weekLow: '$2670.00' } },
        'AMZN': { name: 'Amazon.com Inc.', price: '$3475.00', change: '+0.9%', metrics: { marketCap: '$1.75 Trillion', peRatio: '60.2', dividendYield: '0%', weekHigh: '$3675.00', weekLow: '$3150.00' } },
        'MSFT': { name: 'Microsoft Corp.', price: '$295.60', change: '+0.5%', metrics: { marketCap: '$2.3 Trillion', peRatio: '34.6', dividendYield: '0.70%', weekHigh: '$305.00', weekLow: '$276.00' } },
        'TSLA': { name: 'Tesla Inc.', price: '$890.30', change: '-1.1%', metrics: { marketCap: '$900 Billion', peRatio: '250.0', dividendYield: '0%', weekHigh: '$950.00', weekLow: '$800.00' } },
        'NFLX': { name: 'Netflix Inc.', price: '$520.80', change: '+1.8%', metrics: { marketCap: '$230 Billion', peRatio: '60.1', dividendYield: '0%', weekHigh: '$550.00', weekLow: '$480.00' } },
        'FB': { name: 'Meta Platforms Inc.', price: '$339.80', change: '-0.2%', metrics: { marketCap: '$950 Billion', peRatio: '22.4', dividendYield: '0%', weekHigh: '$370.00', weekLow: '$320.00' } },
        'NVDA': { name: 'NVIDIA Corp.', price: '$230.45', change: '+2.0%', metrics: { marketCap: '$600 Billion', peRatio: '40.0', dividendYield: '0.20%', weekHigh: '$250.00', weekLow: '$200.00' } },
      };

      // Update the stock details
      const selectedStock = stockName[ticker];
      document.getElementById('stock-name').innerText = `${selectedStock.name} (${ticker})`;
      document.getElementById('stock-price').innerText = selectedStock.price;
      document.getElementById('stock-change').innerText = selectedStock.change;

      document.querySelectorAll('.stock-item').forEach(item => item.classList.remove('selected'));
      event.currentTarget.classList.add('selected');

      // Update key metrics
      const metrics = selectedStock.metrics;
      document.querySelector('.metric:nth-child(1) span:nth-child(2)').innerText = metrics.marketCap;
      document.querySelector('.metric:nth-child(2) span:nth-child(2)').innerText = metrics.peRatio;
      document.querySelector('.metric:nth-child(3) span:nth-child(2)').innerText = metrics.dividendYield;
      document.querySelector('.metric:nth-child(4) span:nth-child(2)').innerText = metrics.weekHigh;
      document.querySelector('.metric:nth-child(5) span:nth-child(2)').innerText = metrics.weekLow;

      // Fetch stock data
      fetchStockData(ticker);
    }

    // Initialize with default stock
    fetchStockData('AAPL');
  </script>

</body>
</html>
