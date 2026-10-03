<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>Studio Dessin Animé — Histoires 1 min+</title>
<style>
    * { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }
    :root {
        --bg: #fafafa; --panel: #ffffff; --panel-2: #f5f5f5; --border: #e5e5e5;
        --ink: #1a1a1a; --ink-dim: #777; --ink-faint: #aaa;
        --success: #2d8a4e; --error: #c0392b; --warn: #d4a017; --info: #4a6cf7;
        --radius: 12px;
    }
    body {
        font-family: -apple-system, BlinkMacSystemFont, 'Helvetica Neue', Helvetica, Arial, sans-serif;
        background: var(--bg); color: var(--ink); min-height: 100vh;
        padding: 1.5rem 1rem 6rem; font-size: 15px; line-height: 1.5;
        max-width: 900px; margin: 0 auto;
    }
    header { margin-bottom: 1.5rem; text-align: center; }
    h1 { font-size: 1.4rem; font-weight: 500; letter-spacing: -0.02em; margin-bottom: 0.3rem; }
    .subtitle { font-size: 0.8rem; color: var(--ink-dim); font-style: italic; }

    .toast {
        position: fixed; top: 1.5rem; left: 50%;
        transform: translateX(-50%) translateY(-100px);
        background: var(--ink); color: #fff;
        padding: 0.85rem 1.4rem; border-radius: 10px;
        font-size: 0.85rem; font-weight: 500;
        box-shadow: 0 4px 20px rgba(0,0,0,0.15);
        z-index: 1000; opacity: 0;
        transition: transform 0.35s ease, opacity 0.35s ease;
        max-width: 90vw; text-align: center;
        display: flex; align-items: center; gap: 0.5rem;
    }
    .toast.visible { transform: translateX(-50%) translateY(0); opacity: 1; }
    .toast.success { background: var(--success); }
    .toast.error { background: var(--error); }
    .toast.warn { background: var(--warn); }
    .toast .toast-icon { font-size: 1rem; }

    .info-banner {
        background: #fff3e0; border-left: 3px solid #ff9800;
        padding: 0.75rem 0.95rem; border-radius: 8px;
        font-size: 0.78rem; color: #6b4a1a;
        margin-bottom: 1rem; line-height: 1.45;
    }
    .info-banner strong { color: #1a1a1a; }

    .duration-banner {
        background: linear-gradient(135deg, #fff8e6 0%, #fff3e0 100%);
        border: 1px solid #ffcc80;
        border-radius: 10px;
        padding: 0.9rem 1.1rem;
        margin-bottom: 1rem;
        display: flex;
        justify-content: space-between;
        align-items: center;
        flex-wrap: wrap;
        gap: 0.6rem;
    }
    .duration-banner.ok {
        background: linear-gradient(135deg, #e3f5e9 0%, #f0faf3 100%);
        border-color: #a3d9b5;
    }
    .duration-banner.warn {
        background: linear-gradient(135deg, #fff3e0 0%, #ffe8cc 100%);
        border-color: #ff9800;
    }
    .duration-info {
        display: flex; flex-direction: column; gap: 0.2rem;
    }
    .duration-label {
        font-size: 0.68rem; text-transform: uppercase; letter-spacing: 0.08em;
        color: #6b4a1a; font-weight: 600;
    }
    .duration-banner.ok .duration-label { color: #1a5c2a; }
    .duration-value {
        font-size: 1.2rem; font-weight: 700; color: #1a1a1a;
    }
    .duration-min { font-size: 0.75rem; color: #6b4a1a; }
    .duration-banner.ok .duration-min { color: #1a5c2a; }
    .duration-min strong { color: #1a1a1a; }

    .duration-progress {
        flex: 1;
        min-width: 120px;
        height: 8px;
        background: rgba(0,0,0,0.08);
        border-radius: 4px;
        overflow: hidden;
    }
    .duration-progress-fill {
        height: 100%;
        background: #ff9800;
        transition: width 0.3s ease, background 0.3s;
    }
    .duration-banner.ok .duration-progress-fill { background: var(--success); }

    .section {
        background: var(--panel); border: 1px solid var(--border);
        border-radius: var(--radius); margin-bottom: 1rem;
        overflow: hidden;
    }
    .section-header {
        padding: 0.9rem 1.1rem; cursor: pointer; user-select: none;
        display: flex; justify-content: space-between; align-items: center;
        width: 100%; background: transparent; border: none;
        font-family: inherit; font-size: inherit; color: inherit;
        text-align: left;
    }
    .section-header:active { background: var(--panel-2); }
    .section-header:focus-visible { outline: 2px solid var(--info); outline-offset: -2px; }
    .section-title {
        font-size: 0.75rem; text-transform: uppercase; letter-spacing: 0.1em;
        color: var(--ink-dim); font-weight: 600;
    }
    .section-title .badge {
        display: inline-block; margin-left: 0.4rem; padding: 0.1rem 0.4rem;
        background: var(--ink); color: #fff; border-radius: 10px;
        font-size: 0.65rem; letter-spacing: 0;
    }
    .section-title .badge.soft { background: var(--info); color: #fff; }
    .section-header .chevron {
        font-size: 0.7rem; color: var(--ink-faint); transition: transform 0.2s;
    }
    .section.open .section-header .chevron { transform: rotate(180deg); }
    .section-body { max-height: 0; overflow: hidden; transition: max-height 0.3s ease; }
    .section.open .section-body { max-height: 15000px; }
    .section-content { padding: 0 1.1rem 1.1rem; }

    .api-panel {
        background: var(--panel); border: 1px solid var(--border);
        border-radius: var(--radius); padding: 1rem 1.2rem;
        margin-bottom: 1rem; transition: border-color 0.3s;
    }
    .api-panel.ok { border-color: var(--success); }

    .api-key-input {
        width: 100%; padding: 0.85rem 1rem;
        border-radius: 8px; border: 1px solid var(--border);
        background: #fafafa; color: var(--ink);
        font-family: ui-monospace, 'SF Mono', Menlo, monospace;
        font-size: 0.85rem; margin-bottom: 0.6rem;
    }
    .api-key-input:focus { outline: none; border-color: var(--ink); }

    .api-save-btn {
        width: 100%; padding: 0.8rem 1.2rem;
        border-radius: 8px; border: none;
        background: var(--ink); color: #fff;
        font-size: 0.9rem; font-weight: 600; font-family: inherit;
        cursor: pointer; transition: opacity 0.2s, transform 0.1s;
        margin-bottom: 0.6rem;
    }
    .api-save-btn:active { transform: scale(0.98); }

    .api-status-line {
        font-size: 0.75rem; padding: 0.55rem 0.85rem;
        border-radius: 6px; margin-bottom: 0.5rem;
        display: flex; align-items: center; gap: 0.5rem;
        background: var(--panel-2); color: var(--ink-dim);
    }
    .api-status-line.ok {
        background: #e3f5e9; color: var(--success); font-weight: 600;
    }
    .api-status-line .status-dot {
        width: 8px; height: 8px; border-radius: 50%;
        background: var(--ink-faint); flex-shrink: 0;
    }
    .api-status-line.ok .status-dot { background: var(--success); }

    .api-hint { font-size: 0.72rem; color: var(--ink-dim); margin-top: 0.4rem; }
    .api-hint a { color: var(--ink); text-decoration: underline; }

    .upload-zone {
        border: 2px dashed var(--border); border-radius: var(--radius);
        padding: 1.5rem 1rem; text-align: center; cursor: pointer;
        transition: border-color 0.2s, background 0.2s; margin-bottom: 1rem;
        background: var(--panel);
    }
    .upload-zone:active { border-color: var(--ink); background: #f5f5f5; }
    .upload-zone.loading { pointer-events: none; opacity: 0.6; }
    .upload-zone input[type="file"] { display: none; }
    .upload-icon { font-size: 2rem; margin-bottom: 0.5rem; opacity: 0.6; }
    .upload-text { font-size: 0.9rem; color: var(--ink); margin-bottom: 0.2rem; }
    .upload-hint { font-size: 0.72rem; color: var(--ink-dim); }

    .characters-grid {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(110px, 1fr));
        gap: 0.6rem;
        margin-top: 0.5rem;
    }
    .character-card {
        position: relative;
        border-radius: 10px;
        overflow: hidden;
        border: 2px solid var(--border);
        background: #f0f0f0;
    }
    .character-card img { width: 100%; aspect-ratio: 1/1; object-fit: cover; display: block; }
    .character-card .c-name-input {
        width: 100%; padding: 0.4rem 0.5rem;
        border: none; border-top: 1px solid var(--border);
        background: #fff; font-size: 0.72rem; font-family: inherit;
        text-align: center; color: var(--ink);
    }
    .character-card .c-name-input:focus { outline: none; background: #f0f7ff; }
    .character-card .remove-btn {
        position: absolute; top: 4px; right: 4px;
        background: rgba(0,0,0,0.7); color: #fff; border: none;
        width: 22px; height: 22px; border-radius: 50%; font-size: 11px;
        cursor: pointer; display: flex; align-items: center; justify-content: center;
        line-height: 1; z-index: 2;
    }

    .empty-msg {
        grid-column: 1 / -1;
        padding: 1.2rem;
        text-align: center;
        font-size: 0.82rem;
        color: var(--ink-dim);
        font-style: italic;
        background: var(--panel-2);
        border-radius: 8px;
    }

    .scene-card {
        background: var(--panel);
        border: 1px solid var(--border);
        border-radius: 10px;
        padding: 1rem;
        margin-bottom: 0.8rem;
    }
    .scene-header {
        display: flex;
        align-items: center;
        gap: 0.5rem;
        margin-bottom: 0.7rem;
    }
    .scene-number {
        background: var(--ink);
        color: #fff;
        border-radius: 50%;
        width: 28px; height: 28px;
        display: flex; align-items: center; justify-content: center;
        font-size: 0.75rem; font-weight: 600;
        flex-shrink: 0;
    }
    .scene-title-input {
        flex: 1;
        border: 1px solid var(--border);
        background: #fafafa;
        padding: 0.5rem 0.7rem;
        border-radius: 8px;
        font-size: 0.85rem;
        font-family: inherit;
        font-weight: 600;
        color: var(--ink);
        min-width: 0;
    }
    .scene-title-input:focus { outline: none; border-color: var(--ink); }
    .scene-remove-btn {
        background: transparent;
        border: 1px solid var(--error);
        color: var(--error);
        width: 28px; height: 28px;
        border-radius: 50%;
        cursor: pointer;
        font-size: 0.85rem;
        font-family: inherit;
        flex-shrink: 0;
    }
    .scene-remove-btn:active { background: var(--error); color: #fff; }

    .scene-field { margin-bottom: 0.7rem; }
    .scene-field:last-child { margin-bottom: 0; }
    .scene-label {
        font-size: 0.7rem;
        text-transform: uppercase;
        letter-spacing: 0.06em;
        color: var(--ink-dim);
        font-weight: 600;
        margin-bottom: 0.35rem;
        display: block;
    }

    .scene-characters-list {
        display: flex;
        flex-wrap: wrap;
        gap: 0.4rem;
    }
    .scene-char-chip {
        display: flex;
        align-items: center;
        gap: 0.35rem;
        padding: 0.35rem 0.7rem;
        border-radius: 20px;
        border: 2px solid var(--border);
        background: var(--panel-2);
        font-size: 0.78rem;
        cursor: pointer;
        transition: all 0.15s;
        user-select: none;
        font-family: inherit;
        color: var(--ink);
    }
    .scene-char-chip.selected {
        background: var(--info);
        color: #fff;
        border-color: var(--info);
    }
    .scene-char-chip img {
        width: 22px; height: 22px;
        border-radius: 50%;
        object-fit: cover;
    }
    .no-characters-msg {
        font-size: 0.78rem;
        color: var(--ink-dim);
        font-style: italic;
        padding: 0.5rem;
        background: var(--panel-2);
        border-radius: 8px;
        text-align: center;
        width: 100%;
    }

    .scene-script-textarea {
        width: 100%;
        padding: 0.7rem 0.9rem;
        border-radius: 8px;
        border: 1px solid var(--border);
        background: #fafafa;
        font-family: ui-monospace, 'SF Mono', Menlo, monospace;
        font-size: 0.82rem;
        line-height: 1.6;
        color: var(--ink);
        min-height: 100px;
        resize: vertical;
    }
    .scene-script-textarea:focus { outline: none; border-color: var(--ink); }

    .scene-row {
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 0.6rem;
    }
    @media (max-width: 500px) {
        .scene-row { grid-template-columns: 1fr; }
    }

    .add-scene-btn {
        width: 100%;
        padding: 0.9rem;
        border-radius: 10px;
        border: 2px dashed var(--border);
        background: transparent;
        color: var(--ink-dim);
        font-size: 0.85rem;
        font-weight: 500;
        font-family: inherit;
        cursor: pointer;
        transition: all 0.2s;
        margin-top: 0.5rem;
    }
    .add-scene-btn:active { transform: scale(0.98); }
    .add-scene-btn:hover { border-color: var(--ink); color: var(--ink); }

    .control-row { margin-bottom: 0.9rem; }
    .control-row:last-child { margin-bottom: 0; }
    .control-label {
        display: block; font-size: 0.72rem; color: var(--ink-dim);
        margin-bottom: 0.4rem; text-transform: uppercase; letter-spacing: 0.06em;
        font-weight: 600;
    }
    select, .text-input {
        width: 100%; padding: 0.7rem 0.9rem; border-radius: 8px;
        border: 1px solid var(--border); background: #fafafa;
        color: var(--ink); font-family: inherit; font-size: 0.88rem;
        -webkit-appearance: none; appearance: none;
    }
    select {
        background-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='10' height='6' viewBox='0 0 10 6'><path fill='%231a1a1a' d='M0 0l5 6 5-6z'/></svg>");
        background-repeat: no-repeat;
        background-position: right 0.9rem center;
        background-size: 10px;
        padding-right: 2rem;
    }
    select:focus, .text-input:focus { outline: none; border-color: var(--ink); }

    .btn-primary {
        width: 100%; padding: 1.1rem; border-radius: var(--radius);
        border: none; background: var(--ink); color: #fff;
        font-size: 1rem; font-weight: 600; font-family: inherit;
        cursor: pointer; transition: opacity 0.2s, transform 0.1s;
        margin-bottom: 1rem;
    }
    .btn-primary:active:not(:disabled) { transform: scale(0.98); }
    .btn-primary:disabled { opacity: 0.3; cursor: not-allowed; }

    .btn-stop {
        width: 100%; padding: 0.8rem; border-radius: var(--radius);
        border: 1px solid var(--border); background: var(--panel);
        color: var(--error); font-size: 0.85rem; font-weight: 600;
        font-family: inherit; cursor: pointer; margin-bottom: 1rem;
        display: none;
    }
    .btn-stop.visible { display: block; }

    .queue { margin-top: 1rem; }
    .queue-summary {
        background: var(--panel); border: 1px solid var(--border);
        border-radius: 8px; padding: 0.7rem 0.9rem; margin-bottom: 0.6rem;
        font-size: 0.78rem; display: flex; justify-content: space-between;
        align-items: center; flex-wrap: wrap; gap: 0.4rem;
    }
    .queue-summary .progress-text { color: var(--ink); font-weight: 600; }
    .queue-summary .eta-text { color: var(--ink-dim); }

    .queue-item {
        display: flex; align-items: center; gap: 0.8rem;
        padding: 0.7rem 0.8rem; border-radius: 8px;
        border: 1px solid var(--border); margin-bottom: 0.4rem;
        background: var(--panel); transition: border-color 0.3s, opacity 0.3s;
        font-size: 0.82rem;
    }
    .queue-item.pending { opacity: 0.5; }
    .queue-item.creating { border-color: var(--warn); }
    .queue-item.processing { border-color: var(--ink); }
    .queue-item.done { border-color: var(--success); }
    .queue-item.failed { border-color: var(--error); }
    .queue-item .q-icon { font-size: 1rem; width: 1.5rem; text-align: center; flex-shrink: 0; }
    .queue-item .q-name { flex: 1; min-width: 0; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }
    .queue-item .q-status { font-size: 0.72rem; color: var(--ink-dim); text-align: right; flex-shrink: 0; max-width: 60%; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }

    .gallery { margin-top: 1.5rem; }
    .gallery-grid {
        display: grid; grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
        gap: 0.8rem;
    }
    .gallery-item {
        border-radius: var(--radius); overflow: hidden;
        border: 1px solid var(--border); background: #000;
        animation: fadeIn 0.4s ease;
    }
    .gallery-item video { width: 100%; display: block; aspect-ratio: 9/16; object-fit: cover; }
    .gallery-item .g-caption {
        padding: 0.5rem 0.6rem 0.2rem; background: var(--panel);
        font-size: 0.75rem; color: var(--ink);
        font-weight: 600;
    }
    .gallery-item .g-sub {
        padding: 0 0.6rem 0.5rem; background: var(--panel);
        font-size: 0.68rem; color: var(--ink-dim);
        font-style: italic;
    }

    .status-bar {
        position: fixed; bottom: 0; left: 0; right: 0;
        background: var(--ink); color: #fff; padding: 0.7rem 1rem;
        font-size: 0.78rem; display: flex; align-items: center; gap: 0.6rem;
        transform: translateY(100%); transition: transform 0.3s;
        z-index: 100;
    }
    .status-bar.visible { transform: translateY(0); }
    .status-bar .spinner {
        width: 12px; height: 12px; border: 2px solid rgba(255,255,255,0.3);
        border-top-color: #fff; border-radius: 50%;
        animation: spin 0.8s linear infinite; flex-shrink: 0;
    }
    @keyframes spin { to { transform: rotate(360deg); } }
    @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

    .chips-list {
        display: flex; flex-wrap: wrap; gap: 0.35rem;
    }
    .chip {
        padding: 0.35rem 0.6rem;
        border-radius: 16px;
        border: 1px solid var(--border);
        background: var(--panel-2);
        font-size: 0.72rem;
        cursor: pointer;
        transition: all 0.15s;
        user-select: none;
        display: flex;
        align-items: center;
        gap: 0.3rem;
        font-family: inherit;
        color: var(--ink);
    }
    .chip.selected {
        background: var(--ink);
        color: #fff;
        border-color: var(--ink);
    }
    .chip:active { transform: scale(0.96); }
    .chip:focus-visible { outline: 2px solid var(--info); outline-offset: 2px; }
</style>
</head>
<body>

<header>
    <h1>🎬 Studio Dessin Animé</h1>
    <p class="subtitle">Des histoires animées d'au moins 1 minute</p>
</header>

<div class="info-banner">
    <strong>Comment ça marche :</strong> Ajoutez vos <strong>personnages</strong> (fruits & légumes),
    puis créez vos <strong>scènes</strong>. Chaque scène a ses personnages, un décor, une action
    et un <strong>script / dialogue</strong>. L'IA génère une vidéo par scène.
    <strong>Minimum 1 minute</strong> — l'application vous indique combien de scènes il vous faut.
</div>

<div class="api-panel" id="api-panel">
    <input type="password" class="api-key-input" id="api-key-input"
           placeholder="Collez votre clé API ici (sk-...)" autocomplete="off" spellcheck="false">
    <button type="button" class="api-save-btn" id="api-save-btn">Enregistrer la clé</button>
    <div class="api-status-line" id="api-status-line">
        <span class="status-dot"></span>
        <span id="api-status-text">Aucune clé API enregistrée</span>
    </div>
    <div class="api-hint">
        Clé gratuite sur <a href="https://platform.agnes-ai.com" target="_blank" rel="noopener">platform.agnes-ai.com</a> → Settings → API Keys
    </div>
</div>

<div class="duration-banner warn" id="duration-banner">
    <div class="duration-info">
        <span class="duration-label">Durée totale de l'histoire</span>
        <span class="duration-value" id="duration-value">0,0 s</span>
        <span class="duration-min">Minimum : <strong>1 min (60 s)</strong></span>
    </div>
    <div class="duration-progress">
        <div class="duration-progress-fill" id="duration-progress-fill" style="width:0%"></div>
    </div>
</div>

<div class="section open" id="section-characters">
    <button type="button" class="section-header" data-toggle="section-characters" aria-expanded="true">
        <span class="section-title">👥 Personnages <span class="badge soft">étape 1</span></span>
        <span class="chevron">▼</span>
    </button>
    <div class="section-body">
        <div class="section-content">
            <div class="upload-zone" id="upload-zone">
                <input type="file" id="file-input" accept="image/*" multiple>
                <div class="upload-icon">＋</div>
                <div class="upload-text">Ajoutez vos personnages</div>
                <div class="upload-hint">Une photo par fruit / légume — nom éditable</div>
            </div>
            <div class="characters-grid" id="characters-grid"></div>
            <div class="control-row" style="margin-top:0.8rem;">
                <label class="control-label">Style visuel global</label>
                <select id="style-select"></select>
            </div>
        </div>
    </div>
</div>

<div class="section open" id="section-scenes">
    <button type="button" class="section-header" data-toggle="section-scenes" aria-expanded="true">
        <span class="section-title">🎭 Scènes du scénario <span class="badge soft">étape 2</span></span>
        <span class="chevron">▼</span>
    </button>
    <div class="section-body">
        <div class="section-content">
            <div id="scenes-container"></div>
            <button type="button" class="add-scene-btn" id="add-scene-btn">＋ Ajouter une scène</button>
        </div>
    </div>
</div>

<div class="section" id="section-prompt">
    <button type="button" class="section-header" data-toggle="section-prompt" aria-expanded="false">
        <span class="section-title">✍️ Instructions globales <span class="badge">optionnel</span></span>
        <span class="chevron">▼</span>
    </button>
    <div class="section-body">
        <div class="section-content">
            <textarea class="text-input" id="global-prompt" style="min-height:80px;"
                placeholder="Instructions qui s'appliquent à toutes les scènes. Par exemple :

« Ambiance de conte pour enfants, couleurs vives, musique joyeuse. »"></textarea>
        </div>
    </div>
</div>

<div class="section" id="section-tech">
    <button type="button" class="section-header" data-toggle="section-tech" aria-expanded="false">
        <span class="section-title">📷 Réglages techniques</span>
        <span class="chevron">▼</span>
    </button>
    <div class="section-body">
        <div class="section-content">
            <div class="control-row">
                <label class="control-label">Durée de chaque scène</label>
                <select id="duration-select">
                    <option value="121">5 secondes</option>
                    <option value="153" selected>6,4 secondes (recommandé)</option>
                    <option value="241">10 secondes</option>
                </select>
            </div>
            <div class="control-row">
                <label class="control-label">Voix des personnages</label>
                <select id="voice-style">
                    <option value="auto" selected>Automatique (voix par défaut)</option>
                    <option value="child">Voix enfantine</option>
                    <option value="narrator">Voix de narrateur</option>
                </select>
            </div>
            <div class="control-row">
                <label class="control-label">Intensité du mouvement</label>
                <select id="intensity-select">
                    <option value="subtle">Subtile</option>
                    <option value="moderate" selected>Modérée</option>
                    <option value="strong">Forte (cartoon exagéré)</option>
                </select>
            </div>
        </div>
    </div>
</div>

<button type="button" class="btn-primary" id="generate-btn" disabled>
    Générer toutes les scènes
</button>

<button type="button" class="btn-stop" id="stop-btn">
    ⏹ Arrêter la génération
</button>

<div class="queue" id="queue" style="display:none;"></div>

<div class="gallery" id="gallery" style="display:none;">
    <div class="section-title" style="margin-bottom:0.8rem;">Votre dessin animé</div>
    <div class="gallery-grid" id="gallery-grid"></div>
</div>

<div class="status-bar" id="status-bar">
    <div class="spinner"></div>
    <span id="status-text">Préparation…</span>
</div>

<div class="toast" id="toast">
    <span class="toast-icon" id="toast-icon">✓</span>
    <span id="toast-text">Message</span>
</div>

<script>
// ══════════════════════════════════════════════════════════════════
// CONFIGURATION
// ══════════════════════════════════════════════════════════════════
const API_BASE = 'https://apihub.agnes-ai.com/v1';
const POLL_BASE = 'https://apihub.agnes-ai.com/agnesapi';
const MODEL_VIDEO = 'agnes-video-v2.0';
const FRAME_RATE = 24;
const MIN_DURATION_SEC = 60;

const CREATE_INTERVAL_SAFE = 75000;
const POLL_INTERVAL_SEC = 8;
const MAX_POLL_ATTEMPTS = 100;
const API_KEY_STORAGE = 'agnes_api_key';
const STATE_STORAGE = 'agnes_studio_state';
const MAX_IMAGE_SIZE = 12 * 1024 * 1024;

// ══════════════════════════════════════════════════════════════════
// STYLES
// ══════════════════════════════════════════════════════════════════
const STYLES = [
    { id: 'pixar', name: 'Pixar / Disney — 3D chaleureux',
      prompt: 'high-quality 3D animated character in the style of Pixar and Disney, large expressive eyes, cinematic lighting, charming character design' },
    { id: 'cartoon', name: 'Cartoon classique — Tex Avery',
      prompt: 'classic 1940s American cartoon style, exaggerated expressions, bouncy animation' },
    { id: 'ghibli', name: 'Studio Ghibli — Anime doux',
      prompt: 'Studio Ghibli anime style, Hayao Miyazaki aesthetic, soft hand-painted look, warm natural palette' },
    { id: 'manga', name: 'Manga — Traits noirs expressifs',
      prompt: 'Japanese manga style, bold ink outlines, expressive eyes, dramatic emotional expression' },
    { id: 'claymation', name: 'Claymation — Pâte à modeler',
      prompt: 'claymation stop-motion character, plasticine texture, Aardman Studios style, soft studio lighting' },
    { id: 'watercolor', name: 'Aquarelle — Livre enfant',
      prompt: 'children\'s book watercolor illustration, soft bleeding colors, whimsical hand-drawn character' },
    { id: 'bd', name: 'BD franco-belge — Ligne claire',
      prompt: 'Franco-Belgian bande dessinée style, ligne claire, clean outlines, flat vivid colors, Tintin-influenced' },
    { id: 'modern3d', name: 'Publicité moderne — 3D réaliste',
      prompt: 'modern 3D animated commercial character, photorealistic fruit texture, anthropomorphic design, advertising quality' },
    { id: 'vintage', name: 'Publicité vintage années 50',
      prompt: '1950s vintage advertising cartoon style, retro hand-drawn animation, warm faded colors' },
    { id: 'kawaii', name: 'Kawaii — Mignon japonais',
      prompt: 'kawaii Japanese cute style, chibi proportions, big sparkling eyes, pastel colors, adorable' }
];

// ══════════════════════════════════════════════════════════════════
// DÉCORS
// ══════════════════════════════════════════════════════════════════
const DECORS = [
    { id: 'none', name: 'Fond original' },
    { id: 'kitchen', name: 'Cuisine' },
    { id: 'market', name: 'Marché' },
    { id: 'garden', name: 'Potager' },
    { id: 'forest', name: 'Forêt' },
    { id: 'beach', name: 'Plage' },
    { id: 'mountain', name: 'Montagne' },
    { id: 'party', name: 'Fête / confettis' },
    { id: 'studio', name: 'Studio coloré' },
    { id: 'rain', name: 'Sous la pluie' },
    { id: 'sunset', name: 'Coucher de soleil' },
    { id: 'night', name: 'Nuit étoilée' }
];

// ══════════════════════════════════════════════════════════════════
// ACTIONS DU CORPS
// ══════════════════════════════════════════════════════════════════
const ACTIONS = [
    { id: 'idle', name: 'Immobile', prompt: 'the character stays still, only subtle breathing and blinking' },
    { id: 'walk', name: 'Marcher', prompt: 'the character walks with a cartoon gait, arms and legs swinging' },
    { id: 'run', name: 'Courir', prompt: 'the character runs rapidly, energetic motion, arms pumping' },
    { id: 'jump', name: 'Sauter', prompt: 'the character jumps with joy, both feet off the ground' },
    { id: 'dance', name: 'Danser', prompt: 'the character dances rhythmically, hips and arms moving' },
    { id: 'wave', name: 'Saluer', prompt: 'the character waves hello with one hand' },
    { id: 'sit', name: 'S\'asseoir', prompt: 'the character sits down slowly on a surface' },
    { id: 'stand', name: 'Se lever', prompt: 'the character stands up from a seated position' },
    { id: 'fall', name: 'Tomber', prompt: 'the character trips and falls comically' },
    { id: 'roll', name: 'Rouler', prompt: 'the character rolls like a ball, cartoon style' },
    { id: 'hug', name: 'Câlin', prompt: 'the character opens arms wide for a hug' },
    { id: 'think', name: 'Réfléchir', prompt: 'the character taps chin thoughtfully, thinking pose' },
    { id: 'sleep', name: 'Dormir', prompt: 'the character falls asleep, eyes closing, soft breathing' },
    { id: 'eat', name: 'Manger', prompt: 'the character eats something with joy' },
    { id: 'sing', name: 'Chanter', prompt: 'the character sings, mouth open, expressive gestures' }
];

// ══════════════════════════════════════════════════════════════════
// EXPRESSIONS
// ══════════════════════════════════════════════════════════════════
const EXPRESSIONS = [
    { id: 'smile', name: 'Sourire', prompt: 'a warm happy smile' },
    { id: 'laugh', name: 'Rire', prompt: 'laughing out loud, big open smile' },
    { id: 'surprise', name: 'Surprise', prompt: 'surprised expression, wide eyes, mouth open' },
    { id: 'angry', name: 'Colère', prompt: 'angry expression, furrowed brows, red cheeks' },
    { id: 'sad', name: 'Tristesse', prompt: 'sad expression, tear in one eye, drooping mouth' },
    { id: 'scared', name: 'Peur', prompt: 'scared expression, trembling, eyes wide' },
    { id: 'wink', name: 'Clin d\'œil', prompt: 'playful wink with one eye' },
    { id: 'tongue', name: 'Langue tirée', prompt: 'playful tongue sticking out' },
    { id: 'blush', name: 'Rougir', prompt: 'blushing, pink cheeks, shy smile' },
    { id: 'yawn', name: 'Bâiller', prompt: 'yawning, mouth wide open, sleepy eyes' },
    { id: 'neutral', name: 'Neutre', prompt: 'calm neutral expression' }
];

// ══════════════════════════════════════════════════════════════════
// ÉTAT GLOBAL
// ══════════════════════════════════════════════════════════════════
const state = {
    characters: [],
    scenes: [],
    style: 'pixar',
    durationFrames: 153,
    isRunning: false,
    stopRequested: false,
    queue: [],
    completed: 0,
    failed: 0,
    selectedDurationSec: 6.4
};

// ══════════════════════════════════════════════════════════════════
// OUTILS
// ══════════════════════════════════════════════════════════════════
function sleep(ms) { return new Promise(r => setTimeout(r, ms)); }
function log(m) { console.log('[Studio] ' + m); }
function esc(s) {
    return String(s == null ? '' : s).replace(/[&<>"']/g, c => (
        { '&': '&amp;', '<': '&lt;', '>': '&gt;', '"': '&quot;', "'": '&#39;' }[c]
    ));
}
function setStatus(t) {
    const bar = document.getElementById('status-bar');
    const txt = document.getElementById('status-text');
    if (!bar || !txt) return;
    if (t) { bar.classList.add('visible'); txt.textContent = t; }
    else bar.classList.remove('visible');
}

let toastTimeout = null;
function showToast(msg, type = 'success', dur = 2500) {
    const toast = document.getElementById('toast');
    const icon = document.getElementById('toast-icon');
    const text = document.getElementById('toast-text');
    if (!toast) return;
    toast.classList.remove('visible', 'success', 'error', 'warn');
    void toast.offsetWidth;
    const icons = { success: '✓', error: '✕', warn: '⚠' };
    icon.textContent = icons[type] || '✓';
    text.textContent = msg;
    toast.classList.add(type);
    requestAnimationFrame(() => toast.classList.add('visible'));
    if (toastTimeout) clearTimeout(toastTimeout);
    toastTimeout = setTimeout(() => toast.classList.remove('visible'), dur);
}

// ══════════════════════════════════════════════════════════════════
// CLÉ API
// ══════════════════════════════════════════════════════════════════
function getApiKey() {
    try { return (localStorage.getItem(API_KEY_STORAGE) || '').trim(); }
    catch (e) { return ''; }
}
function saveApiKey() {
    const input = document.getElementById('api-key-input');
    if (!input) return;
    const k = input.value.trim();
    if (!k) {
        try { localStorage.removeItem(API_KEY_STORAGE); } catch (e) {}
        updateApiPanel();
        showToast('Clé supprimée', 'warn');
        return;
    }
    if (!k.startsWith('sk-') && !confirm('La clé ne commence pas par "sk-". Sauvegarder ?')) return;
    try {
        localStorage.setItem(API_KEY_STORAGE, k);
        updateApiPanel();
        showToast('Clé API enregistrée', 'success');
        input.blur();
    } catch (e) {
        showToast('Erreur de sauvegarde', 'error');
    }
}
function updateApiPanel() {
    const panel = document.getElementById('api-panel');
    const input = document.getElementById('api-key-input');
    const line = document.getElementById('api-status-line');
    const txt = document.getElementById('api-status-text');
    const k = getApiKey();
    if (!panel || !input || !line || !txt) return;
    if (k) {
        panel.classList.add('ok');
        line.classList.add('ok');
        txt.textContent = 'Clé active · ' + k.slice(0, 8) + '…' + k.slice(-4);
        input.value = k;
        input.placeholder = '';
    } else {
        panel.classList.remove('ok');
        line.classList.remove('ok');
        txt.textContent = 'Aucune clé API enregistrée';
        input.value = '';
        input.placeholder = 'Collez votre clé API ici (sk-...)';
    }
    updateGenerateBtn();
}

// ══════════════════════════════════════════════════════════════════
// PERSISTANCE D'ÉTAT (scènes, style, réglages — sans images)
// ══════════════════════════════════════════════════════════════════
let saveStateTimeout = null;
function saveStateDebounced() {
    if (saveStateTimeout) clearTimeout(saveStateTimeout);
    saveStateTimeout = setTimeout(() => saveState(), 500);
}
function saveState() {
    try {
        const persisted = {
            style: state.style,
            durationFrames: state.durationFrames,
            selectedDurationSec: state.selectedDurationSec,
            scenes: state.scenes.map(s => ({
                id: s.id,
                title: s.title,
                characterIds: s.characterIds,
                script: s.script,
                decor: s.decor,
                action: s.action,
                expression: s.expression
            })),
            globalPrompt: document.getElementById('global-prompt')?.value || '',
            voiceStyle: document.getElementById('voice-style')?.value || 'auto',
            intensity: document.getElementById('intensity-select')?.value || 'moderate'
        };
        localStorage.setItem(STATE_STORAGE, JSON.stringify(persisted));
    } catch (e) {
        log('Impossible de sauvegarder l\'état : ' + e.message);
    }
}
function loadState() {
    try {
        const raw = localStorage.getItem(STATE_STORAGE);
        if (!raw) return false;
        const d = JSON.parse(raw);
        if (d.style && STYLES.some(s => s.id === d.style)) state.style = d.style;
        if (typeof d.durationFrames === 'number') state.durationFrames = d.durationFrames;
        if (typeof d.selectedDurationSec === 'number') state.selectedDurationSec = d.selectedDurationSec;
        if (Array.isArray(d.scenes)) {
            state.scenes = d.scenes.map(s => ({
                id: s.id || makeId(),
                title: s.title || 'Scène',
                characterIds: Array.isArray(s.characterIds) ? s.characterIds : [],
                script: s.script || '',
                decor: s.decor || 'none',
                action: s.action || 'idle',
                expression: s.expression || 'smile'
            }));
        }
        return d;
    } catch (e) {
        log('Impossible de charger l\'état : ' + e.message);
        return false;
    }
}
function clearState() {
    try { localStorage.removeItem(STATE_STORAGE); } catch (e) {}
}

// ══════════════════════════════════════════════════════════════════
// CHARGEMENT DES PERSONNAGES
// ══════════════════════════════════════════════════════════════════
function fileToDataUri(file) {
    return new Promise((res, rej) => {
        const r = new FileReader();
        r.onload = e => res(e.target.result);
        r.onerror = () => rej(new Error('Erreur lecture'));
        r.readAsDataURL(file);
    });
}
function generateThumbnail(dataUri) {
    return new Promise((res) => {
        const img = new Image();
        img.onload = () => {
            try {
                const c = document.createElement('canvas');
                const ratio = img.height / img.width;
                c.width = 200;
                c.height = Math.round(200 * ratio);
                const ctx = c.getContext('2d');
                ctx.drawImage(img, 0, 0, c.width, c.height);
                res(c.toDataURL('image/jpeg', 0.7));
            } catch (e) { res(dataUri); }
        };
        img.onerror = () => res(dataUri);
        img.src = dataUri;
    });
}
async function processOneFile(file) {
    if (!file.type.startsWith('image/')) return null;
    if (file.size > MAX_IMAGE_SIZE) return null;
    try {
        const dataUri = await fileToDataUri(file);
        const thumb = await generateThumbnail(dataUri);
        const baseName = file.name.replace(/\.[^.]+$/, '');
        return { file, dataUri, thumbnail: thumb, name: baseName.slice(0, 20), id: Date.now() + Math.random() };
    } catch (e) { return null; }
}
async function handleFiles(files) {
    const imgs = Array.from(files).filter(f => f.type.startsWith('image/'));
    if (!imgs.length) return;
    const uploadZone = document.getElementById('upload-zone');
    uploadZone.classList.add('loading');
    setStatus('Chargement…');
    const BATCH = 5;
    for (let i = 0; i < imgs.length; i += BATCH) {
        const batch = imgs.slice(i, i + BATCH);
        const results = await Promise.allSettled(batch.map(f => processOneFile(f)));
        for (const r of results) {
            if (r.status === 'fulfilled' && r.value) state.characters.push(r.value);
        }
        renderCharacters();
    }
    uploadZone.classList.remove('loading');
    setStatus(null);
    renderScenes();
    updateDuration();
    updateGenerateBtn();
}

// ══════════════════════════════════════════════════════════════════
// RENDU PERSONNAGES
// ══════════════════════════════════════════════════════════════════
function renderCharacters() {
    const g = document.getElementById('characters-grid');
    if (!g) return;
    if (!state.characters.length) {
        g.innerHTML = '<div class="empty-msg">Aucun personnage — ajoutez vos fruits et légumes ci-dessus</div>';
        return;
    }
    g.innerHTML = state.characters.map(c =>
        '<div class="character-card" data-id="' + c.id + '">' +
            '<img src="' + (c.thumbnail || c.dataUri) + '" alt="">' +
            '<button class="remove-btn" data-remove="' + c.id + '" aria-label="Supprimer">✕</button>' +
            '<input class="c-name-input" data-name="' + c.id + '" value="' + esc(c.name) + '" placeholder="Nom du personnage">' +
        '</div>'
    ).join('');

    g.querySelectorAll('[data-remove]').forEach(b => b.addEventListener('click', e => {
        e.stopPropagation();
        const id = parseFloat(b.dataset.remove);
        state.characters = state.characters.filter(c => c.id !== id);
        state.scenes.forEach(s => { s.characterIds = s.characterIds.filter(x => x !== id); });
        renderCharacters();
        renderScenes();
        updateGenerateBtn();
    }));
    g.querySelectorAll('[data-name]').forEach(inp => inp.addEventListener('input', e => {
        const id = parseFloat(inp.dataset.name);
        const c = state.characters.find(x => x.id === id);
        if (c) c.name = e.target.value.slice(0, 30);
        renderScenes();
    }));
}

// ══════════════════════════════════════════════════════════════════
// SCÈNES
// ══════════════════════════════════════════════════════════════════
function makeId() { return Date.now() + Math.random(); }

function addScene(data) {
    state.scenes.push({
        id: makeId(),
        title: data?.title || 'Scène ' + (state.scenes.length + 1),
        characterIds: data?.characterIds || [],
        script: data?.script || '',
        decor: data?.decor || 'none',
        action: data?.action || 'idle',
        expression: data?.expression || 'smile'
    });
    renderScenes();
    updateDuration();
    updateGenerateBtn();
    saveStateDebounced();
}
function removeScene(id) {
    state.scenes = state.scenes.filter(s => s.id !== id);
    renderScenes();
    updateDuration();
    updateGenerateBtn();
    saveStateDebounced();
}
function updateScene(id, key, value) {
    const s = state.scenes.find(x => x.id === id);
    if (s) s[key] = value;
    updateDuration();
    saveStateDebounced();
}
function toggleSceneCharacter(sceneId, charId) {
    const s = state.scenes.find(x => x.id === sceneId);
    if (!s) return;
    const idx = s.characterIds.indexOf(charId);
    if (idx >= 0) s.characterIds.splice(idx, 1);
    else s.characterIds.push(charId);
    renderScenes();
    saveStateDebounced();
}

function renderScenes() {
    const cont = document.getElementById('scenes-container');
    if (!cont) return;
    if (!state.scenes.length) {
        cont.innerHTML = '<div class="empty-msg">Aucune scène — cliquez sur « Ajouter une scène »</div>';
        return;
    }

    cont.innerHTML = state.scenes.map((scene, i) => {
        const charChips = state.characters.length
            ? state.characters.map(c => {
                const sel = scene.characterIds.includes(c.id) ? 'selected' : '';
                return '<button type="button" class="scene-char-chip ' + sel + '" data-toggle-char="' + c.id + '" data-scene="' + scene.id + '" aria-pressed="' + (sel ? 'true' : 'false') + '">' +
                    '<img src="' + (c.thumbnail || c.dataUri) + '" alt="">' +
                    esc(c.name) +
                '</button>';
            }).join('')
            : '<div class="no-characters-msg">Ajoutez d\'abord des personnages</div>';

        const decorOptions = DECORS.map(d =>
            '<option value="' + d.id + '" ' + (scene.decor === d.id ? 'selected' : '') + '>' + esc(d.name) + '</option>'
        ).join('');

        const actionChips = ACTIONS.map(a =>
            '<button type="button" class="chip ' + (scene.action === a.id ? 'selected' : '') + '" data-action="' + a.id + '" data-scene="' + scene.id + '" aria-pressed="' + (scene.action === a.id ? 'true' : 'false') + '">' + esc(a.name) + '</button>'
        ).join('');

        const exprChips = EXPRESSIONS.map(e =>
            '<button type="button" class="chip ' + (scene.expression === e.id ? 'selected' : '') + '" data-expr="' + e.id + '" data-scene="' + scene.id + '" aria-pressed="' + (scene.expression === e.id ? 'true' : 'false') + '">' + esc(e.name) + '</button>'
        ).join('');

        return '<div class="scene-card" data-scene-id="' + scene.id + '">' +
            '<div class="scene-header">' +
                '<div class="scene-number">' + (i + 1) + '</div>' +
                '<input class="scene-title-input" data-scene="' + scene.id + '" data-field="title" value="' + esc(scene.title) + '" placeholder="Titre de la scène">' +
                '<button type="button" class="scene-remove-btn" data-remove-scene="' + scene.id + '" aria-label="Supprimer la scène">✕</button>' +
            '</div>' +
            '<div class="scene-field">' +
                '<label class="scene-label">👥 Personnages de cette scène</label>' +
                '<div class="scene-characters-list">' + charChips + '</div>' +
            '</div>' +
            '<div class="scene-field">' +
                '<label class="scene-label">📍 Décor</label>' +
                '<select data-scene="' + scene.id + '" data-field="decor">' + decorOptions + '</select>' +
            '</div>' +
            '<div class="scene-field">' +
                '<label class="scene-label">🚶 Action du corps</label>' +
                '<div class="chips-list">' + actionChips + '</div>' +
            '</div>' +
            '<div class="scene-field">' +
                '<label class="scene-label">😄 Expression du visage</label>' +
                '<div class="chips-list">' + exprChips + '</div>' +
            '</div>' +
            '<div class="scene-field">' +
                '<label class="scene-label">📝 Script / Dialogue</label>' +
                '<textarea class="scene-script-textarea" data-scene="' + scene.id + '" data-field="script" placeholder="Exemple :\n\nPomme : « Bonjour ! »\nCarotte : « Salut ! On y va ? »">' + esc(scene.script) + '</textarea>' +
            '</div>' +
        '</div>';
    }).join('');

    cont.querySelectorAll('[data-remove-scene]').forEach(b => b.addEventListener('click', () => {
        removeScene(parseFloat(b.dataset.removeScene));
    }));
    cont.querySelectorAll('input[data-field], select[data-field], textarea[data-field]').forEach(el => {
        el.addEventListener('input', e => {
            updateScene(parseFloat(el.dataset.scene), el.dataset.field, e.target.value);
        });
        el.addEventListener('change', e => {
            updateScene(parseFloat(el.dataset.scene), el.dataset.field, e.target.value);
        });
    });
    cont.querySelectorAll('[data-toggle-char]').forEach(chip => chip.addEventListener('click', () => {
        toggleSceneCharacter(parseFloat(chip.dataset.scene), parseFloat(chip.dataset.toggleChar));
    }));
    cont.querySelectorAll('[data-action]').forEach(chip => chip.addEventListener('click', () => {
        updateScene(parseFloat(chip.dataset.scene), 'action', chip.dataset.action);
        renderScenes();
    }));
    cont.querySelectorAll('[data-expr]').forEach(chip => chip.addEventListener('click', () => {
        updateScene(parseFloat(chip.dataset.scene), 'expression', chip.dataset.expr);
        renderScenes();
    }));
}

// ══════════════════════════════════════════════════════════════════
// DURÉE TOTALE
// ══════════════════════════════════════════════════════════════════
function updateDuration() {
    const perScene = state.selectedDurationSec || 6.4;
    const total = state.scenes.length * perScene;
    const banner = document.getElementById('duration-banner');
    const val = document.getElementById('duration-value');
    const fill = document.getElementById('duration-progress-fill');
    const needed = Math.ceil(MIN_DURATION_SEC / perScene);

    if (!banner) return;
    banner.classList.remove('ok', 'warn');
    if (total >= MIN_DURATION_SEC) banner.classList.add('ok');
    else banner.classList.add('warn');

    if (val) val.textContent = total.toFixed(1).replace('.', ',') + ' s';
    if (fill) fill.style.width = Math.min(100, (total / MIN_DURATION_SEC) * 100) + '%';

    const minEl = banner.querySelector('.duration-min');
    if (minEl) {
        if (total >= MIN_DURATION_SEC) {
            minEl.innerHTML = '✓ Durée suffisante pour une histoire complète';
        } else {
            const missing = Math.max(0, needed - state.scenes.length);
            minEl.innerHTML = 'Minimum : <strong>1 min (60 s)</strong> — ajoutez encore <strong>' + missing + '</strong> scène' + (missing > 1 ? 's' : '') + ' (total : ' + needed + ' scènes min.)';
        }
    }
}

// ══════════════════════════════════════════════════════════════════
// CONSTRUCTION DU PROMPT
// ══════════════════════════════════════════════════════════════════
function buildScenePrompt(scene, frozenGlobalPrompt, frozenVoice, frozenIntensity) {
    const style = STYLES.find(s => s.id === state.style) || STYLES[0];
    const decor = DECORS.find(d => d.id === scene.decor) || DECORS[0];
    const action = ACTIONS.find(a => a.id === scene.action) || ACTIONS[0];
    const expr = EXPRESSIONS.find(e => e.id === scene.expression) || EXPRESSIONS[0];
    const chars = scene.characterIds
        .map(id => state.characters.find(c => c.id === id))
        .filter(Boolean);

    const charDescriptions = chars.map(c =>
        'Character "' + c.name + '": a fruit or vegetable with a human face, arms and legs, expressive cartoon eyes and mouth, walking and talking like a real character.'
    ).join(' ');

    const parts = [];
    parts.push('Animate this image as the starting frame of a cartoon scene.');
    parts.push('Style: ' + style.prompt + '.');
    parts.push('Keep the exact shape, color, texture and identity of each fruit and vegetable visible in the image. They must remain clearly recognizable as fruits and vegetables.');
    parts.push('Each fruit or vegetable is an anthropomorphic character with a human face (eyes, mouth, eyebrows), arms and legs. They move and speak like cartoon characters.');
    parts.push(charDescriptions);
    parts.push('Action: ' + action.prompt + '.');
    parts.push('Expression: ' + expr.prompt + '.');

    if (scene.decor && scene.decor !== 'none') {
        parts.push('Setting: ' + decor.name + ' environment.');
    }

    if (scene.script && scene.script.trim()) {
        parts.push('The characters say the following lines, with mouth movements matching their speech: ' + scene.script.trim());
    } else {
        parts.push('The characters breathe, blink naturally and move their mouths as if speaking.');
    }

    // Voix & intensité
    if (frozenVoice && frozenVoice !== 'auto') {
        parts.push(frozenVoice === 'child'
            ? 'The voices sound like cheerful children.'
            : 'The voices sound like a warm storyteller narrator.');
    }
    if (frozenIntensity && frozenIntensity !== 'moderate') {
        parts.push(frozenIntensity === 'subtle'
            ? 'Keep movement subtle and calm.'
            : 'Push the movement strong and exaggerated, cartoon-like.');
    }

    if (frozenGlobalPrompt && frozenGlobalPrompt.trim()) {
        parts.push(frozenGlobalPrompt.trim());
    }

    parts.push('Portrait orientation 9:16 vertical, 24fps, cinematic lighting, cartoon quality, no text overlays, no subtitles, no watermarks.');
    return parts.join(' ');
}

// ══════════════════════════════════════════════════════════════════
// COMPOSITION MULTI-PERSONNAGES
// Fusionne les images des personnages d'une scène en une seule
// image (planche contact) envoyée comme image de départ à l'IA.
// ══════════════════════════════════════════════════════════════════
function loadImage(src) {
    return new Promise((res, rej) => {
        const img = new Image();
        img.crossOrigin = 'anonymous';
        img.onload = () => res(img);
        img.onerror = () => rej(new Error('Image illisible'));
        img.src = src;
    });
}

async function composeSceneImage(scene) {
    const chars = scene.characterIds
        .map(id => state.characters.find(c => c.id === id))
        .filter(Boolean);

    if (!chars.length) {
        if (state.characters.length) return state.characters[0].dataUri;
        throw new Error('Aucun personnage disponible pour cette scène');
    }
    if (chars.length === 1) return chars[0].dataUri;

    try {
        const W = 1024, H = 1024;
        const canvas = document.createElement('canvas');
        canvas.width = W;
        canvas.height = H;
        const ctx = canvas.getContext('2d');
        ctx.fillStyle = '#ffffff';
        ctx.fillRect(0, 0, W, H);

        const n = chars.length;
        const cols = Math.ceil(Math.sqrt(n));
        const rows = Math.ceil(n / cols);
        const cellW = W / cols;
        const cellH = H / rows;
        const pad = 12;

        const images = await Promise.all(chars.map(c => loadImage(c.dataUri).catch(() => null)));

        images.forEach((img, i) => {
            if (!img) return;
            const col = i % cols;
            const row = Math.floor(i / cols);
            const cx = col * cellW + pad;
            const cy = row * cellH + pad;
            const cw = cellW - pad * 2;
            const ch = cellH - pad * 2;

            const r = Math.min(cw / img.width, ch / img.height);
            const dw = img.width * r;
            const dh = img.height * r;
            const dx = cx + (cw - dw) / 2;
            const dy = cy + (ch - dh) / 2;

            // Fond doux derrière chaque personnage
            ctx.fillStyle = '#f5f5f5';
            ctx.fillRect(cx, cy, cw, ch);
            ctx.drawImage(img, dx, dy, dw, dh);
        });

        return canvas.toDataURL('image/jpeg', 0.85);
    } catch (e) {
        log('Composition impossible (' + e.message + ') → image unique');
        return chars[0].dataUri;
    }
}

// ══════════════════════════════════════════════════════════════════
// ANTI-VEILLE
// ══════════════════════════════════════════════════════════════════
let wakeLock = null;
async function requestWakeLock() {
    if ('wakeLock' in navigator) {
        try { wakeLock = await navigator.wakeLock.request('screen'); } catch (e) {}
    }
}
async function releaseWakeLock() {
    if (wakeLock) {
        try { await wakeLock.release(); } catch (e) {}
        wakeLock = null;
    }
}
document.addEventListener('visibilitychange', () => {
    if (document.visibilityState === 'visible' && state.isRunning) {
        requestWakeLock();
    }
});

// ══════════════════════════════════════════════════════════════════
// API AGNES
// ══════════════════════════════════════════════════════════════════
async function apiFetch(url, options = {}, label = 'API') {
    for (let a = 0; a < 7; a++) {
        if (state.stopRequested) throw new Error('Arrêt demandé');
        try {
            const res = await fetch(url, options);
            if (res.status === 429) {
                const w = [15, 30, 45, 60, 90, 120, 180][Math.min(a, 6)];
                setStatus('IA en préparation… (' + w + 's)');
                await sleep(w * 1000);
                continue;
            }
            if (res.status === 503) {
                const w = [5, 10, 15, 20, 30, 45][Math.min(a, 5)];
                setStatus('Vidéo en préparation… (' + w + 's)');
                await sleep(w * 1000);
                continue;
            }
            return res;
        } catch (e) {
            if (e.message === 'Arrêt demandé') throw e;
            const w = [3, 5, 8, 12, 20, 30][Math.min(a, 5)];
            await sleep(w * 1000);
        }
    }
    return fetch(url, options);
}

async function createVideoTask(imageDataUri, prompt) {
    const body = {
        model: MODEL_VIDEO,
        prompt: prompt,
        image: imageDataUri,
        num_frames: state.durationFrames,
        frame_rate: FRAME_RATE
    };
    const res = await apiFetch(API_BASE + '/videos', {
        method: 'POST',
        headers: {
            'Authorization': 'Bearer ' + getApiKey(),
            'Content-Type': 'application/json'
        },
        body: JSON.stringify(body)
    }, 'Création');
    if (!res.ok) {
        const err = await res.text();
        throw new Error('HTTP ' + res.status + ' — ' + err.slice(0, 200));
    }
    const data = await res.json();
    const id = data.video_id || data.id || data.task_id;
    if (!id) throw new Error('Pas de video_id retourné');
    return id;
}

async function pollVideo(videoId, onProgress) {
    let wait = 25;
    while (wait > 0) {
        if (state.stopRequested) throw new Error('Arrêt demandé');
        onProgress('Vidéo en préparation… — ' + wait + 's');
        await sleep(1000);
        wait--;
    }
    for (let a = 0; a < MAX_POLL_ATTEMPTS; a++) {
        if (state.stopRequested) throw new Error('Arrêt demandé');
        if (a > 0) {
            let r = POLL_INTERVAL_SEC;
            while (r > 0) {
                if (state.stopRequested) throw new Error('Arrêt demandé');
                onProgress('L\'image prend vie… — ' + r + 's');
                await sleep(1000);
                r--;
            }
        }
        const url = POLL_BASE + '?video_id=' + encodeURIComponent(videoId) + '&model_name=' + encodeURIComponent(MODEL_VIDEO);
        const res = await apiFetch(url, {
            method: 'GET',
            headers: { 'Authorization': 'Bearer ' + getApiKey() }
        }, 'Polling');
        const d = await res.json();
        const status = d.status || 'unknown';
        const progress = d.progress || 0;
        onProgress('Création… — ' + progress + '%');
        if (status === 'completed' || status === 'succeeded' || status === 'done') {
            const url = (d.metadata && d.metadata.url) || d.url || (d.output && d.output.url);
            if (!url) throw new Error('Pas d\'URL retournée');
            return url;
        }
        if (status === 'failed' || status === 'error' || status === 'cancelled') {
            throw new Error('Échec (' + status + ')');
        }
    }
    throw new Error('Délai maximal dépassé');
}

// ══════════════════════════════════════════════════════════════════
// FILE
// ══════════════════════════════════════════════════════════════════
function renderQueue() {
    const q = document.getElementById('queue');
    if (!q) return;
    if (!state.queue.length) { q.style.display = 'none'; return; }
    q.style.display = 'block';

    const total = state.queue.length;
    const done = state.completed + state.failed;

    let html = '<div class="queue-summary">' +
        '<span class="progress-text">Progression : ' + done + '/' + total + '</span>' +
        '<span class="eta-text">' + (done < total ? 'en cours…' : 'Terminé') + '</span>' +
        '</div>';

    html += state.queue.slice(0, 30).map(item => {
        let icon = '○', txt = 'En attente', cls = 'pending';
        if (item.status === 'creating') { icon = '◐'; txt = 'Préparation…'; cls = 'creating'; }
        else if (item.status === 'processing') { icon = '◐'; txt = item.progress || 'En cours…'; cls = 'processing'; }
        else if (item.status === 'done') { icon = '●'; txt = 'Terminé'; cls = 'done'; }
        else if (item.status === 'failed') { icon = '✕'; txt = 'Échec'; cls = 'failed'; }
        return '<div class="queue-item ' + cls + '">' +
            '<div class="q-icon">' + icon + '</div>' +
            '<div class="q-name">' + esc(item.title) + '</div>' +
            '<div class="q-status">' + esc(txt) + '</div>' +
            '</div>';
    }).join('');

    if (state.queue.length > 30) {
        html += '<div class="queue-more">… et ' + (state.queue.length - 30) + ' autres scènes</div>';
    }

    q.innerHTML = html;
}

// ══════════════════════════════════════════════════════════════════
// GALERIE
// ══════════════════════════════════════════════════════════════════
function addToGallery(videoUrl, scene) {
    const gallery = document.getElementById('gallery');
    const grid = document.getElementById('gallery-grid');
    if (!gallery || !grid) return;
    gallery.style.display = 'block';

    const chars = scene.characterIds
        .map(id => state.characters.find(c => c.id === id))
        .filter(Boolean)
        .map(c => c.name)
        .join(', ') || '—';

    const el = document.createElement('div');
    el.className = 'gallery-item';
    el.innerHTML =
        '<video controls preload="metadata" muted playsinline>' +
            '<source src="' + videoUrl + '" type="video/mp4">' +
        '</video>' +
        '<div class="g-caption">' + esc(scene.title) + '</div>' +
        '<div class="g-sub">' + esc(chars) + '</div>';
    grid.appendChild(el);
}

// ══════════════════════════════════════════════════════════════════
// GÉNÉRATION
// ══════════════════════════════════════════════════════════════════
function updateGenerateBtn() {
    const btn = document.getElementById('generate-btn');
    if (!btn) return;
    const hasChars = state.characters.length > 0;
    const hasScenes = state.scenes.length > 0;
    const hasKey = !!getApiKey();
    btn.disabled = !hasChars || !hasScenes || !hasKey || state.isRunning;

    if (state.isRunning) {
        const done = state.completed + state.failed;
        btn.textContent = 'Génération en cours… (' + done + '/' + state.queue.length + ')';
    } else if (!hasKey) {
        btn.textContent = 'Ajoutez votre clé API';
    } else if (!hasChars) {
        btn.textContent = 'Ajoutez des personnages';
    } else if (!hasScenes) {
        btn.textContent = 'Ajoutez des scènes';
    } else {
        btn.textContent = 'Générer ' + state.scenes.length + ' scène' + (state.scenes.length > 1 ? 's' : '');
    }
}

async function startGeneration() {
    if (state.isRunning) return;
    if (!getApiKey()) { showToast('Ajoutez d\'abord votre clé API', 'error'); return; }
    if (!state.characters.length) { showToast('Ajoutez au moins un personnage', 'error'); return; }
    if (!state.scenes.length) { showToast('Ajoutez au moins une scène', 'error'); return; }

    const total = state.scenes.length * state.selectedDurationSec;
    if (total < MIN_DURATION_SEC) {
        const needed = Math.ceil(MIN_DURATION_SEC / state.selectedDurationSec);
        const missing = needed - state.scenes.length;
        if (!confirm('Votre histoire ne dure que ' + total.toFixed(1) + ' s (minimum ' + MIN_DURATION_SEC + ' s).\nAjoutez encore ' + missing + ' scène' + (missing > 1 ? 's' : '') + '.\n\nContinuer quand même ?')) return;
    }

    const emptyScenes = state.scenes.filter(s => s.characterIds.length === 0);
    if (emptyScenes.length) {
        showToast(emptyScenes.length + ' scène(s) sans personnage', 'error');
        return;
    }

    // Fige les réglages au démarrage (évite les modifs en cours de route)
    const frozenGlobalPrompt = document.getElementById('global-prompt')?.value || '';
    const frozenVoice = document.getElementById('voice-style')?.value || 'auto';
    const frozenIntensity = document.getElementById('intensity-select')?.value || 'moderate';

    state.isRunning = true;
    state.stopRequested = false;
    state.completed = 0;
    state.failed = 0;
    state.queue = state.scenes.map((scene, i) => ({
        index: i,
        title: scene.title,
        scene: scene,
        status: 'pending',
        progress: null
    }));

    document.getElementById('gallery-grid').innerHTML = '';
    document.getElementById('gallery').style.display = 'none';
    document.getElementById('stop-btn').classList.add('visible');

    requestWakeLock();
    renderQueue();
    updateGenerateBtn();

    try {
        for (let i = 0; i < state.queue.length; i++) {
            if (state.stopRequested) break;
            const item = state.queue[i];
            item.status = 'creating';
            item.progress = 'Préparation…';
            renderQueue();

            try {
                // 1) Composer l'image de départ (multi-personnages)
                setStatus('Composition de l\'image…');
                const startImage = await composeSceneImage(item.scene);

                // 2) Construire le prompt avec les réglages figés
                const prompt = buildScenePrompt(item.scene, frozenGlobalPrompt, frozenVoice, frozenIntensity);

                // 3) Créer la tâche
                const videoId = await createVideoTask(startImage, prompt);
                item.status = 'processing';
                item.progress = 'En cours…';
                renderQueue();

                // 4) Attendre la vidéo
                const videoUrl = await pollVideo(videoId, (prog) => {
                    item.progress = prog;
                    renderQueue();
                });

                item.status = 'done';
                item.progress = 'Terminé';
                state.completed++;
                renderQueue();
                updateGenerateBtn();
                addToGallery(videoUrl, item.scene);

                // Pause entre scènes
                if (i < state.queue.length - 1 && !state.stopRequested) {
                    for (let r = 10; r > 0; r--) {
                        if (state.stopRequested) break;
                        setStatus('Pause avant la scène suivante… — ' + r + 's');
                        await sleep(1000);
                    }
                }
            } catch (e) {
                if (e.message === 'Arrêt demandé') break;
                log('[Scène ' + (i + 1) + '] ' + e.message);
                item.status = 'failed';
                item.progress = 'Échec : ' + e.message.slice(0, 60);
                state.failed++;
                renderQueue();
                updateGenerateBtn();
            }
        }

        setStatus('Terminé — ' + state.completed + '/' + state.queue.length + ' scènes créées');
        await sleep(3000);
    } finally {
        setStatus(null);
        state.isRunning = false;
        state.stopRequested = false;
        document.getElementById('stop-btn').classList.remove('visible');
        updateGenerateBtn();
        releaseWakeLock();
        if (state.completed > 0) {
            showToast(state.completed + ' scène(s) créée(s)', 'success');
        }
    }
}

function stopGeneration() {
    if (!state.isRunning) return;
    state.stopRequested = true;
    setStatus('Arrêt en cours…');
}

// ══════════════════════════════════════════════════════════════════
// INITIALISATION
// ══════════════════════════════════════════════════════════════════
(function init() {
    // Restaurer l'état sauvegardé
    const saved = loadState();

    // Remplir le select des styles
    const styleSelect = document.getElementById('style-select');
    if (styleSelect) {
        styleSelect.innerHTML = STYLES.map(s =>
            '<option value="' + s.id + '">' + esc(s.name) + '</option>'
        ).join('');
        styleSelect.value = state.style;
        styleSelect.addEventListener('change', e => {
            state.style = e.target.value;
            saveStateDebounced();
        });
    }

    // Restaurer les valeurs sauvegardées des sélecteurs / textarea
    if (saved) {
        const gp = document.getElementById('global-prompt');
        if (gp && saved.globalPrompt) gp.value = saved.globalPrompt;
        const vs = document.getElementById('voice-style');
        if (vs && saved.voiceStyle) vs.value = saved.voiceStyle;
        const is = document.getElementById('intensity-select');
        if (is && saved.intensity) is.value = saved.intensity;
        const ds = document.getElementById('duration-select');
        if (ds) ds.value = String(state.durationFrames);
    }

    // Bouton Enregistrer la clé
    const saveBtn = document.getElementById('api-save-btn');
    if (saveBtn) saveBtn.addEventListener('click', saveApiKey);

    // Bouton Arrêter
    const stopBtn = document.getElementById('stop-btn');
    if (stopBtn) stopBtn.addEventListener('click', stopGeneration);

    // Clé API — Entrée
    const apiInput = document.getElementById('api-key-input');
    if (apiInput) {
        apiInput.addEventListener('keydown', e => {
            if (e.key === 'Enter') { e.preventDefault(); saveApiKey(); }
        });
    }

    // Sections repliables (boutons accessibles)
    document.querySelectorAll('[data-toggle]').forEach(header => {
        header.addEventListener('click', () => {
            const target = document.getElementById(header.dataset.toggle);
            if (!target) return;
            const open = target.classList.toggle('open');
            header.setAttribute('aria-expanded', open ? 'true' : 'false');
        });
    });

    // Upload
    const uploadZone = document.getElementById('upload-zone');
    const fileInput = document.getElementById('file-input');
    if (uploadZone && fileInput) {
        uploadZone.addEventListener('click', () => fileInput.click());
        fileInput.addEventListener('change', e => {
            handleFiles(e.target.files);
            fileInput.value = '';
        });
    }

    // Ajouter scène
    const addSceneBtn = document.getElementById('add-scene-btn');
    if (addSceneBtn) addSceneBtn.addEventListener('click', () => addScene());

    // Sélecteur durée — synchronisation cohérente frames ↔ secondes
    const durationSelect = document.getElementById('duration-select');
    if (durationSelect) {
        durationSelect.addEventListener('change', e => {
            const val = parseInt(e.target.value, 10);
            state.durationFrames = val;
            state.selectedDurationSec = val / FRAME_RATE;
            updateDuration();
            saveStateDebounced();
        });
    }

    // Sauvegarde auto sur les champs globaux
    const gp = document.getElementById('global-prompt');
    if (gp) gp.addEventListener('input', saveStateDebounced);
    const vs = document.getElementById('voice-style');
    if (vs) vs.addEventListener('change', saveStateDebounced);
    const is = document.getElementById('intensity-select');
    if (is) is.addEventListener('change', saveStateDebounced);

    // Bouton Générer
    const genBtn = document.getElementById('generate-btn');
    if (genBtn) genBtn.addEventListener('click', startGeneration);

    // Sauvegarde à la fermeture
    window.addEventListener('beforeunload', () => { saveState(); });

    // Rendu initial
    updateApiPanel();
    renderCharacters();
    renderScenes();
    updateDuration();
    updateGenerateBtn();

    // Message si scènes restaurées mais personnages non (images non persistées)
    if (saved && saved.scenes && saved.scenes.length > 0 && state.characters.length === 0) {
        setTimeout(() => {
            showToast('Scènes restaurées — rechargez vos personnages (images non sauvegardées)', 'warn', 5000);
        }, 400);
    }

    log('Studio prêt.');
})();
</script>

</body>
</html># Yoyoyo
