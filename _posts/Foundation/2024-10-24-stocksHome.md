---
layout: none
permalink: /stocks/test
---
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stock Market Dashboard</title>
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
            padding: 20px;
            margin: 10px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            flex: 1;
            text-align: center;
            color: #fff; /* Text color set to white */
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
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            margin: 20px 0;
        }
        .chart {
            height: 300px;
            background-color: #f9f9f9;
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
            color: #999;
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
    </style>
</head>
<body>

    <!-- Navigation Bar -->
    <nav class="navbar">
        <div class="logo">NITD</div>
        <div class="nav-buttons">
            <a href="#">Home</a>
            <a href="#">Stocks</a>
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
                <input type="text" placeholder="Search..."> <!-- Search bar moved above the graph -->
            </div>

            <div class="chart-container">
                <div class="chart">
                    [Graph Placeholder]
                </div>
            </div>
        </div>

        <!-- Sidebar with "Your Stocks" and Stock Prices -->
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

            <!-- Stock Prices table moved to the bottom -->
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
</html>
