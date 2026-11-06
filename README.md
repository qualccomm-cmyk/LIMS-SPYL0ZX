<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="theme-color" content="#210b0d">
<title>LIMS SPY — Control Interface</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Barlow+Condensed:wght@500;600;700;800;900&family=DM+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.2/css/all.min.css">
<style>
:root{
  --bg:#16090b;--panel:#241014;--panel2:#30151a;--line:#633039;
  --red:#a52c38;--red2:#d34a43;--orange:#f0a16c;--cream:#f7e8d8;
  --muted:#bd9da0;--green:#78d69a;--shadow:0 18px 45px #08030480;
}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--cream);font-family:"DM Sans",sans-serif;min-height:100vh}
body:before{content:"";position:fixed;inset:0;pointer-events:none;opacity:.14;background-image:linear-gradient(135deg,transparent 49.7%,#e7a08a 50%,transparent 50.3%);background-size:54px 54px;mask-image:linear-gradient(to bottom,black,transparent 70%)}
button,input{font:inherit}
button{cursor:pointer}
.shell{width:min(1440px,100%);margin:auto;padding:26px clamp(16px,3vw,42px) 42px;position:relative}
.topline{display:flex;justify-content:space-between;align-items:center;gap:14px;margin-bottom:24px}
.brand{display:flex;align-items:center;gap:12px}
.brand-mark{width:44px;height:44px;display:grid;place-items:center;background:var(--orange);color:#321014;border:2px solid #ffe0bd;box-shadow:4px 4px 0 #6c242c;transform:rotate(-4deg);font-size:20px}
.brand small{display:block;color:var(--muted);font-size:10px;letter-spacing:2px;font-weight:700}
.brand strong{font:800 21px "Barlow Condensed",sans-serif;letter-spacing:1px}
.top-status{border:1px solid var(--line);padding:9px 13px;border-radius:3px;color:#f0c5b5;font-size:11px;letter-spacing:1px}
.top-status i{color:var(--green);font-size:8px;margin-right:7px}
.hero{position:relative;overflow:hidden;background:linear-gradient(112deg,#4b1820 0%,#812b32 53%,#c65b46 100%);border:2px solid #f0a16c;box-shadow:8px 8px 0 #090405, var(--shadow);padding:clamp(23px,4vw,48px);clip-path:polygon(0 0,97% 0,100% 13%,100% 100%,3% 100%,0 88%)}
.hero:after{content:"";position:absolute;width:290px;height:290px;border:30px solid #f6c09b25;right:8%;top:-110px;transform:rotate(34deg);box-shadow:0 0 0 18px #260b1020,0 0 0 42px #260b1015}
.hero-content{position:relative;z-index:1;max-width:760px}
.eyebrow{font-size:10px;letter-spacing:3px;font-weight:700;color:#ffd5b8;margin-bottom:12px}
.hero h1{font:900 clamp(46px,8vw,94px)/.83 "Barlow Condensed",sans-serif;letter-spacing:-1px;margin:0;text-transform:uppercase;text-shadow:4px 4px 0 #5a1c25}
.hero h1 span{color:#ffbd87}
.hero-sub{font:700 clamp(13px,2vw,17px) "Barlow Condensed",sans-serif;letter-spacing:3px;margin-top:18px;color:#ffe6d2}
.hero-foot{display:flex;align-items:center;gap:12px;margin-top:25px;font-size:10px;letter-spacing:2px;color:#f7c9b2}
.hero-foot:before{content:"";width:35px;height:2px;background:var(--orange)}
.layout{display:grid;grid-template-columns:minmax(0,1.35fr) minmax(290px,.8fr);gap:20px;margin-top:24px}
.panel{background:linear-gradient(145deg,#2b1318,#1e0d11);border:1px solid var(--line);box-shadow:5px 5px 0 #090405;position:relative;min-width:0}
.panel-head{padding:17px 19px;border-bottom:1px solid #51252d;display:flex;justify-content:space-between;align-items:center;gap:12px}
.panel-head h2{font:700 19px "Barlow Condensed",sans-serif;letter-spacing:1.2px;margin:0;text-transform:uppercase}
.panel-head h2 i{color:var(--orange);margin-right:9px}
.kicker{font-size:9px;color:var(--muted);letter-spacing:1.5px}
.panel-body{padding:19px}
.field-grid{display:grid;grid-template-columns:1fr 1fr;gap:13px}
.field label{display:block;color:#d9b8b3;font-size:10px;font-weight:700;letter-spacing:1px;margin-bottom:8px}
.field input{width:100%;background:#16090d;border:1px solid #75404a;color:var(--cream);padding:13px 12px;outline:none;border-radius:2px}
.field input:focus{border-color:var(--orange);box-shadow:0 0 0 2px #f0a16c20}
.field input::placeholder{color:#80666a}
.hint{font-size:10px;color:#a98a8d;margin-top:7px}
.action-row{display:flex;gap:10px;flex-wrap:wrap;margin-top:17px}
.btn{border:1px solid #f0a16c;background:var(--orange);color:#351116;font-weight:800;font-size:11px;letter-spacing:1px;padding:13px 17px;box-shadow:4px 4px 0 #090405;transition:.18s}
.btn:hover{transform:translate(-2px,-2px);box-shadow:6px 6px 0 #090405}
.btn.secondary{background:#35171d;color:#f7d8c6;border-color:#80414a}
#connect[hidden]{display:none}
.notice{font-size:10px;color:#bd9da0;line-height:1.6;margin-top:13px}

/* ACCESS LIVE: fullscreen tanpa memaksa rotasi perangkat */
html.video-active,body.video-active{
  width:100%;
  height:100%;
  overflow:hidden;
  background:#000;
}
.video-wrap{display:none}
.video-wrap.show{
  display:block;
  position:fixed;
  inset:0;
  z-index:99999;
  width:100%;
  height:100%;
  height:100dvh;
  margin:0;
  padding:0;
  border:0;
  overflow:hidden;
  background:#000;
}
.video-stage{
  position:absolute;
  inset:0;
  width:100%;
  height:100%;
  display:block;
  overflow:hidden;
  background:#000;
}
.video-stage video{
  position:absolute;
  inset:0;
  display:block;
  width:100%;
  height:100%;
  min-width:100%;
  min-height:100%;
  max-width:none;
  max-height:none;
  object-fit:cover;
  object-position:center;
  background:#000;
  border:0;
}
.video-label{
  position:absolute;
  z-index:2;
  top:max(14px,env(safe-area-inset-top));
  left:max(14px,env(safe-area-inset-left));
  padding:8px 11px;
  background:#16090dcc;
  border:1px solid #ffffff45;
  color:#fff;
  font-size:10px;
  font-weight:700;
  letter-spacing:1.3px;
  pointer-events:none;
}
.video-close{
  position:absolute;
  z-index:3;
  top:max(12px,env(safe-area-inset-top));
  right:max(12px,env(safe-area-inset-right));
  width:44px;
  height:44px;
  display:grid;
  place-items:center;
  border:1px solid #ffffff66;
  border-radius:4px;
  background:#16090ddd;
  color:#fff;
  font-size:18px;
}
.video-close:active{transform:scale(.94)}
.video-wrap:fullscreen{
  width:100%;
  height:100%;
  background:#000;
}

.device-summary{display:grid;grid-template-columns:1fr 1fr;gap:9px;margin-top:15px}
.metric{background:#1a0b0f;border:1px solid #4a252c;padding:12px}
.metric small{display:block;color:#a98a8d;font-size:9px;letter-spacing:1px;margin-bottom:6px}
.metric strong{font-size:12px;overflow-wrap:anywhere}
.status-tag{font-size:9px;color:var(--green);letter-spacing:1px;white-space:nowrap}
.status-tag:before{content:"";display:inline-block;width:6px;height:6px;background:var(--green);border-radius:50%;margin-right:6px}
.control-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.control{background:#1a0b0f;border:1px solid #51252d;padding:14px 12px;text-align:left;color:var(--cream);min-height:96px;position:relative;transition:.2s}
.control:hover{border-color:var(--orange);transform:translateY(-2px)}
.control .ico{display:block;font-size:20px;color:var(--orange);margin-bottom:11px}
.control strong{display:block;font:700 15px "Barlow Condensed",sans-serif;letter-spacing:.6px}
.control small{display:block;color:#a98a8d;font-size:9px;margin-top:4px}
.control.active{border-color:#5c9e72;background:#142019}
.control.active .ico,.control.active .state{color:var(--green)}
.control .state{position:absolute;right:10px;top:11px;color:#a98a8d;font-size:8px;letter-spacing:1px}
.data-stack{display:grid;gap:13px;margin-top:20px}
.data-card{background:#1a0b0f;border:1px solid #51252d;padding:14px}
.data-title{display:flex;justify-content:space-between;gap:10px;align-items:center;margin-bottom:11px}
.data-title strong{font:700 15px "Barlow Condensed",sans-serif;letter-spacing:1px}
.data-title i{color:var(--orange)}
.account{display:flex;align-items:center;gap:10px;padding:9px 0;border-top:1px solid #3d2026}
.avatar{width:30px;height:30px;background:#63303a;color:#ffe0c9;display:grid;place-items:center;border-radius:50%;font-size:11px}
.account span{display:block;font-size:11px}
.account small{display:block;color:#a98a8d;font-size:9px;margin-top:3px}
.sms{padding:10px 0;border-top:1px solid #3d2026}
.sms-top{display:flex;justify-content:space-between;font-size:10px}
.sms-top small{color:#a98a8d}
.sms p{font-size:10px;line-height:1.5;color:#d0b5b2;margin:6px 0 0}
.net-grid{display:grid;grid-template-columns:1fr 1fr;gap:9px}
.net-grid div{background:#16090d;padding:10px;border:1px solid #402027}
.net-grid small{display:block;color:#a98a8d;font-size:9px;margin-bottom:5px}
.net-grid strong{font-size:11px;overflow-wrap:anywhere}
.map-box{height:300px;background:#1a0b0f;border:1px solid #51252d;overflow:hidden}
.map-box iframe{width:100%;height:100%;border:0;filter:grayscale(.75) sepia(.2) hue-rotate(300deg) saturate(.8)}
.map-caption{display:flex;justify-content:space-between;gap:10px;padding-top:10px;font-size:10px;color:#c4a3a1}
.map-caption strong{color:var(--orange)}
.footer{display:flex;justify-content:space-between;gap:12px;align-items:center;margin-top:26px;border-top:1px solid #48232a;padding-top:15px;color:#98797d;font-size:9px;letter-spacing:1.5px}
.toast{position:fixed;left:50%;bottom:22px;transform:translate(-50%,20px);opacity:0;pointer-events:none;background:#1c3325;border:1px solid #65b27d;color:#c6f3d1;padding:11px 16px;font-size:11px;z-index:5;transition:.2s;box-shadow:4px 4px 0 #080405}
.toast.show{opacity:1;transform:translate(-50%,0)}
@media(max-width:850px){.layout{grid-template-columns:1fr}.hero:after{right:-120px}}
@media(max-width:520px){.shell{padding:17px 13px 30px}.topline{align-items:flex-start}.top-status{font-size:9px;padding:8px}.field-grid{grid-template-columns:1fr}.hero{padding:27px 20px}.hero h1{font-size:59px}.panel-body{padding:14px}.footer{flex-direction:column;align-items:flex-start}.device-summary{grid-template-columns:1fr 1fr}}
</style>
</head>
<body>
<div class="shell">
  <header class="topline">
    <div class="brand">
      <div class="brand-mark"><i class="fa-solid fa-crosshairs"></i></div>
      <div><small>SPYWARE CONTROL / 05.5</small><strong>LIMS SYSTEM</strong></div>
    </div>
    <div class="top-status"><i class="fa-solid fa-circle"></i> ACCESS LIVE</div>
  </header>

  <section class="hero">
    <div class="hero-content">
      <div class="eyebrow">SPYWARE SERIES 055</div>
      <h1>LIMS <span>LIVE</span></h1>
      <div class="hero-sub">SPYWARE APT55 / DEVICE CONTROL</div>
      <div class="hero-foot">PROJECT BY L0ZX</div>
    </div>
  </section>

  <main class="layout">
    <div>
      <section class="panel">
        <div class="panel-head">
          <h2><i class="fa-solid fa-mobile-screen-button"></i> Identitas perangkat</h2>
          <span class="kicker">FORM 01 / DEVICE</span>
        </div>
        <div class="panel-body">
          <div class="field-grid">
            <div class="field">
              <label for="imei">NOMOR IMEI · 15 DIGIT</label>
              <input id="imei" inputmode="numeric" maxlength="15" placeholder="Masukkan 15 digit" autocomplete="off">
              <div class="hint">Masukkan 15 digit angka.</div>
            </div>
            <div class="field">
              <label for="serial">NOMOR SERI · 12 KARAKTER</label>
              <input id="serial" maxlength="12" placeholder="Masukkan nomor seri" autocomplete="off">
              <div class="hint">12 karakter huruf dan angka.</div>
            </div>
            <div class="field">
              <label for="whatsapp">NOMOR WHATSAPP</label>
              <input id="whatsapp" inputmode="tel" maxlength="16" placeholder="62812xxxxxxxx" autocomplete="off">
              <div class="hint">Format nomor dengan kode negara.</div>
            </div>
          </div>
          <div class="action-row">
            <button class="btn" id="connect" hidden><i class="fa-solid fa-tower-broadcast"></i> ACCESS LIVE</button>
            <button class="btn secondary" id="reset"><i class="fa-solid fa-rotate-left"></i> ATUR ULANG</button>
          </div>
          <p class="notice">PROSES AKAN DI KIRIM KE DATA SERVER.</p>
          <div class="video-wrap" id="videoWrap" aria-label="Pemutar video layar penuh">
            <div class="video-label">LIMS LIVE / SCREEN ACCESS</div>
            <button class="video-close" id="closeVideo" type="button" aria-label="Tutup video"><i class="fa-solid fa-xmark"></i></button>
            <div class="video-stage">
            <video id="previewVideo" controls playsinline preload="metadata">
              <source src="77_video.mp4" type="video/mp4">
              ERORR
            </video>
            </div>
          </div>
          <div class="device-summary">
            <div class="metric"><small>STATUS FORM</small><strong id="formStatus">MENUNGGU INPUT</strong></div>
            <div class="metric"><small>MODE OPSIONAL</small><strong>LOKAL / PRATINJAU</strong></div>
          </div>
        </div>
      </section>

      <section class="panel" style="margin-top:20px">
        <div class="panel-head">
          <h2><i class="fa-solid fa-sliders"></i> Panel fitur</h2>
          <span class="kicker">FORM 02 / INTERAKSI</span>
        </div>
        <div class="panel-body">
          <div class="control-grid">
            <button class="control" data-feature="Mikrofon"><span class="state">SIAP</span><i class="ico fa-solid fa-microphone"></i><strong>Mikrofon</strong><small>Status live</small></button>
            <button class="control" data-feature="Kamera"><span class="state">SIAP</span><i class="ico fa-solid fa-camera"></i><strong>Kamera</strong><small>Status live</small></button>
            <button class="control" data-feature="Riwayat SMS"><span class="state">SIAP</span><i class="ico fa-solid fa-message"></i><strong>Riwayat SMS</strong><small>Data realtime</small></button>
            <button class="control" data-feature="Lokasi"><span class="state">SIAP</span><i class="ico fa-solid fa-location-dot"></i><strong>Lokasi</strong><small>gps tracker</small></button>
          </div>
          <p class="notice">FITUR BERJALAN NORMAL.</p>
        </div>
      </section>

      <section class="panel" id="locationPanel" style="margin-top:20px">
        <div class="panel-head">
          <h2><i class="fa-solid fa-map-location-dot"></i> Peta area</h2>
          <span class="kicker">LOKASI GPS</span>
        </div>
        <div class="panel-body">
          <div class="map-box">
            <iframe title="Peta area Cileungsi Bogor" loading="lazy" src="https://maps.google.com/maps?q=Cileungsi%2C%20Bogor%2C%20Jawa%20Barat&t=&z=13&ie=UTF8&iwloc=&output=embed"></iframe>
          </div>
          <div class="map-caption"><span><strong>Cileungsi</strong> · Kabupaten Bogor</span><span>Peta area Cileungsi</span></div>
        </div>
      </section>
    </div>

    <aside>
      <section class="panel">
        <div class="panel-head">
          <h2><i class="fa-solid fa-database"></i> Data perangkat</h2>
          <span class="kicker">FORM 03 / DATA</span>
        </div>
        <div class="panel-body">
          <div class="net-grid">
            <div><small>ALAMAT ALAMAT IP</small><strong>192.0.2.55</strong></div>
            <div><small>JARINGAN</small><strong>VLZZ_5G</strong></div>
            <div><small>WILAYAH</small><strong>CILEUNGSI, BOGOR</strong></div>
            <div><small>STATUS PANEL</small><strong style="color:var(--green)">TERHUBUNG*</strong></div>
          </div>
          <p class="notice">*Status ini online sedang aktif.</p>
          <div class="data-stack">
            <div class="data-card">
              <div class="data-title"><strong><i class="fa-brands fa-google"></i> PROFIL AKUN</strong><span class="status-tag">TERSEDIA</span></div>
              <div class="account"><div class="avatar">V</div><div><span>Vlzz86@gmail.com</span><small>Profil contoh · data lokal</small></div></div>
              <div class="account"><div class="avatar">Y</div><div><span>YusikaaV1@gmail.com</span><small>Profil contoh · data lokal</small></div></div>
              <div class="account"><div class="avatar">L</div><div><span>limssample55@gmail.com</span><small>Profil contoh · data lokal</small></div></div>
            </div>
            <div class="data-card">
              <div class="data-title"><strong><i class="fa-solid fa-envelope"></i> ARSIP PESAN</strong><span class="kicker">3 ITEM</span></div>
              <div class="sms"><div class="sms-top"><strong>INFO LAYANAN</strong><small>09:42</small></div><p>Kode verifikasi contoh: 482 190. Jangan bagikan kode kepada siapa pun.</p></div>
              <div class="sms"><div class="sms-top"><strong>PAKET DATA</strong><small>08:16</small></div><p>Paket contoh Anda akan berakhir dalam 2 hari. Periksa aplikasi operator.</p></div>
              <div class="sms"><div class="sms-top"><strong>PENGINGAT</strong><small>KEMARIN</small></div><p>Ini adalah pesan contoh untuk tampilan daftar pesan.</p></div>
            </div>
            <div class="data-card">
              <div class="data-title"><strong><i class="fa-solid fa-satellite-dish"></i> INFORMASI KOORDINAT</strong><span class="kicker">AREA</span></div>
              <div class="net-grid">
                <div><small>GARIS LINTANG</small><strong>Area Cileungsi</strong></div>
                <div><small>GARIS BUJUR</small><strong>Bogor, Jawa Barat</strong></div>
              </div>
              <p class="notice">menampilkan koordinat.</p>
            </div>
          </div>
        </div>
      </section>
    </aside>
  </main>

  <footer class="footer"><span>LIMS LIVE / SPYAPT55</span><span>PROJECT BY L0ZX</span><span>INTERFACE BUILD 01.55</span></footer>
</div>
<div class="toast" id="toast" role="status" aria-live="polite"></div>

<script>
const imei = document.getElementById('imei');
const serial = document.getElementById('serial');
const whatsapp = document.getElementById('whatsapp');
const connectBtn = document.getElementById('connect');
const resetBtn = document.getElementById('reset');
const videoWrap = document.getElementById('videoWrap');
const video = document.getElementById('previewVideo');
const formStatus = document.getElementById('formStatus');
const toast = document.getElementById('toast');

function fieldsAreValid() {
  return /^\d{15}$/.test(imei.value)
    && /^[A-Z0-9]{12}$/.test(serial.value)
    && /^\+?\d{10,15}$/.test(whatsapp.value);
}

function refreshFormState() {
  const valid = fieldsAreValid();
  connectBtn.hidden = !valid;
  if (valid) {
    formStatus.textContent = 'FORMAT VALID';
  } else {
    formStatus.textContent = 'MENUNGGU INPUT';
    videoWrap.classList.remove('show');
    document.documentElement.classList.remove('video-active');
    document.body.classList.remove('video-active');
    video.pause();
    video.currentTime = 0;
  }
}

imei.addEventListener('input', () => {
  imei.value = imei.value.replace(/\D/g, '').slice(0, 15);
  refreshFormState();
});

serial.addEventListener('input', () => {
  serial.value = serial.value.toUpperCase().replace(/[^A-Z0-9]/g, '').slice(0, 12);
  refreshFormState();
});

whatsapp.addEventListener('input', () => {
  whatsapp.value = whatsapp.value.replace(/[^\d+]/g, '').slice(0, 16);
  refreshFormState();
});

function notify(message) {
  toast.textContent = message;
  toast.classList.add('show');
  clearTimeout(notify.timer);
  notify.timer = setTimeout(() => toast.classList.remove('show'), 2400);
}

async function openVideo(){
  if(!fieldsAreValid()){
    refreshFormState();
    notify('Lengkapi ketiga kolom dengan format yang benar.');
    return;
  }

  videoWrap.classList.add('show');
  document.documentElement.classList.add('video-active');
  document.body.classList.add('video-active');

  video.currentTime = 0;
  video.load();

  // Fullscreen hanya untuk pemutar.
  // Tidak ada screen.orientation.lock('landscape'),
  // sehingga perangkat tidak dipaksa berputar.
  try{
    if(videoWrap.requestFullscreen){
      await videoWrap.requestFullscreen();
    }else if(video.requestFullscreen){
      await video.requestFullscreen();
    }
  }catch(error){
    console.warn('Fullscreen API tidak tersedia pada browser/WebView ini.',error);
  }

  try{
    await video.play();
    notify('Pemutar layar penuh aktif.');
  }catch(error){
    notify('Pemutar siap. Tekan tombol play.');
  }
}

async function closeVideo(){
  video.pause();
  video.currentTime = 0;

  videoWrap.classList.remove('show');
  document.documentElement.classList.remove('video-active');
  document.body.classList.remove('video-active');

  try{
    if(document.fullscreenElement){
      await document.exitFullscreen();
    }
  }catch(error){
    console.warn(error);
  }

  // Tidak memanggil screen.orientation.unlock()
  // karena halaman tidak pernah mengunci orientasi.
}

connectBtn.addEventListener('click',openVideo);

const closeVideoBtn = document.getElementById('closeVideo');
closeVideoBtn.addEventListener('click',()=>{
  closeVideo();
  notify('Video ditutup.');
});

document.addEventListener('keydown',event=>{
  if(event.key === 'Escape' && videoWrap.classList.contains('show')){
    closeVideo();
  }
});

document.addEventListener('fullscreenchange',()=>{
  if(!document.fullscreenElement && videoWrap.classList.contains('show')){
    videoWrap.classList.remove('show');
    document.documentElement.classList.remove('video-active');
    document.body.classList.remove('video-active');
    video.pause();
  }
});

resetBtn.addEventListener('click', () => {
  imei.value = '';
  serial.value = '';
  whatsapp.value = '';
  formStatus.textContent = 'MENUNGGU INPUT';
  connectBtn.hidden = true;

  video.pause();
  video.currentTime = 0;
  videoWrap.classList.remove('show');
  document.documentElement.classList.remove('video-active');
  document.body.classList.remove('video-active');

  if(document.fullscreenElement){
    document.exitFullscreen().catch(error=>console.warn(error));
  }

  document.querySelectorAll('.control').forEach(button => {
    button.classList.remove('active');
    button.querySelector('.state').textContent = 'SIAP';
  });

  notify('Form telah diatur ulang.');
});

document.querySelectorAll('.control').forEach(button => {
  button.addEventListener('click', () => {
    const active = button.classList.toggle('active');
    button.querySelector('.state').textContent = active ? 'ACTIVE' : 'SIAP';
    const feature = button.dataset.feature;

    if (feature === 'Lokasi') {
      document.getElementById('locationPanel').scrollIntoView({
        behavior:'smooth',
        block:'center'
      });
      notify(active ? 'Peta area ditampilkan.' : 'Indikator lokasi dinonaktifkan.');
    } else {
      notify(active ? feature + ' — indikator aktif.' : feature + ' — indikator siap.');
    }
  });
});

refreshFormState();
</script>
</body>
</html>
