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
      background-color: transparent;
      overflow-x: hidden;
    }

    .container {
      display: flex;
      flex-direction: column;
      padding: 1rem;
      max-width: 1600px;
      margin: 0 auto;
      box-sizing: border-box;
      gap: 1.5rem;
    }

    /* Desktop Layout: Restoring your original proportions */
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
        width: auto !important; /* Overrides the mobile 100% */
      }
      .results-box {
        flex: 1;
        width: auto !important; /* Overrides the mobile 100% */
        align-self: flex-start; /* Keeps it short until content expands it */
      }
    }

    .calculator, .results-box {
      background-color: white;
      padding: 2rem;
      border-radius: 20px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
      box-sizing: border-box;
      width: 100%; /* Default for mobile */
    }

    .calculator {
      border: 2px solid #f10178;
    }

    .results-box {
      background-color: #f10178;
      color: white;
      min-height: auto; /* Restored: Starts small */
    }

    h2 {
      font-size: 22px;
      margin-top: 0;
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
      border: 1px dashed #5b01fa;
      font-family: 'Montserrat', sans-serif;
      box-sizing: border-box;
    }

    button {
      margin-top: 1rem;
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

    /* The Mobile Wrap Fix: Only drops to vertical on tiny screens */
    .results-line-item {
      display: flex;
      justify-content: space-between;
      margin: 0.3rem 0;
      font-size: 0.75rem;
      gap: 10px;
      flex-wrap: wrap; /* Allows number to drop if no room */
    }

    .results-line-item.bold {
      font-size: 0.9rem;
      font-weight: bold;
    }

    .half-line {
      border-top: 1px solid white;
      margin: 1rem 0;
      width: 50%;
    }

    .total-line {
      font-size: 1.2rem;
      font-weight: bold;
      margin: 2rem 0 1rem 0;
      display: flex;
      justify-content: space-between;
      border-top: 1px dotted white;
      border-bottom: 1px dotted white;
      padding: 0.5rem 0;
      flex-wrap: wrap;
    }

    /* Restore Tooltips */
    .tooltip {
      position: relative;
      cursor: pointer;
      vertical-align: super;
    }
    .tooltip img {
      width: 16px;
      height: 16px;
      vertical-align: middle;
      margin-left: 4px;
      background-color: transparent !important;
    }
    .tooltip:hover::after {
      content: attr(data-tooltip);
      position: absolute;
      background: rgba(0, 0, 0, 0.85);
      color: #fff;
      padding: 0.6rem 0.8rem;
      border-radius: 5px;
      top: 120%;
      left: 50%;
      transform: translateX(-50%);
      display: block;
      max-width: 220px;
      width: max-content;
      font-size: 0.8rem;
      z-index: 999;
      box-sizing: border-box;
      text-align: left;
    }

    .button-group {
      display: none;
      flex-direction: column;
      gap: 0.5rem;
      margin-top: 1.5rem;
    }

    .download-btn, .reset-btn {
      background: white;
      color: #f10178;
      border: 1px dashed #5b01fa;
      font-size: 1rem;
      padding: 0.6rem 1rem;
      border-radius: 30px;
      cursor: pointer;
      text-align: center;
      box-sizing: border-box;
    }

    .reset-btn { background: #5b01fa; color: white; }

    /* Enquiry Form Styling */
    #enquiryForm form input, #enquiryForm textarea {
      width: 100%;
      padding: 0.75rem;
      border-radius: 30px;
      border: 1px dashed #5b01fa;
      margin-bottom: 10px;
      box-sizing: border-box;
      font-family: 'Montserrat', sans-serif;
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
    <label for="women">Number of Women in Organisation <span class="tooltip" data-tooltip="Used to estimate the number of cases using an assumed rate of harassment."><img src="whiteback.png" alt="info" /></span></label>
    <input type="number" id="women" placeholder="Enter total" />

    <label for="men">Number of Men in Organisation <span class="tooltip" data-tooltip="Used to estimate the number of cases using an assumed rate of harassment."><img src="whiteback.png" alt="info" /></span></label>
    <input type="number" id="men" placeholder="Enter total" />

    <label for="salary">Average Gross Monthly Salary (ZAR) <span class="tooltip" data-tooltip="Used to estimate cost impact of each case"><img src="whiteback.png" alt="info" /></span></label>
    <input type="number" id="salary" placeholder="Enter salary" />

    <button onclick="calculateCost()">Calculate</button>
  </div>

  <div class="results-box">
    <h2>Estimated Cost of Sexual Harassment</h2>
    <div id="resultsContent">Enter your details and click calculate to see the estimate.</div>

    <div class="button-group" id="resultButtons">
      <button class="download-btn" onclick="downloadPDF()">Download as PDF</button>
      <button class="download-btn" onclick="toggleEnquiry()">Enquire about our Solution</button>
      <button class="reset-btn" onclick="window.location.reload()">Reset Calculator</button>
    </div>

    <div id="enquiryForm" style="display: none; margin-top: 1rem;">
      <form action="https://formspree.io/f/manjzgjr" method="POST" style="display: flex; flex-direction: column;">
        <input type="text" name="name" placeholder="Your Name" required />
        <input type="email" name="email" placeholder="Email Address" required />
        <button type="submit" style="background-color: #ffb002; color: black;">Send Enquiry</button>
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

    const lowSeverityCost = (salary / 21.5) + (salary / 21.5) + 500;
    const medSeverityCost = ((salary / 21.5) * 5) + ((salary / 21.5) * 5) + (0.20 * 0.50 * salary * 12) + 10000;
    const highSeverityCost = ((salary / 21.5) * 20) + ((salary / 21.5) * 20) + (0.50 * salary * 12) + 200000;

    const totalCost = (lowCases * lowSeverityCost) + (medCases * medSeverityCost) + (highCases * highSeverityCost);

    const formatNumber = (num) => Math.round(num).toLocaleString('en-US');
    const formatCurrency = (num) => 'R' + num.toFixed(2).replace(/\B(?=(\d{3})+(?!\d))/g, ',');

    document.getElementById('resultsContent').innerHTML = `
        <div class='results-line-item bold'><span>Estimated Cases:</span><span>${formatNumber(totalCases)}</span></div>
        <div class='results-line-item'><span>Low Severity (75%):</span><span>${formatNumber(lowCases)}</span></div>
        <div class='results-line-item'><span>Medium Severity (20%):</span><span>${formatNumber(medCases)}</span></div>
        <div class='results-line-item'><span>High Severity (5%):</span><span>${formatNumber(highCases)}</span></div>
        <div class="half-line"></div>
        <div class='results-line-item bold'><span>Per Case Costs:</span></div>
        <div class='results-line-item'><span>Low Severity:</span><span>${formatCurrency(lowSeverityCost)}</span></div>
        <div class='results-line-item'><span>Med Severity:</span><span>${formatCurrency(medSeverityCost)}</span></div>
        <div class='results-line-item'><span>High Severity:</span><span>${formatCurrency(highSeverityCost)}</span></div>
        <div class="total-line"><span>Total Annual Cost:</span><span>${formatCurrency(totalCost)}</span></div>
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
