<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>SGIP Eligibility & Incentive Calculator</title>
  <style>
    :root {
      --primary: #fdb813;
      --secondary: #003c71;
      --accent: #005eb8;
      --bg: #f9f9f9;
      --text: #333;
      --muted: #555;
    }
    body {
      margin: 0;
      padding: 0;
      background: var(--bg);
      color: var(--text);
      font-family: Arial, sans-serif;
    }
    h1 {
      color: var(--primary);
      text-align: center;
      margin: 20px 0;
      font-size: 1.8rem;
    }
    .container {
      display: flex;
      flex-wrap: wrap;
      max-width: 1200px;
      margin: 0 auto;
      padding: 10px;
      gap: 20px;
    }
    .maps, .calculator {
      flex: 1 1 100%;
    }
    @media (min-width: 768px) {
      .maps { flex: 1 1 60%; }
      .calculator { flex: 1 1 38%; }
    }
    .map-container {
      border: 1px solid var(--accent);
      border-radius: 4px;
      overflow: hidden;
      margin-bottom: 20px;
    }
    .map-container h2 {
      margin: 0;
      padding: 10px;
      background: var(--secondary);
      color: white;
      font-size: 1rem;
    }
    .map-container iframe {
      width: 100%;
      height: 400px;
      border: 0;
    }
    form > div {
      margin-bottom: 15px;
    }
    label {
      display: block;
      font-weight: bold;
      color: var(--secondary);
      margin-bottom: 5px;
      font-size: 1rem;
    }
    select, input {
      width: 100%;
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 4px;
      box-sizing: border-box;
      font-size: 1rem;
    }
    button {
      background: var(--primary);
      color: white;
      border: none;
      padding: 12px 20px;
      font-size: 1rem;
      border-radius: 4px;
      cursor: pointer;
      transition: background 0.3s;
    }
    button:hover {
      background: var(--accent);
    }
    .result {
      margin-top: 20px;
      padding: 15px;
      background: white;
      border-left: 5px solid var(--primary);
      border-radius: 4px;
      font-size: 1rem;
      line-height: 1.4;
    }
    small {
      color: var(--muted);
      font-size: 0.875rem;
    }
    /* Mobile-specific adjustments */
    @media (max-width: 767px) {
      .container {
        flex-direction: column;
        padding: 5px;
        gap: 10px;
      }
      h1 { font-size: 1.5rem; margin: 10px 0; }
      .map-container iframe { height: 250px; }
      .map-container h2 { font-size: 0.9rem; padding: 8px; }
      label { font-size: 0.9rem; }
      select, input { font-size: 0.95rem; padding: 8px; }
      button {
        width: 100%;
        font-size: 1rem;
        padding: 12px;
      }
    }
  </style>
</head>
<body>
  <h1>SGIP Eligibility & Incentive Calculator</h1>
  <div class="container">
    <div class="maps">
      <div class="map-container">
        <h2>SB 535 Disadvantaged Communities Map</h2>
        <iframe src="https://experience.arcgis.com/experience/1c21c53da8de48f1b946f3402fbae55c/page/SB-535-Disadvantaged-Communities/" title="DAC Map"></iframe>
      </div>
      <div class="map-container">
        <h2>Community Air Protection (CAP UC) Map</h2>
        <iframe src="https://capuc.maps.arcgis.com/apps/webappviewer/index.html?id=5bdb921d747a46929d9f00dbdb6d0fa2" title="CAP UC Map"></iframe>
      </div>
      <div class="map-container">
        <h2>SCE Shutoff (Outage Status) Tool</h2>
        <p style="padding:10px;"><a href="https://www.sce.com/outages-safety/outage-center/check-outage-status" target="_blank" style="color:var(--accent); text-decoration:none; font-weight:bold;">🔗 Check Public Safety Shutoff Status</a></p>
      </div>
    </div>
    <div class="calculator">
      <!-- Calculator form -->
      <form id="calcForm">
        <div>
          <label for="customerType">1. Host Customer Class</label>
          <select id="customerType">
            <option value="">Select type</option>
            <option value="residential-single">Residential Single-Family</option>
            <option value="residential-multi">Residential Multifamily</option>
            <option value="commercial">Commercial/Business</option>
            <option value="industrial">Industrial/Agricultural</option>
          </select>
          <small>Must be utility customer of record; rentals need explanation letter.</small>
        </div>
        <div>
          <label for="inDAC">2. Disadvantaged Community (DAC)?</label>
          <select id="inDAC"><option value=""></option><option value="yes">Yes</option><option value="no">No</option></select>
        </div>
        <div>
          <label for="inFire">3. Tier 2/3 Wildfire Threat Zone?</label>
          <select id="inFire"><option value=""></option><option value="yes">Yes</option><option value="no">No</option></select>
        </div>
        <div>
          <label for="inPSPS">4. Located in a PSPS Shutoff Area?</label>
          <select id="inPSPS"><option value=""></option><option value="yes">Yes</option><option value="no">No</option></select>
          <small>Refer to CPUC PSPS lookup tool separate from this calculator.</small>
        </div>
        <div>
          <label for="equityPathway1">5. Multifamily Equity Pathway</label>
          <select id="equityPathway1"><option value=""></option><option value="deed">Deed-restricted low-income housing (≥5 units)</option><option value="80pct">≥80% units ≤60% AMI</option><option value="mash">Reserved MASH/SOMAH funds</option></select>
        </div>
        <div>
          <label for="singleEquity">6. Single-Family Equity Criterion</label>
          <select id="singleEquity"><option value=""></option><option value="income">Income verified per HUD</option><option value="program">Participated in SASH/DAC-SASH/CARE/FERA/ESA</option></select>
        </div>
        <div>
          <label for="care">7. CARE Program Participation</label>
          <select id="care"><option value=""></option><option value="yes">Yes</option><option value="no">No</option><option value="unsure">Unsure</option></select>
        </div>
        <div>
          <label for="helpEnroll">8. Help enrolling in CARE discount?</label>
          <select id="helpEnroll"><option value=""></option><option value="yes">Yes</option><option value="no">No</option></select>
        </div>
        <div>
          <label for="capacity">9. Storage Capacity (kWh)</label>
          <input type="number" id="capacity" min="0" placeholder="e.g., 30 for 30 kWh" />
        </div>
        <div>
          <label for="solarCapacity">10. Solar PV Capacity (kW)</label>
          <input type="number" id="solarCapacity" min="0" step="0.1" placeholder="e.g., 5 for 5 kW" />
        </div>
        <div>
          <label for="backup">11. Backup Capability?</label>
          <select id="backup"><option value=""></option><option value="yes">Yes</option><option value="no">No</option></select>
        </div>
        <div>
          <button type="button" id="btnCheck">Calculate Eligibility & Incentive</button>
        </div>
      </form>
      <div id="result" class="result" style="display:none;"></div>
      <script>
        const generalRates=[0.50,0.40,0.35,0.30,0.25,0.20,0.15];const resiliencyAdder=0.15;const equityRate=0.85;const resiliencyEqRate=1.00;const solarRate=3100;
        document.getElementById('btnCheck').addEventListener('click',()=>{const cust=document.getElementById('customerType').value;const inFire=document.getElementById('inFire').value==='yes';const inPSPS=document.getElementById('inPSPS').value==='yes';const multiPath=document.getElementById('equityPathway1').value;const singlePath=document.getElementById('singleEquity').value;const careSelected=document.getElementById('care').value==='yes';const helpEnroll=document.getElementById('helpEnroll').value==='yes';const capacity=parseFloat(document.getElementById('capacity').value)||0;const solarCap=parseFloat(document.getElementById('solarCapacity').value)||0;let rate=0,budget='';if((cust==='residential-multi'&&multiPath)||(cust==='residential-single'&&singlePath)){budget='Equity Storage';rate=equityRate;}else if(inFire||inPSPS){budget='Equity Resiliency Storage';rate=resiliencyEqRate;}else{budget='General Market Storage';const step=Math.min(Math.floor(capacity/30),generalRates.length-1);rate=generalRates[step];if(inFire||inPSPS)rate+=resiliencyAdder;}const storageIncentive=capacity*1000*rate;const solarIncentive=solarCap*solarRate;const totalIncentive=storageIncentive+solarIncentive;let explanation=`You qualify under the **${budget}** category at a rate of $${rate.toFixed(2)}/Wh, resulting in $${storageIncentive.toLocaleString()} for ${capacity.toLocaleString()} kWh of storage. `;if(solarCap>0)explanation+=`Additionally, ${solarCap.toLocaleString()} kW of solar PV earns $${solarIncentive.toLocaleString()} at $${solarRate}/kW. `;if(careSelected)explanation+=`As a CARE participant, you save 20% on your electric bill. `;if(helpEnroll)explanation+=`We can assist you with enrolling in the CARE discount. `;explanation+=`Total SGIP incentives: $${totalIncentive.toLocaleString()}.`;const res=document.getElementById('result');res.innerHTML=`<p>${explanation}</p>`;res.style.display='block';});
      </script>
    </div>
  </div>
</body>
</html>
