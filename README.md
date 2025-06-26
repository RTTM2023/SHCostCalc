<!DOCTYPE html>
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
    .results-divider {
      border-top: 1px solid white;
      margin: 1rem 0;
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
    .tooltip {
      position: relative;
      cursor: pointer;
      vertical-align: super;
    }
    .tooltip img {
      width: 16px;
      height: 16px;
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
  </style>
</head>
<body>
  <div class="container">
    <div class="calculator">
      <h2>SH Cost Calculator</h2>
      <label for="numEmployees">Number of Employees</label>
      <input type="number" id="numEmployees" placeholder="e.g. 100" />

      <label for="percentWomen">% Women in the Organisation</label>
      <input type="number" id="percentWomen" placeholder="e.g. 60" />

      <label for="avgSalary">Average Monthly Gross Salary</label>
      <input type="number" id="avgSalary" placeholder="e.g. 25000" />

      <button id="calculateBtn">Calculate</button>
      <button id="resetBtn" class="reset-btn">Reset Calculator</button>
    </div>

    <div class="results-box">
      <h2>Estimated Sexual Harassment Cost</h2>

      <div class="results-line-item bold">Estimated Cases:</div>
      <div class="results-line-item">Low Severity Cases (75% of X): <span class="tooltip" data-tooltip="Unreported and minor cases"><img src="Untitled design.png" alt="?" /></span> <span id="lowCases">0</span></div>
      <div class="results-line-item">Medium Severity Cases (20% of X): <span class="tooltip" data-tooltip="Internally reported and resolved"><img src="Untitled design.png" alt="?" /></span> <span id="mediumCases">0</span></div>
      <div class="results-line-item">High Severity Cases (5% of X): <span class="tooltip" data-tooltip="Escalated and potential legal cases"><img src="Untitled design.png" alt="?" /></span> <span id="highCases">0</span></div>

      <div class="results-divider"></div>

      <div class="results-line-item bold">Estimated Costs:</div>
      <div class="results-line-item">Low Severity Cost (75% of Y): <span class="tooltip" data-tooltip="Low = 0.33 × average gross salary"><img src="Untitled design.png" alt="?" /></span> <span id="lowCost">R0</span></div>
      <div class="results-line-item">Medium Severity Cost (20% of Y): <span class="tooltip" data-tooltip="Medium = 1.0 × average gross salary"><img src="Untitled design.png" alt="?" /></span> <span id="mediumCost">R0</span></div>
      <div class="results-line-item">High Severity Cost (5% of Y): <span class="tooltip" data-tooltip="High = 3.0 × average gross salary"><img src="Untitled design.png" alt="?" /></span> <span id="highCost">R0</span></div>
    </div>
  </div>

  <script>
    document.getElementById('calculateBtn').addEventListener('click', function () {
      const numEmployees = parseFloat(document.getElementById('numEmployees').value);
      const percentWomen = parseFloat(document.getElementById('percentWomen').value);
      const avgSalary = parseFloat(document.getElementById('avgSalary').value);

      const incidenceRateFemale = 0.015;
      const incidenceRateMale = 0.0025;

      const numWomen = numEmployees * (percentWomen / 100);
      const numMen = numEmployees - numWomen;

      const totalIncidents = (numWomen * incidenceRateFemale) + (numMen * incidenceRateMale);

      const lowCases = Math.round(totalIncidents * 0.75);
      const mediumCases = Math.round(totalIncidents * 0.2);
      const highCases = Math.round(totalIncidents * 0.05);

      const lowCost = Math.round(lowCases * avgSalary * 0.33);
      const mediumCost = Math.round(mediumCases * avgSalary);
      const highCost = Math.round(highCases * avgSalary * 3);

      document.getElementById('lowCases').innerText = lowCases;
      document.getElementById('mediumCases').innerText = mediumCases;
      document.getElementById('highCases').innerText = highCases;

      document.getElementById('lowCost').innerText = `R${lowCost}`;
      document.getElementById('mediumCost').innerText = `R${mediumCost}`;
      document.getElementById('highCost').innerText = `R${highCost}`;
    });

    document.getElementById('resetBtn').addEventListener('click', function () {
      document.getElementById('numEmployees').value = '';
      document.getElementById('percentWomen').value = '';
      document.getElementById('avgSalary').value = '';

      document.getElementById('lowCases').innerText = '0';
      document.getElementById('mediumCases').innerText = '0';
      document.getElementById('highCases').innerText = '0';

      document.getElementById('lowCost').innerText = 'R0';
      document.getElementById('mediumCost').innerText = 'R0';
      document.getElementById('highCost').innerText = 'R0';
    });
  </script>
</body>
</html>
