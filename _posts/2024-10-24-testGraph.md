---
layout: page
hide: false
permalink: /stocks/pricecheck2
title: Stocks Login
---
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Price Check</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script>
      async function getStockData(stockSymbol) {
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
        new Chart(ctx, {
            type: 'line',
            data: {
                labels: labels,
                datasets: [{
                    label: `Stock Price for ${stockSymbol}`,
                    data: data,
                    borderColor: 'rgba(75, 192, 192, 1)',
                    fill: false,
                    tension: 0.1
                }]
            },
            options: {
                scales: {
                    x: { title: { display: true, text: 'Timestamp' } },
                    y: { title: { display: true, text: 'Price (USD)' } }
                }
            }
        });
      }

      // Call the function for a sample stock, e.g., AAPL
      getStockData("AAPL");
    </script>
</head>
<body>
    <h1>Stock Price Chart</h1>
    <canvas id="stockChart" width="400" height="200"></canvas>
    <p id="output"></p>
</body>
</html>
