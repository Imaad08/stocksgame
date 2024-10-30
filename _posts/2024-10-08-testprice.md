---
layout: page
hide: false
permalink: /stocks/pricecheck
title: Stocks Login
---

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Price Check</title>
    <script>
      async function getStockPrice(stockSymbol) {
        try {
            const response = await fetch(`http://localhost:8085/api/stocks/${stockSymbol}`);
            const data = await response.json();

            console.log(data);

            const price = data?.chart?.result?.[0]?.meta?.regularMarketPrice;

            const outputElement = document.getElementById("output");

            if (price !== undefined) {
                outputElement.textContent = `The price of ${stockSymbol} is: $${price}`;
            } else {
                outputElement.textContent = `Price not found for ${stockSymbol}.`;
                console.error(`Price not found for ${stockSymbol}. Response structure:`, data);
            }
        } catch (error) {
            console.error('Error fetching stock data:', error);
            document.getElementById("output").textContent = "Error fetching stock data. Please try again later.";
        }
      }

      getStockPrice("AAPL");
    </script>

</head>
<body>
    <h1>Price Check Result</h1>
    <pre id="output">Loading...</pre>
</body>
</html>
