---
layout: none
permalink: /stocks/viewer
title: Stocks Viewer
---

<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
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
    }
    canvas {
      width: 100% !important; /* Ensures the chart takes full width */
      height: 375px !important; /* Sets the height for the chart */
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
  <div class="stock-item" onclick="selectStock('AAPL')">
    <span>AAPL</span>
    <span class="price" id="AAPLprice"> $271.19</span>
    <span class="change" id="AAPLchange">+1.2%</span>
  </div>
  <div class="stock-item" onclick="selectStock('GOOGL')">
    <span>GOOGL</span>
    <span class="price" id="GOOGprice">$2812.50</span>
    <span class="change" id="GOOGchange">-0.3%</span>
  </div>
  <div class="stock-item" onclick="selectStock('AMZN')">
    <span>AMZN</span>
    <span class="price" id="AMZNprice">$3475.00</span>
    <span class="change" id="AMZNchange">+0.9%</span>
  </div>
  <div class="stock-item" onclick="selectStock('MSFT')">
    <span>MSFT</span>
    <span class="price" id="MSFTprice">$295.60</span>
    <span class="change" id="MSFTchange">+0.5%</span>
  </div>
  <div class="stock-item" onclick="selectStock('TSLA')">
    <span>TSLA</span>
    <span class="price" id="TSLAprice">$890.30</span>
    <span class="change" id="TSLAchange">-1.1%</span>
  </div>
  <div class="stock-item" onclick="selectStock('NFLX')">
    <span>NFLX</span>
    <span class="price" id="NFLXprice">$520.80</span>
    <span class="change" id="NFLXchange">+1.8%</span>
  </div>
  <div class="stock-item" onclick="selectStock('META')">
    <span>FB</span>
    <span class="price" id="METAprice">$339.80</span>
    <span class="change" id="METAchange">-0.2%</span>
  </div>
  <div class="stock-item" onclick="selectStock('NVDA')">
    <span>NVDA</span>
    <span class="price" id="NVDAprice">$230.45</span>
    <span class="change" id="NVDAchange">+2.0%</span>
  </div>
  <div class="stock-item" onclick="selectStock('BABA')">
    <span>BABA</span>
    <span class="price" id="BABAprice">$188.50</span>
    <span class="change" id="BABAchange">+1.1%</span>
  </div>
  <div class="stock-item" onclick="selectStock('V')">
    <span>V</span>
    <span class="price" id="Vprice">$212.30</span>
    <span class="change" id="Vchange">+0.7%</span>
  </div>
  <div class="stock-item" onclick="selectStock('MA')">
    <span>MA</span>
    <span class="price" id="MAprice">$360.25</span>
    <span class="change" id="MAchange">-0.4%</span>
  </div>
  <div class="stock-item" onclick="selectStock('DIS')">
    <span>DIS</span>
    <span class="price" id="DISprice">$181.40</span>
    <span class="change" id="DISchange">+1.5%</span>
  </div>
  <div class="stock-item" onclick="selectStock('ADBE')">
    <span>ADBE</span>
    <span class="price" id="ADBEprice">$651.75</span>
    <span class="change" id="ADBEchange">-0.6%</span>
  </div>
  <div class="stock-item" onclick="selectStock('PYPL')">
    <span>PYPL</span>
    <span class="price" id="PYPLprice">$269.90</span>
    <span class="change" id="PYPLchange">+1.3%</span>
  </div>
  <div class="stock-item" onclick="selectStock('INTC')">
    <span>INTC</span>
    <span class="price" id="INTCprice">$53.20</span>
    <span class="change" id="INTCchange">-0.8%</span>
  </div>
</div>
    </div>
    <!-- Main Content -->
    <div class="main-content">
      <!-- Header -->
      <div class="header">
        <h1 id="stock-name">N/A</h1>
        <p id="stock-symbol">NASDAQ: N/A</p>
      </div>
      <!-- Price Info -->
      <div class="price-info">
        <h2 id="stock-price">N/A</h2>
        <p id="stock-change" class="change positive">N/A</p>
      </div>
      <!-- Key Metrics -->
      <div class="metrics">
    <div class="metric">
        <span>Volume:</span>
        <span id="volume">N/A</span>
    </div>
    <div class="metric">
        <span>Day High:</span>
        <span id="day-high">N/A</span>
    </div>
    <div class="metric">
        <span>52-Week High:</span>
        <span id="year-high">N/A</span>
    </div>
    <div class="metric">
        <span>Day Low:</span>
        <span id="day-low">N/A</span>
    </div>
    <div class="metric">
        <span>52-Week Low:</span>
        <span id="year-low">N/A</span>
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

    let currentlySelectedStock = null; 
    let stockChart;

async function selectStock(stock) {
    if (currentlySelectedStock) {
        currentlySelectedStock.classList.remove("selected");
    }

    const selectedStockElement = document.querySelector(`.stock-item[onclick="selectStock('${stock}')"]`);
    if (selectedStockElement) {
        selectedStockElement.classList.add("selected");
        currentlySelectedStock = selectedStockElement;
    }

    try {
        const response = await fetch(`http://localhost:8085/api/stocks/${stock}`);
        const data = await response.json();

        const stockName = data?.chart?.result?.[0]?.meta?.symbol;
        const stockPrice = data?.chart?.result?.[0]?.meta?.regularMarketPrice;
        const percentChange = await getPercentChange(stock);

        document.getElementById('stock-name').textContent = `${stockName} (${stock})`;
        document.getElementById('stock-symbol').textContent = `NASDAQ: ${stock}`;
        document.getElementById('stock-price').textContent = `$${stockPrice.toFixed(2)}`;

        const changeElement = document.getElementById('stock-change');
        changeElement.textContent = `${percentChange}%`;
        if (percentChange < 0) {
            changeElement.classList.add("negative");
            changeElement.classList.remove("positive");
        } else {
            changeElement.classList.add("positive");
            changeElement.classList.remove("negative");
        }

        const volume = data?.chart?.result?.[0]?.meta?.regularMarketVolume;
        const dayHigh = data?.chart?.result?.[0]?.meta?.regularMarketDayHigh;
        const dayLow = data?.chart?.result?.[0]?.meta?.regularMarketDayLow;
        const yearHigh = data?.chart?.result?.[0]?.meta?.fiftyTwoWeekHigh;
        const yearLow = data?.chart?.result?.[0]?.meta?.fiftyTwoWeekLow;

        document.getElementById('volume').textContent = volume ? volume.toLocaleString() : 'N/A';

        document.getElementById('day-high').textContent = dayHigh ? `$${dayHigh.toFixed(2)}` : 'N/A';
        document.getElementById('year-high').textContent = dayHigh ? `$${yearHigh.toFixed(2)}` : 'N/A';

        document.getElementById('day-low').textContent = dayLow ? `$${dayLow.toFixed(2)}` : 'N/A';
        document.getElementById('year-low').textContent = dayLow ? `$${yearLow.toFixed(2)}` : 'N/A';



        const timestamps = data?.chart?.result?.[0]?.timestamp;
        const prices = data?.chart?.result?.[0]?.indicators?.quote?.[0]?.close;
        if (timestamps && prices) {
            const labels = timestamps.map(ts => new Date(ts * 1000).toLocaleString());
            displayChart(labels, prices, stock);
        }
    } catch (error) {
        console.error('Error fetching stock data:', error);
    }
}



async function getStockData(stockSymbol) {
    try {
        const response = await fetch(`http://localhost:8085/api/stocks/${stockSymbol}`);
        const data = await response.json();

        // Extract relevant information for metrics
        const volume = data?.chart?.result?.[0]?.meta?.regularMarketVolume || "N/A";
        const dayHigh = data?.chart?.result?.[0]?.meta?.regularMarketDayHigh || "N/A";
        const dayLow = data?.chart?.result?.[0]?.meta?.regularMarketDayLow || "N/A";
        const yearHigh = data?.chart?.result?.[0]?.meta?.fiftyTwoWeekHigh || "N/A";
        const yearLow = data?.chart?.result?.[0]?.meta?.fiftyTwoWeekLow || "N/A";

        // Update metric elements
        document.getElementById("volume").textContent = volume;
        document.getElementById("day-high").textContent = `$${dayHigh}`;
        document.getElementById("day-low").textContent = `$${dayLow}`;
        document.getElementById("year-high").textContent = `$${yearHigh}`;
        document.getElementById("year-low").textContent = `$${yearLow}`;

        // Extract timestamps and prices for chart
        const timestamps = data?.chart?.result?.[0]?.timestamp || [];
        const prices = data?.chart?.result?.[0]?.indicators?.quote?.[0]?.close || [];

        if (timestamps.length && prices.length) {
            const labels = timestamps.map(ts => new Date(ts * 1000).toLocaleString());
            displayChart(labels, prices, stockSymbol);
        } else {
            console.error(`Data not found for ${stockSymbol}`);
        }
    } catch (error) {
        console.error('Error fetching stock data:', error);
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
    gradient.addColorStop(0, 'rgba(106, 13, 173, 0.6)'); // Purple start
    gradient.addColorStop(1, 'rgba(255, 255, 255, 0.0)'); // Transparent end

    // Create a new chart
    stockChart = new Chart(ctx, {
        type: 'line',
        data: {
            labels: labels,
            datasets: [{
                label: tickerSymbol.toUpperCase(),
                data: prices,
                borderColor: '#001f3f',
                borderWidth: 2,
                fill: true,
                backgroundColor: gradient,
                spanGaps: true,
                pointRadius: 0,
                tension: 0.1
            }]
        },
        options: {
            responsive: true,
            maintainAspectRatio: false,
            plugins: {
                legend: { display: false },
                tooltip: { mode: 'index', intersect: false }
            },
            scales: {
                x: {
                    title: { display: true, text: 'Timestamp' },
                    ticks: {
                        callback: function(value) {
                            return new Date(value).toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
                        }
                    }
                },
                y: {
                    title: { display: true, text: 'Price (USD)' }
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
            //const outputElement = document.getElementById("output");
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
}
        async function getPercentChange(stock) {
        try {
            const response = await fetch(`http://localhost:8085/api/stocks/${stock}`);
            const data = await response.json();
            console.log(data);
            const newValue = data?.chart?.result?.[0]?.meta?.regularMarketPrice;
            const oldValue = data?.chart?.result?.[0]?.meta?.chartPreviousClose;
            const percentChange = ((newValue - oldValue) / oldValue) * 100;
            //const outputElement = document.getElementById("output");
            if (percentChange !== undefined) {
                //outputElement.textContent = `The price of ${stock} is: $${price}`;
                return percentChange.toFixed(2);
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
            initializeStockSelection();
        });
function initializeStockSelection() {
    selectStock('AAPL'); // Automatically selects and loads data for Apple
}

async function updateStockPrices() {
  const tickerSymbols = [
  'AAPL', 'GOOG', 'AMZN', 'MSFT', 'TSLA', 'NFLX', 'META', 'NVDA', 'BABA', 'V', 'MA', 'DIS', 'ADBE', 'PYPL', 'INTC'];
  const tickerPrices = [];
  let counter = 0;

  for (const stock of tickerSymbols) {
    const price = await getStockPrice(stock);
    const percentChange = await getPercentChange(stock);
    tickerPrices.push(price);

    const priceElement = document.getElementById(`${tickerSymbols[counter]}price`);
    const changeElement = document.getElementById(`${tickerSymbols[counter]}change`);

    if (priceElement) {
      priceElement.textContent = `$${price}`;
    } else {
      console.error(`Element with ID ${stock}price not found.`);
    }

    if (changeElement) {
      changeElement.textContent = `${percentChange}%`;
      
      // Update class based on whether percentChange is positive or negative
      if (percentChange < 0) {
        changeElement.classList.add("negative");
        changeElement.classList.remove("positive");
      } else {
        changeElement.classList.add("positive");
        changeElement.classList.remove("negative");
      }
    } else {
      console.error(`Element with ID ${stock}change not found.`);
    }

    counter++;
  }
}


  </script>

</body>
</html>
