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
      background-color: #f8f8f8;
    }
    .container {
      display: flex;
      flex-direction: column;
      padding: 2rem;
      max-width: 1600px;
      margin: 0 auto;
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
      flex: 1;
      margin-right: 2rem;
      border: 2px solid #f10178;
    }
    .results-box {
      flex: 1;
      background-color: #f10178;
      color: white;
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
      margin: 0.5rem 0;
      font-size: 0.9rem;
    }
    .results-line-item.bold {
      font-size: 1.1rem;
      font-weight: bold;
    }
    .half-line {
      border-top: 1px solid white;
      margin: 1rem 0;
    }
    .total-line {
      font-size: 1.2rem;
      font-weight: bold;
      margin-top: 1rem;
      display: flex;
      justify-content: space-between;
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
    }
    .advanced-settings p {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .advanced-settings ul {
      padding-left: 2rem;
      margin-top: 0.25rem;
    }
    .advanced-settings li {
      margin-bottom: 0.25rem;
    }
  </style>
</head>
<body>
<div class="container">
  <div class="calculator">
    <h2>Sexual Harassment Cost Calculator</h2>
    <label for="women">Number of Women in Organisation <span class="tooltip" data-tooltip="Ultra conservative rate based on international benchmarks"><img src="Untitled design.png" alt="info icon" /></span></label>
    <input type="number" id="women" />

    <label for="men">Number of Men in Organisation <span class="tooltip" data-tooltip="Ultra conservative rate based on international benchmarks"><img src="Untitled design.png" alt="info icon" /></span></label>
    <input type="number" id="men" />

    <label for="salary">Average Gross Monthly Salary (R) <span class="tooltip" data-tooltip="Used to estimate cost impact of each case"><img src="Untitled design.png" alt="info icon" /></span></label>
    <input type="number" id="salary" />

    <button onclick="calculateCost()">Calculate</button>
  </div>

  <div class="results-box">
    <h2>Estimated Sexual Harassment Cost</h2>
    <div id="resultsContent"></div>

    <button class="advanced-toggle" id="toggleBtn" onclick="toggleAdvanced()">Show/Hide Assumptions</button>
    <div class="advanced-settings" id="advancedSettings">
      <p><strong>Female Incidence Rate:</strong><span>3% <span class="tooltip" data-tooltip="Ultra conservative rate based on international benchmarks"><img src="Untitled design.png" alt="info icon" /></span></labe
      <p><strong>Male Incidence Rate:</strong><span>1% <span class="tooltip" data-tooltip="Ultra conservative rate based on international benchmarks"><img src="Untitled design.png" alt="info icon" /></span></labe
      <p><strong>Severity of Cases Split:</strong></p>
      <ul>
        <li>Low = 75% <span class="tooltip" data-tooltip="Unreported and minor cases"><img src="Untitled design.png" alt="info icon" /></span></li>
        <li>Medium = 20% <span class="tooltip" data-tooltip="Internally reported and resolved"><img src="Untitled design.png" alt="info icon" /></span></labe
        <li>High = 5% <span class="tooltip" data-tooltip="Escalated and potential legal cases"><img src="Untitled design.png" alt="info icon" /></span></labe
      <p><strong>Cost to Company per Case Type:</strong></p>
      <ul>
        <li>Low = 0.33 × average gross salary <span class="tooltip" data-tooltip="absenteeism, presenteeism, minor team disruption"><img src="Untitled design.png" alt="info icon" /></span></labe
        <li>Medium = 1.43 × average gross salary <span class="tooltip" data-tooltip="HR case involvement, exit risk, longer disruption"><img src="Untitled design.png" alt="info icon" /></span></labe
        <li>High = 6.43 × average gross salary <span class="tooltip" data-tooltip="legal risk, reputational damage, settlement costs"><img src="Untitled design.png" alt="info icon" /></span></labe
      </ul>
    </div>

    <div class="button-group" id="resultButtons">
      <button class="download-btn" onclick="downloadPDF()">Download as PDF</button>
      <button class="source-btn">View Research Sources</button>
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

    const femaleRate = 0.03;
    const maleRate = 0.01;
    const totalCases = (women * femaleRate) + (men * maleRate);

    const low = totalCases * 0.75;
    const med = totalCases * 0.2;
    const high = totalCases * 0.05;

    const lowCost = low * 0.33 * salary;
    const medCost = med * 1.43 * salary;
    const highCost = high * 6.43 * salary;
    const totalCost = lowCost + medCost + highCost;

    document.getElementById('resultsContent').innerHTML = `
      <div class='results-line-item bold'><span>Estimated Cases:</span><span>${Math.round(totalCases)}</span></div>
      <div class='results-line-item'><span>Low Severity Cases (75% of ${Math.round(totalCases)}):<span class="tooltip" data-tooltip="Unreported and minor cases"><img src="Untitled design.png" alt="info icon" /></span></span><span>${Math.round(low)}</span></div>
      <div class='results-line-item'><span>Medium Severity Cases (20% of ${Math.round(totalCases)}):<span class="tooltip" data-tooltip="Internally reported and resolved">?</span></span><span>${Math.round(med)}</span></div>
      <div class='results-line-item'><span>High Severity Cases (5% of ${Math.round(totalCases)}):<span class="tooltip" data-tooltip="Escalated and potential legal cases">?</span></span><span>${Math.round(high)}</span></div>
      <div class="half-line"></div>
      <div class='results-line-item'><span>Low Severity Cost:<span class="tooltip" data-tooltip="absenteeism, presenteeism, minor team disruption">?</span></span><span>R${lowCost.toLocaleString(undefined, {minimumFractionDigits: 2, maximumFractionDigits: 2})}</span></div>
      <div class='results-line-item'><span>Medium Severity Cost:<span class="tooltip" data-tooltip="HR case involvement, exit risk, longer disruption">?</span></span><span>R${medCost.toLocaleString(undefined, {minimumFractionDigits: 2, maximumFractionDigits: 2})}</span></div>
      <div class='results-line-item'><span>High Severity Cost:<span class="tooltip" data-tooltip="legal risk, reputational damage, settlement costs">?</span></span><span>R${Math.round(highCost).toLocaleString()}</span></div>
      <div class="total-line"><span>Total Annual Cost:</span><span>R${Math.round(totalCost).toLocaleString()}</span></div>
    `;

    document.getElementById('resultButtons').style.display = 'flex';
    document.getElementById('toggleBtn').style.display = 'inline-block';
  }

  function downloadPDF() {
    const element = document.querySelector('.container');
    const opt = {
      margin: 0.5,
      filename: 'Sexual_Harassment_Cost_Estimate.pdf',
      image: { type: 'jpeg', quality: 0.98 },
      html2canvas: { scale: 3, useCORS: true },
      jsPDF: { unit: 'in', format: 'letter', orientation: 'landscape' }
    };
    html2pdf().set(opt).from(element).save();
  }

  function toggleAdvanced() {
    const section = document.getElementById('advancedSettings');
    section.style.display = section.style.display === 'none' || section.style.display === '' ? 'block' : 'none';
  }
</script>
</body>
</html>
