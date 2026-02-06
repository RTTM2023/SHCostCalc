<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
  <title>Sexual Harassment Cost Calculator</title>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap" rel="stylesheet" />
  <style>
    * {
      box-sizing: border-box; /* Crucial: ensures padding doesn't add to width */
    }

    body {
      font-family: 'Montserrat', sans-serif;
      margin: 0;
      padding: 0;
      background-color: transparent;
      overflow-x: hidden; /* Hard stop for horizontal scrolling */
      width: 100%;
    }

    .container {
      display: flex;
      flex-direction: column;
      padding: 10px; /* Minimal padding for mobile */
      width: 100%;
      max-width: 1600px;
      margin: 0 auto;
      gap: 1.5rem;
    }

    /* Desktop Layout */
    @media (min-width: 1024px) {
      .container {
        flex-direction: row;
        justify-content: space-between;
        padding: 2rem;
      }
      .calculator {
        flex: 1.3;
        margin-right: 2rem;
        width: auto;
      }
      .results-box {
        flex: 1;
        width: auto;
      }
    }

    .calculator, .results-box {
      background-color: white;
      padding: 1.5rem;
      border-radius: 20px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
      width: 100%; /* Force full width of container */
      max-width: 100%;
    }

    .calculator {
      border: 2px solid #f10178;
    }

    .results-box {
      background-color: #f10178;
      color: white;
      min-height: 200px;
      word-wrap: break-word; /* Prevents long text from stretching width */
    }

    h2 {
      font-size: 1.4rem;
      margin-top: 0;
    }

    label {
      font-weight: bold;
      display: block;
      margin-top: 1.2rem;
      font-size: 0.9rem;
    }

    input[type="number"] {
      width: 100%;
      padding: 12px;
      margin-top: 5px;
      font-size: 16px; /* Prevents iOS auto-zoom on focus */
      border-radius: 30px;
      border: 1px dashed #5b01fa;
      font-family: 'Montserrat', sans-serif;
    }

    button {
      margin-top: 1.5rem;
      width: 100%;
      padding: 1rem;
      font-size: 1.1rem;
      background-color: #f10178;
      color: white;
      border: none;
      border-radius: 30px;
      cursor: pointer;
      font-weight: bold;
    }

    /* Fix for the results lines on mobile */
    .results-line-item {
      display: flex;
      justify-content: space-between;
      align-items: flex-start; /* Alignment for wrapped text */
      margin: 0.5rem 0;
      font-size: 0.8rem;
      gap: 10px;
    }

    .results-line-item span:first-child {
      flex: 1; /* Allows text to wrap if it needs space */
    }

    .total-line {
      font-size: 1.1rem;
      font-weight: bold;
      margin-top: 1.5rem;
      padding: 10px 0;
      border-top: 1px dotted white;
      border-bottom: 1px dotted white;
      display: flex;
      justify-content: space-between;
    }

    /* Tooltip Mobile Safety */
    .tooltip {
      position: relative;
      cursor: pointer;
    }

    .tooltip img {
      width: 14px;
      height: 14px;
      vertical-align: middle;
    }

    .tooltip:hover::after {
      content: attr(data-tooltip);
      position: absolute;
      background: #333;
      color: #fff;
      padding: 8px;
      border-radius: 5px;
      width: 160px;
      font-size: 0.7rem;
      z-index: 10;
      bottom: 125%;
      left: 50%;
      transform: translateX(-50%);
    }

    /* Enquiry Form Mobile Polish */
    #enquiryForm form input, #enquiryForm textarea {
      width: 100%;
      margin-bottom: 10px;
      padding: 12px;
      border-radius: 20px;
      border: 1px solid #ccc;
    }

    .button-group {
      display: none;
      flex-direction: column;
      gap: 10px;
      margin-top: 20px;
    }

    .download-btn, .reset-btn {
      width: 100%;
      padding: 12px;
      border-radius: 30px;
      border: 1px dashed #5b01fa;
      cursor: pointer;
      font-family: 'Montserrat', sans-serif;
    }

    .reset-btn { background: #5b01fa; color: white; }
  </style>
</head>
<body>

<div class="container">
  <div class="calculator">
    <h2>Cost Calculator</h2>
    <label>Women in Organisation <span class="tooltip" data-tooltip="Estimated harassment rate applies."><img src="whiteback.png" /></span></label>
    <input type="number" id="women" placeholder="0" />

    <label>Men in Organisation <span class="tooltip" data-tooltip="Estimated harassment rate applies."><img src="whiteback.png" /></span></label>
    <input type="number" id="men" placeholder="0" />

    <label>Avg Monthly Salary (ZAR)</label>
    <input type="number" id="salary" placeholder="0" />

    <button onclick="calculateCost()">Calculate</button>
  </div>

  <div class="results-box">
    <h2>Estimate</h2>
    <div id="resultsContent">Enter details and click calculate to see the estimated impact.</div>
    
    <div class="button-group" id="resultButtons">
      <button class="download-btn" onclick="downloadPDF()">Download PDF</button>
      <button class="reset-btn" onclick="window.location.reload()">Reset</button>
    </div>
  </div>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
<script>
function calculateCost() {
    const women = parseInt(document.getElementById('women').value) || 0;
    const men = parseInt(document.getElementById('men').value) || 0;
    const salary = parseFloat(document.getElementById('salary').value) || 0;

    const totalCases = (women * 0.03) + (men * 0.01);
    const lowCases = totalCases * 0.75;
    const medCases = totalCases * 0.20;
    const highCases = totalCases * 0.05;

    const lowCost = (salary * 0.33) * lowCases;
    const medCost = (salary * 1.43) * medCases;
    const highCost = (salary * 6.43) * highCases;
    const total = lowCost + medCost + highCost;

    const formatNum = (n) => Math.round(n).toLocaleString();
    const formatCur = (n) => 'R' + n.toLocaleString(undefined, {minimumFractionDigits: 2});

    document.getElementById('resultsContent').innerHTML = `
        <div class="results-line-item"><span>Est. Total Cases:</span><span>${formatNum(totalCases)}</span></div>
        <div class="results-line-item"><span>Low Severity (75%):</span><span>${formatNum(lowCases)}</span></div>
        <div class="results-line-item"><span>Med Severity (20%):</span><span>${formatNum(medCases)}</span></div>
        <div class="results-line-item"><span>High Severity (5%):</span><span>${formatNum(highCases)}</span></div>
        <div class="total-line"><span>Total Annual Cost:</span><span>${formatCur(total)}</span></div>
    `;
    document.getElementById('resultButtons').style.display = 'flex';
}

function downloadPDF() {
  const element = document.querySelector('.container');
  html2pdf().from(element).save('Cost_Estimate.pdf');
}
</script>
</body>
</html>
