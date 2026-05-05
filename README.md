<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>For the Record</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Mono:ital,wght@0,400;0,500;1,400&family=Playfair+Display:ital,wght@0,400;0,700;0,900;1,700&display=swap" rel="stylesheet">
<style>
/* ═══════════════════════════════════════════
   BASE
═══════════════════════════════════════════ */
:root {
  --bg: #0b0b0b;
  --surface: #141414;
  --surface2: #1b1b1b;
  --surface3: #212121;
  --border: #272727;
  --border2: #333;
  --accent: #e2b94a;
  --accent-dim: rgba(226,185,74,0.1);
  --accent2: #c47a3a;
  --text: #e6e1d6;
  --text2: #9a9088;
  --muted: #555;
  --green: #6fcf7a;
  --yellow: #f0c060;
  --red: #e07050;
  --panel-w: 490px;
}
*,*::before,*::after { box-sizing: border-box; margin: 0; padding: 0; }
body {
  background: var(--bg); color: var(--text);
  font-family: 'DM Mono', monospace;
  min-height: 100vh; overflow-x: hidden;
}

/* ═══════════════════════════════════════════
   SHARED BUTTONS
═══════════════════════════════════════════ */
.btn {
  background: var(--accent); color: #000; border: none;
  font-family: 'DM Mono', monospace; font-size: 0.72rem; font-weight: 500;
  padding: 9px 16px; border-radius: 3px; cursor: pointer;
  letter-spacing: 0.07em; text-transform: uppercase;
  transition: background 0.15s; white-space: nowrap; display: inline-block;
}
.btn:hover { background: #ecca60; }
.btn:disabled { opacity: 0.35; cursor: not-allowed; }

.btn-ghost {
  background: none; border: 1px solid var(--border2); color: var(--text2);
  font-family: 'DM Mono', monospace; font-size: 0.72rem;
  padding: 9px 16px; border-radius: 3px; cursor: pointer;
  letter-spacing: 0.06em; text-transform: uppercase;
  transition: border-color 0.15s, color 0.15s; white-space: nowrap;
}
.btn-ghost:hover { border-color: var(--accent); color: var(--accent); }
.btn-ghost:disabled { opacity: 0.35; cursor: not-allowed; }

.btn-outline-accent {
  background: none; border: 1px solid var(--accent); color: var(--accent);
  font-family: 'DM Mono', monospace; font-size: 0.72rem;
  padding: 9px 16px; border-radius: 3px; cursor: pointer;
  letter-spacing: 0.06em; text-transform: uppercase;
  transition: background 0.15s; white-space: nowrap;
}
.btn-outline-accent:hover { background: var(--accent-dim); }
.btn-outline-accent:disabled { opacity: 0.35; cursor: not-allowed; }

/* ═══════════════════════════════════════════
   SHARED HEADER
═══════════════════════════════════════════ */
.app-header {
  background: var(--surface); border-bottom: 1px solid var(--border);
  padding: 16px 36px; display: flex; align-items: center; gap: 20px;
  position: sticky; top: 0; z-index: 30; flex-wrap: wrap;
}
.wordmark {
  display: flex; flex-direction: column; line-height: 1;
  border-right: 1px solid var(--border); padding-right: 20px; flex-shrink: 0;
}
.wordmark-eyebrow { font-size: 0.48rem; letter-spacing: 0.2em; text-transform: uppercase; color: var(--muted); margin-bottom: 2px; }
.wordmark-name {
  font-family: 'Playfair Display', serif;
  font-size: 1.45rem; font-weight: 900; font-style: italic;
  color: var(--accent); letter-spacing: -0.02em;
}
.wordmark-tagline { font-size: 0.46rem; letter-spacing: 0.16em; text-transform: uppercase; color: var(--muted); margin-top: 2px; }

.mode-switcher {
  display: flex; gap: 6px; align-items: center;
}
.mode-tab {
  background: none; border: 1px solid var(--border); color: var(--muted);
  font-family: 'DM Mono', monospace; font-size: 0.64rem;
  padding: 6px 12px; border-radius: 3px; cursor: pointer;
  letter-spacing: 0.06em; text-transform: uppercase;
  transition: all 0.15s;
}
.mode-tab:hover { border-color: var(--border2); color: var(--text2); }
.mode-tab.active { border-color: var(--accent); color: var(--accent); background: var(--accent-dim); }

.header-right { margin-left: auto; display: flex; align-items: center; gap: 8px; }
.back-home {
  background: none; border: none; color: var(--muted); font-family: 'DM Mono', monospace;
  font-size: 0.62rem; letter-spacing: 0.08em; text-transform: uppercase;
  cursor: pointer; padding: 5px 8px; border-radius: 3px;
  transition: color 0.15s;
}
.back-home:hover { color: var(--accent); }

/* ═══════════════════════════════════════════
   SCREENS
═══════════════════════════════════════════ */
.screen { display: none; }
.screen.active { display: block; }

/* ═══════════════════════════════════════════
   HOME / MODE SELECT
═══════════════════════════════════════════ */
#screen-home {
  min-height: 100vh; display: none;
  flex-direction: column; align-items: center; justify-content: center;
  padding: 40px 20px; gap: 0;
  background: radial-gradient(ellipse at 50% 30%, rgba(226,185,74,0.04) 0%, transparent 65%);
}
#screen-home.active { display: flex; }

.home-logo {
  text-align: center; margin-bottom: 52px;
}
.home-eyebrow { font-size: 0.58rem; letter-spacing: 0.25em; text-transform: uppercase; color: var(--muted); margin-bottom: 10px; }
.home-title {
  font-family: 'Playfair Display', serif;
  font-size: clamp(3rem, 8vw, 5.5rem); font-weight: 900; font-style: italic;
  color: var(--accent); letter-spacing: -0.03em; line-height: 0.95;
  display: block;
}
.home-subtitle { font-size: 0.68rem; letter-spacing: 0.18em; text-transform: uppercase; color: var(--muted); margin-top: 14px; }

.home-prompt { font-size: 0.72rem; color: var(--text2); margin-bottom: 28px; text-align: center; letter-spacing: 0.03em; }

.mode-cards {
  display: flex; gap: 20px; flex-wrap: wrap; justify-content: center;
  max-width: 700px; width: 100%;
}

.mode-card {
  flex: 1; min-width: 260px; max-width: 320px;
  background: var(--surface); border: 1px solid var(--border);
  border-radius: 6px; padding: 32px 28px;
  cursor: pointer; transition: border-color 0.2s, background 0.2s, transform 0.2s;
  text-align: center; display: flex; flex-direction: column; gap: 14px; align-items: center;
}
.mode-card:hover {
  border-color: var(--accent); background: rgba(226,185,74,0.03);
  transform: translateY(-3px);
}
.mode-card-icon { font-size: 2.4rem; line-height: 1; }
.mode-card-title {
  font-family: 'Playfair Display', serif; font-size: 1.2rem; font-weight: 700; font-style: italic;
  color: var(--text);
}
.mode-card-desc { font-size: 0.68rem; color: var(--text2); line-height: 1.75; }
.mode-card-cta {
  margin-top: 6px; font-size: 0.62rem; letter-spacing: 0.1em;
  text-transform: uppercase; color: var(--accent);
}

.home-footer { margin-top: 52px; font-size: 0.58rem; color: var(--muted); letter-spacing: 0.1em; text-align: center; }

/* ═══════════════════════════════════════════
   SNAP & ANALYZE (PHOTO MODE)
═══════════════════════════════════════════ */
#screen-snap { min-height: calc(100vh - 57px); }

.snap-layout {
  display: grid; grid-template-columns: 1fr 1fr;
  min-height: calc(100vh - 57px);
}
@media (max-width: 768px) { .snap-layout { grid-template-columns: 1fr; } }

/* Left: Upload zone */
.snap-left {
  border-right: 1px solid var(--border);
  padding: 36px; display: flex; flex-direction: column; gap: 20px;
  background: var(--surface);
}
.snap-left h2 { font-family: 'Playfair Display', serif; font-size: 1.1rem; font-weight: 700; color: var(--text); }
.snap-left p { font-size: 0.7rem; color: var(--text2); line-height: 1.7; }

.drop-zone {
  border: 2px dashed var(--border2); border-radius: 6px;
  aspect-ratio: 1; display: flex; flex-direction: column;
  align-items: center; justify-content: center; gap: 12px;
  cursor: pointer; transition: border-color 0.2s, background 0.2s;
  position: relative; overflow: hidden; background: var(--bg);
  min-height: 240px;
}
.drop-zone:hover, .drop-zone.drag-over { border-color: var(--accent); background: var(--accent-dim); }
.drop-zone-icon { font-size: 2.4rem; opacity: 0.35; }
.drop-zone-text { font-size: 0.7rem; color: var(--muted); text-align: center; line-height: 1.6; }
.drop-zone-text em { color: var(--accent); font-style: normal; }
.drop-zone input[type="file"] { position: absolute; inset: 0; opacity: 0; cursor: pointer; font-size: 0; }

.drop-zone-preview {
  width: 100%; height: 100%; object-fit: contain;
  position: absolute; inset: 0;
}

.snap-meta { display: flex; flex-direction: column; gap: 10px; }
.snap-meta-row { display: flex; flex-direction: column; gap: 4px; }
.snap-meta-label { font-size: 0.58rem; text-transform: uppercase; letter-spacing: 0.1em; color: var(--muted); }
.snap-meta-input {
  background: var(--bg); border: 1px solid var(--border); color: var(--text);
  font-family: 'DM Mono', monospace; font-size: 0.74rem;
  padding: 8px 10px; border-radius: 3px; width: 100%;
  transition: border-color 0.2s;
}
.snap-meta-input:focus { outline: none; border-color: var(--accent); }
.snap-meta-input::placeholder { color: var(--muted); }

.snap-actions { display: flex; gap: 9px; }

/* Right: Analysis output */
.snap-right {
  padding: 36px; display: flex; flex-direction: column; gap: 0;
  overflow-y: auto;
}

.snap-idle {
  flex: 1; display: flex; flex-direction: column;
  align-items: center; justify-content: center; gap: 14px;
  color: var(--muted); text-align: center; padding: 40px;
}
.snap-idle-icon { font-size: 3rem; opacity: 0.2; }
.snap-idle-text { font-size: 0.72rem; line-height: 1.75; }

.snap-analyzing {
  flex: 1; display: none; flex-direction: column;
  align-items: center; justify-content: center; gap: 18px;
  color: var(--text2); text-align: center; padding: 40px;
}
.big-spinner {
  width: 36px; height: 36px; border: 2px solid var(--border2);
  border-top-color: var(--accent); border-radius: 50%;
  animation: spin 0.85s linear infinite;
}
@keyframes spin { to { transform: rotate(360deg); } }
.analyzing-text { font-size: 0.76rem; line-height: 1.8; }

/* Analysis result */
.snap-result { display: none; flex-direction: column; gap: 0; }

.result-score-header {
  display: flex; align-items: center; gap: 18px;
  padding-bottom: 20px; border-bottom: 1px solid var(--border);
  margin-bottom: 20px;
}
.result-big-score {
  font-family: 'Playfair Display', serif;
  font-size: 3.5rem; font-weight: 900; line-height: 1; flex-shrink: 0;
}
.score-S { color: var(--green); }
.score-A { color: #9ee0a5; }
.score-B { color: var(--accent); }
.score-C { color: var(--accent2); }
.score-D { color: var(--red); }

.result-score-text {}
.result-score-label { font-size: 0.85rem; font-weight: 500; color: var(--text); margin-bottom: 4px; }
.result-score-reason { font-size: 0.68rem; color: var(--text2); line-height: 1.6; }

.result-section { margin-bottom: 20px; }
.result-section-title {
  font-size: 0.55rem; text-transform: uppercase; letter-spacing: 0.14em;
  color: var(--accent); margin-bottom: 8px; padding-bottom: 5px;
  border-bottom: 1px solid var(--border);
}
.result-body { font-size: 0.74rem; line-height: 1.8; color: var(--text); }

.flags-row { display: flex; flex-wrap: wrap; gap: 5px; margin-top: 8px; }
.flag { padding: 3px 8px; border-radius: 2px; font-size: 0.6rem; letter-spacing: 0.04em; }
.flag-green { background: rgba(111,207,122,0.1); color: var(--green); border: 1px solid rgba(111,207,122,0.22); }
.flag-yellow { background: rgba(226,185,74,0.08); color: var(--accent); border: 1px solid rgba(226,185,74,0.2); }
.flag-red { background: rgba(224,112,80,0.08); color: var(--red); border: 1px solid rgba(224,112,80,0.18); }
.flag-gray { background: var(--surface2); color: var(--muted); border: 1px solid var(--border2); }

.result-verdict-box {
  background: var(--surface2); border: 1px solid var(--border2);
  border-left: 3px solid var(--accent);
  border-radius: 3px; padding: 14px 16px;
  font-size: 0.74rem; line-height: 1.8; color: var(--text);
  margin-bottom: 20px;
}

.result-retry { margin-top: 4px; }

/* ═══════════════════════════════════════════
   SELLER BROWSER
═══════════════════════════════════════════ */
#screen-seller { min-height: calc(100vh - 57px); }

.seller-controls {
  padding: 10px 36px; background: var(--surface2);
  border-bottom: 1px solid var(--border);
  display: flex; gap: 12px; align-items: center; flex-wrap: wrap;
}
.ctrl-label { font-size: 0.56rem; color: var(--muted); text-transform: uppercase; letter-spacing: 0.1em; margin-right: 3px; }
select {
  background: var(--bg); border: 1px solid var(--border); color: var(--text);
  font-family: 'DM Mono', monospace; font-size: 0.68rem;
  padding: 5px 8px; border-radius: 3px; cursor: pointer;
}
select:focus { outline: none; border-color: var(--accent); }
.ctrl-search {
  background: var(--bg); border: 1px solid var(--border); color: var(--text);
  font-family: 'DM Mono', monospace; font-size: 0.68rem;
  padding: 5px 8px; border-radius: 3px; width: 155px;
}
.ctrl-search:focus { outline: none; border-color: var(--accent); }
.ctrl-search::placeholder { color: var(--muted); }
.ctrl-spacer { flex: 1; }

.stats-bar {
  padding: 7px 36px; display: flex; gap: 18px;
  font-size: 0.6rem; color: var(--muted);
  border-bottom: 1px solid var(--border); background: var(--bg);
}
.stats-bar em { color: var(--accent); font-style: normal; font-weight: 500; }

.seller-main { padding: 18px 36px 80px; transition: padding-right 0.32s cubic-bezier(0.4,0,0.2,1); }
.seller-main.panel-open { padding-right: calc(var(--panel-w) + 18px); }

/* state */
.state-msg { text-align: center; padding: 80px 20px; color: var(--muted); }
.state-icon { font-family: 'Playfair Display', serif; font-size: 2.8rem; color: var(--border2); display: block; margin-bottom: 12px; }
.state-text { font-size: 0.76rem; line-height: 1.75; }
.spinner-sm { display: inline-block; width: 13px; height: 13px; border: 1.5px solid var(--border2); border-top-color: var(--accent); border-radius: 50%; animation: spin 0.75s linear infinite; vertical-align: middle; margin-right: 5px; }
.error-bar { background: rgba(224,112,80,0.07); border: 1px solid rgba(224,112,80,0.22); color: var(--red); padding: 10px 14px; border-radius: 3px; font-size: 0.7rem; margin-bottom: 14px; }

/* table */
table { width: 100%; border-collapse: collapse; font-size: 0.71rem; }
thead tr { background: var(--surface); border-bottom: 2px solid var(--accent); }
th { padding: 9px 10px; text-align: left; font-size: 0.55rem; text-transform: uppercase; letter-spacing: 0.11em; color: var(--muted); cursor: pointer; white-space: nowrap; user-select: none; transition: color 0.15s; }
th:hover { color: var(--accent); }
tbody tr { border-bottom: 1px solid var(--border); transition: background 0.1s; cursor: pointer; }
tbody tr:hover { background: var(--surface2); }
tbody tr.row-active { background: rgba(226,185,74,0.05); border-left: 2px solid var(--accent); }
td { padding: 9px 10px; vertical-align: middle; }

.cell-release { max-width: 230px; }
.rel-title { font-size: 0.74rem; font-weight: 500; color: var(--text); white-space: nowrap; overflow: hidden; text-overflow: ellipsis; max-width: 210px; }
.rel-artist { font-size: 0.6rem; color: var(--text2); margin-top: 1px; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; max-width: 210px; }
.rel-fmt { font-size: 0.54rem; color: var(--muted); margin-top: 2px; }

.badge { display: inline-block; padding: 2px 5px; border-radius: 2px; font-size: 0.57rem; font-weight: 500; white-space: nowrap; }
.b-nm  { background: rgba(111,207,122,0.13); color: var(--green); border: 1px solid rgba(111,207,122,0.26); }
.b-vgp { background: rgba(111,207,122,0.07); color: #9ee0a5; border: 1px solid rgba(111,207,122,0.14); }
.b-vg  { background: rgba(240,192,96,0.09); color: var(--yellow); border: 1px solid rgba(240,192,96,0.2); }
.b-low { background: rgba(224,112,80,0.08); color: var(--red); border: 1px solid rgba(224,112,80,0.18); }

.cell-price { color: var(--accent); font-weight: 500; font-size: 0.76rem; white-space: nowrap; }
.cell-ship  { color: var(--muted); font-size: 0.6rem; white-space: nowrap; }
.cell-total { color: var(--accent2); font-weight: 500; font-size: 0.71rem; white-space: nowrap; }
.cell-year  { color: var(--muted); font-size: 0.65rem; }

.score-pill { display: inline-flex; align-items: center; gap: 4px; padding: 2px 7px; border-radius: 10px; font-size: 0.61rem; font-weight: 500; cursor: pointer; transition: opacity 0.15s; white-space: nowrap; }
.score-pill:hover { opacity: 0.7; }
.score-pip { width: 5px; height: 5px; border-radius: 50%; background: currentColor; flex-shrink: 0; }
.pill-S { background: rgba(111,207,122,0.15); color: var(--green); border: 1px solid rgba(111,207,122,0.32); }
.pill-A { background: rgba(111,207,122,0.08); color: #9ee0a5; border: 1px solid rgba(111,207,122,0.18); }
.pill-B { background: rgba(226,185,74,0.09); color: var(--accent); border: 1px solid rgba(226,185,74,0.25); }
.pill-C { background: rgba(196,122,58,0.09); color: var(--accent2); border: 1px solid rgba(196,122,58,0.25); }
.pill-D { background: rgba(224,112,80,0.08); color: var(--red); border: 1px solid rgba(224,112,80,0.2); }
.pill-p { background: var(--surface2); color: var(--muted); border: 1px solid var(--border2); font-style: italic; }

.ext-link { display: inline-block; background: none; border: 1px solid var(--border); color: var(--muted); font-size: 0.54rem; padding: 2px 5px; border-radius: 2px; text-decoration: none; transition: all 0.15s; }
.ext-link:hover { border-color: var(--accent); color: var(--accent); }

.pager { display: flex; align-items: center; gap: 10px; margin-top: 20px; justify-content: center; font-size: 0.66rem; }
.pager-btn { background: var(--surface); border: 1px solid var(--border); color: var(--text2); font-family: 'DM Mono', monospace; font-size: 0.63rem; padding: 5px 11px; border-radius: 3px; cursor: pointer; letter-spacing: 0.04em; transition: all 0.15s; }
.pager-btn:hover { border-color: var(--accent); color: var(--accent); }
.pager-btn:disabled { opacity: 0.3; cursor: not-allowed; }
.pager-info { color: var(--muted); }

/* ═══════════════════════════════════════════
   SIDE PANEL (Seller Browser)
═══════════════════════════════════════════ */
.panel {
  position: fixed; top: 0; right: 0;
  width: var(--panel-w); height: 100vh;
  background: var(--surface); border-left: 1px solid var(--border);
  z-index: 100; display: flex; flex-direction: column;
  transform: translateX(100%);
  transition: transform 0.32s cubic-bezier(0.4,0,0.2,1);
  overflow: hidden;
}
.panel.open { transform: translateX(0); }

.panel-head { padding: 15px 20px 12px; border-bottom: 1px solid var(--border); display: flex; align-items: flex-start; gap: 10px; flex-shrink: 0; }
.panel-head-text { flex: 1; min-width: 0; }
.panel-title { font-family: 'Playfair Display', serif; font-size: 0.98rem; font-weight: 700; color: var(--text); line-height: 1.3; }
.panel-artist { font-size: 0.61rem; color: var(--accent); margin-top: 3px; letter-spacing: 0.07em; text-transform: uppercase; }
.panel-x { background: none; border: 1px solid var(--border); color: var(--muted); width: 26px; height: 26px; padding: 0; font-size: 0.85rem; border-radius: 3px; cursor: pointer; display: flex; align-items: center; justify-content: center; transition: all 0.15s; flex-shrink: 0; }
.panel-x:hover { border-color: var(--accent); color: var(--accent); }

.panel-meta { padding: 11px 20px; border-bottom: 1px solid var(--border); display: grid; grid-template-columns: 1fr 1fr; gap: 8px; flex-shrink: 0; }
.meta-l { font-size: 0.54rem; text-transform: uppercase; letter-spacing: 0.1em; color: var(--muted); margin-bottom: 2px; }
.meta-v { font-size: 0.73rem; color: var(--text); }

.panel-score-row { padding: 11px 20px; border-bottom: 1px solid var(--border); display: flex; align-items: center; gap: 12px; flex-shrink: 0; }
.panel-big-score { font-family: 'Playfair Display', serif; font-size: 2.5rem; font-weight: 900; line-height: 1; flex-shrink: 0; }
.panel-score-label { font-size: 0.7rem; color: var(--text); font-weight: 500; }
.panel-score-sub { font-size: 0.61rem; color: var(--text2); margin-top: 3px; line-height: 1.55; }

/* Photo upload inside panel */
.panel-photo-zone {
  padding: 11px 20px; border-bottom: 1px solid var(--border); flex-shrink: 0;
}
.photo-zone-label { font-size: 0.54rem; text-transform: uppercase; letter-spacing: 0.1em; color: var(--muted); margin-bottom: 7px; display: flex; align-items: center; gap: 6px; }
.photo-zone-label span { color: var(--accent-dim); }
.photo-drop {
  border: 1.5px dashed var(--border2); border-radius: 4px;
  padding: 10px 14px; display: flex; align-items: center; gap: 10px;
  cursor: pointer; transition: border-color 0.2s, background 0.2s;
  background: var(--bg); position: relative; overflow: hidden;
}
.photo-drop:hover { border-color: var(--accent); background: var(--accent-dim); }
.photo-drop.has-image { border-color: rgba(111,207,122,0.4); }
.photo-drop input { position: absolute; inset: 0; opacity: 0; cursor: pointer; font-size: 0; }
.photo-thumb { width: 40px; height: 40px; object-fit: cover; border-radius: 3px; flex-shrink: 0; display: none; }
.photo-thumb.visible { display: block; }
.photo-drop-text { font-size: 0.64rem; color: var(--text2); line-height: 1.5; }
.photo-drop-text em { color: var(--accent); font-style: normal; }
.photo-clear { background: none; border: none; color: var(--muted); cursor: pointer; font-size: 0.8rem; margin-left: auto; padding: 4px; transition: color 0.15s; flex-shrink: 0; }
.photo-clear:hover { color: var(--red); }

.panel-body { flex: 1; overflow-y: auto; padding: 16px 20px; }
.panel-body::-webkit-scrollbar { width: 3px; }
.panel-body::-webkit-scrollbar-thumb { background: var(--border2); border-radius: 2px; }

.p-section { margin-bottom: 17px; }
.p-section h4 { font-size: 0.54rem; text-transform: uppercase; letter-spacing: 0.13em; color: var(--accent); margin-bottom: 7px; padding-bottom: 4px; border-bottom: 1px solid var(--border); }
.p-text { font-size: 0.71rem; line-height: 1.8; color: var(--text); }
.p-verdict { font-size: 0.71rem; line-height: 1.8; color: var(--text); font-style: italic; }

.panel-idle-prompt { text-align: center; padding: 36px 14px; color: var(--muted); }
.panel-idle-icon { font-size: 1.8rem; opacity: 0.25; margin-bottom: 12px; display: block; }
.panel-idle-text { font-size: 0.7rem; line-height: 1.75; margin-bottom: 18px; }

.panel-analyzing { display: none; align-items: center; justify-content: center; flex-direction: column; gap: 12px; padding: 36px 14px; text-align: center; }
.panel-analyzing-text { font-size: 0.7rem; color: var(--text2); line-height: 1.75; }

.panel-foot { padding: 11px 20px; border-top: 1px solid var(--border); display: flex; gap: 8px; flex-shrink: 0; }
.panel-foot a { flex: 1; display: block; text-align: center; background: var(--accent); color: #000; text-decoration: none; padding: 8px; border-radius: 3px; font-size: 0.66rem; font-weight: 500; letter-spacing: 0.07em; text-transform: uppercase; transition: background 0.15s; }
.panel-foot a:hover { background: #ecca60; }
.panel-foot a.sec { background: none; border: 1px solid var(--border2); color: var(--text2); }
.panel-foot a.sec:hover { border-color: var(--accent); color: var(--accent); background: none; }
</style>
</head>
<body>

<!-- ═══════════════════════════════════════════
     HOME SCREEN
═══════════════════════════════════════════ -->
<div id="screen-home" class="active">
  <div class="home-logo">
    <div class="home-eyebrow">A vinyl intelligence tool</div>
    <span class="home-title">For the Record</span>
    <div class="home-subtitle">Know what you're buying. Every time.</div>
  </div>

  <div class="home-prompt">How would you like to dig today?</div>

  <div class="mode-cards">
    <div class="mode-card" onclick="goMode('snap')">
      <div class="mode-card-icon">📷</div>
      <div class="mode-card-title">Snap &amp; Analyze</div>
      <div class="mode-card-desc">At a record store? Drop a photo of any sleeve or label and get an instant AI verdict — pressing quality, market value, and whether it's worth the price tag.</div>
      <div class="mode-card-cta">Open Camera Mode →</div>
    </div>
    <div class="mode-card" onclick="goMode('seller')">
      <div class="mode-card-icon">🗂</div>
      <div class="mode-card-title">Seller Browser</div>
      <div class="mode-card-desc">Browsing a Discogs seller? Pull their full inventory, filter by condition and format, and let AI score every listing for pressing quality and value.</div>
      <div class="mode-card-cta">Open Seller Browser →</div>
    </div>
  </div>

  <div class="home-footer">Powered by the Discogs API &amp; Claude · For the Record v2</div>
</div>

<!-- ═══════════════════════════════════════════
     SHARED HEADER (shown in both app modes)
═══════════════════════════════════════════ -->
<div id="app-header" class="app-header" style="display:none">
  <div class="wordmark">
    <div class="wordmark-eyebrow">Vinyl Intelligence</div>
    <div class="wordmark-name">For the Record</div>
    <div class="wordmark-tagline">Know what you're buying</div>
  </div>

  <div class="mode-switcher">
    <button class="mode-tab" id="tab-snap" onclick="goMode('snap')">📷 Snap &amp; Analyze</button>
    <button class="mode-tab" id="tab-seller" onclick="goMode('seller')">🗂 Seller Browser</button>
  </div>

  <div class="header-right">
    <button class="back-home" onclick="goHome()">← Home</button>
  </div>
</div>

<!-- ═══════════════════════════════════════════
     SNAP & ANALYZE SCREEN
═══════════════════════════════════════════ -->
<div id="screen-snap" class="screen">
  <div class="snap-layout">

    <!-- LEFT: controls -->
    <div class="snap-left">
      <div>
        <h2>Drop a Photo</h2>
        <p style="margin-top:8px">Snap the sleeve, label, or dead wax. Add context if you know it — price, format, where you found it. Claude will do the rest.</p>
      </div>

      <div class="drop-zone" id="snapDropZone">
        <input type="file" id="snapFileInput" accept="image/*" onchange="handleSnapFile(event)" />
        <img id="snapPreview" class="drop-zone-preview" style="display:none" />
        <div id="snapDropPlaceholder">
          <div class="drop-zone-icon">🖼</div>
          <div class="drop-zone-text">
            Drag &amp; drop a photo here<br/>
            or <em>click to browse</em><br/>
            <span style="font-size:0.6rem;color:var(--muted);margin-top:4px;display:block">JPG, PNG, WEBP supported</span>
          </div>
        </div>
      </div>

      <div class="snap-meta">
        <div class="snap-meta-row">
          <div class="snap-meta-label">Artist &amp; Title (optional)</div>
          <input class="snap-meta-input" id="snapTitle" placeholder="e.g. Led Zeppelin – Houses of the Holy" />
        </div>
        <div class="snap-meta-row">
          <div class="snap-meta-label">Price you're being asked (optional)</div>
          <input class="snap-meta-input" id="snapPrice" placeholder="e.g. $24.99" />
        </div>
        <div class="snap-meta-row">
          <div class="snap-meta-label">Any other context (optional)</div>
          <input class="snap-meta-input" id="snapContext" placeholder="e.g. found at a thrift store, no sleeve" />
        </div>
      </div>

      <div class="snap-actions">
        <button class="btn" id="snapAnalyzeBtn" onclick="runSnapAnalysis()" disabled>Analyze Record</button>
        <button class="btn-ghost" onclick="clearSnap()">Clear</button>
      </div>
    </div>

    <!-- RIGHT: results -->
    <div class="snap-right" id="snapRight">

      <div class="snap-idle" id="snapIdle">
        <div class="snap-idle-icon">◈</div>
        <div class="snap-idle-text">Upload a photo of a record, sleeve, or label<br/>and hit <em style="color:var(--accent)">Analyze Record</em> to get your verdict.</div>
      </div>

      <div class="snap-analyzing" id="snapAnalyzing">
        <div class="big-spinner"></div>
        <div class="analyzing-text">Reading the pressing...<br/>Checking the matrix...<br/>Consulting the wax oracle...</div>
      </div>

      <div class="snap-result" id="snapResult">
        <div class="result-score-header">
          <div class="result-big-score" id="snapBigScore">—</div>
          <div class="result-score-text">
            <div class="result-score-label" id="snapScoreLabel">—</div>
            <div class="result-score-reason" id="snapScoreReason">—</div>
          </div>
        </div>

        <div class="result-section">
          <div class="result-section-title">What Claude Sees in the Photo</div>
          <div class="result-body" id="snapPhotoRead">—</div>
        </div>

        <div class="result-section">
          <div class="result-section-title">About This Record</div>
          <div class="result-body" id="snapOverview">—</div>
        </div>

        <div class="result-section">
          <div class="result-section-title">Pressing Analysis</div>
          <div class="result-body" id="snapPressing">—</div>
          <div class="flags-row" id="snapFlags"></div>
        </div>

        <div class="result-section">
          <div class="result-section-title">Value Assessment</div>
          <div class="result-body" id="snapValue">—</div>
        </div>

        <div class="result-verdict-box" id="snapVerdict">—</div>

        <div class="result-retry">
          <button class="btn-ghost" onclick="runSnapAnalysis()" style="font-size:0.64rem;padding:6px 12px">Re-analyze</button>
        </div>
      </div>

    </div>
  </div>
</div>

<!-- ═══════════════════════════════════════════
     SELLER BROWSER SCREEN
═══════════════════════════════════════════ -->
<div id="screen-seller" class="screen">

  <!-- inline seller search in header area -->
  <div style="background:var(--surface);border-bottom:1px solid var(--border);padding:10px 36px;display:flex;align-items:center;gap:9px;flex-wrap:wrap;">
    <span style="font-size:0.6rem;color:var(--muted);text-transform:uppercase;letter-spacing:0.1em;">Seller</span>
    <input type="text" id="sellerInput" placeholder="Discogs username" value="cryan12" style="width:170px;" />
    <button class="btn" id="loadBtn" onclick="loadInventory()">Load</button>
    <span style="font-size:0.6rem;color:var(--muted);margin-left:4px;" id="sellerHint"></span>
  </div>

  <div class="seller-controls" id="sellerControls" style="display:none">
    <span class="ctrl-label">Media</span>
    <select id="condFilter" onchange="applyFilters()">
      <option value="">All conditions</option>
      <option value="Mint">Mint</option>
      <option value="Near Mint">Near Mint (NM)</option>
      <option value="Very Good Plus">VG+</option>
      <option value="Very Good">VG</option>
      <option value="Good Plus">G+</option>
      <option value="Good">Good</option>
    </select>
    <span class="ctrl-label" style="margin-left:6px">Format</span>
    <select id="formatFilter" onchange="applyFilters()">
      <option value="">All formats</option>
      <option value="Vinyl">Vinyl</option>
      <option value="CD">CD</option>
      <option value="Cassette">Cassette</option>
    </select>
    <span class="ctrl-label" style="margin-left:6px">Sort</span>
    <select id="sortSelect" onchange="applyFilters()">
      <option value="score_desc">Score: Best First</option>
      <option value="price_asc">Price: Low→High</option>
      <option value="price_desc">Price: High→Low</option>
      <option value="title_asc">Title: A–Z</option>
      <option value="condition_desc">Condition: Best First</option>
      <option value="year_asc">Year: Oldest First</option>
    </select>
    <input class="ctrl-search" id="searchFilter" placeholder="Search..." oninput="applyFilters()" />
    <div class="ctrl-spacer"></div>
    <button class="btn-outline-accent" style="font-size:0.63rem;padding:6px 11px;" id="scoreAllBtn" onclick="scoreVisible()">✦ Score Visible</button>
    <button class="btn-ghost" style="font-size:0.63rem;padding:6px 11px;" id="loadAllBtn" onclick="loadAllPages()">Load All Pages</button>
  </div>

  <div class="stats-bar" id="statsBar" style="display:none">
    <div>Showing <em id="stShowing">0</em></div>
    <div>Loaded <em id="stTotal">0</em></div>
    <div>Avg <em id="stAvg">—</em></div>
    <div>AI scored <em id="stScored">0</em></div>
    <div>Pages <em id="stPages">?</em></div>
  </div>

  <div class="seller-main" id="sellerMain">
    <div class="state-msg" id="stateMsg">
      <span class="state-icon">◈</span>
      <div class="state-text">Enter a Discogs seller username above<br/>and hit Load to browse their inventory.</div>
    </div>
    <div class="error-bar" id="errorBar" style="display:none"></div>
    <div id="tableWrap" style="display:none">
      <table>
        <thead><tr>
          <th onclick="setSort('title_asc')">Release</th>
          <th onclick="setSort('condition_desc')">Media</th>
          <th>Sleeve</th>
          <th onclick="setSort('year_asc')">Year</th>
          <th onclick="setSort('price_asc')">Price</th>
          <th>+Ship</th>
          <th>Total</th>
          <th onclick="setSort('score_desc')">Score ✦</th>
          <th></th>
        </tr></thead>
        <tbody id="tableBody"></tbody>
      </table>
      <div class="pager" id="pager"></div>
    </div>
  </div>

  <!-- SIDE PANEL -->
  <div class="panel" id="sidePanel">
    <div class="panel-head">
      <div class="panel-head-text">
        <div class="panel-title" id="pTitle">—</div>
        <div class="panel-artist" id="pArtist">—</div>
      </div>
      <button class="panel-x" onclick="closePanel()">✕</button>
    </div>

    <div class="panel-meta" id="pMeta"></div>

    <div class="panel-score-row" id="pScoreRow" style="display:none">
      <div class="panel-big-score" id="pBigScore">—</div>
      <div>
        <div class="panel-score-label" id="pScoreLabel">—</div>
        <div class="panel-score-sub" id="pScoreSub">—</div>
      </div>
    </div>

    <!-- Photo upload inside panel -->
    <div class="panel-photo-zone">
      <div class="photo-zone-label">📷 Add a photo for deeper analysis <span>(optional)</span></div>
      <div class="photo-drop" id="panelPhotoDrop">
        <input type="file" id="panelPhotoInput" accept="image/*" onchange="handlePanelPhoto(event)" />
        <img id="panelPhotoThumb" class="photo-thumb" />
        <div class="photo-drop-text" id="panelPhotoText">Drop sleeve / label photo · <em>click to browse</em></div>
        <button class="photo-clear" id="panelPhotoClear" style="display:none" onclick="clearPanelPhoto(event)">✕</button>
      </div>
    </div>

    <div class="panel-body" id="pBody">
      <div class="panel-idle-prompt" id="pIdle">
        <span class="panel-idle-icon">✦</span>
        <div class="panel-idle-text">Get a full AI breakdown of this pressing — what it is, how it sounds, whether the price is fair, and whether you should buy it.</div>
        <button class="btn" onclick="runPanelAnalysis(activeListing)" style="margin:0 auto">Analyze This Record</button>
      </div>
      <div class="panel-analyzing" id="pAnalyzing">
        <div class="big-spinner" style="width:26px;height:26px;border-width:2px"></div>
        <div class="panel-analyzing-text">Reading the listing...<br/>Analyzing pressing &amp; value...</div>
      </div>
      <div id="pContent"></div>
    </div>

    <div class="panel-foot">
      <a href="#" id="pLink" target="_blank">View on Discogs →</a>
      <a href="#" class="sec" onclick="closePanel();return false">Close</a>
    </div>
  </div>
</div>

<script>
/* ═══════════════ ROUTING ═══════════════ */
let currentMode = 'home';

function goHome() {
  currentMode = 'home';
  document.getElementById('screen-home').classList.add('active');
  document.getElementById('screen-snap').classList.remove('active');
  document.getElementById('screen-seller').classList.remove('active');
  document.getElementById('app-header').style.display = 'none';
  closePanel();
}

function goMode(mode) {
  currentMode = mode;
  document.getElementById('screen-home').classList.remove('active');
  document.getElementById('screen-snap').classList.remove('active');
  document.getElementById('screen-seller').classList.remove('active');
  document.getElementById('screen-' + mode).classList.add('active');
  document.getElementById('app-header').style.display = 'flex';
  document.getElementById('tab-snap').classList.toggle('active', mode === 'snap');
  document.getElementById('tab-seller').classList.toggle('active', mode === 'seller');
  if (mode === 'seller') closePanel();
}

/* ═══════════════ SNAP & ANALYZE ═══════════════ */
let snapImageB64 = null;
let snapMimeType = 'image/jpeg';

function handleSnapFile(e) {
  const file = e.target.files[0];
  if (!file) return;
  readImageFile(file, (b64, mime) => {
    snapImageB64 = b64;
    snapMimeType = mime;
    const preview = document.getElementById('snapPreview');
    preview.src = `data:${mime};base64,${b64}`;
    preview.style.display = 'block';
    document.getElementById('snapDropPlaceholder').style.display = 'none';
    document.getElementById('snapAnalyzeBtn').disabled = false;
  });
}

// Drag and drop for snap zone
const snapZone = document.getElementById('snapDropZone');
snapZone.addEventListener('dragover', e => { e.preventDefault(); snapZone.classList.add('drag-over'); });
snapZone.addEventListener('dragleave', () => snapZone.classList.remove('drag-over'));
snapZone.addEventListener('drop', e => {
  e.preventDefault(); snapZone.classList.remove('drag-over');
  const file = e.dataTransfer.files[0];
  if (file && file.type.startsWith('image/')) {
    readImageFile(file, (b64, mime) => {
      snapImageB64 = b64; snapMimeType = mime;
      const preview = document.getElementById('snapPreview');
      preview.src = `data:${mime};base64,${b64}`;
      preview.style.display = 'block';
      document.getElementById('snapDropPlaceholder').style.display = 'none';
      document.getElementById('snapAnalyzeBtn').disabled = false;
    });
  }
});

function clearSnap() {
  snapImageB64 = null;
  document.getElementById('snapPreview').style.display = 'none';
  document.getElementById('snapDropPlaceholder').style.display = 'flex';
  document.getElementById('snapDropPlaceholder').style.flexDirection = 'column';
  document.getElementById('snapDropPlaceholder').style.alignItems = 'center';
  document.getElementById('snapFileInput').value = '';
  document.getElementById('snapTitle').value = '';
  document.getElementById('snapPrice').value = '';
  document.getElementById('snapContext').value = '';
  document.getElementById('snapAnalyzeBtn').disabled = true;
  document.getElementById('snapIdle').style.display = 'flex';
  document.getElementById('snapAnalyzing').style.display = 'none';
  document.getElementById('snapResult').style.display = 'none';
}

async function runSnapAnalysis() {
  if (!snapImageB64) return;
  document.getElementById('snapIdle').style.display = 'none';
  document.getElementById('snapAnalyzing').style.display = 'flex';
  document.getElementById('snapResult').style.display = 'none';

  const title = document.getElementById('snapTitle').value.trim();
  const price = document.getElementById('snapPrice').value.trim();
  const context = document.getElementById('snapContext').value.trim();

  const extraCtx = [
    title ? `Artist/Title: ${title}` : '',
    price ? `Asking price: ${price}` : '',
    context ? `Additional context: ${context}` : ''
  ].filter(Boolean).join('\n');

  const prompt = `You are an expert vinyl record appraiser with encyclopedic knowledge of pressing plants, mastering engineers, matrix codes, label variations, and Discogs market values across all genres and eras.

Examine the photo of this vinyl record (could be a sleeve, label, dead wax, or full record shot) and provide a detailed collector's assessment.
${extraCtx ? '\nAdditional info provided:\n' + extraCtx : ''}

Look carefully at:
- Label color, design, catalog number, and pressing plant indicators
- Any visible matrix/dead wax etchings or stamper codes
- Sleeve condition, printing quality, country of origin indicators
- Any text indicating original vs reissue, club pressing, promo, etc.
- Physical condition visible in the photo

Respond ONLY with valid JSON, no markdown:
{
  "score": "S|A|B|C|D",
  "score_label": "3-5 word verdict",
  "score_reason": "one punchy sentence",
  "photo_read": "2-3 sentences on what you can actually see in the photo — label details, condition, any visible matrix, pressing indicators, catalog number if visible",
  "overview": "2-3 sentences on this album's significance and why collectors want it (infer from what you can identify)",
  "pressing_analysis": "2-3 sentences on pressing quality based on what you see. Be specific about label era, plant indicators, original vs reissue, analog vs digital source if determinable",
  "pressing_flags": [{"label": "text", "type": "green|yellow|red|gray"}],
  "value_verdict": "2-3 sentences on fair market value. What should this cost on Discogs in this condition? Is the asking price fair if provided?",
  "verdict": "1-2 direct sentences: buy or pass, and why"
}

Score: S=steal, A=solid buy, B=fair, C=mediocre/concerns, D=skip.
Flags: green=positive, yellow=neutral/mixed, red=negative, gray=uncertain.`;

  try {
    const res = await fetch('https://api.anthropic.com/v1/messages', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        model: 'claude-sonnet-4-20250514',
        max_tokens: 1000,
        messages: [{
          role: 'user',
          content: [
            { type: 'image', source: { type: 'base64', media_type: snapMimeType, data: snapImageB64 } },
            { type: 'text', text: prompt }
          ]
        }]
      })
    });

    const data = await res.json();
    const raw = data.content?.find(b => b.type === 'text')?.text || '';
    const analysis = JSON.parse(raw.replace(/```json|```/g,'').trim());

    document.getElementById('snapAnalyzing').style.display = 'none';
    document.getElementById('snapResult').style.display = 'flex';

    const scoreEl = document.getElementById('snapBigScore');
    scoreEl.textContent = analysis.score;
    scoreEl.className = 'result-big-score score-' + analysis.score;
    document.getElementById('snapScoreLabel').textContent = analysis.score_label || '';
    document.getElementById('snapScoreReason').textContent = analysis.score_reason || '';
    document.getElementById('snapPhotoRead').textContent = analysis.photo_read || '';
    document.getElementById('snapOverview').textContent = analysis.overview || '';
    document.getElementById('snapPressing').textContent = analysis.pressing_analysis || '';
    document.getElementById('snapValue').textContent = analysis.value_verdict || '';
    document.getElementById('snapVerdict').textContent = analysis.verdict || '';

    const flagsEl = document.getElementById('snapFlags');
    flagsEl.innerHTML = (analysis.pressing_flags||[]).map(f =>
      `<span class="flag flag-${f.type}">${esc(f.label)}</span>`).join('');

  } catch(err) {
    document.getElementById('snapAnalyzing').style.display = 'none';
    document.getElementById('snapIdle').style.display = 'flex';
    document.getElementById('snapIdle').innerHTML = `<div class="snap-idle-icon">⚠</div><div class="snap-idle-text" style="color:var(--red)">Analysis failed: ${esc(err.message)}</div><button class="btn" onclick="runSnapAnalysis()" style="margin-top:12px">Retry</button>`;
  }
}

/* ═══════════════ SELLER BROWSER ═══════════════ */
let allListings = [], filtered = [], totalPages = 1, currentSeller = '';
let displayPage = 1, activeListing = null;
const ROWS = 50, PER_PAGE = 50;
const analysisCache = {};

// Panel photo state
let panelPhotoB64 = null, panelPhotoMime = 'image/jpeg';

const condOrder = {'Mint (M)':7,'Near Mint (NM or M-)':6,'Very Good Plus (VG+)':5,'Very Good (VG)':4,'Good Plus (G+)':3,'Good (G)':2,'Fair (F)':1,'Poor (P)':0};
const scoreOrder = {'S':5,'A':4,'B':3,'C':2,'D':1,'?':0};

function condClass(c) {
  if (!c) return '';
  if (c.includes('Mint') && !c.includes('Near')) return 'b-nm';
  if (c.includes('Near Mint')) return 'b-nm';
  if (c.includes('Very Good Plus')||c.includes('VG+')) return 'b-vgp';
  if (c.includes('Very Good')) return 'b-vg';
  return 'b-low';
}
function condShort(c) {
  if (!c) return '—';
  if (c.includes('Near Mint')) return 'NM';
  if (c.includes('Very Good Plus')||c.includes('VG+')) return 'VG+';
  if (c.includes('Very Good')) return 'VG';
  if (c.includes('Good Plus')) return 'G+';
  if (c.includes('Good')) return 'G';
  if (c.includes('Mint')) return 'M';
  if (c.includes('Fair')) return 'F';
  if (c.includes('Poor')) return 'P';
  return c.substring(0,3);
}
function esc(s) { return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;'); }

async function fetchPage(seller, page) {
  const res = await fetch(`https://api.discogs.com/users/${seller}/inventory?per_page=${PER_PAGE}&page=${page}&sort=listed&sort_order=desc`, {headers:{'User-Agent':'ForTheRecord/2.0'}});
  if (!res.ok) throw new Error(`API error ${res.status} — seller not found or inventory is private`);
  return res.json();
}

async function loadInventory() {
  const seller = document.getElementById('sellerInput').value.trim();
  if (!seller) return;
  currentSeller = seller; allListings = []; displayPage = 1;
  closePanel();
  const btn = document.getElementById('loadBtn');
  btn.disabled = true; btn.textContent = 'Loading...';
  document.getElementById('errorBar').style.display = 'none';
  document.getElementById('stateMsg').style.display = 'block';
  document.getElementById('stateMsg').innerHTML = '<span class="spinner-sm"></span> Fetching inventory...';
  document.getElementById('tableWrap').style.display = 'none';

  try {
    const data = await fetchPage(seller, 1);
    totalPages = data.pagination.pages;
    allListings = parseListings(data.listings);
    document.getElementById('stPages').textContent = totalPages;
    document.getElementById('sellerControls').style.display = 'flex';
    document.getElementById('statsBar').style.display = 'flex';
    document.getElementById('stateMsg').style.display = 'none';
    applyFilters();
  } catch(e) { showErr(e.message); }
  btn.disabled = false; btn.textContent = 'Load';
}

async function loadAllPages() {
  if (!currentSeller) return;
  const btn = document.getElementById('loadAllBtn');
  btn.disabled = true; btn.textContent = 'Loading...';
  try {
    for (let p = 2; p <= Math.min(totalPages, 20); p += 3) {
      const batch = [];
      for (let i = p; i < p+3 && i <= Math.min(totalPages,20); i++) batch.push(fetchPage(currentSeller,i));
      const results = await Promise.all(batch);
      results.forEach(d => allListings = allListings.concat(parseListings(d.listings)));
      btn.textContent = `Loading... (${allListings.length})`;
      if (p+3 <= Math.min(totalPages,20)) await sleep(500);
    }
    applyFilters();
  } catch(e) { showErr(e.message); }
  btn.disabled = false; btn.textContent = 'Load All Pages';
}

function parseListings(ls) {
  return ls.map(l => ({
    id: l.id,
    title: l.release?.title||'—', artist: l.release?.artist||'—',
    year: l.release?.year||null,
    format: (l.release?.formats||[]).map(f=>f.name).join(', '),
    format_desc: (l.release?.formats||[]).flatMap(f=>f.descriptions||[]).join(', '),
    condition: l.condition||'', sleeve_condition: l.sleeve_condition||'',
    price: parseFloat(l.price?.value)||0, currency: l.price?.currency||'USD',
    shipping_price: parseFloat(l.shipping_price?.value)||null,
    comments: l.comments||'',
    url: l.uri ? `https://www.discogs.com${l.uri}` : '#',
    genres: l.release?.genres||[], styles: l.release?.styles||[],
    score: analysisCache[l.id]?.score||'?'
  }));
}

function applyFilters() {
  const cond = document.getElementById('condFilter').value;
  const fmt  = document.getElementById('formatFilter').value;
  const srch = document.getElementById('searchFilter').value.toLowerCase();
  const sort = document.getElementById('sortSelect').value;

  filtered = allListings.filter(l => {
    if (cond && !l.condition.includes(cond)) return false;
    if (fmt && !l.format.includes(fmt)) return false;
    if (srch && !l.title.toLowerCase().includes(srch) && !l.artist.toLowerCase().includes(srch)) return false;
    return true;
  });

  filtered.sort((a,b) => {
    switch(sort) {
      case 'score_desc': return (scoreOrder[b.score]||0)-(scoreOrder[a.score]||0);
      case 'price_asc':  return a.price-b.price;
      case 'price_desc': return b.price-a.price;
      case 'title_asc':  return a.title.localeCompare(b.title);
      case 'condition_desc': return (condOrder[b.condition]||0)-(condOrder[a.condition]||0);
      case 'year_asc':   return (a.year||9999)-(b.year||9999);
      default: return a.price-b.price;
    }
  });

  updateStats(); displayPage = 1; renderPage();
}

function setSort(v) { document.getElementById('sortSelect').value = v; applyFilters(); }

function updateStats() {
  document.getElementById('stShowing').textContent = filtered.length;
  document.getElementById('stTotal').textContent = allListings.length;
  const avg = filtered.length ? '$'+(filtered.reduce((s,l)=>s+l.price,0)/filtered.length).toFixed(2):'—';
  document.getElementById('stAvg').textContent = avg;
  document.getElementById('stScored').textContent = Object.keys(analysisCache).length;
}

function renderPage() {
  const slice = filtered.slice((displayPage-1)*ROWS, displayPage*ROWS);
  if (!filtered.length) {
    document.getElementById('tableWrap').style.display = 'none';
    document.getElementById('stateMsg').style.display = 'block';
    document.getElementById('stateMsg').innerHTML = '<span class="state-icon">∅</span><div class="state-text">No listings match your filters.</div>';
    return;
  }
  document.getElementById('tableWrap').style.display = 'block';
  document.getElementById('stateMsg').style.display = 'none';

  document.getElementById('tableBody').innerHTML = slice.map(l => {
    const ship = l.shipping_price !== null ? `+$${l.shipping_price.toFixed(2)}` : '—';
    const total = l.shipping_price !== null ? `$${(l.price+l.shipping_price).toFixed(2)}` : '—';
    const fmt = [l.format, l.format_desc].filter(Boolean).join(' · ');
    const sc = analysisCache[l.id]?.score||'?';
    const isActive = activeListing?.id === l.id;
    const pill = sc==='?' ?
      `<span class="score-pill pill-p" onclick="openAndScore(${l.id},event)">analyze</span>` :
      `<span class="score-pill pill-${sc}" onclick="openPanel(${l.id},event)"><span class="score-pip"></span>${sc}</span>`;

    return `<tr id="row-${l.id}" class="${isActive?'row-active':''}" onclick="openPanel(${l.id})">
      <td class="cell-release">
        <div class="rel-title" title="${esc(l.title)}">${esc(l.title)}</div>
        <div class="rel-artist">${esc(l.artist)}</div>
        <div class="rel-fmt">${esc(fmt)}</div>
      </td>
      <td><span class="badge ${condClass(l.condition)}">${condShort(l.condition)}</span></td>
      <td><span class="badge ${condClass(l.sleeve_condition)}">${condShort(l.sleeve_condition)}</span></td>
      <td class="cell-year">${l.year||'—'}</td>
      <td class="cell-price">$${l.price.toFixed(2)}</td>
      <td class="cell-ship">${ship}</td>
      <td class="cell-total">${total}</td>
      <td>${pill}</td>
      <td><a href="${l.url}" target="_blank" class="ext-link" onclick="event.stopPropagation()">↗</a></td>
    </tr>`;
  }).join('');

  const totalPg = Math.ceil(filtered.length/ROWS);
  document.getElementById('pager').innerHTML = totalPg<=1 ? '' : `
    <button class="pager-btn" onclick="changePage(-1)" ${displayPage===1?'disabled':''}>← Prev</button>
    <span class="pager-info">${displayPage} / ${totalPg}</span>
    <button class="pager-btn" onclick="changePage(1)" ${displayPage===totalPg?'disabled':''}>Next →</button>`;
}

function changePage(d) {
  displayPage = Math.max(1,Math.min(Math.ceil(filtered.length/ROWS), displayPage+d));
  renderPage(); window.scrollTo({top:0,behavior:'smooth'});
}

function getListing(id) { return allListings.find(l=>l.id===id); }

function openPanel(id, e) {
  if (e) e.stopPropagation();
  const l = getListing(id);
  if (!l) return;
  activeListing = l;

  document.querySelectorAll('tbody tr').forEach(r=>r.classList.remove('row-active'));
  const row = document.getElementById('row-'+id);
  if (row) row.classList.add('row-active');

  document.getElementById('pTitle').textContent = l.title;
  document.getElementById('pArtist').textContent = l.artist;
  document.getElementById('pLink').href = l.url;

  const total = l.shipping_price!==null ? `$${(l.price+l.shipping_price).toFixed(2)} all-in` : `$${l.price.toFixed(2)}`;
  document.getElementById('pMeta').innerHTML = `
    <div><div class="meta-l">Media</div><div class="meta-v">${condShort(l.condition)}</div></div>
    <div><div class="meta-l">Sleeve</div><div class="meta-v">${condShort(l.sleeve_condition)}</div></div>
    <div><div class="meta-l">Year</div><div class="meta-v">${l.year||'—'}</div></div>
    <div><div class="meta-l">Format</div><div class="meta-v">${l.format||'—'}</div></div>
    <div><div class="meta-l">Price + Ship</div><div class="meta-v">${total}</div></div>
    <div><div class="meta-l">Genre</div><div class="meta-v">${l.genres[0]||l.styles[0]||'—'}</div></div>`;

  document.getElementById('sidePanel').classList.add('open');
  document.getElementById('sellerMain').classList.add('panel-open');

  // Reset photo zone
  clearPanelPhoto(null, true);

  const cached = analysisCache[id];
  if (cached) renderPanelAnalysis(cached);
  else showPanelIdle(id);
}

function openAndScore(id, e) {
  if (e) e.stopPropagation();
  openPanel(id);
  if (!analysisCache[id]) runPanelAnalysis(getListing(id));
}

function closePanel() {
  activeListing = null;
  document.getElementById('sidePanel').classList.remove('open');
  document.getElementById('sellerMain').classList.remove('panel-open');
  document.querySelectorAll('tbody tr').forEach(r=>r.classList.remove('row-active'));
}

function showPanelIdle(id) {
  document.getElementById('pScoreRow').style.display = 'none';
  document.getElementById('pAnalyzing').style.display = 'none';
  document.getElementById('pContent').innerHTML = '';
  document.getElementById('pIdle').style.display = 'block';
  document.getElementById('pIdle').innerHTML = `
    <span class="panel-idle-icon">✦</span>
    <div class="panel-idle-text">Get a full AI breakdown — pressing quality, market value, and a direct verdict.</div>
    <button class="btn" onclick="runPanelAnalysis(getListing(${id}))" style="margin:0 auto">Analyze This Record</button>`;
}

async function runPanelAnalysis(l) {
  if (!l) return;
  document.getElementById('pIdle').style.display = 'none';
  document.getElementById('pScoreRow').style.display = 'none';
  document.getElementById('pAnalyzing').style.display = 'flex';
  document.getElementById('pContent').innerHTML = '';

  const fmt = [l.format, l.format_desc].filter(Boolean).join(', ');
  const total = l.shipping_price!==null ? `$${(l.price+l.shipping_price).toFixed(2)}` : `$${l.price.toFixed(2)} (shipping TBD)`;
  const sellerNote = l.comments ? `Seller notes: "${l.comments}"` : 'No seller notes.';

  const prompt = `You are an expert vinyl record appraiser with deep knowledge of pressing plants, mastering engineers, matrix codes, and Discogs market values.

Analyze this Discogs listing:
- Artist: ${l.artist}
- Title: ${l.title}
- Year: ${l.year||'unknown'}
- Format: ${fmt}
- Media: ${l.condition}
- Sleeve: ${l.sleeve_condition}
- Price: $${l.price.toFixed(2)} + ship ${l.shipping_price!==null?'$'+l.shipping_price.toFixed(2):'unknown'}
- All-in: ${total}
- Genre: ${[...l.genres,...l.styles].join(', ')||'unknown'}
- ${sellerNote}
${panelPhotoB64 ? '\nA photo of the record/sleeve has also been provided. Use it to refine your analysis.' : ''}

Respond ONLY with valid JSON:
{
  "score": "S|A|B|C|D",
  "score_label": "3-5 word verdict",
  "score_reason": "one punchy sentence",
  "overview": "2-3 sentences on the album — significance, sound, why collectors want it",
  "pressing_analysis": "2-3 sentences on pressing quality — plant, mastering, analog/digital, original/reissue. Flag RL, MO, SP, PR, club, 180g, remaster, etc.",
  "pressing_flags": [{"label":"text","type":"green|yellow|red|gray"}],
  "condition_notes": "1-2 sentences on what the condition grades mean for playability and value",
  "value_verdict": "2-3 sentences on pricing vs Discogs market. Specific ranges.",
  "verdict": "1-2 direct opinionated sentences: buy or pass?"
}
Score: S=steal, A=solid buy, B=fair, C=mediocre, D=skip.`;

  try {
    const msgContent = panelPhotoB64
      ? [
          { type: 'image', source: { type: 'base64', media_type: panelPhotoMime, data: panelPhotoB64 } },
          { type: 'text', text: prompt }
        ]
      : [{ type: 'text', text: prompt }];

    const res = await fetch('https://api.anthropic.com/v1/messages', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        model: 'claude-sonnet-4-20250514',
        max_tokens: 1000,
        messages: [{ role: 'user', content: msgContent }]
      })
    });
    const data = await res.json();
    const raw = data.content?.find(b=>b.type==='text')?.text||'';
    const analysis = JSON.parse(raw.replace(/```json|```/g,'').trim());
    analysis.id = l.id;
    analysisCache[l.id] = analysis;
    const listing = allListings.find(x=>x.id===l.id);
    if (listing) listing.score = analysis.score;
    if (activeListing?.id === l.id) renderPanelAnalysis(analysis);
    updateRowScore(l.id, analysis.score);
    updateStats();
  } catch(err) {
    document.getElementById('pAnalyzing').style.display = 'none';
    document.getElementById('pContent').innerHTML = `<div class="error-bar">Analysis failed: ${esc(err.message)}</div><div style="text-align:center;margin-top:12px"><button class="btn" onclick="runPanelAnalysis(activeListing)">Retry</button></div>`;
  }
}

function renderPanelAnalysis(a) {
  document.getElementById('pAnalyzing').style.display = 'none';
  document.getElementById('pIdle').style.display = 'none';

  const scoreRow = document.getElementById('pScoreRow');
  scoreRow.style.display = 'flex';
  const bigScore = document.getElementById('pBigScore');
  bigScore.textContent = a.score;
  bigScore.className = 'panel-big-score score-'+a.score;
  document.getElementById('pScoreLabel').textContent = a.score_label||'';
  document.getElementById('pScoreSub').textContent = a.score_reason||'';

  const flags = (a.pressing_flags||[]).map(f=>`<span class="flag flag-${f.type}">${esc(f.label)}</span>`).join('');

  document.getElementById('pContent').innerHTML = `
    <div class="p-section"><h4>About This Record</h4><div class="p-text">${esc(a.overview||'')}</div></div>
    <div class="p-section"><h4>Pressing Analysis</h4><div class="p-text">${esc(a.pressing_analysis||'')}</div>${flags?`<div class="flags-row">${flags}</div>`:''}</div>
    <div class="p-section"><h4>Condition</h4><div class="p-text">${esc(a.condition_notes||'')}</div></div>
    <div class="p-section"><h4>Value Assessment</h4><div class="p-text">${esc(a.value_verdict||'')}</div></div>
    <div class="p-section"><h4>Verdict</h4><div class="p-verdict">${esc(a.verdict||'')}</div></div>
    ${panelPhotoB64 ? '<div style="font-size:0.58rem;color:var(--green);margin-top:4px">📷 Photo included in analysis</div>' : ''}`;
}

function updateRowScore(id, score) {
  const row = document.getElementById('row-'+id);
  if (!row) return;
  const cell = row.querySelector('td:nth-child(8)');
  if (cell) cell.innerHTML = `<span class="score-pill pill-${score}" onclick="openPanel(${id},event)"><span class="score-pip"></span>${score}</span>`;
}

async function scoreVisible() {
  const btn = document.getElementById('scoreAllBtn');
  btn.disabled = true;
  const slice = filtered.slice((displayPage-1)*ROWS, displayPage*ROWS);
  const unscored = slice.filter(l=>!analysisCache[l.id]);
  if (!unscored.length) { btn.disabled = false; return; }
  for (let i=0; i<unscored.length; i++) {
    btn.textContent = `Scoring ${i+1}/${unscored.length}...`;
    await runPanelAnalysis(unscored[i]);
    if (i<unscored.length-1) await sleep(300);
  }
  btn.disabled = false; btn.textContent = '✦ Score Visible';
  applyFilters();
}

/* Panel photo */
function handlePanelPhoto(e) {
  const file = e.target.files[0];
  if (!file) return;
  readImageFile(file, (b64, mime) => {
    panelPhotoB64 = b64; panelPhotoMime = mime;
    const thumb = document.getElementById('panelPhotoThumb');
    thumb.src = `data:${mime};base64,${b64}`;
    thumb.classList.add('visible');
    document.getElementById('panelPhotoText').innerHTML = '<em style="color:var(--green)">Photo attached</em> — included in next analysis';
    document.getElementById('panelPhotoClear').style.display = 'block';
    document.getElementById('panelPhotoDrop').classList.add('has-image');
  });
}

function clearPanelPhoto(e, silent) {
  if (e) e.stopPropagation();
  panelPhotoB64 = null;
  document.getElementById('panelPhotoThumb').classList.remove('visible');
  document.getElementById('panelPhotoThumb').src = '';
  document.getElementById('panelPhotoText').innerHTML = 'Drop sleeve / label photo · <em>click to browse</em>';
  document.getElementById('panelPhotoClear').style.display = 'none';
  document.getElementById('panelPhotoDrop').classList.remove('has-image');
  document.getElementById('panelPhotoInput').value = '';
}

/* Helpers */
function readImageFile(file, cb) {
  const reader = new FileReader();
  reader.onload = ev => {
    const parts = ev.target.result.split(',');
    const mime = parts[0].match(/:(.*?);/)[1];
    cb(parts[1], mime);
  };
  reader.readAsDataURL(file);
}
function sleep(ms) { return new Promise(r=>setTimeout(r,ms)); }
function showErr(msg) {
  const el = document.getElementById('errorBar');
  el.textContent = '⚠ '+msg; el.style.display = 'block';
  document.getElementById('stateMsg').style.display = 'none';
}

/* Global key handlers */
document.addEventListener('keydown', e => {
  if (e.key === 'Escape') closePanel();
});
document.getElementById('sellerInput').addEventListener('keydown', e => {
  if (e.key === 'Enter') loadInventory();
});
</script>
</body>
</html>
