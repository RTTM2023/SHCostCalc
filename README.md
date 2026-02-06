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
      overflow-x: hidden; /* This kills the side-scroll */
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

    /* Desktop Proportions Logic */
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
        align-self: flex-start; /* Keeps it shorter until filled */
      }
    }

    .calculator, .results-box {
      background-color: white;
      padding: 1.5rem;
      border-radius: 20px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
      box-sizing: border-box;
      width: 100%;
    }

    @media (min-width: 1024px) {
      .calculator, .results-box { padding: 2rem; }
    }

    .calculator { border: 2px solid #f10178; }

    .results-box {
      background-color: #f10178;
      color: white;
    }

    h2 { font-size: 22px; margin-top: 0; }
    label { font-weight: bold; display: block; margin-top: 1.5rem; }

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

    /* THE FIX: Vertical stack for results on mobile */
    .results-line-item {
      display: flex;
      flex-direction: column; /* Stack on mobile */
      margin: 0.8rem 0;
      font-size: 0.8rem;
      gap: 4px;
    }

    /* Side-by-side for results on tablets/desktop */
    @media (min-width: 600px) {
      .results-line-item {
        flex-direction: row;
        justify-content: space-between;
      }
    }

    .results-line-item span:last-child {
      font-weight: bold;
    }

    .total-line {
      font-size: 1.1rem;
      font-weight: bold;
      margin: 1.5rem 0 1rem 0;
      display: flex;
      flex-direction: column; /* Stack total cost on mobile */
      gap: 10px;
      border-top: 1px dotted white;
      border-bottom: 1px dotted white;
      padding: 0.8rem 0;
    }

    @media (min-width: 600px) {
      .total-line { flex-direction: row; justify-content: space-between; }
    }

    .half-line { border-top: 1px solid white; margin: 1rem 0; width: 50%; }

    /* Tooltip Fix */
    .tooltip { position: relative; cursor: pointer; }
    .tooltip img { width: 16px; height: 16px; vertical-align: middle; }
    .tooltip:hover::after {
      content: attr(data-tooltip);
      position: absolute;
      background: rgba(0, 0, 0, 0.9);
      padding: 0.8rem;
      border-radius: 5px;
      width: 180px;
      font-size: 0.75rem;
      z-index: 100;
      top: 25px;
      left: 0;
    }

    .button-group { display: none; flex-direction: column; gap: 0.5rem; margin-top: 1.5rem; }
    .download-btn, .reset-btn {
      background: white; color: #f10178; border: 1px dashed #5b01fa;
      padding: 0.7rem; border-radius: 30px; width: 100%; cursor: pointer;
    }
    .reset-btn { background: #5b01fa; color: white; }

    #enquiryForm form input, #enquiryForm textarea {
      width: 100%; padding: 0.75rem; border-radius: 30px; margin-bottom: 10px; box-sizing: border-box;
    }
  </style>
</head>
<body>

<div class="container">
  <div class="calculator">
    <h2>Sexual Harassment Cost Calculator</h2>
    <label for="women">Number of Women <span class="tooltip" data-tooltip="Based on assumed incidence rate."><img src="whiteback.png" /></span></label>
    <input type="number" id="women" placeholder="0" />

    <label for="men">Number of Men <span class="tooltip" data-tooltip="Based on assumed incidence rate."><img src="whiteback.png" /></span></label>
    <input type="number" id="men" placeholder="0" />

    <label for="salary">Avg Gross Monthly Salary (ZAR) <span class="tooltip" data-tooltip="Used to estimate case impact."><img src="whiteback.png" /></span></label>
    <input type="number" id="salary" placeholder="0" />

    <button onclick="calculateCost()">Calculate</button>
  </div>

  <div class="results-box">
    <h2>Estimated Cost</h2>
    <div id="resultsContent">Enter details and click calculate.</div>

    <div class="button-group" id="resultButtons">
      <button class="download-btn" onclick="downloadPDF()">Download as PDF</button>
      <button class="download-btn" onclick="toggleEnquiry()">Enquire about Solution</button>
      <button class="reset-btn" onclick="window.location.reload()">Reset Calculator</button>
    </div>

    <div id="enquiryForm" style="display: none; margin-top: 1rem;">
      <form action="https://formspree.io/f/manjzgjr" method="POST">
        <input type="text" name="name" placeholder="Name" required />
        <input type="email" name="email" placeholder="Email" required />
        <button type="submit" style="background-color: #ffb002; color: black; border-radius: 30px; padding: 1rem; border: none; cursor: pointer;">Send Enquiry</button>
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

    const lowSeverityCost = (salary * 0.33) + 500;
    const medSeverityCost = (salary * 1.43) + 10000;
    const highSeverityCost = (salary * 6.43) + 200000;

    const totalCost = (lowCases * lowSeverityCost) + (medCases * medSeverityCost) + (highCases * highSeverityCost);

    const formatNumber = (num) => Math.round(num).toLocaleString('en-US');
    const formatCurrency = (num) => 'R' + num.toFixed(2).replace(/\B(?=(\d{3})+(?!\d))/g, ',');

    document.getElementById('resultsContent').innerHTML = `
        <div class='results-line-item'><span>Estimated Cases:</span><span>${formatNumber(totalCases)}</span></div>
        <div class='results-line-item'><span>Low Severity (75%):</span><span>${formatNumber(lowCases)}</span></div>
        <div class='results-line-item'><span>Med Severity (20%):</span><span>${formatNumber(medCases)}</span></div>
        <div class='results-line-item'><span>High Severity (5%):</span><span>${formatNumber(highCases)}</span></div>
        <div class="half-line"></div>
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
