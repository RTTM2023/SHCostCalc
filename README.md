<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Sexual Harassment Cost Calculator</title>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap" rel="stylesheet" />
  <style>
    body {
      font-family: 'Montserrat', sans-serif;
      margin: 0;
      background-color: #f8f8f8;
    }
    .container {
      display: flex;
      flex-direction: column;
      padding: 2rem;
      max-width: 1600px;
      margin: 0 auto;
    }
    @media (min-width: 1024px) {
      .container {
        flex-direction: row;
        justify-content: space-between;
      }
    }
    .calculator, .results-box {
      background-color: white;
      padding: 2rem;
      border-radius: 20px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    }
    .calculator {
      flex: 1;
      margin-right: 2rem;
      border: 2px solid #F75C36;
    }
    .results-box {
      flex: 1;
      background-color: #F75D36;
      color: white;
    }
    label {
      font-weight: bold;
      display: block;
      margin-top: 1.5rem;
    }
    input[type="number"] {
      width: 100%;
      padding: 0.6rem;
      font-size: 1rem;
      border-radius: 30px;
      border: 1px dashed #F87171;
      font-family: 'Montserrat', sans-serif;
    }
    button {
      margin-top: 2rem;
      width: 100%;
      padding: 1rem;
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
      font-size: 0.9rem;
    }
    .total-line {
      font-size: 1.2rem;
      font-weight: bold;
      margin-top: 1rem;
      display: flex;
      justify-content: space-between;
    }
  </style>
</head>
<body>
<div class="container">
  <div class="calculator">
    <h2>Sexual Harassment Cost Calculator</h2>
    <label for="women">Number of Women in Organisation:</label>
    <input type="number" id="women" />

    <label for="men">Number of Men in Organisation:</label>
    <input type="number" id="men" />

    <label for="salary">Average Gross Monthly Salary (R):</label>
    <input type="number" id="salary" />

    <button onclick="calculateCost()">Calculate</button>
  </div>

  <div class="results-box">
    <h2>Estimated SH Cost</h2>
    <div id="resultsContent"></div>
  </div>
</div>

<script>
  function calculateCost() {
    const women = parseInt(document.getElementById('women').value) || 0;
    const men = parseInt(document.getElementById('men').value) || 0;
    const salary = parseFloat(document.getElementById('salary').value) || 0;

    const totalEmployees = women + men;

    // Incidence assumptions
    const femaleRate = 0.03;
    const maleRate = 0.01;
    const totalCases = (women * femaleRate) + (men * maleRate);

    const low = totalCases * 0.75;
    const med = totalCases * 0.2;
    const high = totalCases * 0.05;

    // Costs per case based on salary multiple (conservative)
    const lowCost = low * 0.33 * salary;     // ~1/3 month salary
    const medCost = med * 1.43 * salary;     // ~1.43 months
    const highCost = high * 6.43 * salary;   // ~6.43 months

    const totalCost = lowCost + medCost + highCost;

    document.getElementById('resultsContent').innerHTML = `
      <div class='results-line-item'><span>Estimated Cases:</span><span>${totalCases.toFixed(1)}</span></div>
      <div class='results-line-item'><span>Low Severity (75%):</span><span>${low.toFixed(1)} cases</span></div>
      <div class='results-line-item'><span>Medium Severity (20%):</span><span>${med.toFixed(1)} cases</span></div>
      <div class='results-line-item'><span>High Severity (5%):</span><span>${high.toFixed(1)} cases</span></div>
      <div class='results-line-item'><span>Cost of Low Severity:</span><span>R${lowCost.toLocaleString()}</span></div>
      <div class='results-line-item'><span>Cost of Medium Severity:</span><span>R${medCost.toLocaleString()}</span></div>
      <div class='results-line-item'><span>Cost of High Severity:</span><span>R${highCost.toLocaleString()}</span></div>
      <div class="total-line"><span>Total Annual Cost:</span><span>R${totalCost.toLocaleString()}</span></div>
    `;
  }
</script>
</body>
</html>
