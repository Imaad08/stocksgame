---
layout: none
permalink: /stocks/portfolio
title: Stocks Home
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
            gap: 20px;
            justify-content: space-around;
        }
        .card {
            flex: 1;
            text-align: center;
            color: #fff;
            padding: 20px;
            border-radius: 8px;
            font-size: 16px;
            font-weight: bold;
        }
        .card-orange {
            background-color: #FF8C00;
        }
        .card-purple {
            background-color: #6A0DAD;
        }
        .card-darkblue {
            background-color: #001f3f;
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
      <a href="#">Upgrades</a>
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
                        <h3>Today's Gain</h3>
                        <p>$3,400</p>
                    </div>
                    <div class="card card-purple">
                        <h3>Today's Growth</h3>
                        <p>15%</p>
                    </div>
                    <div class="card card-darkblue">
                        <h3>Overall Value</h3>
                        <p>$50,000</p>
                    </div>
                </div>
            </div>
            <!-- Portfolio Stocks Table -->
            <div class="portfolio-stocks">
                <h3>Your Stocks</h3>
                <table>
                    <tr>
                        <th>Stock</th>
                        <th>Price</th>
                        <th># of Shares</th>
                        <th>Total Value</th>
                        <th>% Change</th>
                        <th>Upgrades</th>
                        <th>Buy</th>
                        <th>Sell</th>
 <!-- Portfolio Stocks Table
                        <th>Stock</th>
                        <th>Number of Shares</th>
                        <th>Purchase Date</th>
                        <th>Purchase Price</th>
                        <th>Current Price</th>
                        <th>Dollar Gain from Purchase Price</th>
                        <th>Percent Gain from Purchase Price</th>
                        <th>Dollar Gain from Day</th>
                        <th>Percent Gain from Day</th>
                        <th>Upgrades</th>
                        <th>Buy</th>
                        <th>Sell</th>
                    -->
                    </tr>   
                    <tr>
                        <td>Apple</td>
                        <td id="AAPLPrice">$142</td>
                        <td id="AAPLStock">50</td>
                        <td id="AAPLTotal">$7,100</td>
                        <td id="AAPLChange">-0.13%</td>
                        <th></th>
                        <th>Buy</th>
                        <th>Sell</th>
                    </tr>
                    <tr>
                        <td>Microsoft</td>
                        <td id="MSFTPrice">$330</td>
                        <td id="MSFTStock">50</td>
                        <td id="MSFTTotal">$9,900</td>
                        <td id="MSFTChange">-27%</td>
                        <th></th>
                        <th>Buy</th>
                        <th>Sell</th>
                    </tr>
                    <!-- More stocks can be added here -->
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
        async function updatePrices() {
            const stocks = ["AAPL", "MSFT"]; // //THIS NEEDS TO BE CHANGED FOR THE STOCKS INVESTED IN *****
            for (let stock of stocks) {
                const price = await getStockPrice(stock);
                const priceElement = document.getElementById(stock + "Price");
                const percentChange = await getPercentChange(stock);
                const percentChangeElement = document.getElementById(stock + "Change");
                const stockTotal = await getStockTotal(stock);
                const stockTotalElement = document.getElementById(stock + "Total");
                if (priceElement) priceElement.textContent = `$${price}`;
                if (percentChangeElement) percentChangeElement.textContent = `${percentChange}%`;
                if (stockTotalElement) stockTotalElement.textContent = `$${stockTotal}`;
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
        function createPortfolioChart() {
            const ctx = document.getElementById("portfolioChart").getContext("2d");
            new Chart(ctx, {
                type: "bar",
                data: {
                    labels: ["Apple", "Microsoft", "Netflix", "Amazon"],
                    datasets: [{
                        label: "Portfolio Distribution",
                        data: [7100, 9900, 3900, 3200],
                        backgroundColor: ["#FF8C00", "#6A0DAD", "#001f3f", "#FF8C00"],
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
        async function getStockTotal(stock) {
        try {
            const response = await fetch(`http://localhost:8085/api/stocks/${stock}`);
            const data = await response.json();
            console.log(data);
            const price = data?.chart?.result?.[0]?.meta?.regularMarketPrice;
            const stockNumber = 50;   //THIS NEEDS TO BE CHANGED FOR THE NUMBER OF STOCKS *****
            const totalValue = price * stockNumber;
            //const outputElement = document.getElementById("output");
            if (totalValue !== undefined) {
                //outputElement.textContent = `The price of ${stock} is: $${price}`;
                console.log(totalValue.toFixed(2));
                return totalValue.toFixed(2);
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
        async function getUserStock(user) {
        try {
            const response = await fetch(`http://localhost:8085/user/getStocks?username=${user}`);
            const data = await response.json();
            console.log(data);
            //const outputElement = document.getElementById("output");
            if (data !== undefined) {
                //outputElement.textContent = `The price of ${stock} is: $${price}`;
                //console.log(`The price of ${stock} is: $${price}`);
                return(data)
            } else {
                outputElement.textContent = `Price not found for ${stock}.`;
                console.error(`Price not found for ${stock}. Response structure:`, data);
            }
        } catch (error) {
            console.error('Error fetching stock data:', error);
            document.getElementById("output").textContent = "Error fetching stock data. Please try again later.";
        }
      }
        document.addEventListener("DOMContentLoaded", () => {
            updatePrices();
            createPortfolioChart();
            getUserStock("testUser4");
        });
    </script>
</body>
</html>
