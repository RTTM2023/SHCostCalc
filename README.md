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
      padding: 0.8rem; /* Even smaller for mobile */
      max-width: 1600px;
      margin: 0 auto;
      gap: 1.5rem;
      box-sizing: border-box;
    }

    /* Desktop Layout */
    @media (min-width: 1024px) {
      .container {
        flex-direction: row;
        justify-content: space-between;
        padding: 2rem;
      }
      .calculator { flex: 1.3; margin-right: 2rem; }
      .results-box { flex: 1; }
      .results-line-item { flex-direction: row; align-items: center; }
    }

    .calculator, .results-box {
      background-color: white;
      padding: 1.2rem; /* Compact for mobile */
      border-radius: 20px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
      width: 100%;
      box-sizing: border-box;
    }

    .calculator { border: 2px solid #f10178; }
    .results-box {
      background-color: #f10178;
      color: white;
      height: auto;
      min-height: 300px; 
      align-self: flex-start;
    }

    /* MOBILE SPECIFIC: Make results wrap vertically if too wide */
    .results-line-item {
      display: flex;
      flex-direction: column; /* Stack label and price on mobile */
      margin: 0.6rem 0;
      font-size: 0.85rem;
      gap: 2px;
    }

    @media (min-width: 480px) {
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
      margin: 1.5rem 0;
      display: flex;
      justify-content: space-between;
      border-top: 1px dotted white;
      border-bottom: 1px dotted white;
      padding: 0.8rem 0;
    }

    label { font-weight: bold; display: block; margin-top: 1.5rem; }

    input[type="number"], input[type="text"], input[type="email"], textarea {
      width: 100%;
      box-sizing: border-box;
      padding: 0.7rem;
      font-size: 1rem;
      border-radius: 30px;
      border: 1px dashed #5b01fa;
      margin-top: 0.5rem;
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
    }

    .tooltip:hover::after {
      content: attr(data-tooltip);
      position: absolute;
      background: rgba(0,0,0,0.9);
      padding: 0.6rem;
      border-radius: 5px;
      width: 180px;
      font-size: 0.75rem;
      z-index: 999;
      left: 0;
    }

    .button-group { display: none; flex-direction: column; gap: 0.8rem; margin-top: 1.5rem; }
    .download-btn, .reset-btn {
      background: white; color: #f10178; border: 1px dashed #5b01fa;
      padding: 0.7rem; border-radius: 30px; cursor: pointer; width: 100%;
    }
    .reset-btn { background: #5b01fa; color: white; }

    #enquiryForm form { display: flex; flex-direction: column; gap: 0.75rem; }
    
    @media print {
      .container { flex-direction: row !important; }
      .button-group, .advanced-toggle, button { display: none !important; }
    }
  </style>
</head>
<body>
<div class="container">
  <div class="calculator">
    <h2>Sexual Harassment Cost Calculator</h2>
    <label for="women">Number of Women</label>
    <input type="number" id="women" placeholder="0" />
    <label for="men">Number of Men</label>
    <input type="number" id="men" placeholder="0" />
    <label for="salary">Avg Gross Monthly Salary (ZAR)</label>
    <input type="number" id="salary" placeholder="e.g. 25000" />
    <button onclick="calculateCost()">Calculate</button>
  </div>

  <div class="results-box">
    <h2>Estimated Cost</h2>
    <div id="resultsContent"></div>
    <div class="button-group" id="resultButtons">
      <button class="download-btn" onclick="downloadPDF()">Download as PDF</button>
      <button class="download-btn" onclick="toggleEnquiry()">Enquire about our Solution</button>
      <button class="reset-btn" onclick="window.location.reload()">Reset</button>
    </div>

    <div id="enquiryForm" style="display: none; margin-top: 1rem;">
      <form action="https://formspree.io/f/manjzgjr" method="POST">
        <input type="text" name="name" placeholder="Your Name" required />
        <input type="email" name="email" placeholder="Email" required />
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
    const medSeverityCost = ((salary / 21.5) * 10) + (0.1 * salary * 12) + 10000;
    const highSeverityCost = ((salary / 21.5) * 40) + (0.5 * salary * 12) + 200000;

    const totalCost = (lowCases * lowSeverityCost) + (medCases * medSeverityCost) + (highCases * highSeverityCost);

    const formatNumber = (num) => Math.round(num).toLocaleString();
    const formatCurrency = (num) => 'R' + num.toLocaleString(undefined, {minimumFractionDigits: 2, maximumFractionDigits: 2});

    document.getElementById('resultsContent').innerHTML = `
        <div class='results-line-item'><span>Estimated Cases:</span><span>${formatNumber(totalCases)}</span></div>
        <div class='results-line-item'><span>Low Severity (75%):</span><span>${formatNumber(lowCases)}</span></div>
        <div class='results-line-item'><span>Medium Severity (20%):</span><span>${formatNumber(medCases)}</span></div>
        <div class='results-line-item'><span>High Severity (5%):</span><span>${formatNumber(highCases)}</span></div>
        <div class="total-line"><span>Total Annual Cost:</span><span>${formatCurrency(totalCost)}</span></div>
    `;

    document.getElementById('resultButtons').style.display = 'flex';
}

function downloadPDF() {
  const container = document.querySelector('.container');
  const opt = {
    margin: 0.5,
    filename: 'Cost_Estimate.pdf',
    jsPDF: { unit: 'in', format: 'letter', orientation: 'portrait' }
  };
  html2pdf().set(opt).from(container).save();
}

function toggleEnquiry() {
  const form = document.getElementById('enquiryForm');
  form.style.display = form.style.display === 'none' ? 'block' : 'none';
}
</script>
</body>
</html>
