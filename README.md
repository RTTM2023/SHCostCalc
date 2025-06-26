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
      margin-left: 1rem;
      margin-bottom: 0.25rem;
    }
  </style>
</head>
<body>
  <div class="results-box">
    <h2>Estimated Sexual Harassment Cost</h2>

    <div class="results-line-item bold">Estimated Cases:</div>
    <div class="results-line-item">Low Severity Cases (75% of X): <span class="tooltip" data-tooltip="Unreported and minor cases"><img src="assets/images/Untitled design.png" alt="?" /></span> <span id="lowCases">0</span></div>
    <div class="results-line-item">Medium Severity Cases (20% of X): <span class="tooltip" data-tooltip="Internally reported and resolved"><img src="assets/images/Untitled design.png" alt="?" /></span> <span id="mediumCases">0</span></div>
    <div class="results-line-item">High Severity Cases (5% of X): <span class="tooltip" data-tooltip="Escalated and potential legal cases"><img src="assets/images/Untitled design.png" alt="?" /></span> <span id="highCases">0</span></div>

    <div class="results-divider"></div>

    <div class="results-line-item bold">Estimated Costs:</div>
    <div class="results-line-item">Low Severity Cost (75% of Y): <span class="tooltip" data-tooltip="Low = 0.33 × average gross salary"><img src="assets/images/Untitled design.png" alt="?" /></span> <span id="lowCost">R0</span></div>
    <div class="results-line-item">Medium Severity Cost (20% of Y): <span class="tooltip" data-tooltip="Medium = 1.0 × average gross salary"><img src="assets/images/Untitled design.png" alt="?" /></span> <span id="mediumCost">R0</span></div>
    <div class="results-line-item">High Severity Cost (5% of Y): <span class="tooltip" data-tooltip="High = 3.0 × average gross salary"><img src="assets/images/Untitled design.png" alt="?" /></span> <span id="highCost">R0</span></div>
  </div>

  <div class="advanced-settings">
    <p>Female Incidence Rate: <span class="tooltip" data-tooltip="Ultra conservative rate based on international benchmarks"><img src="assets/images/Untitled design.png" alt="?" /></span></p>
    <p>Male Incidence Rate: <span class="tooltip" data-tooltip="Ultra conservative rate based on international benchmarks"><img src="assets/images/Untitled design.png" alt="?" /></span></p>

    <p><strong>Severity of Cases Split:</strong></p>
    <ul>
      <li>Low = 75% <span class="tooltip" data-tooltip="Unreported and minor cases"><img src="assets/images/Untitled design.png" alt="?" /></span></li>
      <li>Medium = 20% <span class="tooltip" data-tooltip="Internally reported and resolved"><img src="assets/images/Untitled design.png" alt="?" /></span></li>
      <li>High = 5% <span class="tooltip" data-tooltip="Escalated and potential legal cases"><img src="assets/images/Untitled design.png" alt="?" /></span></li>
    </ul>

    <p><strong>Cost to Company per Case Type:</strong></p>
    <ul>
      <li>Low = 0.33 × average gross salary <span class="tooltip" data-tooltip="Low = 0.33 × average gross salary"><img src="assets/images/Untitled design.png" alt="?" /></span></li>
      <li>Medium = 1.0 × average gross salary <span class="tooltip" data-tooltip="Medium = 1.0 × average gross salary"><img src="assets/images/Untitled design.png" alt="?" /></span></li>
      <li>High = 3.0 × average gross salary <span class="tooltip" data-tooltip="High = 3.0 × average gross salary"><img src="assets/images/Untitled design.png" alt="?" /></span></li>
    </ul>
  </div>
</body>
</html>
