<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Sanat Fabrikası</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap');
        :root { --bg: #050508; --card: #11111a; --cyan: #22d3ee; --gray: #6b7280; }
        * { box-sizing: border-box; -webkit-tap-highlight-color: transparent; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background-color: var(--bg); color: white; margin: 0; padding: 0; display: flex; justify-content: center; }
        #app { width: 100%; max-width: 450px; min-height: 100vh; position: relative; background-color: var(--bg); overflow-x: hidden; }
        .landing-container { height: 100vh; display: flex; flex-direction: column; align-items: center; justify-content: center; padding: 2rem; text-align: center; }
        .cyan-text { color: var(--cyan); text-shadow: 0 0 15px rgba(34, 211, 238, 0.4); }
        .main-btn { width: 100%; background: var(--cyan); color: black; border: none; padding: 1.2rem; border-radius: 1rem; font-weight: 800; text-transform: uppercase; letter-spacing: 1px; cursor: pointer; margin-top: 1rem; }
        .glass-card { background: var(--card); border: 1px solid rgba(255, 255, 255, 0.05); border-radius: 2rem; padding: 1.5rem; margin-bottom: 1rem; }
        .grid { display: grid; grid-template-columns: 1fr 1fr; gap: 1rem; padding: 1rem; }
        .role-card { background: var(--card); border-radius: 1.5rem; padding: 1.5rem; display: flex; flex-direction: column; align-items: center; border: 1px solid rgba(255, 255, 255, 0.05); cursor: pointer; }
        .icon-box { width: 50px; height: 50px; background: rgba(34, 211, 238, 0.1); color: var(--cyan); border-radius: 12px; display: flex; align-items: center; justify-content: center; margin-bottom: 0.5rem; font-size: 1.5rem; }
        input { width: 100%; padding: 1.2rem; background: rgba(255, 255, 255, 0.05); border: 1px solid rgba(255, 255, 255, 0.1); border-radius: 1rem; color: white; margin-bottom: 1rem; font-family: inherit; }
        header { padding: 1.5rem; display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid rgba(255, 255, 255, 0.05); }
        .balance-card { background: linear-gradient(135deg, #0891b2, #1e40af); padding: 2rem; border-radius: 2.5rem; margin: 1rem; }
        nav { position: fixed; bottom: 0; width: 100%; max-width: 450px; background: rgba(10, 10, 15, 0.95); padding: 1.5rem; display: flex; justify-content: space-around; border-top: 1px solid rgba(255, 255, 255, 0.05); }
        .fade-in { animation: fadeIn 0.4s ease; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
    </style>
</head>
<body>
<div id="app"></div>
<script>
    const state = { view: 'landing', stageName: '', role: '' };
    function render() {
        const app = document.getElementById('app');
        if (state.view === 'landing') {
            app.innerHTML = `<div class="landing-container fade-in">
                <h1 style="font-size: 3rem; font-weight: 800; line-height: 1; margin: 0;">SANAT <br><span class="cyan-text">FABRİKASI</span></h1>
                <p style="color: var(--gray); font-size: 10px; font-weight: 800; letter-spacing: 3px; margin: 2rem 0;">DİJİTAL SANATÇI EKOSİSTEMİ</p>
                <button class="main-btn" onclick="setView('roles')">Hemen Başla</button>
            </div>`;
        } else if (state.view === 'roles') {
            app.innerHTML = `<div class="fade-in" style="padding: 1rem;">
                <h2 style="font-size: 2rem; font-weight: 800; italic">ROLÜNÜ <span class="cyan-text">SEÇ</span></h2>
                <div class="grid">
                    <div class="role-card" onclick="setRole('Müzisyen')"><div class="icon-box">🎤</div><small>MÜZİSYEN</small></div>
                    <div class="role-card" onclick="setRole('Grafiker')"><div class="icon-box">🎨</div><small>GRAFİKER</small></div>
                    <div class="role-card" onclick="setRole('Yapımcı')"><div class="icon-box">🏢</div><small>YAPIMCI</small></div>
                    <div class="role-card" onclick="setRole('Yönetmen')"><div class="icon-box">🎬</div><small>YÖNETMEN</small></div>
                </div>
            </div>`;
        } else if (state.view === 'register') {
            app.innerHTML = `<div class="fade-in" style="padding: 2rem;">
                <h2 style="font-size: 1.5rem; font-weight: 800;">PROFİLİNİ <span class="cyan-text">TAMAMLA</span></h2>
                <p style="font-size: 10px; color: var(--cyan); font-weight: 800; margin-bottom: 2rem;">SEÇİLEN: ${state.role}</p>
                <input type="text" id="nameInp" placeholder="Sahne Adın">
                <button class="main-btn" onclick="finish()">Tamamla</button>
            </div>`;
        } else if (state.view === 'dashboard') {
            app.innerHTML = `<div class="fade-in">
                <header><b style="font-style: italic;">FABRİKA</b>
                <div style="width: 35px; height: 35px; background: var(--cyan); border-radius: 10px; display: flex; align-items: center; justify-content: center; font-weight: 800; color: black;">${state.stageName[0]}</div>
                </header>
                <div style="padding: 1.5rem;">
                    <h2 style="font-size: 2rem; font-weight: 800;">SELAM <span class="cyan-text">${state.stageName}</span></h2>
                    <div class="balance-card">
                        <small style="font-weight: 800; opacity: 0.7;">BAKİYE</small>
                        <h3 style="font-size: 2.5rem; margin: 0; font-weight: 800;">₺14.250</h3>
                    </div>
                </div>
                <nav><span>🏠</span><span>🔍</span><span style="background: var(--cyan); padding: 0.5rem 1rem; border-radius: 10px; color: black;">+</span><span>💬</span><span>⚙️</span></nav>
            </div>`;
        }
    }
    function setView(v) { state.view = v; render(); }
    function setRole(r) { state.role = r; setView('register'); }
    function finish() { state.stageName = document.getElementById('nameInp').value || 'Sanatçı'; setView('dashboard'); }
    render();
</script>
</body>
</html>

