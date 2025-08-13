# Mission-shine-site
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Mission Shine Detailing | Book Now</title>
  <meta name="theme-color" content="#2563eb" />
  <link href="https://assets.calendly.com/assets/external/widget.css" rel="stylesheet" />
  <script src="https://assets.calendly.com/assets/external/widget.js" type="text/javascript"></script>
  <style>
    :root{--blue-600:#2563eb;--bg:#f8fafc}
    *{box-sizing:border-box} html,body{margin:0;padding:0;font-family:Inter,system-ui,-apple-system,Segoe UI,Roboto,Helvetica,Arial,sans-serif;color:#1f2937;background:var(--bg)}
    .container{max-width:1100px;margin:0 auto;padding:0 16px}
    header{position:sticky;top:0;z-index:40;background:rgba(255,255,255,.92);border-bottom:1px solid #e5e7eb;backdrop-filter:blur(8px)}
    .nav{display:flex;justify-content:space-between;align-items:center;padding:12px 0}
    .btn{display:inline-flex;align-items:center;justify-content:center;padding:12px 16px;border-radius:12px;border:1px solid #cbd5e1;background:#fff;text-decoration:none;font-weight:700;color:#0f172a}
    .btn-primary{background:var(--blue-600);border-color:transparent;color:#fff}
    .hero{padding:54px 0;background:linear-gradient(135deg,#eef2ff,#f8fafc)}
    .badge{display:inline-flex;gap:8px;align-items:center;border:1px solid #bfdbfe;background:#eff6ff;color:#1e3a8a;padding:6px 10px;border-radius:999px;font-weight:700;font-size:12px}
    .section{padding:54px 0} .cards{display:grid;grid-template-columns:repeat(auto-fit,minmax(260px,1fr));gap:12px;margin-top:18px}
    .card{background:#fff;border:1px solid #e5e7eb;border-radius:16px;padding:16px;box-shadow:0 2px 6px rgba(0,0,0,.04)}
    .row{display:flex;justify-content:space-between;margin:6px 0} .small{font-size:12px;color:#64748b}
    label{font-size:14px;font-weight:600;color:#334155} input,select,textarea{width:100%;padding:12px;border:1px solid #cbd5e1;border-radius:12px;background:#fff}
  </style>
</head>
<body>
  <header>
    <div class="container nav">
      <div style="display:flex;gap:10px;align-items:center">
        <div style="width:40px;height:40px;border-radius:10px;background:#2563eb"></div>
        <div><div style="font-weight:900">Mission Shine Detailing</div><div class="small">San Antonio, TX</div></div>
      </div>
      <a href="#book" class="btn btn-primary">Book Now</a>
    </div>
  </header>

  <section class="hero">
    <div class="container">
      <span class="badge">Launch Special • FIRST20 makes Simple Clean $20 (first 20 customers)</span>
      <h1>Premium, friendly detailing in San Antonio</h1>
      <p>Pick a time with Calendly, then send your booking request. We’ll confirm by text or email.</p>
      <div style="display:flex;gap:10px;flex-wrap:wrap;margin-top:14px">
        <a class="btn btn-primary" href="#" id="btnCalendly">Pick a time (Calendly)</a>
        <a class="btn" href="#book">Send booking request</a>
      </div>
    </div>
  </section>

  <section id="book" class="section">
    <div class="container">
      <div class="card">
        <h3>Booking request</h3>
        <div style="display:grid;gap:12px;grid-template-columns:1fr 1fr">
          <label>Service
            <select id="service">
              <option>Simple Clean</option>
              <option>Deluxe Detail</option>
              <option>Premium Detail</option>
              <option>Ultimate Showroom</option>
            </select>
          </label>
          <label>Promo
            <div style="display:flex;gap:8px">
              <input id="promo" placeholder="FIRST20" style="flex:1" />
              <button id="applyPromo" class="btn" type="button">Apply</button>
            </div>
          </label>
          <label>Your name <input id="name" /></label>
          <label>Email <input id="email" type="email" value="Rajesrd1@gmail.com" /></label>
          <label>Phone <input id="phone" /></label>
          <label>Preferred date <input id="date" type="date" /></label>
          <label>Preferred time <input id="time" type="time" /></label>
          <label>Vehicle <input id="vehicle" placeholder="e.g., 2020 Toyota Camry" /></label>
          <label>Address (if mobile) <input id="address" placeholder="Street, City" /></label>
        </div>
        <label style="display:block;margin-top:12px">Notes
          <textarea id="notes" rows="3" placeholder="Stains, pet hair, etc."></textarea>
        </label>

        <div class="row"><span>Package</span> <strong id="row-package">Simple Clean ($35.00)</strong></div>
        <div class="row"><span>Estimated total</span> <strong id="row-total">$35.00</strong></div>
        <div id="promo-alert" class="small"></div>

        <div style="display:flex;gap:10px;flex-wrap:wrap;margin-top:12px">
          <button id="sendEmail" class="btn btn-primary">Send booking email</button>
          <span class="small">Opens your email app with details filled in.</span>
        </div>
      </div>
    </div>
  </section>

  <footer>
    <div class="container" style="padding:24px 0">
      <div class="small">© <span id="yr"></span> Mission Shine Detailing</div>
    </div>
  </footer>

  <script>
    const CALENDLY_URL = "https://calendly.com/rajesrd1";
    const PRICES = {"Simple Clean":35,"Deluxe Detail":79,"Premium Detail":149,"Ultimate Showroom":249};
    const usd = n => `$${n.toFixed(2)}`;
    function updatePrice(){
      const svc = document.getElementById('service').value;
      let price = PRICES[svc] || 35;
      if (document.body.dataset.promo==='1' && svc==='Simple Clean') price = 20;
      document.getElementById('row-package').textContent = `${svc} (${usd(price)})`;
      document.getElementById('row-total').textContent = usd(price);
    }
    document.getElementById('applyPromo').addEventListener('click',()=>{
      const code = document.getElementById('promo').value.trim().toUpperCase();
      const a = document.getElementById('promo-alert');
      if(code==='FIRST20'){ document.body.dataset.promo='1'; a.textContent='Promo applied! Simple Clean is $20.'; }
      else { document.body.dataset.promo='0'; a.textContent='Promo not recognized. Use FIRST20.'; }
      updatePrice();
    });
    document.getElementById('service').addEventListener('change',updatePrice);
    document.getElementById('sendEmail').addEventListener('click',()=>{
      const need=['name','email','phone','date','time'];
      for(const id of need){ if(!(document.getElementById(id).value||'').trim()) return alert('Please complete Name, Email, Phone, Date, and Time.'); }
      const svc=service.value, promo=document.body.dataset.promo==='1', priceText=document.getElementById('row-total').textContent;
      const body=[
        `Name: ${name.value}`,
        `Email: ${email.value}`,
        `Phone: ${phone.value}`,
        `Vehicle: ${vehicle.value}`,
        `Service: ${svc}`,
        `Date/Time: ${date.value} ${time.value}`,
        `Service Address: ${address.value}`,
        `Notes: ${notes.value||'(none)'}`,
        promo ? "Promo: FIRST20 (Simple Clean $20)" : "Promo: (none)",
        `Quoted Total (pre-tax): ${priceText}`
      ].join('%0A');
      const subject=encodeURIComponent(`Mission Shine Detailing Booking – ${svc} on ${date.value} at ${time.value}`);
      location.href=`mailto:Rajesrd1@gmail.com?subject=${subject}&body=${body}`;
    });
    document.getElementById('btnCalendly').addEventListener('click',(e)=>{
      e.preventDefault();
      Calendly.initPopupWidget({ url: CALENDLY_URL + '?hide_landing_page_details=1&hide_gdpr_banner=1' });
    });
    document.getElementById('yr').textContent=new Date().getFullYear();
    updatePrice();
  </script>
</body>
</html>
