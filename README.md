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
    .tooltip {
      position: relative;
      cursor: help;
      text-decoration: underline dotted white;
    }
    .tooltip:hover::after {
      content: attr(data-tooltip);
      position: absolute;
      background: rgba(0, 0, 0, 0.8);
      color: #fff;
      padding: 0.5rem;
      border-radius: 5px;
      top: 100%;
      left: 0;
      white-space: nowrap;
      font-size: 0.8rem;
      margin-top: 0.25rem;
      z-index: 10;
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
    <button onclick="downloadPDF()">Download as PDF</button>
  </div>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
<script>
  function calculateCost() {
    const women = parseInt(document.getElementById('women').value) || 0;
    const men = parseInt(document.getElementById('men').value) || 0;
    const salary = parseFloat(document.getElementById('salary').value) || 0;

    const totalEmployees = women + men;
    const femaleRate = 0.03;
    const maleRate = 0.01;
    const totalCases = (women * femaleRate) + (men * maleRate);

    const low = totalCases * 0.75;
    const med = totalCases * 0.2;
    const high = totalCases * 0.05;

    const lowCost = low * 0.33 * salary;
    const medCost = med * 1.43 * salary;
    const highCost = high * 6.43 * salary;
    const totalCost = lowCost + medCost + highCost;

    document.getElementById('resultsContent').innerHTML = `
      <div class='results-line-item'><span>Estimated Cases:</span><span>${totalCases.toFixed(1)}</span></div>
      <div class='results-line-item'><span>Low Severity Cost (75% of ${totalCases.toFixed(1)}):</span><span>R${lowCost.toLocaleString()}</span></div>
      <div class='results-line-item'><span>Medium Severity Cost (20% of ${totalCases.toFixed(1)}):</span><span>R${medCost.toLocaleString()}</span></div>
      <div class='results-line-item'><span>High Severity Cost (5% of ${totalCases.toFixed(1)}):</span><span>R${highCost.toLocaleString()}</span></div>
      <div class="total-line"><span>Total Annual Cost:</span><span>R${totalCost.toLocaleString()}</span></div>
    `;
  }

  function downloadPDF() {
    const element = document.querySelector('.container');
    const opt = {
      margin: 0.5,
      filename: 'Sexual_Harassment_Cost_Estimate.pdf',
      image: { type: 'jpeg', quality: 0.98 },
      html2canvas: { scale: 3, useCORS: true },
      jsPDF: { unit: 'in', format: 'letter', orientation: 'landscape' }
    };
    html2pdf().set(opt).from(element).save();
  }
</script>
</body>
</html>
