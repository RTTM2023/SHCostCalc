<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0" />
  <title>Sexual Harassment Cost Calculator</title>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap" rel="stylesheet" />
  <style>
    /* 1. Global Mobile Fixes */
    * { box-sizing: border-box; max-width: 100%; }
    
    header, #header, .site-header, h1:first-of-type, #title-with-line {
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

    /* 2. Desktop Layout (1024px+) */
    @media (min-width: 1024px) {
      .container {
        flex-direction: row;
        justify-content: space-between;
        padding: 2rem;
        max-width: 1600px;
      }
      .calculator { flex: 1.3; margin-right: 2rem; }
      .results-box { flex: 1; align-self: flex-start; }
    }

    .calculator, .results-box {
      background-color: white;
      padding: 20px;
      border-radius: 20px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
      width: 100%;
    }

    .calculator { border: 2px solid #f10178; }

    .results-box {
      background-color: #f10178;
      color: white;
      word-wrap: break-word;
      min-height: 300px;
    }

    h2 { font-size: 1.4rem; margin-top: 0; line-height: 1.2; }

    label {
      font-weight: bold;
      display: block;
      margin-top: 1.5rem;
      font-size: 0.9rem;
    }

    input[type="number"], input[type="text"], input[type="email"], textarea {
      width: 100%;
      padding: 12px;
      margin-top: 8px;
      font-size: 16px; 
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

    /* 3. Results List Styles */
    .results-line-item {
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
      margin: 8px 0;
      font-size: 0.75rem;
      gap: 10px;
    }

    .results-line-item.bold { font-size: 0.9rem; font-weight: bold; }

    .total-line {
      font-size: 1.15rem;
      font-weight: bold;
      margin: 20px 0;
      display: flex;
      justify-content: space-between;
      border-top: 1px dotted white;
      border-bottom: 1px dotted white;
      padding: 10px 0;
    }

    .half-line { border-top: 1px solid white; margin: 15px 0; width: 50%; }

    /* 4. Tooltips - Mobile Friendly */
    .tooltip { position: relative; cursor: pointer; display: inline-block; }
    .tooltip img { width: 16px; height: 16px; vertical-align: middle; margin-left: 4px; }
    
    .tooltip:hover::after {
      content: attr(data-tooltip);
      position: absolute;
      background: rgba(0, 0, 0, 0.9);
      color: #fff;
      padding: 10px;
      border-radius: 8px;
      bottom: 125%;
      left: 50%;
      transform: translateX(-50%);
      width: 200px;
      font-size: 0.75rem;
      z-index: 999;
    }

    .button-group { display: none; flex-direction: column; gap: 10px; margin-top: 20px; }
    
    .download-btn, .reset-btn {
      background: white; color: #f10178; border: 1px dashed #5b01fa;
      padding: 12px; border-radius: 30px; font-weight: bold; text-align: center;
    }
    .reset-btn { background: #5b01fa; color: white; }

    .advanced-toggle {
      background: none; border: none; color: #fff; text-decoration: underline;
      font-weight: bold; cursor: pointer; display: none; margin-top: 15px; padding: 0;
    }

    .advanced-settings {
      display: none; background: rgba(255,255,255,0.1);
      padding: 15px; border-radius: 15px; font-size: 0.75rem; margin-top: 10px;
    }
    .advanced-settings p { display: flex; justify-content: space-between; margin: 5px 0; }
  </style>
</head>
<body>

<div class="container">
  <div class="calculator">
    <h2>Sexual Harassment Cost Calculator</h2>
    
    <label for="women">Number of Women in Organisation 
      <span class="tooltip" data-tooltip="Used to estimate the number of cases using an assumed rate of harassment."><img src="whiteback.png" /></span>
    </label>
    <input type="number" id="women" placeholder="0" />

    <label for="men">Number of Men in Organisation 
      <span class="tooltip" data-tooltip="Used to estimate the number of cases using an assumed rate of harassment."><img src="whiteback.png" /></span>
    </label>
    <input type="number" id="men" placeholder="0" />

    <label for="salary">Average Gross Monthly Salary (ZAR) 
      <span class="tooltip" data-tooltip="Used to estimate cost impact of each case"><img src="whiteback.png" /></span>
    </label>
    <input type="number" id="salary" placeholder="0" />

    <button onclick="calculateCost()">Calculate</button>
  </div>

  <div class="results-box">
    <h2>Estimated Cost of Sexual Harassment</h2>
    <div id="resultsContent">Enter details to see calculations.</div>

    <button class="advanced-toggle" id="toggleBtn" onclick="toggleAdvanced()">Show/Hide Assumptions</button>
    
    <div class="advanced-settings" id="advancedSettings">
      <p><strong>Female Incidence Rate:</strong> <span>3%</span></p>
      <p><strong>Male Incidence Rate:</strong> <span>1%</span></p>
      <p><strong>Severity Split:</strong> 75 / 20 / 5 %</p>
      <p><strong>Assumed Costs:</strong></p>
      <ul style="padding-left: 15px; margin: 5px 0;">
        <li>Low: 0.33 × Salary</li>
        <li>Med: 1.43 × Salary</li>
        <li>High: 6.43 × Salary</li>
      </ul>
    </div>

    <div class="button-group" id="resultButtons">
      <button class="download-btn" onclick="downloadPDF()">Download as PDF</button>
      <button class="download-btn" onclick="toggleEnquiry()">Enquire about our Solution</button>
    </div>

    <div id="enquiryForm" style="display: none; margin-top: 15px;">
      <form action="https://formspree.io/f/manjzgjr" method="POST" style="display: flex; flex-direction: column; gap: 10px;">
        <input type="text" name="name" placeholder="Your Name" required />
        <input type="text" name="organisation" placeholder="Organisation" required />
        <input type="email" name="email" placeholder="Email Address" required />
        <textarea name="message" readonly style="height: 80px; border-radius: 15px;">I would like to find out more about your sexual harassment prevention programme.</textarea>
        <button type="submit" style="background-color: #ffb002; color: black; margin-top: 5px;">Send Enquiry</button>
      </form>
    </div>

    <div id="resetButton" style="display: none; margin-top: 15px;">
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

    // RESTORED ORIGINAL FORMULAS
    const totalCases = (women * 0.03) + (men * 0.01);
    const lowCases = totalCases * 0.75;
    const medCases = totalCases * 0.20;
    const highCases = totalCases * 0.05;

    const lowSeverityCost = (salary / 21.5) + (salary / 21.5) + 500;
    const medSeverityCost = ((salary / 21.5) * 5) + ((salary / 21.5) * 5) + (0.20 * 0.50 * salary * 12) + 10000;
    const highSeverityCost = ((salary / 21.5) * 20) + ((salary / 21.5) * 20) + (0.50 * salary * 12) + 200000;

    const totalLowCost = lowCases * lowSeverityCost;
    const totalMedCost = medCases * medSeverityCost;
    const totalHighCost = highCases * highSeverityCost;
    const totalCost = totalLowCost + totalMedCost + totalHighCost;

    const formatNumber = (num) => Math.round(num).toLocaleString('en-US');
    const formatCurrency = (num) => 'R' + num.toFixed(2).replace(/\B(?=(\d{3})+(?!\d))/g, ',');

    document.getElementById('resultsContent').innerHTML = `
        <div class='results-line-item bold'><span>Estimated Cases:</span><span>${formatNumber(totalCases)}</span></div>
        <div class='results-line-item'><span>Low Severity (75%):</span><span>${formatNumber(lowCases)}</span></div>
        <div class='results-line-item'><span>Med Severity (20%):</span><span>${formatNumber(medCases)}</span></div>
        <div class='results-line-item'><span>High Severity (5%):</span><span>${formatNumber(highCases)}</span></div>
        <div class="half-line"></div>
        <div class='results-line-item bold'><span>Costs Per Case:</span></div>
        <div class='results-line-item'><span>Low:</span><span>${formatCurrency(lowSeverityCost)}</span></div>
        <div class='results-line-item'><span>Med:</span><span>${formatCurrency(medSeverityCost)}</span></div>
        <div class='results-line-item'><span>High:</span><span>${formatCurrency(highSeverityCost)}</span></div>
        <div class="total-line"><span>Total Annual Cost:</span><span>${formatCurrency(totalCost)}</span></div>
    `;

    document.getElementById('resultButtons').style.display = 'flex';
    document.getElementById('toggleBtn').style.display = 'block';
    document.getElementById('resetButton').style.display = 'block';
}

function toggleAdvanced() {
    const section = document.getElementById('advancedSettings');
    section.style.display = (section.style.display === 'none' || section.style.display === '') ? 'block' : 'none';
}

function toggleEnquiry() {
    const form = document.getElementById('enquiryForm');
    form.style.display = (form.style.display === 'none') ? 'block' : 'none';
}

function downloadPDF() {
    const element = document.querySelector('.container');
    const opt = {
        margin: [0.5, 0.5],
        filename: 'Harassment_Cost_Report.pdf',
        image: { type: 'jpeg', quality: 0.98 },
        html2canvas: { scale: 2, useCORS: true },
        jsPDF: { unit: 'in', format: 'letter', orientation: 'portrait' }
    };
    html2pdf().set(opt).from(element).save();
}
</script>
</body>
</html>
