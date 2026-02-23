<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0" />
  <title>Sexual Harassment Cost Calculator</title>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap" rel="stylesheet" />
  <style>
    /* Mobile-First Responsive Shell */
    * { box-sizing: border-box; max-width: 100%; }
    header, #header, .site-header, h1:first-of-type, #title-with-line { display: none !important; }

    body {
      font-family: 'Montserrat', sans-serif;
      margin: 0;
      padding: 0;
      background-color: transparent;
      overflow-x: hidden;
      width: 100%;
      padding-bottom: 24px; /* helps prevent bottom clipping in iframe */
    }

    .container {
      display: flex;
      flex-direction: column;
      padding: 15px;
      width: 100%;
      margin: 0 auto;
      gap: 20px;
    }

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
      padding: 2rem;
      border-radius: 20px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
      width: 100%;
    }

    .calculator { border: 2px solid #f10178; }
    .results-box { background-color: #f10178; color: white; min-height: 300px; }

    h2 { font-size: 22px; margin-top: 0; }
    label { font-weight: bold; display: block; margin-top: 1.5rem; }

    input[type="number"], input[type="text"], input[type="email"], textarea {
      width: 100%;
      padding: 0.6rem;
      font-size: 16px;
      border-radius: 30px;
      border: 1px dashed #5b01fa;
      font-family: 'Montserrat', sans-serif;
      margin-top: 5px;
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

    .results-line-item { display: flex; justify-content: space-between; margin: 0.15rem 0; font-size: 0.75rem; gap: 8px; }
    .results-line-item.bold { font-size: 0.9rem; font-weight: bold; }

    .total-line {
      font-size: 1.2rem; font-weight: bold; margin: 2rem 0 1rem 0;
      display: flex; justify-content: space-between;
      border-top: 1px dotted white; border-bottom: 1px dotted white; padding: 0.5rem 0;
    }
    .half-line { border-top: 1px solid white; margin: 1rem 0; width: 50%; }

    .tooltip { position: relative; cursor: pointer; vertical-align: middle; }
    .tooltip img { width: 16px; height: 16px; vertical-align: middle; margin-left: 4px; background-color: transparent !important; }

    .tooltip:hover::after {
      content: attr(data-tooltip);
      position: absolute;
      background: rgba(0, 0, 0, 0.9);
      color: #fff;
      padding: 0.6rem 0.8rem;
      border-radius: 5px;
      bottom: 125%;
      left: 50%;
      transform: translateX(-50%);
      display: block;
      max-width: 240px;
      width: max-content;
      min-width: 120px;
      font-size: 0.8rem;
      z-index: 999;
      text-align: left;
    }

    .button-group { display: none; flex-direction: column; gap: 0.5rem; margin-top: 1.5rem; }
    .download-btn, .reset-btn {
      background: white; color: #f10178; border: 1px dashed #5b01fa;
      padding: 0.6rem 1rem; border-radius: 30px; font-weight: 500; cursor: pointer; text-align: center;
    }
    .reset-btn { background: #5b01fa; color: white; }
  </style>
</head>
<body>

<div class="container">
  <div class="calculator">
    <h2>Sexual Harassment Cost Calculator</h2>

    <label for="women">
      Number of Women in Organisation
      <span class="tooltip" data-tooltip="Used to estimate the number of cases using an assumed rate of harassment.">
        <img src="whiteback.png" alt="info icon" />
      </span>
    </label>
    <input type="number" id="women" />

    <label for="men">
      Number of Men in Organisation
      <span class="tooltip" data-tooltip="Used to estimate the number of cases using an assumed rate of harassment.">
        <img src="whiteback.png" alt="info icon" />
      </span>
    </label>
    <input type="number" id="men" />

    <label for="salary">
      Average Gross MONTHLY Salary (ZAR)
      <span class="tooltip" data-tooltip="Used to estimate cost impact of each case">
        <img src="whiteback.png" alt="info icon" />
      </span>
    </label>
    <input type="number" id="salary" />

    <button onclick="calculateCost()">Calculate</button>
  </div>

  <div class="results-box">
    <h2>Estimated Cost of Sexual Harassment</h2>
    <div id="resultsContent"></div>

    <div class="button-group" id="resultButtons">
      <button class="download-btn" onclick="downloadPDF()">Download as PDF</button>
      <button class="download-btn" onclick="toggleEnquiry()">Enquire about our Solution</button>
    </div>

    <div id="enquiryForm" style="display: none; margin-top: 1rem;">
      <form action="https://formspree.io/f/manjzgjr" method="POST" style="display: flex; flex-direction: column; gap: 0.75rem;">
        <input type="text" name="name" placeholder="Your Name" required />
        <input type="text" name="organisation" placeholder="Organisation" required />
        <input type="email" name="email" placeholder="Email Address" required />
        <textarea name="message" readonly>I would like to find out more about your sexual harassment prevention programme.</textarea>
        <button type="submit" style="background-color: #ffb002; color: black; border-radius: 30px; padding: 1rem; border:none; cursor:pointer; font-weight: bold;">Send Enquiry</button>
      </form>
    </div>

    <div id="resetButton" style="display: none; margin-top: 1.5rem;">
      <button class="reset-btn" onclick="window.location.reload()">Reset Calculator</button>
    </div>
  </div>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>

<script>
/* ============================================================
   IFRAME AUTO-RESIZE (CHILD / GITHUB PAGE)
   MUST match Squarespace iframe id="shCalcFrame"
   ============================================================ */
(function () {
  const IFRAME_ID = "shCalcFrame";

  function getDocHeight() {
    const body = document.body;
    const html = document.documentElement;
    return Math.max(
      body.scrollHeight, body.offsetHeight,
      html.clientHeight, html.scrollHeight, html.offsetHeight
    );
  }

  function postHeight() {
    try {
      const height = getDocHeight();
      window.parent.postMessage(
        { type: "RTTM_IFRAME_HEIGHT", iframeId: IFRAME_ID, height: height },
        "*"
      );
    } catch (e) {}
  }

  window.addEventListener("load", function () {
    postHeight();
    setTimeout(postHeight, 150);
    setTimeout(postHeight, 600);
  });

  window.addEventListener("resize", function () {
    postHeight();
    setTimeout(postHeight, 150);
  });

  const observer = new MutationObserver(function () { postHeight(); });
  observer.observe(document.body, { childList: true, subtree: true });

  window.__postIframeHeight = postHeight;
})();

/* ============================================================
   Calculator Logic
   ============================================================ */
function calculateCost() {
  const women = parseInt(document.getElementById('women').value, 10) || 0;
  const men = parseInt(document.getElementById('men').value, 10) || 0;
  const salary = parseFloat(document.getElementById('salary').value) || 0;

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
  const formatCurrency = (num) => 'R' + Number(num).toFixed(2).replace(/\B(?=(\d{3})+(?!\d))/g, ',');

  document.getElementById('resultsContent').innerHTML = `
    <div class="results-line-item bold"><span>Estimated Cases:</span><span>${formatNumber(totalCases)}</span></div>

    <div class="results-line-item">
      <span>Low Severity Cases (75% of ${formatNumber(totalCases)}):
        <span class="tooltip" data-tooltip="Unreported and minor cases"><img src="whiteback.png" alt="info icon" /></span>
      </span>
      <span>${formatNumber(lowCases)}</span>
    </div>

    <div class="results-line-item">
      <span>Medium Severity Cases (20% of ${formatNumber(totalCases)}):
        <span class="tooltip" data-tooltip="Internally reported and resolved"><img src="whiteback.png" alt="info icon" /></span>
      </span>
      <span>${formatNumber(medCases)}</span>
    </div>

    <div class="results-line-item">
      <span>High Severity Cases (5% of ${formatNumber(totalCases)}):
        <span class="tooltip" data-tooltip="Escalated and potential legal cases"><img src="whiteback.png" alt="info icon" /></span>
      </span>
      <span>${formatNumber(highCases)}</span>
    </div>

    <div class="half-line"></div>

    <div class="results-line-item bold"><span>Estimated Costs:</span><span></span></div>

    <div class="results-line-item">
      <span>Low Severity Cost (per case):
        <span class="tooltip" data-tooltip="Absenteeism, presenteeism, minor team disruption"><img src="whiteback.png" alt="info icon" /></span>
      </span>
      <span>${formatCurrency(lowSeverityCost)}</span>
    </div>

    <div class="results-line-item">
      <span>Medium Severity Cost (per case):
        <span class="tooltip" data-tooltip="HR case involvement, exit risk, longer disruption"><img src="whiteback.png" alt="info icon" /></span>
      </span>
      <span>${formatCurrency(medSeverityCost)}</span>
    </div>

    <div class="results-line-item">
      <span>High Severity Cost (per case):
        <span class="tooltip" data-tooltip="Legal risk, reputational damage, settlement costs"><img src="whiteback.png" alt="info icon" /></span>
      </span>
      <span>${formatCurrency(highSeverityCost)}</span>
    </div>

    <div class="half-line"></div>

    <div class="results-line-item"><span>Total Low Severity Cost:</span><span>${formatCurrency(totalLowCost)}</span></div>
    <div class="results-line-item"><span>Total Medium Severity Cost:</span><span>${formatCurrency(totalMedCost)}</span></div>
    <div class="results-line-item"><span>Total High Severity Cost:</span><span>${formatCurrency(totalHighCost)}</span></div>

    <div class="total-line"><span>Total Annual Cost:</span><span>${formatCurrency(totalCost)}</span></div>
  `;

  document.getElementById('resultButtons').style.display = 'flex';
  document.getElementById('resetButton').style.display = 'block';

  if (window.__postIframeHeight) {
    window.__postIframeHeight();
    setTimeout(window.__postIframeHeight, 250);
  }
}

function toggleEnquiry() {
  const form = document.getElementById('enquiryForm');
  form.style.display = (form.style.display === 'none') ? 'block' : 'none';
  if (window.__postIframeHeight) {
    window.__postIframeHeight();
    setTimeout(window.__postIframeHeight, 250);
  }
}

function downloadPDF() {
  const element = document.querySelector('.container');
  const opt = {
    margin: [0.3, 0.3],
    filename: 'SH_Cost_Report.pdf',
    image: { type: 'jpeg', quality: 0.98 },
    html2canvas: { scale: 3, useCORS: true },
    jsPDF: { unit: 'in', format: 'letter', orientation: 'portrait' }
  };
  html2pdf().set(opt).from(element).save();
}
</script>
</body>
</html>
