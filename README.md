<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Sexual Harassment Cost Calculator</title>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap" rel="stylesheet" />
  <style>
    /* 1. Global Reset to prevent width leakage */
    * {
      box-sizing: border-box;
    }

    body {
      font-family: 'Montserrat', sans-serif;
      margin: 0;
      background-color: transparent;
      overflow-x: hidden; /* Stops horizontal scrolling */
      width: 100%;
    }

    .container {
      display: flex;
      flex-direction: column;
      padding: 1rem;
      max-width: 1600px;
      margin: 0 auto;
      gap: 1.5rem;
    }

    /* 2. Desktop Layout (Restores side-by-side proportions) */
    @media (min-width: 1024px) {
      .container {
        flex-direction: row;
        justify-content: space-between;
        padding: 2rem;
        gap: 0;
      }
      .calculator {
        flex: 1.3;
        margin-right: 2rem;
      }
      .results-box {
        flex: 1;
        align-self: flex-start; /* Keeps it short on desktop until needed */
      }
    }

    .calculator, .results-box {
      background-color: white;
      padding: 1.5rem;
      border-radius: 20px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
      width: 100%;
    }

    .calculator {
      border: 2px solid #f10178;
    }

    .results-box {
      background-color: #f10178;
      color: white;
      min-height: auto;
    }

    h2 {
      font-size: 22px;
      margin-top: 0;
    }

    label {
      font-weight: bold;
      display: block;
      margin-top: 1.5rem;
      font-size: 0.95rem;
    }

    input[type="number"] {
      width: 100%;
      padding: 0.6rem;
      margin-top: 5px;
      font-size: 1rem;
      border-radius: 30px;
      border: 1px dashed #5b01fa;
      font-family: 'Montserrat', sans-serif;
    }

    button {
      margin-top: 1.5rem;
      width: 100%;
      padding: 1rem;
      font-size: 1.2rem;
      background-color: #f10178;
      color: white;
      border: none;
      border-radius: 30px;
      cursor: pointer;
      font-family: 'Montserrat', sans-serif;
    }

    /* 3. The Mobile Wrap Fix for Results */
    .results-line-item {
      display: flex;
      justify-content: space-between;
      flex-wrap: wrap; /* Allows text to drop to next line if screen is too narrow */
      margin: 0.5rem 0;
      font-size: 0.8rem;
      gap: 10px;
    }

    .results-line-item.bold {
      font-size: 0.95rem;
      font-weight: bold;
    }

    .total-line {
      font-size: 1.2rem;
      font-weight: bold;
      margin-top: 1.5rem;
      display: flex;
      justify-content: space-between;
      flex-wrap: wrap;
      border-top: 1px dotted white;
      border-bottom: 1px dotted white;
      padding: 0.8rem 0;
    }

    .half-line {
      border-top: 1px solid white;
      margin: 1rem 0;
      width: 50%;
    }

    /* 4. Restore Info Tooltips */
    .tooltip {
      position: relative;
      cursor: pointer;
      display: inline-block;
    }

    .tooltip img {
      width: 16px;
      height: 16px;
      vertical-align: middle;
      margin-left: 4px;
      background: transparent !important;
    }

    .tooltip:hover::after {
      content: attr(data-tooltip);
      position: absolute;
      background: rgba(0, 0, 0, 0.9);
      color: #fff;
      padding: 0.6rem;
      border-radius: 5px;
      bottom: 125%;
      left: 50%;
      transform: translateX(-50%);
      width: 200px;
      font-size: 0.75rem;
      z-index: 1000;
      text-align: left;
    }

    .button-group {
      display: none;
      flex-direction: column;
      gap: 0.8rem;
      margin-top: 1.5rem;
    }

    .download-btn, .reset-btn {
      background: white;
      color: #f10178;
      border: 1px dashed #5b01fa;
      padding: 0.7rem;
      border-radius: 30px;
      cursor: pointer;
      font-family: 'Montserrat', sans-serif;
      font-weight: 500;
    }

    .reset-btn { background: #5b01fa; color: white; }

    #enquiryForm form input, #enquiryForm textarea {
      width: 100%;
      padding: 0.7rem;
      border-radius: 20px;
      margin-bottom: 10px;
      border: 1px solid #ccc;
    }

    @media print {
      .container { flex-direction: row !important; }
      .button-group, button { display: none !important; }
    }
  </style>
</head>
<body>

<div class="container">
  <div class="calculator">
    <h2>Sexual Harassment Cost Calculator</h2>
    
    <label for="women">Number of Women in Organisation 
      <span class="tooltip" data-tooltip="Used to estimate cases based on assumed rate."><img src="whiteback.png" /></span>
    </label>
    <input type="number" id="women" placeholder="Enter number" />

    <label for="men">Number of Men in Organisation 
      <span class="tooltip" data-tooltip="Used to estimate cases based on assumed rate."><img src="whiteback.png" /></span>
    </label>
    <input type="number" id="men" placeholder="Enter number" />

    <label for="salary">Average Gross Monthly Salary (ZAR) 
      <span class="tooltip" data-tooltip="Used to calculate the impact cost per case."><img src="whiteback.png" /></span>
    </label>
    <input type="number" id="salary" placeholder="Enter amount" />

    <button onclick="calculateCost()">Calculate</button>
  </div>

  <div class="results-box">
    <h2>Estimated Cost of Sexual Harassment</h2>
    <div id="resultsContent">Results will appear here after calculation.</div>

    <div class="button-group" id="resultButtons">
      <button class="download-btn" onclick="downloadPDF()">Download as PDF</button>
      <button class="download-btn" onclick="toggleEnquiry()">Enquire about Solution</button>
      <button class="reset-btn" onclick="window.location.reload()">Reset Calculator</button>
    </div>

    <div id="enquiryForm" style="display: none; margin-top: 1.5rem;">
      <form action="https://formspree.io/f/manjzgjr" method="POST">
        <input type="text" name="name" placeholder="Your Name" required />
        <input type="email" name="email" placeholder="Email Address" required />
        <button type="submit" style="background-color: #ffb002; color: #000; padding: 0.8rem;">Send Enquiry</button>
      </form>
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

    const formatNum = (n) => Math.round(n).toLocaleString('en-US');
    const formatCur = (n) => 'R' + n.toLocaleString(undefined, {minimumFractionDigits: 2, maximumFractionDigits: 2});

    document.getElementById('resultsContent').innerHTML = `
        <div class="results-line-item bold"><span>Estimated Cases:</span><span>${formatNum(totalCases)}</span></div>
        <div class="results-line-item"><span>Low Severity (75%):</span><span>${formatNum(lowCases)}</span></div>
        <div class="results-line-item"><span>Med Severity (20%):</span><span>${formatNum(medCases)}</span></div>
        <div class="results-line-item"><span>High Severity (5%):</span><span>${formatNum(highCases)}</span></div>
        <div class="half-line"></div>
        <div class="total-line"><span>Total Annual Cost:</span><span>${formatCur(total)}</span></div>
    `;

    document.getElementById('resultButtons').style.display = 'flex';
}

function downloadPDF() {
  const element = document.querySelector('.container');
  html2pdf().from(element).save('Cost_Estimate.pdf');
}

function toggleEnquiry() {
  const form = document.getElementById('enquiryForm');
  form.style.display = form.style.display === 'none' ? 'block' : 'none';
}
</script>
</body>
</html>
