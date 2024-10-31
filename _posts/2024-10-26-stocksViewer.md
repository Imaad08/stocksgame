---
layout: none
permalink: /stocks/viewer
title: Stocks Viewer
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
      background-color: rgba(240, 146, 53, 0.7);
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
        <div class="stock-item selected" onclick="selectStock('AAPL')">
          <span>AAPL</span>
          <span class="price">$271.19</span>
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
    async function getStockData() {
        const stockSymbol = document.getElementById("searchBar").value;
        document.getElementById("output").textContent = ""; // Clear previous messages
     try {
        const response = await fetch(`http://localhost:8085/api/stocks/${stockSymbol}`);
        const data = await response.json();
        // Extract timestamps and prices
        const timestamps = data?.chart?.result?.[0]?.timestamp;
        const prices = data?.chart?.result?.[0]?.indicators?.quote?.[0]?.close;
        // Check if data exists
        if (timestamps && prices) {
                // Convert timestamps to readable dates
                const labels = timestamps.map(ts => new Date(ts * 1000).toLocaleString());
               displayChart(labels, prices, stockSymbol);
            } else {
                console.error(`Data not found for ${stockSymbol}. Response structure:`, data);
                document.getElementById("output").textContent = `Data not found for ${stockSymbol}.`;
            }
        } catch (error) {
            console.error('Error fetching stock data:', error);
            document.getElementById("output").textContent = "Error fetching stock data. Please try again later.";
        }
}
function displayChart(labels, prices, tickerSymbol) {
    const ctx = document.getElementById('stockChart').getContext('2d');
    // Destroy the old chart if it exists
    if (stockChart) {
        stockChart.destroy();
    }
    // Create a gradient fill
    const gradient = ctx.createLinearGradient(0, 0, 0, 400);
    gradient.addColorStop(0, 'rgba(106, 13, 173, 0.6)'); // Start with purple (rgba)
    gradient.addColorStop(1, 'rgba(255, 255, 255, 0.0)'); // Fade to transparent
    // Determine min and max values for the y-axis based on prices
    const minPrice = Math.min(...prices) * 0.55; // 5% below the minimum price
    const maxPrice = Math.max(...prices) * 1.05; // 5% above the maximum price
    // Create a new chart
    stockChart = new Chart(ctx, {
        type: 'line',
        data: {
            labels: labels,
            datasets: [{
                label: tickerSymbol.toUpperCase(),
                data: prices,
                borderColor: '#001f3f', // Dark blue color for the line
                borderWidth: 2,
                fill: true,
                backgroundColor: gradient,
                spanGaps: true,
                pointRadius: 0, // Remove dots
                tension: 0.1 // Smooth the line
            }]
        },
        options: {
            plugins: {
                legend: {
                    display: false // Hide the legend
                },
                tooltip: {
                    enabled: true, // Enable tooltips
                    mode: 'index', // Tooltip for closest point
                    intersect: false // Show tooltip when hovering close to the line
                }
            },
            responsive: true,
            maintainAspectRatio: false,
            scales: {
                x: {
                    title: { display: true, text: 'Timestamp' },
                    ticks: {
                        callback: function(value) {
                            // Format the timestamp to display only hours
                            return new Date(value).toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
                        }
                    },
                    grid: {
                        display: false // Remove grid lines on x-axis
                    }
                },
                y: {
                    title: { display: true, text: 'Price (USD)' },
                    grid: {
                        display: false // Remove grid lines on y-axis
                    }
                }
            }
        }
    });
}
async function getStockPrice(stock) {
        try {
            const response = await fetch(`http://localhost:8085/api/stocks/${stock}`);
            const data = await response.json();
            console.log(data);
            const price = data?.chart?.result?.[0]?.meta?.regularMarketPrice;
            const outputElement = document.getElementById("output");
            if (price !== undefined) {
                //outputElement.textContent = `The price of ${stock} is: $${price}`;
                return(price)
            } else {
                outputElement.textContent = `Price not found for ${stock}.`;
                console.error(`Price not found for ${stock}. Response structure:`, data);
            }
        } catch (error) {
            console.error('Error fetching stock data:', error);
            document.getElementById("output").textContent = "Error fetching stock data. Please try again later.";
        }
return new Promise((resolve) => {
                setTimeout(() => {
                    resolve(prices[symbol]);
                }, 0); // Simulate network delay
            }); 
      }
      document.addEventListener("DOMContentLoaded", () => {
            updateStockPrices(); // Call the function after DOM is fully loaded
        });
async function updateStockPrices() {
            const stockSymbols = ['Netflix', 'Tesla', 'Amazon', 'Adobe', 'Nvidia', 'Spotify', 'Apple', 'Google', 'Facebook', 'Microsoft'];
            const tickerSymbols = ['NFLX', 'TSLA', 'AMZN', 'ADBE', 'NVDA', 'SPOT', 'AAPL', 'GOOG', 'META', 'MSFT'];
            const tickerPrices = [];
            counter = 0; 
            for (const stock of tickerSymbols) {
                const price = await getStockPrice(stock);
                tickerPrices.push(price)              
                const priceElement = document.getElementById(stockSymbols[counter] + "Price");
                if (priceElement) {
                    priceElement.textContent = `$${price}`;
                } else {
                    console.error(`Element with ID ${stock + "Price"} not found.`);
                }
                counter++;                 
                //console.log(price);
                //console.log(tickerPrices);
                //console.log(priceElement);
                //console.log(counter);
            }
        }
  </script>

</body>
</html>
