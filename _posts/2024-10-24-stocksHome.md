---
layout: none
permalink: /stocks/home
title: Stocks Home
---
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stock Market Dashboard</title>
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
        .dashboard {
            padding: 20px;
            display: flex;
            justify-content: flex-start;
            gap: 40px;
        }
        .dashboard-content {
            width: 70%; /* Increased width for the left side */
        }
        .sidebar {
            width: 25%; /* Width for the right side */
            display: flex;
            flex-direction: column;
            gap: 20px;
        }
        .stock-table, .your-stocks {
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }
        .your-stocks, .stock-table {
            height: 300px; /* Height for tables */
        }
        .stock-table table, .your-stocks table {
            width: 100%;
            border-collapse: collapse;
        }
        .stock-table table, th, td, .your-stocks table, th, td {
            border: none; /* Removed the border to make it invisible */
        }
        .stock-table th, td, .your-stocks th, td {
            padding: 10px;
            text-align: left;
        }
        .stock-table th, .your-stocks th {
            background-color: #f2f2f2;
        }
        .welcome {
            font-size: 24px;
            font-weight: bold;
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
        .chart-container {
            position: relative;
            background-color: #fff;
            padding: 50px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            margin: 20px 0;
            display: flex;
            gap: 20px;
        }
        .chart {
            height: 100%; /* Set height to 100% to fill the container */
            width: 100%; /* Set height to 100% to fill the container */
            background-color: #fff; /* Set the chart background to white */
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
            color: #999;
            flex: 1;
        }
        .search-container {
            margin-bottom: 20px; /* Add margin to space it out */
            display: flex;
        }
        .search-container input[type="text"] {
            width: 100%; /* Full width of the graph */
            padding: 12px;
            border: none;
            border-radius: 4px;
            outline: none;
            font-size: 16px;
        }
        .search-button {
            background-color: #ff8c00; /* Orange color */
            color: #fff;
            border: none;
            border-radius: 0 4px 4px 0; /* Rounded corners on the right */
            padding: 12px 20px;
            cursor: pointer;
            font-size: 16px;
            transition: background-color 0.3s;
        }
        .search-button:hover {
            background-color: #e07b00; /* Darker orange on hover */
        }
        .add-chart-button, .remove-chart-button {
            position: absolute;
            top: 10px;
            right: 10px;
            background-color: #ff8c00;
            color: #fff;
            border: none;
            border-radius: 50%;
            width: 30px;
            height: 30px;
            font-size: 20px;
            font-weight: bold;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .remove-chart-button {
            right: 40px; /* Adjust position for minus button */
            display: none;
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
    <!-- Dashboard Content -->
    <div class="dashboard">
        <div class="dashboard-content">
            <h1 class="welcome">Hi Rafael, Welcome Back</h1>
            <p>Invest your money with small risk!</p>
            <div class="summary-cards">
                <div class="card card-orange">
                    <h2>Today's Return</h2>
                    <p>$39,345</p>
                </div>
                <div class="card card-purple">
                    <h2>Total Return</h2>
                    <p>$42,345</p>
                </div>
                <div class="card card-darkblue">
                    <h2>Revenue Return</h2>
                    <p>$52,345</p>
                </div>
            </div>
            <div class="search-container">
               <input type="text" id = "searchBar" placeholder="Search...">
               <button class="search-button" onclick="getStockData()">Search</button> <!-- Search button added -->
            </div>
            <div class="chart-container" id="chartContainer">
                <button class="add-chart-button" onclick="addNewChart()">+</button>
                <button class="remove-chart-button" onclick="removeNewChart()">-</button>
                <div class="chart" id="chart1">
                    <canvas id="stockChart" width="450" height="400">[Graph Placeholder]</canvas>
                </div>
            </div>
<div id="output" style="color: red; padding-top: 10px;"></div>
        </div>
        <!-- Sidebar -->
        <div class="sidebar">
            <!-- "Your Stocks" section with table -->
            <div class="your-stocks">
                <h3>Your Stocks</h3>
                <table>
                    <tr>
                        <th>Stock</th>
                        <th>Price</th>
                    </tr>
                    <tr>
                        <td>Netflix</td>
                        <td>$490,123</td>
                    </tr>
                    <tr>
                        <td>Tesla</td>
                        <td>$920,456</td>
                    </tr>
                    <tr>
                        <td>Amazon</td>
                        <td>$1,123,987</td>
                    </tr>
                    <tr>
                        <td>Adobe</td>
                        <td>$670,345</td>
                    </tr>
                    <tr>
                        <td>Nvidia</td>
                        <td>$820,321</td>
                    </tr>
                </table>
            </div>
            <div class="stock-table">
                <h3>Stock Prices</h3>
                <table>
                    <tr>
                        <th>Stock</th>
                        <th>Price</th>
                    </tr>
                    <tr>
                        <td>Spotify</td>
                        <td>$297,408</td>
                    </tr>
                    <tr>
                        <td>Apple</td>
                        <td>$142,845</td>
                    </tr>
                    <tr>
                        <td>Google</td>
                        <td>$273,402</td>
                    </tr>
                    <tr>
                        <td>Facebook</td>
                        <td>$97,213</td>
                    </tr>
                    <tr>
                        <td>Microsoft</td>
                        <td>$342,981</td>
                    </tr>
                </table>
            </div>
        </div>
    </div>

</body>

<script>
    function addNewChart() {
        const chartContainer = document.getElementById('chartContainer');
        const chart1 = document.getElementById('chart1');

        // Adjust the width of the original chart to 50%
        chart1.style.flex = '0 0 50%';

        // Create a new chart element
        const newChart = document.createElement('div');
        newChart.className = 'chart';
        newChart.id = 'newChart';
        newChart.innerText = '[New Graph Placeholder]';

        // Add the new chart to the chart container
        chartContainer.appendChild(newChart);

        // Update the add button to show remove button
        document.querySelector('.add-chart-button').style.display = 'none';
        const removeButton = document.querySelector('.remove-chart-button');
        removeButton.style.display = 'block';
    }

    function removeNewChart() {
        const chartContainer = document.getElementById('chartContainer');
        const newChart = document.getElementById('newChart');
        const chart1 = document.getElementById('chart1');

        if (newChart) {
            // Remove the new chart element
            chartContainer.removeChild(newChart);

            // Restore the original chart's width
            chart1.style.flex = '1';

            // Show the add button and hide the remove button
            document.querySelector('.add-chart-button').style.display = 'block';
            document.querySelector('.remove-chart-button').style.display = 'none';
        }
    }
    async function getStockData() {

        const stockSymbol = document.getElementById("searchBar").value;
        //console.log("Ticker Symbol:", stockSymbol);

        try {
            const response = await fetch(`http://localhost:8085/api/stocks/${stockSymbol}`);
            const data = await response.json();
            console.log(data);

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

function displayChart(labels, data, stockSymbol) {
    const ctx = document.getElementById('stockChart').getContext('2d');

    // Create a gradient for the area under the line
    const gradient = ctx.createLinearGradient(0, 0, 0, 400); // Adjust the height as necessary
    gradient.addColorStop(0, 'rgba(106, 13, 173, 0.6)'); // Start with purple (rgba)
    gradient.addColorStop(1, 'rgba(255, 255, 255, 0.0)'); // Fade to transparent

    new Chart(ctx, {
        type: 'line',
        data: {
            labels: labels,
            datasets: [{
                label: `Stock Price for ${stockSymbol}`,
                data: data,
                borderColor: '#001f3f', // Dark blue color for the line
                backgroundColor: gradient, // Gradient background
                fill: true, // Enable filling under the line
                pointRadius: 0, // Remove dots
                tension: 0.1 // Smooth the line
            }]
        },
        options: {
            responsive: true,
            maintainAspectRatio: false, // Allow chart to fill the container
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


    

</script>
</html>
