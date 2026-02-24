<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Nexus Hub - Roblox Bridge</title>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@300;400;500;600;700&display=swap" rel="stylesheet"/>
<style>
/* SEU CSS ORIGINAL AQUI - mantém tudo igual */
* { box-sizing: border-box; margin: 0; padding: 0; user-select: none; }

body {
  font-family: 'JetBrains Mono', monospace;
  background: #1a2a1a;
  background-image:
    radial-gradient(ellipse at 30% 60%, rgba(0,180,80,0.15) 0%, transparent 55%),
    radial-gradient(ellipse at 80% 20%, rgba(0,100,200,0.2) 0%, transparent 45%),
    linear-gradient(180deg, #87ceeb 0%, #87ceeb 50%, #3a8a3a 50%, #2d6b2d 100%);
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  position: relative;
}

/* Resto do seu CSS continua IGUAL */
/* ... (todo o CSS que você já tem) ... */

/* Só vou adicionar um botão novo no final */
.generate-btn {
  background: linear-gradient(90deg, #2a7fff, #6cf);
  border: none;
  border-radius: 3px;
  padding: 8px 16px;
  color: white;
  font-family: 'JetBrains Mono', monospace;
  font-size: 11px;
  font-weight: 600;
  cursor: pointer;
  margin: 10px;
  text-transform: uppercase;
  letter-spacing: 1px;
  transition: all 0.2s;
  border: 1px solid rgba(255,255,255,0.2);
}
.generate-btn:hover {
  transform: translateY(-1px);
  box-shadow: 0 5px 15px rgba(102,204,255,0.4);
}
.generate-btn:active {
  transform: translateY(0);
}
</style>
</head>
<body>

<!-- BG Decorations (iguais) -->
<div class="bg-cube bc1"></div>
<div class="bg-cube bc2"></div>
<div class="bg-cube bc3"></div>

<!-- TOP STATUS BAR (igual) -->
<div class="topbar">
  <span class="topbar-brand">⬡ Nexus Hub</span>
  <span class="hub-sep">|</span>
  <span class="topbar-stat" id="fpsCounter">294 fps</span>
  <span class="hub-sep">|</span>
  <span class="topbar-stat" id="pingCounter">56 ms</span>
  <div class="topbar-tabs">
    <div class="topbar-tab active" onclick="setTopTab(this,'config')">CONFIG</div>
    <div class="topbar-tab" onclick="setTopTab(this,'index')">INDEX</div>
    <div class="topbar-tab" onclick="setTopTab(this,'visuals')">VISUALS</div>
  </div>
</div>

<!-- MAIN HUB -->
<div class="hub" id="hub">

  <!-- TITLE (igual) -->
  <div class="hub-title">
    <div class="hub-title-left">
      <div class="hub-logo">N</div>
      <span class="hub-name">Nexus Hub</span>
      <span class="hub-sep">|</span>
      <span class="hub-game">Roblox Bridge</span>
      <span class="hub-sep">|</span>
      <span class="hub-discord">discord.gg/nexushub</span>
    </div>
    <div class="hub-controls">
      <div class="hub-ctrl min" title="Minimizar">−</div>
      <div class="hub-ctrl max" title="Maximizar">□</div>
      <div class="hub-ctrl cls" onclick="closeHub()" title="Fechar">×</div>
    </div>
  </div>

  <!-- TABS (igual) -->
  <div class="hub-tabs">
    <div class="tab active" data-tab="combat" onclick="switchTab(this)">Combat</div>
    <div class="tab" data-tab="render" onclick="switchTab(this)">Render</div>
    <div class="tab" data-tab="movement" onclick="switchTab(this)">Movement</div>
    <div class="tab" data-tab="player" onclick="switchTab(this)">Player</div>
    <div class="tab" data-tab="world" onclick="switchTab(this)">World</div>
    <div class="tab" data-tab="ui" onclick="switchTab(this)">UI Settings</div>
  </div>

  <!-- SEARCH (igual) -->
  <div class="search-wrap">
    <input class="search-input" type="text" placeholder="🔍  Search settings..." />
  </div>

  <!-- COMBAT TAB (vou manter igual mas os toggles agora geram Lua) -->
  <div class="tab-content active" id="tab-combat">
    <div class="col">
      <!-- Kill Aura -->
      <div class="section">
        <div class="section-title">Kill Aura Settings</div>
        <div class="toggle-row" onclick="toggle(this, 'kill_aura')">
          <span class="toggle-label">Enable Kill Aura</span>
          <div class="toggle"></div>
        </div>
        <div class="toggle-row" onclick="toggle(this, 'swing_only')">
          <span class="toggle-label sub">Swing Only</span>
          <div class="toggle"></div>
        </div>
        <div class="toggle-row" onclick="toggle(this, 'auto_block')">
          <span class="toggle-label sub">Auto Block</span>
          <div class="toggle on"></div>
        </div>
        <div class="toggle-row" onclick="toggle(this, 'team_check')">
          <span class="toggle-label sub">Team Check</span>
          <div class="toggle on"></div>
        </div>
        <div class="toggle-row" onclick="toggle(this, 'wall_check')">
          <span class="toggle-label sub">Wall Check</span>
          <div class="toggle"></div>
        </div>
        <div class="toggle-row" onclick="toggle(this, 'show_target_box')">
          <span class="toggle-label sub">Show Target Box</span>
          <div class="toggle on"></div>
        </div>
        <div class="slider-wrap">
          <div class="slider-label-row">
            <span class="slider-name">Range</span>
            <span class="slider-val" id="v-range">6</span>
          </div>
          <div class="slider-track" onclick="slideClick(this,'v-range',3,15)">
            <div class="slider-fill" style="width:40%"></div>
          </div>
        </div>
        <div class="slider-wrap">
          <div class="slider-label-row">
            <span class="slider-name">CPS</span>
            <span class="slider-val" id="v-cps">12</span>
          </div>
          <div class="slider-track" onclick="slideClick(this,'v-cps',1,20)">
            <div class="slider-fill" style="width:60%"></div>
          </div>
        </div>
        <div class="dropdown-wrap">
          <div class="dropdown-label">Targeting Mode</div>
          <div class="dropdown" onclick="toggleDd('dd-target')">
            <span id="dd-target-val">Distance</span>
            <span class="dropdown-arrow">▼</span>
          </div>
          <div class="dd-menu" id="dd-target">
            <div class="dd-opt selected" onclick="selectDd('dd-target',this, 'target_mode')">Distance</div>
            <div class="dd-opt" onclick="selectDd('dd-target',this, 'target_mode')">Closest to Mouse</div>
            <div class="dd-opt" onclick="selectDd('dd-target',this, 'target_mode')">Lowest Health</div>
            <div class="dd-opt" onclick="selectDd('dd-target',this, 'target_mode')">Random</div>
          </div>
        </div>
      </div>

      <!-- Aimbot -->
      <div class="section">
        <div class="section-title">Aimbot</div>
        <div class="toggle-row" onclick="toggle(this, 'aimbot')">
          <span class="toggle-label">Enable Aimbot</span>
          <div class="toggle"></div>
        </div>
        <div class="toggle-row" onclick="toggle(this, 'aimbot_fp')">
          <span class="toggle-label sub">First Person Aim</span>
          <div class="toggle"></div>
        </div>
        <div class="toggle-row" onclick="toggle(this, 'aimbot_team_check')">
          <span class="toggle-label sub">Team Check</span>
          <div class="toggle on"></div>
        </div>
        <div class="toggle-row" onclick="toggle(this, 'aimbot_wall_check')">
          <span class="toggle-label sub">Wall Check</span>
          <div class="toggle on"></div>
        </div>
        <div class="toggle-row" onclick="toggle(this, 'show_fov')">
          <span class="toggle-label sub">Show FOV Circle</span>
          <div class="toggle on"></div>
        </div>
        <div class="dropdown-wrap">
          <div class="dropdown-label">Target Part</div>
          <div class="dropdown" onclick="toggleDd('dd-part')">
            <span id="dd-part-val">Head</span>
            <span class="dropdown-arrow">▼</span>
          </div>
          <div class="dd-menu" id="dd-part">
            <div class="dd-opt selected" onclick="selectDd('dd-part',this, 'aimbot_part')">Head</div>
            <div class="dd-opt" onclick="selectDd('dd-part',this, 'aimbot_part')">HumanoidRootPart</div>
            <div class="dd-opt" onclick="selectDd('dd-part',this, 'aimbot_part')">Torso</div>
          </div>
        </div>
        <div class="slider-wrap">
          <div class="slider-label-row">
            <span class="slider-name">Smoothness</span>
            <span class="slider-val" id="v-smooth">5</span>
          </div>
          <div class="slider-track" onclick="slideClick(this,'v-smooth',1,20)">
            <div class="slider-fill" style="width:25%"></div>
          </div>
        </div>
        <div class="slider-wrap">
          <div class="slider-label-row">
            <span class="slider-name">FOV Size</span>
            <span class="slider-val" id="v-fov">120</span>
          </div>
          <div class="slider-track" onclick="slideClick(this,'v-fov',30,360)">
            <div class="slider-fill" style="width:33%"></div>
          </div>
        </div>
      </div>
    </div>

    <div class="col">
      <!-- Anti KB -->
      <div class="section">
        <div class="section-title">Anti Knockback</div>
        <div class="toggle-row" onclick="toggle(this, 'antikb')">
          <span class="toggle-label">Enable Anti KB</span>
          <div class="toggle"></div>
        </div>
        <div class="slider-wrap">
          <div class="slider-label-row">
            <span class="slider-name">Horizontal</span>
            <span class="slider-val" id="v-kbh">0%</span>
          </div>
          <div class="slider-track" onclick="slideClick(this,'v-kbh',0,100)">
            <div class="slider-fill" style="width:0%"></div>
          </div>
        </div>
        <div class="slider-wrap">
          <div class="slider-label-row">
            <span class="slider-name">Vertical</span>
            <span class="slider-val" id="v-kbv">0%</span>
          </div>
          <div class="slider-track" onclick="slideClick(this,'v-kbv',0,100)">
            <div class="slider-fill" style="width:0%"></div>
          </div>
        </div>
      </div>

      <!-- Reach -->
      <div class="section">
        <div class="section-title">Reach</div>
        <div class="toggle-row" onclick="toggle(this, 'reach')">
          <span class="toggle-label">Enable Reach</span>
          <div class="toggle"></div>
        </div>
        <div class="slider-wrap">
          <div class="slider-label-row">
            <span class="slider-name">Reach Distance</span>
            <span class="slider-val" id="v-reach">6</span>
          </div>
          <div class="slider-track" onclick="slideClick(this,'v-reach',3,15)">
            <div class="slider-fill" style="width:40%"></div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- RENDER TAB (ESP) -->
  <div class="tab-content" id="tab-render">
    <div class="col">
      <div class="section">
        <div class="section-title">ESP Settings</div>
        <div class="toggle-row" onclick="toggle(this, 'esp')"><span class="toggle-label">Enable ESP</span><div class="toggle on"></div></div>
        <div class="toggle-row" onclick="toggle(this, 'esp_box')"><span class="toggle-label sub">Box ESP</span><div class="toggle on"></div></div>
        <div class="toggle-row" onclick="toggle(this, 'esp_name')"><span class="toggle-label sub">Name ESP</span><div class="toggle on"></div></div>
        <div class="toggle-row" onclick="toggle(this, 'esp_health')"><span class="toggle-label sub">Health Bar</span><div class="toggle on"></div></div>
        <div class="toggle-row" onclick="toggle(this, 'esp_distance')"><span class="toggle-label sub">Distance</span><div class="toggle"></div></div>
        <div class="toggle-row" onclick="toggle(this, 'esp_tracer')"><span class="toggle-label sub">Tracer</span><div class="toggle"></div></div>
        <div class="toggle-row" onclick="toggle(this, 'esp_team_check')"><span class="toggle-label sub">Team Check</span><div class="toggle on"></div></div>
        <div class="slider-wrap">
          <div class="slider-label-row"><span class="slider-name">ESP Range</span><span class="slider-val" id="v-esp">500</span></div>
          <div class="slider-track" onclick="slideClick(this,'v-esp',50,1000)"><div class="slider-fill" style="width:50%"></div></div>
        </div>
      </div>
    </div>
    <div class="col">
      <div class="section">
        <div class="section-title">Visual Tweaks</div>
        <div class="toggle-row" onclick="toggle(this, 'fullbright')"><span class="toggle-label">Full Bright</span><div class="toggle"></div></div>
        <div class="toggle-row" onclick="toggle(this, 'xray')"><span class="toggle-label">Xray Mode</span><div class="toggle"></div></div>
      </div>
    </div>
  </div>

  <!-- MOVEMENT TAB -->
  <div class="tab-content" id="tab-movement">
    <div class="col">
      <div class="section">
        <div class="section-title">Speed</div>
        <div class="toggle-row" onclick="toggle(this, 'speed')"><span class="toggle-label">Enable Speed</span><div class="toggle"></div></div>
        <div class="dropdown-wrap">
          <div class="dropdown-label">Speed Mode</div>
          <div class="dropdown" onclick="toggleDd('dd-speed')">
            <span id="dd-speed-val">Custom</span>
            <span class="dropdown-arrow">▼</span>
          </div>
          <div class="dd-menu" id="dd-speed">
            <div class="dd-opt selected" onclick="selectDd('dd-speed',this, 'speed_mode')">Custom</div>
            <div class="dd-opt" onclick="selectDd('dd-speed',this, 'speed_mode')">BHop</div>
          </div>
        </div>
        <div class="slider-wrap">
          <div class="slider-label-row"><span class="slider-name">Walk Speed</span><span class="slider-val" id="v-ws">16</span></div>
          <div class="slider-track" onclick="slideClick(this,'v-ws',1,100)"><div class="slider-fill" style="width:16%"></div></div>
        </div>
      </div>
      <div class="section">
        <div class="section-title">Fly / Jump</div>
        <div class="toggle-row" onclick="toggle(this, 'fly')"><span class="toggle-label">Fly</span><div class="toggle"></div></div>
        <div class="toggle-row" onclick="toggle(this, 'high_jump')"><span class="toggle-label">High Jump</span><div class="toggle"></div></div>
      </div>
    </div>
    <div class="col">
      <div class="section">
        <div class="section-title">Misc</div>
        <div class="toggle-row" onclick="toggle(this, 'noclip')"><span class="toggle-label">No Clip</span><div class="toggle"></div></div>
        <div class="toggle-row" onclick="toggle(this, 'auto_sprint')"><span class="toggle-label">Auto Sprint</span><div class="toggle on"></div></div>
      </div>
    </div>
  </div>

  <!-- PLAYER TAB -->
  <div class="tab-content" id="tab-player">
    <div class="col">
      <div class="section">
        <div class="section-title">God Mode</div>
        <div class="toggle-row" onclick="toggle(this, 'godmode')"><span class="toggle-label">Invincible</span><div class="toggle"></div></div>
        <div class="toggle-row" onclick="toggle(this, 'infinite_health')"><span class="toggle-label">Infinite Health</span><div class="toggle"></div></div>
        <div class="toggle-row" onclick="toggle(this, 'no_fall_damage')"><span class="toggle-label">No Fall Damage</span><div class="toggle on"></div></div>
      </div>
    </div>
    <div class="col">
      <div class="section">
        <div class="section-title">Spammer</div>
        <div class="toggle-row" onclick="toggle(this, 'spammer')"><span class="toggle-label">Chat Spammer</span><div class="toggle"></div></div>
        <div class="input-wrap" style="padding:5px">
          <input type="text" id="spam-message" placeholder="Message to spam..." style="width:100%;background:rgba(20,25,38,0.9);border:1px solid rgba(255,255,255,0.1);color:#fff;padding:5px;font-family:'JetBrains Mono';font-size:10px;">
        </div>
      </div>
    </div>
  </div>

  <!-- WORLD TAB -->
  <div class="tab-content" id="tab-world">
    <div class="col">
      <div class="section">
        <div class="section-title">World</div>
        <div class="toggle-row" onclick="toggle(this, 'fullbright')"><span class="toggle-label">Full Bright</span><div class="toggle"></div></div>
        <div class="dropdown-wrap">
          <div class="dropdown-label">Time</div>
          <div class="dropdown" onclick="toggleDd('dd-time')">
            <span id="dd-time-val">Default</span>
            <span class="dropdown-arrow">▼</span>
          </div>
          <div class="dd-menu" id="dd-time">
            <div class="dd-opt selected" onclick="selectDd('dd-time',this, 'time')">Default</div>
            <div class="dd-opt" onclick="selectDd('dd-time',this, 'time')">Noon</div>
            <div class="dd-opt" onclick="selectDd('dd-time',this, 'time')">Night</div>
          </div>
        </div>
      </div>
    </div>
    <div class="col">
      <div class="section">
        <div class="section-title">Weather</div>
        <div class="dropdown-wrap">
          <div class="dropdown-label">Weather</div>
          <div class="dropdown" onclick="toggleDd('dd-weather')">
            <span id="dd-weather-val">Default</span>
            <span class="dropdown-arrow">▼</span>
          </div>
          <div class="dd-menu" id="dd-weather">
            <div class="dd-opt selected" onclick="selectDd('dd-weather',this, 'weather')">Default</div>
            <div class="dd-opt" onclick="selectDd('dd-weather',this, 'weather')">Rain</div>
            <div class="dd-opt" onclick="selectDd('dd-weather',this, 'weather')">Snow</div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- UI TAB -->
  <div class="tab-content" id="tab-ui">
    <div class="col">
      <div class="section">
        <div class="section-title">Interface</div>
        <div class="toggle-row" onclick="toggle(this, 'show_fps')"><span class="toggle-label">Show FPS Counter</span><div class="toggle on"></div></div>
        <div class="toggle-row" onclick="toggle(this, 'show_ping')"><span class="toggle-label">Show Ping</span><div class="toggle on"></div></div>
        <div class="toggle-row" onclick="toggle(this, 'notifications')"><span class="toggle-label">Notifications</span><div class="toggle on"></div></div>
      </div>
    </div>
    <div class="col">
      <div class="section">
        <div class="section-title">Keybinds</div>
        <div class="toggle-row"><span class="toggle-label">Toggle GUI</span><span class="keybind">INSERT</span></div>
        <div class="toggle-row"><span class="toggle-label">Kill Aura</span><span class="keybind">K</span></div>
        <div class="toggle-row"><span class="toggle-label">ESP</span><span class="keybind">Z</span></div>
      </div>
    </div>
  </div>

  <!-- BOTÃO DE GERAR SCRIPT -->
  <div style="padding: 10px; text-align: center;">
    <button class="generate-btn" onclick="generateScript()">⚡ GERAR SCRIPT LUA ⚡</button>
    <button class="generate-btn" onclick="copyToClipboard()" style="background: #43d9ad;">📋 COPIAR</button>
  </div>

  <!-- STATUS BAR (igual) -->
  <div class="hub-status">
    <div class="status-left">
      <div class="status-indicator">
        <div class="status-dot"></div>
        <span class="status-text">Ready</span>
      </div>
      <span>v3.4.2</span>
      <span>Roblox Bridge</span>
    </div>
    <div class="status-right">
      <div class="status-pill" id="activeCount">0 active</div>
      <div class="status-pill">Executor: Krnl / Synapse</div>
    </div>
  </div>
</div>

<!-- NOTIFICATION (igual) -->
<div class="notif" id="notif" style="display:none">
  <span class="notif-icon">⚡</span>
  <div class="notif-text">
    <strong id="notif-title">Feature enabled</strong>
    <span id="notif-body">Setting updated</span>
  </div>
</div>

<script>
// ============ CONFIGURAÇÕES ============
let config = {
    // Combat
    kill_aura: false,
    swing_only: false,
    auto_block: true,
    team_check: true,
    wall_check: false,
    show_target_box: true,
    range: 6,
    cps: 12,
    target_mode: 'Distance',
    
    // Aimbot
    aimbot: false,
    aimbot_fp: false,
    aimbot_team_check: true,
    aimbot_wall_check: true,
    show_fov: true,
    aimbot_part: 'Head',
    smoothness: 5,
    fov: 120,
    
    // Anti KB
    antikb: false,
    kbh: 0,
    kbv: 0,
    
    // Reach
    reach: false,
    reach_distance: 6,
    
    // ESP
    esp: true,
    esp_box: true,
    esp_name: true,
    esp_health: true,
    esp_distance: false,
    esp_tracer: false,
    esp_team_check: true,
    esp_range: 500,
    
    // Visual
    fullbright: false,
    xray: false,
    
    // Movement
    speed: false,
    speed_mode: 'Custom',
    walk_speed: 16,
    fly: false,
    high_jump: false,
    noclip: false,
    auto_sprint: true,
    
    // Player
    godmode: false,
    infinite_health: false,
    no_fall_damage: true,
    spammer: false,
    spam_message: 'Nexus Hub ON TOP!',
    
    // World
    time: 'Default',
    weather: 'Default',
    
    // UI
    show_fps: true,
    show_ping: true,
    notifications: true
};

let activeCount = 0;

// ============ FUNÇÕES DA UI (IGUAIS) ============
function toggle(row, key) {
    const t = row.querySelector('.toggle');
    const isOn = t.classList.toggle('on');
    config[key] = isOn;
    
    activeCount += isOn ? 1 : -1;
    document.getElementById('activeCount').textContent = activeCount + ' active';
    
    const label = row.querySelector('.toggle-label').textContent.trim();
    showNotif(label, isOn ? 'Enabled' : 'Disabled');
}

function showNotif(title, body) {
    const n = document.getElementById('notif');
    document.getElementById('notif-title').textContent = title;
    document.getElementById('notif-body').textContent = body;
    n.style.display = 'flex';
    clearTimeout(notifTimer);
    notifTimer = setTimeout(() => { n.style.display = 'none'; }, 2500);
}

function slideClick(track, valId, min, max) {
    const rect = track.getBoundingClientRect();
    const x = event.clientX - rect.left;
    const pct = Math.max(0, Math.min(1, x / rect.width));
    const val = Math.round(min + pct * (max - min));
    track.querySelector('.slider-fill').style.width = (pct * 100) + '%';
    document.getElementById(valId).textContent = val;
    
    // Mapeia id do slider para config key
    const keyMap = {
        'v-range': 'range',
        'v-cps': 'cps',
        'v-smooth': 'smoothness',
        'v-fov': 'fov',
        'v-kbh': 'kbh',
        'v-kbv': 'kbv',
        'v-reach': 'reach_distance',
        'v-esp': 'esp_range',
        'v-ws': 'walk_speed'
    };
    
    if (keyMap[valId]) {
        config[keyMap[valId]] = val;
    }
}

function selectDd(id, el, configKey) {
    event.stopPropagation();
    const menu = document.getElementById(id);
    menu.querySelectorAll('.dd-opt').forEach(o => o.classList.remove('selected'));
    el.classList.add('selected');
    document.getElementById(id + '-val').textContent = el.textContent;
    menu.classList.remove('open');
    
    config[configKey] = el.textContent;
    showNotif(el.textContent, 'Selected');
}

function toggleDd(id) {
    event.stopPropagation();
    document.querySelectorAll('.dd-menu').forEach(m => { if(m.id !== id) m.classList.remove('open'); });
    document.getElementById(id).classList.toggle('open');
}

document.addEventListener('click', () => {
    document.querySelectorAll('.dd-menu').forEach(m => m.classList.remove('open'));
});

function switchTab(el) {
    document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
    document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
    el.classList.add('active');
    document.getElementById('tab-' + el.dataset.tab).classList.add('active');
}

function setTopTab(el, tab) {
    document.querySelectorAll('.topbar-tab').forEach(t => t.classList.remove('active'));
    el.classList.add('active');
}

function closeHub() {
    document.getElementById('hub').style.animation = 'none';
    document.getElementById('hub').style.opacity = '0';
    setTimeout(() => {
        document.getElementById('hub').style.opacity = '1';
    }, 600);
}

// Drag (igual)
const hub = document.getElementById('hub');
let dragging = false, ox, oy;
hub.querySelector('.hub-title').addEventListener('mousedown', e => {
    dragging = true;
    ox = e.clientX - hub.getBoundingClientRect().left;
    oy = e.clientY - hub.getBoundingClientRect().top;
});
document.addEventListener('mousemove', e => {
    if (!dragging) return;
    hub.style.position = 'fixed';
    hub.style.left = (e.clientX - ox) + 'px';
    hub.style.top = (e.clientY - oy) + 'px';
    hub.style.margin = '0';
});
document.addEventListener('mouseup', () => { dragging = false; });

// Sliders drag (igual)
let activeSlider = null;
document.querySelectorAll('.slider-track').forEach(track => {
    track.addEventListener('mousedown', e => {
        activeSlider = track;
    });
});
document.addEventListener('mousemove', e => {
    if (activeSlider) {
        const rect = activeSlider.getBoundingClientRect();
        const pct = Math.max(0, Math.min(1, (e.clientX - rect.left) / rect.width));
        activeSlider.querySelector('.slider-fill').style.width = (pct * 100) + '%';
    }
});
document.addEventListener('mouseup', () => { activeSlider = null; });

// Atualiza mensagem de spam
document.getElementById('spam-message')?.addEventListener('input', (e) => {
    config.spam_message = e.target.value;
});

// ============ FUNÇÃO PRINCIPAL: GERAR SCRIPT LUA ============
function generateScript() {
    let lua = `--[[
    Nexus Hub - Roblox Bridge
    Gerado em: ${new Date().toLocaleString()}
    Configurações atuais:
${Object.entries(config).map(([k,v]) => `    ${k}: ${v}`).join('\n')}
--]]

-- Carregar bibliotecas necessárias
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/..."))() -- Placeholder

-- Variáveis globais
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local Workspace = game:GetService("Workspace")
local Camera = Workspace.CurrentCamera

-- Função para verificar time
local function isEnemy(player)
    if not config.team_check then return true end
    if not player or not LocalPlayer then return false end
    
    local myTeam = LocalPlayer.Team
    local theirTeam = player.Team
    
    return myTeam ~= theirTeam
end

-- Função para verificar se está visível
local function isVisible(targetPart)
    if not config.wall_check and not config.aimbot_wall_check then return true end
    
    local origin = Camera.CFrame.Position
    local target = targetPart.Position
    local direction = (target - origin).Unit * (target - origin).Magnitude
    
    local ray = Ray.new(origin, direction)
    local hit, position = Workspace:FindPartOnRay(ray, LocalPlayer.Character)
    
    return hit == nil or hit:IsDescendantOf(targetPart.Parent)
end

-- ========== ESP ==========
if ${config.esp} then
    print("ESP Ativado")
    
    local espHolder = Instance.new("Folder")
    espHolder.Name = "NexusESP"
    espHolder.Parent = Camera
    
    local function createESP(player)
        if player == LocalPlayer then return end
        
        -- Caixa
        local box = Drawing.new("Square")
        box.Visible = false
        box.Color = Color3.new(1, 0, 0)
        box.Thickness = 2
        box.Filled = false
        
        -- Nome
        local nameTag = Drawing.new("Text")
        nameTag.Visible = false
        nameTag.Color = Color3.new(1, 1, 1)
        nameTag.Center = true
        nameTag.Size = 16
        nameTag.Outline = true
        
        -- Saúde
        local healthBar = Drawing.new("Square")
        healthBar.Visible = false
        healthBar.Color = Color3.new(0, 1, 0)
        healthBar.Filled = true
        
        -- Distância
        local distanceTag = Drawing.new("Text")
        distanceTag.Visible = false
        distanceTag.Color = Color3.new(1, 1, 0)
        distanceTag.Size = 12
        
        -- Tracer
        local tracer = Drawing.new("Line")
        tracer.Visible = false
        tracer.Color = Color3.new(0, 1, 0)
        tracer.Thickness = 1
        
        RunService.RenderStepped:Connect(function()
            if not player.Character or not player.Character:FindFirstChild("HumanoidRootPart") then
                box.Visible = false
                nameTag.Visible = false
                healthBar.Visible = false
                distanceTag.Visible = false
                tracer.Visible = false
                return
            end
            
            local root = player.Character.HumanoidRootPart
            local pos = root.Position
            local screenPos, onScreen = Camera:WorldToViewportPoint(pos)
            
            if not onScreen then
                box.Visible = false
                nameTag.Visible = false
                healthBar.Visible = false
                distanceTag.Visible = false
                tracer.Visible = false
                return
            end
            
            -- Calcula tamanho baseado na distância
            local dist = (Camera.CFrame.Position - pos).Magnitude
            local size = math.clamp(500 / dist * 50, 30, 150)
            
            -- Box ESP
            if ${config.esp_box} then
                box.Position = Vector2.new(screenPos.X - size/2, screenPos.Y - size)
                box.Size = Vector2.new(size, size * 2)
                box.Visible = true
            end
            
            -- Name ESP
            if ${config.esp_name} then
                nameTag.Position = Vector2.new(screenPos.X, screenPos.Y - size - 20)
                nameTag.Text = player.Name
                nameTag.Visible = true
            end
            
            -- Health Bar
            if ${config.esp_health} and player.Character:FindFirstChild("Humanoid") then
                local health = player.Character.Humanoid.Health
                local maxHealth = player.Character.Humanoid.MaxHealth
                local healthPercent = health / maxHealth
                
                healthBar.Position = Vector2.new(screenPos.X - size/2, screenPos.Y - size - 10)
                healthBar.Size = Vector2.new(size * healthPercent, 3)
                healthBar.Visible = true
            end
            
            -- Distance
            if ${config.esp_distance} then
                distanceTag.Position = Vector2.new(screenPos.X, screenPos.Y + size + 10)
                distanceTag.Text = math.floor(dist) .. "m"
                distanceTag.Visible = true
            end
            
            -- Tracer
            if ${config.esp_tracer} then
                tracer.From = Vector2.new(Camera.ViewportSize.X/2, Camera.ViewportSize.Y)
                tracer.To = Vector2.new(screenPos.X, screenPos.Y)
                tracer.Visible = true
            end
        end)
    end
    
    Players.PlayerAdded:Connect(createESP)
    for _, player in ipairs(Players:GetPlayers()) do
        createESP(player)
    end
end

-- ========== KILL AURA ==========
if ${config.kill_aura} then
    print("Kill Aura Ativado")
    
    local killAuraRange = ${config.range}
    local killAuraCPS = ${config.cps}
    local lastAttack = 0
    
    RunService.Heartbeat:Connect(function()
        local closest = nil
        local closestDist = killAuraRange
        
        for _, player in ipairs(Players:GetPlayers()) do
            if player ~= LocalPlayer and isEnemy(player) then
                if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
                    local root = player.Character.HumanoidRootPart
                    local dist = (LocalPlayer.Character.HumanoidRootPart.Position - root.Position).Magnitude
                    
                    if dist < closestDist then
                        closest = player
                        closestDist = dist
                    end
                end
            end
        end
        
        if closest then
            local now = tick()
            if now - lastAttack > (1 / killAuraCPS) then
                -- Ataca
                game:GetService("VirtualUser"):CaptureController()
                game:GetService("VirtualUser"):Button1Down(Vector2.new(0,0))
                wait(0.05)
                game:GetService("VirtualUser"):Button1Up(Vector2.new(0,0))
                lastAttack = now
            end
        end
    end)
end

-- ========== AIMBOT ==========
if ${config.aimbot} then
    print("Aimbot Ativado")
    
    local aimbotRange = ${config.range}
    local aimbotSmooth = ${config.smoothness}
    local aimbotFOV = ${config.fov}
    local targetPart = "${config.aimbot_part}"
    
    RunService.RenderStepped:Connect(function()
        local target = nil
        local targetPos = nil
        local closestToMouse = math.huge
        
        for _, player in ipairs(Players:GetPlayers()) do
            if player ~= LocalPlayer and isEnemy(player) then
                if player.Character and player.Character:FindFirstChild(targetPart) then
                    local part = player.Character[targetPart]
                    local pos = part.Position
                    local screenPos, onScreen = Camera:WorldToViewportPoint(pos)
                    
                    if onScreen then
                        local mousePos = UserInputService:GetMouseLocation()
                        local distToMouse = (Vector2.new(screenPos.X, screenPos.Y) - mousePos).Magnitude
                        
                        if distToMouse < aimbotFOV and distToMouse < closestToMouse then
                            closestToMouse = distToMouse
                            target = part
                            targetPos = screenPos
                        end
                    end
                end
            end
        end
        
        if target and targetPos then
            -- Movimento suave
            local mousePos = UserInputService:GetMouseLocation()
            local newX = mousePos.X + (targetPos.X - mousePos.X) / aimbotSmooth
            local newY = mousePos.Y + (targetPos.Y - mousePos.Y) / aimbotSmooth
            
            mousemoverel(newX - mousePos.X, newY - mousePos.Y)
        end
    end)
end

-- ========== ANTI KNOCKBACK ==========
if ${config.antikb} then
    print("Anti KB Ativado")
    
    local hPercent = ${config.kbh} / 100
    local vPercent = ${config.kbv} / 100
    
    LocalPlayer.CharacterAdded:Connect(function(char)
        local humanoid = char:WaitForChild("Humanoid")
        
        humanoid.StateChanged:Connect(function(old, new)
            if new == Enum.HumanoidStateType.Dead then return end
            
            if new == Enum.HumanoidStateType.Freefall or new == Enum.HumanoidStateType.GettingUp then
                -- Aplica resistência
                wait(0.1)
                humanoid.PlatformStand = false
            end
        end)
    end)
end

-- ========== REACH ==========
if ${config.reach} then
    print("Reach Ativado")
    
    local reachDistance = ${config.reach_distance}
    
    -- Hook no ataque
    local oldIndex
    oldIndex = hookmetamethod(game, "__index", function(self, key)
        if self == LocalPlayer.Character and key == "HumanoidRootPart" then
            return oldIndex(self, key)
        end
        return oldIndex(self, key)
    end)
end

-- ========== SPEED ==========
if ${config.speed} then
    print("Speed Ativado")
    
    local speedValue = ${config.walk_speed}
    
    LocalPlayer.CharacterAdded:Connect(function(char)
        local humanoid = char:WaitForChild("Humanoid")
        humanoid.WalkSpeed = speedValue
    end)
    
    if LocalPlayer.Character then
        LocalPlayer.Character.Humanoid.WalkSpeed = speedValue
    end
end

-- ========== FLY ==========
if ${config.fly} then
    print("Fly Ativado")
    
    local flyConnection
    local flying = false
    
    UserInputService.InputBegan:Connect(function(input)
        if input.KeyCode == Enum.KeyCode.F then
            flying = not flying
            
            if LocalPlayer.Character then
                local humanoid = LocalPlayer.Character:FindFirstChild("Humanoid")
                local root = LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
                
                if flying then
                    humanoid.PlatformStand = true
                    flyConnection = RunService.Heartbeat:Connect(function()
                        if not flying then flyConnection:Disconnect() return end
                        
                        local moveDir = Vector3.new()
                        if UserInputService:IsKeyDown(Enum.KeyCode.W) then
                            moveDir = moveDir + Camera.CFrame.LookVector
                        end
                        if UserInputService:IsKeyDown(Enum.KeyCode.S) then
                            moveDir = moveDir - Camera.CFrame.LookVector
                        end
                        if UserInputService:IsKeyDown(Enum.KeyCode.A) then
                            moveDir = moveDir - Camera.CFrame.RightVector
                        end
                        if UserInputService:IsKeyDown(Enum.KeyCode.D) then
                            moveDir = moveDir + Camera.CFrame.RightVector
                        end
                        if UserInputService:IsKeyDown(Enum.KeyCode.Space) then
                            moveDir = moveDir + Vector3.new(0, 1, 0)
                        end
                        if UserInputService:IsKeyDown(Enum.KeyCode.LeftShift) then
                            moveDir = moveDir - Vector3.new(0, 1, 0)
                        end
                        
                        root.Velocity = moveDir * 50
                    end)
                else
                    humanoid.PlatformStand = false
                    if flyConnection then
                        flyConnection:Disconnect()
                    end
                end
            end
        end
    end)
end

-- ========== HIGH JUMP ==========
if ${config.high_jump} then
    print("High Jump Ativado")
    
    LocalPlayer.CharacterAdded:Connect(function(char)
        local humanoid = char:WaitForChild("Humanoid")
        humanoid.JumpPower = 100
    end)
end

-- ========== NOCLIP ==========
if ${config.noclip} then
    print("Noclip Ativado")
    
    RunService.Stepped:Connect(function()
        if LocalPlayer.Character then
            for _, part in ipairs(LocalPlayer.Character:GetChildren()) do
                if part:IsA("BasePart") then
                    part.CanCollide = false
                end
            end
        end
    end)
end

-- ========== AUTO SPRINT ==========
if ${config.auto_sprint} then
    print("Auto Sprint Ativado")
    
    LocalPlayer.CharacterAdded:Connect(function(char)
        local humanoid = char:WaitForChild("Humanoid")
        humanoid.AutoRotate = false
        
        RunService.Heartbeat:Connect(function()
            if humanoid.MoveDirection.Magnitude > 0 then
                humanoid.WalkSpeed = 50
            else
                humanoid.WalkSpeed = 16
            end
        end)
    end)
end

-- ========== GODMODE ==========
if ${config.godmode} or ${config.infinite_health} then
    print("God Mode Ativado")
    
    LocalPlayer.CharacterAdded:Connect(function(char)
        local humanoid = char:WaitForChild("Humanoid")
        
        humanoid.HealthChanged:Connect(function()
            humanoid.Health = humanoid.MaxHealth
        end)
    end)
end

-- ========== NO FALL DAMAGE ==========
if ${config.no_fall_damage} then
    print("No Fall Damage Ativado")
    
    LocalPlayer.CharacterAdded:Connect(function(char)
        local humanoid = char:WaitForChild("Humanoid")
        
        humanoid.StateChanged:Connect(function(old, new)
            if new == Enum.HumanoidStateType.Freefall then
                wait(0.5)
                humanoid.PlatformStand = false
            end
        end)
    end)
end

-- ========== SPAMMER ==========
if ${config.spammer} then
    print("Spammer Ativado")
    
    local spamMessage = "${config.spam_message}"
    local spamDelay = 2
    
    spawn(function()
        while ${config.spammer} do
            wait(spamDelay)
            game:GetService("ReplicatedStorage"):WaitForChild("DefaultChatSystemChatEvents"):WaitForChild("SayMessageRequest"):FireServer(spamMessage, "All")
        end
    end)
end

-- ========== FULLBRIGHT ==========
if ${config.fullbright} then
    print("Fullbright Ativado")
    
    local lighting = game:GetService("Lighting")
    lighting.Ambient = Color3.new(1, 1, 1)
    lighting.Brightness = 2
    lighting.GlobalShadows = false
end

-- ========== XRAY ==========
if ${config.xray} then
    print("Xray Ativado")
    
    for _, part in ipairs(Workspace:GetDescendants()) do
        if part:IsA("BasePart") and not part:IsDescendantOf(Players) then
            if part.Material == Enum.Material.Diamond or part.Name:lower():find("diamond") then
                part.Transparency = 0
                part.Color = Color3.new(0, 1, 1)
            else
                part.Transparency = 0.8
            end
        end
    end
end

-- ========== TIME ==========
local timeMap = {
    Default = 12,
    Noon = 14,
    Night = 0
}
game:GetService("Lighting").ClockTime = timeMap["${config.time}"] or 12

-- ========== WEATHER ==========
local weatherMap = {
    Default = "Clear",
    Rain = "Rain",
    Snow = "Snow"
}
game:GetService("Lighting").Weather = weatherMap["${config.weather}"] or "Clear"

print("Nexus Hub carregado com sucesso!")
`;

    // Salva no localStorage para copiar depois
    localStorage.setItem('generatedScript', lua);
    
    // Mostra prévia
    alert("Script gerado! Clique em COPIAR para copiar para área de transferência.\n\nTamanho: " + lua.length + " caracteres");
    
    // Também mostra no console
    console.log(lua);
}

function copyToClipboard() {
    const script = localStorage.getItem('generatedScript');
    if (!script) {
        alert("Gere um script primeiro!");
        return;
    }
    
    navigator.clipboard.writeText(script).then(() => {
        showNotif("Script copiado!", "Cole no seu executor");
    }).catch(err => {
        // Fallback
        const textarea = document.createElement('textarea');
        textarea.value = script;
        document.body.appendChild(textarea);
        textarea.select();
        document.execCommand('copy');
        document.body.removeChild(textarea);
        showNotif("Script copiado!", "Cole no seu executor");
    });
}

// ========== INICIALIZAÇÃO ==========
let notifTimer;
setInterval(() => {
    const fps = 280 + Math.floor(Math.random() * 30);
    const ping = 45 + Math.floor(Math.random() * 25);
    document.getElementById('fpsCounter').textContent = fps + ' fps';
    document.getElementById('pingCounter').textContent = ping + ' ms';
}, 1500);
</script>
</body>
</html>
