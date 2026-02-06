<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
  <title>Sexual Harassment Cost Calculator</title>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap" rel="stylesheet" />
  <style>
    /* 1. NUCLEAR RESET: Stop padding from adding to width */
    * {
      box-sizing: border-box;
      -webkit-tap-highlight-color: transparent;
    }

    body {
      font-family: 'Montserrat', sans-serif;
      margin: 0;
      padding: 0;
      background-color: transparent;
      overflow-x: hidden; /* Force hide horizontal scroll */
      width: 100vw;
    }

    .container {
      display: flex;
      flex-direction: column;
      padding: 10px; /* Minimal padding to keep it on screen */
      width: 100%;
      margin: 0 auto;
      gap: 20px;
    }

    /* 2. DESKTOP LOGIC: Proportions restored only for large screens */
    @media (min-width: 1024px) {
      .container {
        flex-direction: row;
        padding: 40px;
        max-width: 1600px;
      }
      .calculator {
        flex: 1.3;
        margin-right: 40px;
      }
      .results-box {
        flex: 1;
        align-self: flex-start; /* Keeps box short on desktop */
      }
    }

    .calculator, .results-box {
      background-color: #ffffff;
      padding: 20px;
      border-radius: 20px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
      width: 100%; /* Full width on mobile */
    }

    .calculator {
      border: 2px solid #f10178;
    }

    .results-box {
      background-color: #f10178;
      color: white;
    }

    h2 {
      font-size: 1.5rem;
      margin-top: 0;
      line-height: 1.2;
    }

    label {
      font-weight: bold;
      display: block;
      margin-top: 20px;
      font-size: 0.9rem;
    }

    input[type="number"] {
      width: 100%;
      padding: 12px;
      margin-top: 8px;
      border-radius: 30px;
      border: 1px dashed #5b01fa;
      font-family: 'Montserrat', sans-serif;
      font-size: 16px; /* Prevents iPhone zoom-in */
    }

    button {
      margin-top: 20px;
      width: 100%;
      padding: 15px;
      font-size: 1.1rem;
      font-weight: bold;
      background-color: #f10178;
      color: white;
      border: none;
      border-radius: 30px;
      cursor: pointer;
    }

    /* 3. THE MOBILE FIX: Stack results vertically so they can't overflow */
    .results-line-item {
      display: flex;
      flex-direction: column; /* Stack on mobile */
      margin-bottom: 12px;
      border-bottom: 1px solid rgba(255,255,255,0.2);
      padding-bottom: 8px;
    }

    @media (min-width: 600px) {
      .results-line-item {
        flex-direction: row;
        justify-content: space-between;
        border-bottom: none;
      }
    }

    .results-line-item span:first-child {
      font-size: 0.75rem;
      text-transform: uppercase;
      opacity: 0.9;
    }

    .results-line-item span:last-child {
      font-size: 1.1rem;
      font-weight: bold;
    }

    .total-line {
      margin-top: 20px;
      padding: 15px 0;
      border-top: 2px dotted white;
      border-bottom: 2px dotted white;
      display: flex;
      flex-direction: column;
      gap: 5px;
    }

    @media (min-width: 600px) {
      .total-line {
        flex-direction: row;
        justify-content: space-between;
      }
    }

    /* Tooltip Mobile Safety */
    .tooltip {
      display: inline-block;
      margin-left: 5px;
    }
    .tooltip img {
      width: 14px;
      height: 14px;
      background: transparent !important;
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
      background: white;
      color: #f10178;
      font-weight: bold;
      cursor: pointer;
    }

    .reset-btn {
      background: #5b01fa;
      color: white;
    }

    #enquiryForm form {
      display: flex;
      flex-direction: column;
      gap: 10px;
      margin-top: 20px;
    }

    #enquiryForm input {
      width: 100%;
      padding: 12px;
      border-radius: 30px;
      border: none;
    }
  </style>
</head>
<body>

<div class="container">
  <div class="calculator">
    <h2>Sexual Harassment Cost Calculator</h2>
    
    <label>Number of Women</label>
    <input type="number" id="women" placeholder="0" />

    <label>Number of Men</label>
    <input type="number" id="men" placeholder="0" />

    <label>Avg Monthly Salary (ZAR)</label>
    <input type="number" id="salary" placeholder="0" />

    <button onclick="calculateCost()">Calculate</button>
  </div>

  <div class="results-box">
    <h2>Estimated Cost</h2>
    <div id="resultsContent">Enter details to see results.</div>

    <div class="button-group" id="resultButtons">
      <button class="download-btn" onclick="downloadPDF()">Download PDF</button>
      <button class="download-btn" onclick="toggleEnquiry()">Enquire Now</button>
      <button class="reset-btn" onclick="window.location.reload()">Reset</button>
    </div>

    <div id="enquiryForm" style="display: none;">
      <form action="https://formspree.io/f/manjzgjr" method="POST">
        <input type="text" name="name" placeholder="Name" required />
        <input type="email" name="email" placeholder="Email" required />
        <button type="submit" style="background-color: #ffb002; color: #000;">Send</button>
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

    const formatNum = (n) => Math.round(n).toLocaleString();
    const formatCur = (n) => 'R' + n.toLocaleString(undefined, {minimumFractionDigits: 2, maximumFractionDigits: 2});

    document.getElementById('resultsContent').innerHTML = `
        <div class="results-line-item"><span>Est. Total Cases</span><span>${formatNum(totalCases)}</span></div>
        <div class="results-line-item"><span>Low Severity (75%)</span><span>${formatNum(lowCases)}</span></div>
        <div class="results-line-item"><span>Med Severity (20%)</span><span>${formatNum(medCases)}</span></div>
        <div class="results-line-item"><span>High Severity (5%)</span><span>${formatNum(highCases)}</span></div>
        <div class="total-line"><span>TOTAL ANNUAL COST</span><span>${formatCur(total)}</span></div>
    `;

    document.getElementById('resultButtons').style.display = 'flex';
}

function downloadPDF() {
  const element = document.querySelector('.container');
  html2pdf().from(element).save('Cost_Estimate.pdf');
}

function toggleEnquiry() {
  const f = document.getElementById('enquiryForm');
  f.style.display = f.style.display === 'none' ? 'block' : 'none';
}
</script>

</body>
</html>
