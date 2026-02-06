<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0" />
  <title>Sexual Harassment Cost Calculator</title>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap" rel="stylesheet" />
  <style>
    /* 1. Prevent any element from exceeding screen width */
    * {
      box-sizing: border-box;
      max-width: 100%; 
    }
    /* Removes the GitHub auto-generated header and title line */
header, 
#header,
.site-header,
h1:first-of-type {
  display: none !important;
}

/* If the blue text is wrapped in a specific GitHub ID */
#title-with-line {
  display: none !important;
}

    body {
      font-family: 'Montserrat', sans-serif;
      margin: 0;
      padding: 0;
      background-color: transparent;
      overflow-x: hidden;
      width: 100%;
    }

    .container {
      display: flex;
      flex-direction: column;
      padding: 15px;
      width: 100%;
      margin: 0 auto;
      gap: 20px;
    }

    /* 2. Desktop Proportions: Only triggers on screens wider than 1024px */
    @media (min-width: 1024px) {
      .container {
        flex-direction: row;
        justify-content: space-between;
        padding: 2rem;
        max-width: 1600px;
      }
      .calculator {
        flex: 1.3;
        margin-right: 2rem;
      }
      .results-box {
        flex: 1;
        align-self: flex-start; /* Keeps it shorter than calc box */
      }
    }

    .calculator, .results-box {
      background-color: white;
      padding: 20px;
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
      word-wrap: break-word; /* Forces long text to wrap */
    }

    h2 {
      font-size: 1.4rem;
      margin-top: 0;
      line-height: 1.2;
    }

    label {
      font-weight: bold;
      display: block;
      margin-top: 1.5rem;
      font-size: 0.9rem;
    }

    input[type="number"] {
      width: 100%;
      padding: 12px;
      margin-top: 8px;
      font-size: 16px; /* Best for mobile keyboard inputs */
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

    /* 3. The Result Items Fix: Force Wrap */
    .results-line-item {
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
      margin: 10px 0;
      font-size: 0.8rem;
      gap: 15px;
      flex-wrap: wrap; /* Allows label/value to stack if screen is too small */
    }

    .results-line-item span:first-child {
      flex: 1;
      min-width: 150px; /* Ensures text gets enough room before wrapping */
    }

    .results-line-item.bold {
      font-size: 0.95rem;
      font-weight: bold;
    }

    .total-line {
      font-size: 1.1rem;
      font-weight: bold;
      margin-top: 20px;
      display: flex;
      justify-content: space-between;
      flex-wrap: wrap;
      border-top: 1px dotted white;
      border-bottom: 1px dotted white;
      padding: 10px 0;
    }

    .half-line {
      border-top: 1px solid white;
      margin: 15px 0;
      width: 50%;
    }

    /* 4. Info Tags (Tooltips) - Mobile Optimized */
    .tooltip {
      position: relative;
      cursor: pointer;
      display: inline-block;
    }

    .tooltip img {
      width: 16px;
      height: 16px;
      vertical-align: middle;
      margin-left: 5px;
      background: transparent !important;
    }

    .tooltip:hover::after {
      content: attr(data-tooltip);
      position: absolute;
      background: rgba(0, 0, 0, 0.95);
      color: #fff;
      padding: 10px;
      border-radius: 8px;
      bottom: 130%;
      left: 50%;
      transform: translateX(-50%);
      width: 220px;
      font-size: 0.75rem;
      z-index: 9999;
      text-align: left;
      pointer-events: none;
    }

    .button-group {
      display: none;
      flex-direction: column;
      gap: 10px;
      margin-top: 20px;
    }

    .download-btn, .reset-btn {
      background: white;
      color: #f10178;
      border: 1px dashed #5b01fa;
      padding: 12px;
      border-radius: 30px;
      cursor: pointer;
      font-weight: bold;
      text-align: center;
      text-decoration: none;
    }

    .reset-btn { background: #5b01fa; color: white; }

    #enquiryForm form input, #enquiryForm textarea {
      width: 100%;
      padding: 12px;
      border-radius: 25px;
      margin-bottom: 10px;
      border: 1px solid #ccc;
      font-family: 'Montserrat', sans-serif;
    }
  </style>
</head>
<body>

<div class="container">
  <div class="calculator">
    <h2>Sexual Harassment Cost Calculator</h2>
    
    <label for="women">Number of Women in Organisation 
      <span class="tooltip" data-tooltip="We use a conservative 3% incidence rate for females."><img src="whiteback.png" /></span>
    </label>
    <input type="number" id="women" placeholder="0" />

    <label for="men">Number of Men in Organisation 
      <span class="tooltip" data-tooltip="We use a conservative 1% incidence rate for males."><img src="whiteback.png" /></span>
    </label>
    <input type="number" id="men" placeholder="0" />

    <label for="salary">Average Gross Monthly Salary (ZAR) 
      <span class="tooltip" data-tooltip="This is used to calculate the time and productivity loss per case."><img src="whiteback.png" /></span>
    </label>
    <input type="number" id="salary" placeholder="0" />

    <button onclick="calculateCost()">Calculate</button>
  </div>

  <div class="results-box">
    <h2>Estimated Cost of Sexual Harassment</h2>
    <div id="resultsContent">Results will appear here once you calculate.</div>

    <div class="button-group" id="resultButtons">
      <button class="download-btn" onclick="downloadPDF()">Download PDF</button>
      <button class="download-btn" onclick="toggleEnquiry()">Enquire Now</button>
      <button class="reset-btn" onclick="window.location.reload()">Reset</button>
    </div>

    <div id="enquiryForm" style="display: none; margin-top: 20px;">
      <form action="https://formspree.io/f/manjzgjr" method="POST">
        <input type="text" name="name" placeholder="Name" required />
        <input type="email" name="email" placeholder="Email" required />
        <button type="submit" style="background-color: #ffb002; color: #000;">Send Enquiry</button>
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
