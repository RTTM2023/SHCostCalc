<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Sexual Harassment Cost Calculator (Exact Excel Match)</title>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Montserrat', sans-serif;
      margin: 0;
      padding: 0;
      background-color: #f8f8f8;
      color: #333;
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
      margin-bottom: 2rem;
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
    }
    h2 {
      margin-top: 0;
      color: inherit;
    }
    label {
      font-weight: bold;
      display: block;
      margin-top: 1.5rem;
    }
    input[type="number"] {
      width: 100%;
      padding: 0.8rem;
      font-size: 1rem;
      border-radius: 30px;
      border: 1px dashed #5b01fa;
      font-family: 'Montserrat', sans-serif;
      margin-top: 0.5rem;
    }
    button {
      margin-top: 2rem;
      width: 100%;
      padding: 1rem;
      font-size: 1.2rem;
      background-color: #f10178;
      color: white;
      border: none;
      border-radius: 30px;
      cursor: pointer;
      font-family: 'Montserrat', sans-serif;
      font-weight: bold;
      transition: background-color 0.3s;
    }
    button:hover {
      background-color: #d0006a;
    }
    .results-line-item {
      display: flex;
      justify-content: space-between;
      margin: 0.5rem 0;
      font-size: 0.9rem;
    }
    .results-line-item.bold {
      font-weight: bold;
      font-size: 1rem;
    }
    .divider {
      border-top: 1px solid rgba(255,255,255,0.5);
      margin: 1rem 0;
    }
    .total-line {
      font-size: 1.2rem;
      font-weight: bold;
      margin: 1.5rem 0;
      padding: 0.5rem 0;
      border-top: 2px dotted white;
      border-bottom: 2px dotted white;
      display: flex;
      justify-content: space-between;
    }
    .tooltip {
      position: relative;
      display: inline-block;
      cursor: help;
    }
    .tooltip:hover::after {
      content: attr(data-tooltip);
      position: absolute;
      background: rgba(0, 0, 0, 0.9);
      color: #fff;
      padding: 0.5rem 1rem;
      border-radius: 5px;
      top: 100%;
      left: 0;
      width: 300px;
      font-size: 0.8rem;
      margin-top: 0.5rem;
      z-index: 10;
      white-space: normal;
    }
    .button-group {
      display: none;
      flex-direction: column;
      gap: 1rem;
      margin-top: 2rem;
    }
    .download-btn, .reset-btn, .source-btn {
      background: white;
      color: #f10178;
      border: 1px solid #f10178;
      font-size: 1rem;
      font-weight: 600;
      padding: 0.8rem;
      border-radius: 30px;
      cursor: pointer;
      text-align: center;
      transition: all 0.3s;
    }
    .download-btn:hover, .source-btn:hover {
      background: #f8f8f8;
    }
    .reset-btn {
      background: #5b01fa;
      color: white;
      border-color: #5b01fa;
    }
    .reset-btn:hover {
      background: #4a00d1;
    }
    .advanced-toggle {
      margin-top: 1.5rem;
      background: none;
      border: none;
      color: white;
      font-size: 0.9rem;
      text-decoration: underline;
      cursor: pointer;
      padding: 0;
      display: none;
    }
    .advanced-settings {
      display: none;
      margin-top: 1.5rem;
      background: rgba(255,255,255,0.1);
      padding: 1.5rem;
      border-radius: 15px;
      font-size: 0.85rem;
    }
    .advanced-settings p {
      margin: 0.5rem 0;
      display: flex;
      justify-content: space-between;
    }
    .advanced-settings strong {
      font-weight: 700;
    }
    .advanced-settings ul {
      padding-left: 1.5rem;
      margin: 0.5rem 0;
    }
    .advanced-settings li {
      margin-bottom: 0.3rem;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="calculator">
      <h2>Sexual Harassment Cost Calculator</h2>
      <p>This calculator exactly matches the Excel formulas from your original spreadsheet</p>
      
      <label for="women">Number of Women in Organisation</label>
      <input type="number" id="women" value="442">
      
      <label for="men">Number of Men in Organisation</label>
      <input type="number" id="men" value="408">
      
      <label for="salary">Average Gross Monthly Salary (ZAR)</label>
      <input type="number" id="salary" value="59100">
      
      <button onclick="calculateCost()">Calculate Exact Costs</button>
    </div>

    <div class="results-box">
      <h2>Estimated Cost of Sexual Harassment</h2>
      <div id="resultsContent"></div>

      <button class="advanced-toggle" id="toggleBtn" onclick="toggleAdvanced()">Show Detailed Assumptions</button>
      <div class="advanced-settings" id="advancedSettings">
        <p><strong>Female Incidence Rate:</strong> <span>3% <span class="tooltip" data-tooltip="Ultra conservative rate based on international benchmarks">(?)</span></span></p>
        <p><strong>Male Incidence Rate:</strong> <span>1% <span class="tooltip" data-tooltip="Ultra conservative rate based on international benchmarks">(?)</span></span></p>
        <p><strong>Severity Distribution:</strong></p>
        <ul>
          <li>Low Severity: 75% of cases</li>
          <li>Medium Severity: 20% of cases</li>
          <li>High Severity: 5% of cases</li>
        </ul>
        <p><strong>Cost Components:</strong></p>
        <ul>
          <li>Low Severity: 2 days salary + R500 HR costs</li>
          <li>Medium Severity: 10 days salary + 20% chance of turnover (at 50% annual salary) + R10,000 HR</li>
          <li>High Severity: 40 days salary + 50% chance of turnover (at full annual salary) + R200,000 legal</li>
        </ul>
      </div>

      <div class="button-group" id="resultButtons">
        <button class="download-btn" onclick="downloadPDF()">Download as PDF</button>
        <button class="source-btn" onclick="showSources()">View Research Sources</button>
        <button class="reset-btn" onclick="resetCalculator()">Reset Calculator</button>
      </div>
    </div>
  </div>

  <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
  <script>
    // Exact match to Excel formulas
    function calculateCost() {
      // Get input values
      const women = parseFloat(document.getElementById('women').value) || 0;
      const men = parseFloat(document.getElementById('men').value) || 0;
      const salary = parseFloat(document.getElementById('salary').value) || 0;

      // Constants from Excel
      const FEMALE_INCIDENCE = 0.03; // Cell E1
      const MALE_INCIDENCE = 0.01;   // Cell E2
      const WORK_DAYS_PER_MONTH = 21.5; // Used in severity calculations

      // Calculate total expected cases (Excel B5)
      const totalCases = (women * FEMALE_INCIDENCE) + (men * MALE_INCIDENCE);

      // Case distribution (Excel B6-B8)
      const lowCases = totalCases * 0.75;
      const medCases = totalCases * 0.2;
      const highCases = totalCases * 0.05;

      // Calculate cost per case type (matches Severity Case Table)
      // Low severity cost (Excel E4)
      const lowCostPerCase = (salary / WORK_DAYS_PER_MONTH) + (salary / WORK_DAYS_PER_MONTH) + 500;
      // Medium severity cost (Excel E5)
      const medCostPerCase = ((salary / WORK_DAYS_PER_MONTH) * 5) + 
                            ((salary / WORK_DAYS_PER_MONTH) * 5) + 
                            (0.2 * 0.5 * salary * 12) + 
                            10000;
      // High severity cost (Excel E6)
      const highCostPerCase = ((salary / WORK_DAYS_PER_MONTH) * 20) + 
                             ((salary / WORK_DAYS_PER_MONTH) * 20) + 
                             (0.5 * salary * 12) + 
                             200000;

      // Total costs by severity (Excel B10)
      const totalLowCost = lowCases * lowCostPerCase;
      const totalMedCost = medCases * medCostPerCase;
      const totalHighCost = highCases * highCostPerCase;
      const totalCostWithoutTraining = totalLowCost + totalMedCost + totalHighCost;

      // Formatting functions
      const formatCurrency = (num) => 'R' + Math.round(num).toLocaleString('en-ZA');
      const formatCases = (num) => num.toFixed(2);

      // Display main results
      document.getElementById('resultsContent').innerHTML = `
        <div class="results-line-item bold"><span>Total Expected Cases Per Year:</span><span>${formatCases(totalCases)}</span></div>
        <div class="divider"></div>
        <div class="results-line-item"><span>Low Severity Cases (75%):</span><span>${formatCases(lowCases)}</span></div>
        <div class="results-line-item"><span>Medium Severity Cases (20%):</span><span>${formatCases(medCases)}</span></div>
        <div class="results-line-item"><span>High Severity Cases (5%):</span><span>${formatCases(highCases)}</span></div>
        <div class="divider"></div>
        <div class="results-line-item"><span>Cost of Low Severity Cases:</span><span>${formatCurrency(totalLowCost)}</span></div>
        <div class="results-line-item"><span>Cost of Medium Severity Cases:</span><span>${formatCurrency(totalMedCost)}</span></div>
        <div class="results-line-item"><span>Cost of High Severity Cases:</span><span>${formatCurrency(totalHighCost)}</span></div>
        <div class="total-line"><span>Total Annual Cost Without Training:</span><span>${formatCurrency(totalCostWithoutTraining)}</span></div>
      `;

      // Show additional UI elements
      document.getElementById('resultButtons').style.display = 'flex';
      document.getElementById('toggleBtn').style.display = 'inline-block';
    }

    function toggleAdvanced() {
      const section = document.getElementById('advancedSettings');
      section.style.display = section.style.display === 'none' ? 'block' : 'none';
      document.getElementById('toggleBtn').textContent = 
        section.style.display === 'none' ? 'Show Detailed Assumptions' : 'Hide Detailed Assumptions';
    }

    function resetCalculator() {
      document.getElementById('women').value = '442';
      document.getElementById('men').value = '408';
      document.getElementById('salary').value = '59100';
      document.getElementById('resultsContent').innerHTML = '';
      document.getElementById('resultButtons').style.display = 'none';
      document.getElementById('advancedSettings').style.display = 'none';
      document.getElementById('toggleBtn').style.display = 'none';
      document.getElementById('toggleBtn').textContent = 'Show Detailed Assumptions';
    }

    function downloadPDF() {
      const element = document.querySelector('.container');
      const opt = {
        margin: 10,
        filename: 'Sexual_Harassment_Cost_Calculator.pdf',
        image: { type: 'jpeg', quality: 0.98 },
        html2canvas: { scale: 2, useCORS: true },
        jsPDF: { unit: 'mm', format: 'a4', orientation: 'portrait' }
      };
      html2pdf().set(opt).from(element).save();
    }

    function showSources() {
      alert("Research sources would be displayed here.\n\nThis would include references to:\n- International benchmarks for harassment incidence rates\n- Studies on productivity loss from harassment\n- Legal cost averages for harassment cases");
    }

    // Initialize with default values
    window.onload = function() {
      calculateCost();
    };
  </script>
</body>
</html>
