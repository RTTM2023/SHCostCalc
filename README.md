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
      /* Prevents tiny horizontal shifts on mobile */
      overflow-x: hidden; 
    }

    .container {
      display: flex;
      flex-direction: column;
      padding: 1rem; /* Reduced padding for mobile */
      max-width: 1600px;
      margin: 0 auto;
      box-sizing: border-box;
      gap: 1.5rem; /* Adds space between boxes on mobile */
    }

    /* Side-by-side layout for Desktop (1024px and up) */
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
      }
    }

    .container, .calculator, .results-box {
      box-sizing: border-box;
    }

    .calculator, .results-box {
      background-color: white;
      padding: 1.5rem; /* Slightly smaller for mobile */
      border-radius: 20px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
      width: 100%; /* Ensures they take full width on mobile */
    }

    @media (min-width: 1024px) {
      .calculator, .results-box {
        padding: 2rem;
      }
    }

    .calculator {
      border: 2px solid #f10178;
    }

    .results-box {
      background-color: #f10178;
      color: white;
      height: auto;
      min-height: 300px; 
      align-self: flex-start;
    }

    .results-box h2 {
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
      font-size: 1.1rem;
      background-color: #f10178;
      color: white;
      border: none;
      border-radius: 30px;
      cursor: pointer;
      font-family: 'Montserrat', sans-serif;
    }

    .results-line-item {
      display: flex;
      justify-content: space-between;
      margin: 0.4rem 0;
      font-size: 0.75rem;
      gap: 10px; /* Space between text and numbers */
    }

    .results-line-item.bold {
      font-size: 0.9rem;
      font-weight: bold;
      margin-top: 1rem;
    }

    .half-line {
      border-top: 1px solid white;
      margin: 1rem 0;
      width: 50%;
    }

    .total-line {
      font-size: 1.1rem;
      font-weight: bold;
      margin: 1.5rem 0 1rem 0;
      display: flex;
      justify-content: space-between;
      border-top: 1px dotted white;
      border-bottom: 1px dotted white;
      padding: 0.7rem 0;
    }

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
      background-color: transparent !important;
    }

    /* Fixed tooltips on mobile so they don't cause overflow */
    .tooltip:hover::after {
      content: attr(data-tooltip);
      position: absolute;
      background: rgba(0, 0, 0, 0.9);
      color: #fff;
      padding: 0.6rem 0.8rem;
      border-radius: 5px;
      top: 120%;
      left: 50%;
      transform: translateX(-50%);
      display: block;
      max-width: 200px;
      width: max-content;
      min-width: 120px;
      white-space: normal;
      word-break: normal;
      font-size: 0.75rem;
      z-index: 999;
      box-sizing: border-box;
      text-align: left;
    }

    .button-group {
      display: none;
      flex-direction: column;
      gap: 0.75rem;
      margin-top: 1.5rem;
    }

    .download-btn, .reset-btn {
      background: white;
      color: #f10178;
      border: 1px dashed #5b01fa;
      font-size: 0.95rem;
      font-weight: 500;
      font-family: 'Montserrat', sans-serif;
      padding: 0.7rem 1rem;
      border-radius: 30px;
      cursor: pointer;
      text-align: center;
      width: 100%;
      box-sizing: border-box;
    }

    .reset-btn {
      background: #5b01fa;
      color: white;
    }

    .advanced-toggle {
      margin-top: 2rem;
      background: none;
      border: none;
      color: #fff;
      font-size: 0.9rem;
      font-weight: bold;
      cursor: pointer;
      text-align: left;
      padding: 0;
      display: none;
      text-decoration: underline;
    }

    .advanced-settings {
      display: none;
      margin-top: 1rem;
      background: rgba(255,255,255,0.1);
      padding: 1rem;
      border-radius: 15px;
      font-size: 0.7rem;
    }

    .advanced-settings p {
      display: flex;
      justify-content: space-between;
      margin-bottom: 0.2rem;
    }

    /* Enquiry Form Mobile Fixes */
    #enquiryForm input, #enquiryForm textarea {
      width: 100%;
      padding: 0.75rem;
      border-radius: 30px;
      border: 1px dashed #5b01fa;
      font-family: 'Montserrat', sans-serif;
      box-sizing: border-box;
    }

    @media print {
      .container { padding-top: 0 !important; flex-direction: row !important; }
      .button-group, .advanced-toggle, button { display: none !important; }
      .calculator { flex: 1 !important; margin-right: 1rem !important; }
      .results-box { flex: 1.8 !important; }
    }
  </style>
</head>
<body>
<div class="container">
  <div class="calculator">
    <h2>Sexual Harassment Cost Calculator</h2>
    <label for="women">Number of Women in Organisation <span class="tooltip" data-tooltip="Used to estimate the number of cases using an assumed rate of harassment."><img src="whiteback.png" alt="info icon" /></span></label>
    <input type="number" id="women" placeholder="0" />

    <label for="men">Number of Men in Organisation <span class="tooltip" data-tooltip="Used to estimate the number of cases using an assumed rate of harassment."><img src="whiteback.png" alt="info icon" /></span></label>
    <input type="number" id="men" placeholder="0" />

    <label for="salary">Average Gross Monthly Salary (ZAR) <span class="tooltip" data-tooltip="Used to estimate cost impact of each case"><img src="whiteback.png" alt="info icon" /></span></label>
    <input type="number" id="salary" placeholder="0" />

    <button onclick="calculateCost()">Calculate</button>
  </div>

  <div class="results-box">
    <h2>Estimated Cost</h2>
    <div id="resultsContent"></div>

    <button class="advanced-toggle" id="toggleBtn" onclick="toggleAdvanced()">Show/Hide Assumptions</button>
    <div class="advanced-settings" id="advancedSettings">
      <p><strong>Female Incidence Rate:</strong><span>3%</span></p>
      <p><strong>Male Incidence Rate:</strong><span>1%</span></p>
      <p><strong>Assumed Severity:</strong></p>
      <ul style="padding-left: 1.2rem; margin: 0.2rem 0;">
        <li>Low: 0.33 × salary</li>
        <li>Med: 1.43 × salary</li>
        <li>High: 6.43 × salary</li>
      </ul>
    </div>

    <div class="button-group" id="resultButtons">
      <button class="download-btn" onclick="downloadPDF()">Download PDF</button>
      <button class="download-btn" onclick="toggleEnquiry()">Enquiry</button>
    </div>

    <div id="enquiryForm" style="display: none; margin-top: 1rem;">
      <form action="https://formspree.io/f/manjzgjr" method="POST" style="display: flex; flex-direction: column; gap: 0.75rem;">
        <input type="text" name="name" placeholder="Your Name" required />
        <input type="text" name="organisation" placeholder="Organisation" required />
        <input type="email" name="email" placeholder="Email Address" required />
        <textarea name="message" readonly style="height: 60px;">I would like to find out more about your prevention programme.</textarea>
        <button type="submit" style="background-color: #ffb002; color: black;">Send Enquiry</button>
      </form>
    </div>

    <div id="resetButton" style="display: none; margin-top: 1.5rem;">
      <button class="reset-btn" onclick="window.location.reload()">Reset Calculator</button>
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
        <div class='results-line-item bold'><span>Estimated Total Cost:</span></div>
        <div class="total-line"><span>Annual Cost:</span><span>${formatCurrency(totalCost)}</span></div>
    `;

    document.getElementById('resultButtons').style.display = 'flex';
    document.getElementById('toggleBtn').style.display = 'inline-block';
    document.getElementById('resetButton').style.display = 'block';
}

function downloadPDF() {
  const element = document.querySelector('.container');
  const opt = {
    margin: 0.5,
    filename: 'Harassment_Cost_Estimate.pdf',
    image: { type: 'jpeg', quality: 0.98 },
    html2canvas: { scale: 2 },
    jsPDF: { unit: 'in', format: 'letter', orientation: 'portrait' }
  };
  html2pdf().set(opt).from(element).save();
}

function toggleAdvanced() {
    const section = document.getElementById('advancedSettings');
    section.style.display = section.style.display === 'none' || section.style.display === '' ? 'block' : 'none';
}

function toggleEnquiry() {
  const form = document.getElementById('enquiryForm');
  form.style.display = form.style.display === 'none' ? 'block' : 'none';
}
</script>
</body>
</html>
