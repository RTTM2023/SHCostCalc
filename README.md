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
}
    .container {
      display: flex;
      flex-direction: column;
      padding: 2rem;
      max-width: 1600px;
      margin: 0 auto;
    }
    .container,
.calculator,
.results-box {
  box-sizing: border-box;
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
      flex: 1.3;
      margin-right: 2rem;
      border: 2px solid #f10178;
    }
.results-box {
  flex: 1;
  background-color: #f10178;
  color: white;
  height: auto;
  min-height: 300px; 
  align-self: flex-start;
}
    .results-box h2 {
      font-size: 22px;
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
    .results-line-item {
      display: flex;
      justify-content: space-between;
      margin: 0.15rem 0;
      font-size: 0.75rem;
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
}
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
    .button-group {
      display: none;
      flex-direction: column;
      gap: 0.5rem;
      margin-top: 1.5rem;
    }
    .download-btn, .reset-btn, .source-btn {
      background: white;
      color: #f10178;
      border: 1px dashed #5b01fa;
      font-size: 1rem;
      font-weight: 500;
      font-family: 'Montserrat', sans-serif;
      padding: 0.6rem 1rem;
      border-radius: 30px;
      cursor: pointer;
      text-align: center;
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
      font-size: 1rem;
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
      font-size: 0.75rem;
    }
    .advanced-settings p {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 0.1rem;
    }
    .advanced-settings ul {
      padding-left: 2rem;
      margin-top: 0.25rem;
    }
    .advanced-settings li {
      margin-bottom: 0.1rem;
      font-size: inherit;
    }
    .tooltip img {
  background-color: transparent !important;
}
    .assumption-description {
  font-weight: normal;
  font-size: 0.85rem;
  display: block;
  margin-top: 0.25rem;
}
    header, h1 {
  display: none !important;
}
    .advanced-settings strong {
  text-decoration: underline;
}
@media print {
  .container {
    padding-top: 0 !important;
  }
}
@media print {
  .button-group,
  .advanced-toggle,
  button {
    display: none !important;
  }
}
@media print {
  .calculator {
    flex: 1 !important;
    margin-right: 1rem !important;
  }

  .results-box {
    flex: 1.8 !important;
  }
}

  </style>
</head>
<body>
<div class="container">
  <div class="calculator">
    <h2>Sexual Harassment Cost Calculator</h2>
    <label for="women">Number of Women in Organisation <span class="tooltip" data-tooltip="Conservative rate based on international benchmarks"><img src="whiteback.png" alt="info icon" /></span></label>
    <input type="number" id="women" />

    <label for="men">Number of Men in Organisation <span class="tooltip" data-tooltip="Conservative rate based on international benchmarks"><img src="whiteback.png" alt="info icon" /></span></label>
    <input type="number" id="men" />

    <label for="salary">Average Gross Monthly Salary (ZAR) <span class="tooltip" data-tooltip="Used to estimate cost impact of each case"><img src="whiteback.png" alt="info icon" /></span></label>
    <input type="number" id="salary" />

    <button onclick="calculateCost()">Calculate</button>
  </div>

  <div class="results-box">
    <h2>Estimated Cost of Sexual Harassment</h2>
    <div id="resultsContent"></div>

    <button class="advanced-toggle" id="toggleBtn" onclick="toggleAdvanced()">Show/Hide Assumptions</button>
    <div class="advanced-settings" id="advancedSettings">
<p><strong>Female Incidence Rate:</strong><span>3% <span class="tooltip" data-tooltip="Conservative rate based on international benchmarks"><img src="whiteback.png" alt="info icon" /></span></span></p>
<p><strong>Male Incidence Rate:</strong><span>1% <span class="tooltip" data-tooltip="Conservative rate based on international benchmarks"><img src="whiteback.png" alt="info icon" /></span></span></p>
<p><strong>Severity of Cases Split (75/20/5):</strong></p>
<p style="font-size: inherit; font-weight: normal; margin-bottom: 0.1rem; margin-left: 1rem;">These percentages are based on assumptions about how common each severity level is likely to be.</p>
      <p><strong>Assumed Cost of Severity:</strong></p>
      <ul>
        <li>Low = 0.33 × ave. gross monthly salary <span class="tooltip" data-tooltip="Absenteeism, presenteeism, minor team disruption"><img src="whiteback.png" alt="info icon" /></span></li>
        <li>Med. = 1.43 × ave. gross monthly salary <span class="tooltip" data-tooltip="HR case involvement, exit risk, longer disruption"><img src="whiteback.png" alt="info icon" /></span></li>
        <li>High = 6.43 × ave. gross monthly salary <span class="tooltip" data-tooltip="Legal risk, reputational damage, settlement costs"><img src="whiteback.png" alt="info icon" /></span></li>
      </ul>
    </div>

    <div class="button-group" id="resultButtons">
      <button class="download-btn" onclick="downloadPDF()">Download as PDF</button>
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

    // Calculate total expected cases (matches Excel formula =B1*E1+B2*E2)
    const femaleRate = 0.03;
    const maleRate = 0.01;
    const totalCases = (women * femaleRate) + (men * maleRate);

    // Calculate severity distribution (matches Excel percentages)
    const lowCases = totalCases * 0.75;
    const medCases = totalCases * 0.20;
    const highCases = totalCases * 0.05;

    // Calculate cost per severity level (matches Excel 'Severity Case Table' sheet)
    const lowSeverityCost = (salary / 21.5) + (salary / 21.5) + 500;
    const medSeverityCost = ((salary / 21.5) * 5) + ((salary / 21.5) * 5) + (0.20 * 0.50 * salary * 12) + 10000;
    const highSeverityCost = ((salary / 21.5) * 20) + ((salary / 21.5) * 20) + (0.50 * salary * 12) + 200000;

    // Calculate total costs (matches Excel formula =B6*E4+B7*E5+B8*E6)
    const totalLowCost = lowCases * lowSeverityCost;
    const totalMedCost = medCases * medSeverityCost;
    const totalHighCost = highCases * highSeverityCost;
    const totalCost = totalLowCost + totalMedCost + totalHighCost;

    // Formatting functions
    const formatNumber = (num) => Math.round(num).toLocaleString('en-US');
const formatCurrency = (num) => 'R' + num.toFixed(2).replace(/\B(?=(\d{3})+(?!\d))/g, ',');

    document.getElementById('resultsContent').innerHTML = `
        <div class='results-line-item bold'><span>Estimated Cases:</span><span>${formatNumber(totalCases)}</span></div>
        <div class='results-line-item'><span>Low Severity Cases (75% of ${formatNumber(totalCases)}):<span class="tooltip" data-tooltip="Unreported and minor cases"><img src="whiteback.png" alt="info icon" /></span></span><span>${formatNumber(lowCases)}</span></div>
        <div class='results-line-item'><span>Medium Severity Cases (20% of ${formatNumber(totalCases)}):<span class="tooltip" data-tooltip="Internally reported and resolved"><img src="whiteback.png" alt="info icon" /></span></span><span>${formatNumber(medCases)}</span></div>
        <div class='results-line-item'><span>High Severity Cases (5% of ${formatNumber(totalCases)}):<span class="tooltip" data-tooltip="Escalated and potential legal cases"><img src="whiteback.png" alt="info icon" /></span></span><span>${formatNumber(highCases)}</span></div>
        <div class="half-line"></div>
        <div class='results-line-item bold'><span>Estimated Costs:</span></div>
        <div class='results-line-item'><span>Low Severity Cost (per case):<span class="tooltip" data-tooltip="Absenteeism, presenteeism, minor team disruption @ 33% of Average Gross Monthly Salary"><img src="whiteback.png" alt="info icon" /></span></span><span>${formatCurrency(lowSeverityCost)}</span></div>
        <div class='results-line-item'><span>Medium Severity Cost (per case):<span class="tooltip" data-tooltip="HR case involvement, exit risk, longer disruption @ 143% of Average Gross Monthly Salary"><img src="whiteback.png" alt="info icon" /></span></span><span>${formatCurrency(medSeverityCost)}</span></div>
        <div class='results-line-item'><span>High Severity Cost (per case):<span class="tooltip" data-tooltip="Legal risk, reputational damage, settlement costs @ 643% of Average Gross Monthly Salary"><img src="whiteback.png" alt="info icon" /></span></span><span>${formatCurrency(highSeverityCost)}</span></div>
        <div class="half-line"></div>
        <div class='results-line-item'><span>Total Low Severity Cost:</span><span>${formatCurrency(totalLowCost)}</span></div>
        <div class='results-line-item'><span>Total Medium Severity Cost:</span><span>${formatCurrency(totalMedCost)}</span></div>
        <div class='results-line-item'><span>Total High Severity Cost:</span><span>${formatCurrency(totalHighCost)}</span></div>
        <div class="total-line"><span>Total Annual Cost:</span><span>${formatCurrency(totalCost)}</span></div>
    `;

    document.getElementById('resultButtons').style.display = 'flex';
    document.getElementById('toggleBtn').style.display = 'inline-block';
}
  
function downloadPDF() {
  const container = document.querySelector('.container');
  const assumptions = document.getElementById('advancedSettings');
  const toggleBtn = document.getElementById('toggleBtn');
  const calculator = document.querySelector('.calculator');
  const resultsBox = document.querySelector('.results-box');

  // Save current styles
  const previousAssumptionDisplay = assumptions.style.display;
  const previousToggleDisplay = toggleBtn.style.display;
const prevCalculatorFlex = calculator.style.flex;
const prevResultsFlex = resultsBox.style.flex;
const prevCalculatorMargin = calculator.style.marginRight;

  // Show assumptions and hide toggle
  assumptions.style.display = 'block';
  toggleBtn.style.display = 'none';

  // Resize boxes for PDF
calculator.style.flex = '1.2';
resultsBox.style.flex = '1.6';
calculator.style.marginRight = '1rem';

  // Hide buttons
  document.querySelectorAll('.results-box button').forEach(btn => btn.style.display = 'none');

  const opt = {
    margin: [0.2, 0.4, 0.2, 0.4],
    filename: 'How Much Does Sexual Harassment Cost Us? (Run to the Monster).pdf',
    image: { type: 'jpeg', quality: 1 },
    html2canvas: {
      scale: 4,
      useCORS: true,
      scrollX: 0,
      scrollY: 0,
      windowWidth: document.body.scrollWidth,
      windowHeight: document.body.scrollHeight
    },
    jsPDF: {
      unit: 'cm',
      format: 'a4',
      orientation: 'landscape'
    }
  };

  html2pdf().set(opt).from(container).save().then(() => {
    // Restore original layout
    assumptions.style.display = previousAssumptionDisplay;
    toggleBtn.style.display = previousToggleDisplay;
calculator.style.flex = prevCalculatorFlex;
resultsBox.style.flex = prevResultsFlex;
calculator.style.marginRight = prevCalculatorMargin;
    document.querySelectorAll('.results-box button').forEach(btn => btn.style.display = '');
  });
}


  function toggleAdvanced() {
    const section = document.getElementById('advancedSettings');
    section.style.display = section.style.display === 'none' || section.style.display === '' ? 'block' : 'none';
  }
</script>
</body>
</html>
