---
layout: none
permalink: /stocks/portfolio
title: Stocks Portfolio
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Stock Portfolio</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            margin: 0;
            padding: 0;
        }
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
        .portfolio {
            padding: 20px;
            display: flex;
            gap: 40px;
        }
        .portfolio-content {
            width: 70%;
        }
        .summary-section, .watchlist, .portfolio-stocks {
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            margin-bottom: 20px;
        }
        .summary-section h2, .watchlist h3, .portfolio-stocks h3 {
            margin-top: 0;
        }
        .summary-cards {
            display: flex;
            justify-content: space-between;
            margin: 20px 0;
        }
        .card {
            padding: 0px;
            margin: 10px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            flex: 1;
            text-align: center;
            color: #fff; /* Text color set to white */
            padding-bottom: -40px;
        }
        .card-orange {
            background-color: #FF8C00; /* Orange color */
        }
        .card-purple {
            background-color: #6A0DAD; /* Purple color */
        }
        .card-darkblue {
            background-color: #001f3f; /* Dark blue color */
        }
        .card h2 {
            font-size: 20px;
        }
        .card p {
            font-size: 36px;
            font-weight: bold;
        }
        .portfolio-stocks table, .watchlist table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 10px;
        }
        .portfolio-stocks th, .portfolio-stocks td, .watchlist th, .watchlist td {
            padding: 12px;
            text-align: left;
            border-bottom: 1px solid #ddd;
        }
        .chart-container {
            margin-top: 20px;
            padding: 20px;
            background-color: #fff;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
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
      <a href="{{site.baseurl}}/stocks/portfolio">Portfolio</a>
      <a href="{{site.baseurl}}/stocks/buysell">Buy/Sell</a>
      <a href="#">Profile</a>
        </div>
    </nav>
    <!-- Portfolio Content -->
    <div class="portfolio">
        <div class="portfolio-content">
            <!-- Summary Cards -->
            <div class="summary-section">
                <h2>Portfolio Overview</h2>
                <div class="summary-cards">
                    <div class="card card-orange">
                    <h3>Today's Dollar Change</h3>
                    <p id="totalGain">NA</p>
                </div>
                <div class="card card-purple">
                    <h3>Today's Percent Change</h3>
                    <p id="percentIncrease">NA</p>
                </div>
                    <div class="card card-darkblue">
                        <h3>Overall Value</h3>
                        <p id="portfolioValue">NA</p>
                    </div>
                </div>
            </div>
            <!-- Portfolio Stocks Table -->
            <div class="portfolio-stocks">
                <h3>Your Stocks</h3>
                <table id="portfolioTable">
                    <tr>
                        <th>Stock</th>
                        <th>Price</th>
                        <th># of Shares</th>
                        <th>Total Value</th>
                        <th>% Change</th>
                    </tr>
                </table>
            </div>
            <!-- Chart Container -->
            <div class="chart-container">
                <canvas id="portfolioChart"></canvas>
            </div>
        </div>
        <!-- Watchlist Sidebar -->
        <div class="watchlist">
            <h3>Watchlist</h3>
            <table>
                <tr>
                    <th>Stock</th>
                    <th>Price</th>
                </tr>
                <tr>
                    <td>Netflix</td>
                    <td id="NetflixPrice">$390</td>
                </tr>
                <tr>
                    <td>Amazon</td>
                    <td id="AmazonPrice">$3,200</td>
                </tr>
            </table>
        </div>
    </div>
    <!-- JavaScript to Fetch Data and Display Chart -->
    <script>
    var userID = localStorage.getItem('userID')
    console.log(userID);
        async function getStockPrice(stock) {
        try {
            const response = await fetch(`http://localhost:8085/api/stocks/${stock}`);
            const data = await response.json();
            console.log(data);
            const price = data?.chart?.result?.[0]?.meta?.regularMarketPrice;
            const outputElement = document.getElementById("output");
            if (price !== undefined) {
                //outputElement.textContent = `The price of ${stock} is: $${price}`;
                 console.log(`The price of ${stock} is: $${price}`);
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
      async function getOldStockPrice(stock) {
        try {
            const response = await fetch(`http://localhost:8085/api/stocks/${stock}`);
            const data = await response.json();
            console.log(data);
            const oldPrice = data?.chart?.result?.[0]?.meta?.chartPreviousClose;
            const outputElement = document.getElementById("output");
            if (oldPrice !== undefined) {
                //outputElement.textContent = `The price of ${stock} is: $${price}`;
                 console.log(`The previous close price of ${stock} is: $${oldPrice}`);
                return(oldPrice)
            } else {
                outputElement.textContent = `Price not found for ${stock}.`;
                console.error(`Price not found for ${stock}. Response structure:`, data);
            }
        } catch (error) {
            console.error('Error fetching stock data:', error);
            document.getElementById("output").textContent = "Error fetching stock data. Please try again later.";
        }
      }
        async function updatePrices() {
            const stocks = ["AAPL", "MSFT"]; // //THIS NEEDS TO BE CHANGED FOR THE STOCKS INVESTED IN *****
            for (let stock of stocks) {
                const price = await getStockPrice(stock);
                const priceElement = document.getElementById(stock + "Price");
                const percentChange = await getPercentChange(stock);
                const percentChangeElement = document.getElementById(stock + "Change");
                //const stockTotal = await getStockTotal(stock);
                const stockTotalElement = document.getElementById(stock + "Total");
                if (priceElement) priceElement.textContent = `$${price}`;
                if (percentChangeElement) percentChangeElement.textContent = `${percentChange}%`;
                //if (stockTotalElement) stockTotalElement.textContent = `$${stockTotal}`;
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
    async function createPortfolioChart() {
        const userStocks = await getUserStock(userID);
        const labels = [];
        const dataValues = [];
        const backgroundColors = ["#FF8C00", "#6A0DAD", "#001f3f", "#FF8C00"]; // Define colors for each stock
        for (const stockInfo of userStocks) {
            const { stockSymbol, quantity } = stockInfo;
            const price = await getStockPrice(stockSymbol);
            const totalValue = price * quantity;
            // Push symbol and calculated total value to arrays
            labels.push(stockSymbol);
            dataValues.push(totalValue);
        }
        const ctx = document.getElementById("portfolioChart").getContext("2d");
        new Chart(ctx, {
            type: "bar",
            data: {
                labels: labels,
                datasets: [{
                    label: "Portfolio Distribution",
                    data: dataValues,
                    backgroundColor: backgroundColors.slice(0, labels.length),
                    borderColor: "#001f3f",
                    borderWidth: 1,
                }]
            },
            options: {
                responsive: true,
                scales: {
                    y: {
                        beginAtZero: true
                    }
                }
            }
        });
    }
        async function getStockTotal(stock, quantity) {
            try {
                const response = await fetch(`http://localhost:8085/api/stocks/${stock}`);
                const data = await response.json();
                const price = data?.chart?.result?.[0]?.meta?.regularMarketPrice;
                const totalValue = price * quantity;
                return totalValue ? totalValue.toFixed(2) : "N/A";
            } catch (error) {
                console.error("Error fetching stock data:", error);
                return "N/A";
            }
        }
        async function getUserStock(user) {
            try {
                const response = await fetch(`http://localhost:8085/user/getStocks?username=${user}`);
                const stocksData = await response.json();
                console.log(stocksData);
                return stocksData;
            } catch (error) {
                console.error("Error fetching user stocks:", error);
                return [];
            }
        }
        async function populatePortfolioTable() {
            const userStocks = await getUserStock(userID);
            const portfolioTable = document.getElementById("portfolioTable");
            for (const stockInfo of userStocks) {
                const { stockSymbol, quantity } = stockInfo;
                // Fetch dynamic stock data
                const price = await getStockPrice(stockSymbol);
                const percentChange = await getPercentChange(stockSymbol);
                const totalValue = await getStockTotal(stockSymbol, quantity);
                // Create a new row for the stock
                const row = document.createElement("tr");
                row.innerHTML = `
                    <td>${stockSymbol}</td>
                    <td id="${stockSymbol}Price">$${price}</td>
                    <td>${quantity}</td>
                    <td id="${stockSymbol}Total">$${totalValue}</td>
                    <td id="${stockSymbol}Change">${percentChange}%</td>
                `;
                // Append the row to the table
                portfolioTable.appendChild(row);
            }
        }
        async function getPortfolioPerformance(user) {
            // Fetch user's stocks and quantities
            const userStocks = await getUserStock(user);
            const userValue = await getUserValue(user);
            let totalGain = 0;
            let totalLatestValue = 0;
            let totalOldValue = 0;
            for (const { stockSymbol, quantity } of userStocks) {
                const latestPrice = await getStockPrice(stockSymbol);
                const oldPrice = await getOldStockPrice(stockSymbol);
                // Calculate gain for each stock
                const stockGain = (latestPrice - oldPrice) * quantity;
                totalGain += stockGain;
                // Calculate total values for percent increase calculation
                totalLatestValue += latestPrice * quantity;
                totalOldValue += oldPrice * quantity;
            }
            // Calculate percent increase
            const percentIncrease = ((totalLatestValue - totalOldValue) / totalOldValue) * 100;
            console.log(`total increase: $${totalGain.toFixed(2)}, percent increase: ${percentIncrease.toFixed(2)}%`);
            const totalElement = document.getElementById("totalGain");
            const percentElement = document.getElementById("percentIncrease");
            const valueElement = document.getElementById("portfolioValue");
            totalElement.textContent = `$${totalGain.toFixed(2)}`;
            percentElement.textContent = `${percentIncrease.toFixed(2)}%`;
            valueElement.textContent = `$${userValue.toFixed(2)}`;
        }
        async function getUserValue(user) {
            try {
                const response = await fetch(`http://localhost:8085/user/portfolioValue?username=${user}`);
                const stocksData = await response.json();
                console.log(stocksData);
                return stocksData;
            } catch (error) {
                console.error("Error fetching user stocks:", error);
                return [];
            }
        }
        document.addEventListener("DOMContentLoaded", () => {
            updatePrices();
            populatePortfolioTable();
            createPortfolioChart();
            getPortfolioPerformance(userID);
        });
    </script>
</body>
</html>
