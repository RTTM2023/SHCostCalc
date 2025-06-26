<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Sexual Harassment Cost Calculator</title>
  <style>
    body {
      background-color: transparent;
      font-family: 'Montserrat', sans-serif;
      margin: 0;
      padding: 0;
      overflow-x: hidden;
    }
    .container {
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      width: 100%;
      max-width: 1600px;
      margin: 0 auto;
      gap: 2rem;
      padding: 2rem;
      box-sizing: border-box;
    }
    .calculator, .results-box {
      background-color: #ffffff;
      border: 2px solid #F75C36;
      border-radius: 20px;
      padding: 2rem;
      box-sizing: border-box;
    }
    .calculator {
      width: 100%;
      max-width: 800px;
    }
    .results-box {
      background-color: #F75D36;
      color: white;
      width: 100%;
      max-width: 600px;
    }
    label {
      display: block;
      font-weight: bold;
      margin-top: 1rem;
    }
    input[type="number"] {
      width: 100%;
      padding: 0.6rem;
      font-size: 1rem;
      border: 1px dashed #F87171;
      border-radius: 30px;
      margin-top: 0.3rem;
      font-family: 'Montserrat', sans-serif;
    }
    button {
      margin-top: 2rem;
      padding: 1rem;
      width: 100%;
      font-size: 1.2rem;
      background-color: #F75D36;
      color: white;
      border: none;
      border-radius: 30px;
      cursor: pointer;
      font-family: 'Montserrat', sans-serif;
    }
    .results-line-item {
      display: flex;
      justify-content: space-between;
      margin: 0.5rem 0;
      font-size: 0.95rem;
    }
    .total-line {
      font-size: 1.2rem;
      font-weight: bold;
      display: flex;
      justify-content: space-between;
      margin-top: 1rem;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="calculator">
      <h1>Sexual Harassment Cost Calculator</h1>
      <label for="women">Number of Women in the Organisation:</label>
      <input type="number" id="women" placeholder="e.g. 525" />

      <label for="men">Number of Men in the Organisation:</label>
      <input type="number" id="men" placeholder="e.g. 525" />

      <label for="salary">Average Gross Monthly Salary (ZAR):</label>
      <input type="number" id="salary" placeholder="e.g. 96666.67" />

      <button onclick="calculateCost()">Calculate</button>
    </div>

    <div class="results-box">
      <h2>Estimated Annual Cost of Sexual Harassment</h2>
      <div id="resultsContent"></div>
    </div>
  </div>

  <script>
    function calculateCost() {
      const numWomen = parseInt(document.getElementById("women").value) || 0;
      const numMen = parseInt(document.getElementById("men").value) || 0;
      const salary = parseFloat(document.getElementById("salary").value) || 0;

      const femaleRate = 0.03;
      const maleRate = 0.01;

      const totalCases = (numWomen * femaleRate) + (numMen * maleRate);
      const low = totalCases * 0.75;
      const medium = totalCases * 0.20;
      const high = totalCases * 0.05;

      const lowCost = low * 9492;
      const mediumCost = medium * 40705;
      const highCost = high * 182828;

      const totalCost = lowCost + mediumCost + highCost;

      const results = `
        <div class='results-line-item'><span>Estimated Cases Per Year:</span><span>${totalCases.toFixed(2)}</span></div>
        <div class='results-line-item'><span>Low Severity Cost:</span><span>R${lowCost.toLocaleString()}</span></div>
        <div class='results-line-item'><span>Medium Severity Cost:</span><span>R${mediumCost.toLocaleString()}</span></div>
        <div class='results-line-item'><span>High Severity Cost:</span><span>R${highCost.toLocaleString()}</span></div>
        <div class="total-line"><span>Total Cost:</span><span>R${totalCost.toLocaleString()}</span></div>
      `;

      document.getElementById("resultsContent").innerHTML = results;
    }
  </script>
</body>
</html>
