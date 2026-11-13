<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
  <title>Flight Command — Arcade Space Combat</title>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      user-select: none;
      -webkit-user-select: none;
    }

    body, html {
      width: 100%;
      height: 100%;
      background-color: #05070d;
      color: #e0f2fe;
      font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
      overflow: hidden;
    }

    #game-container {
      position: relative;
      width: 100vw;
      height: 100vh;
    }

    canvas#gameCanvas {
      display: block;
      width: 100%;
      height: 100%;
      background: radial-gradient(circle at center, #0b132b 0%, #03050a 100%);
    }

    .hidden {
      display: none !important;
    }

    .overlay {
      position: absolute;
      inset: 0;
      background: rgba(3, 7, 18, 0.82);
      backdrop-filter: blur(6px);
      display: flex;
      align-items: center;
      justify-content: center;
      z-index: 10;
    }

    .panel {
      background: rgba(15, 23, 42, 0.9);
      border: 1px solid #38bdf8;
      box-shadow: 0 0 25px rgba(56, 189, 248, 0.25);
      border-radius: 12px;
      padding: 2rem 2.5rem;
      text-align: center;
      max-width: 420px;
      width: 90%;
    }

    .title {
      font-size: 2rem;
      letter-spacing: 3px;
      color: #38bdf8;
      text-shadow: 0 0 12px rgba(56, 189, 248, 0.6);
      margin-bottom: 0.25rem;
    }

    .subtitle {
      font-size: 0.75rem;
      letter-spacing: 1.5px;
      color: #94a3b8;
      margin-bottom: 2rem;
    }

    .ui-btn {
      display: block;
      width: 100%;
      padding: 0.85rem 1.2rem;
      margin-bottom: 0.85rem;
      border: none;
      border-radius: 6px;
      font-size: 0.95rem;
      font-weight: 700;
      letter-spacing: 1px;
      cursor: pointer;
      transition: transform 0.1s ease, box-shadow 0.2s ease;
    }

    .ui-btn:active {
      transform: scale(0.97);
    }

    .ui-btn.primary {
      background: #0284c7;
      color: #ffffff;
      box-shadow: 0 0 15px rgba(2, 132, 199, 0.5);
    }

    .ui-btn.primary:hover {
      background: #0369a1;
    }

    .ui-btn.secondary {
      background: transparent;
      color: #38bdf8;
      border: 1px solid #38bdf8;
    }

    .ui-btn.small {
      width: auto;
      padding: 0.4rem 0.8rem;
      margin: 0;
      font-size: 0.75rem;
      background: rgba(15, 23, 42, 0.8);
      color: #38bdf8;
      border: 1px solid #38bdf8;
    }

    .status-text {
      font-size: 0.8rem;
      color: #94a3b8;
      margin-top: 0.5rem;
    }

    #hud {
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      padding: 1rem 1.5rem;
      z-index: 5;
      pointer-events: none;
    }

    .hud-top {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .hud-top button {
      pointer-events: auto;
    }

    .hud-item {
      font-weight: 700;
      font-size: 0.9rem;
      letter-spacing: 1px;
      color: #e0f2fe;
      text-shadow: 0 2px 4px rgba(0, 0, 0, 0.8);
    }
  </style>
</head>
<body>
  <div id="game-container">
    <canvas id="gameCanvas"></canvas>

    <!-- HUD Overlay -->
    <div id="hud" class="hidden">
      <div class="hud-top">
        <div class="hud-item">SCORE: <span id="hud-score">0</span></div>
        <div class="hud-item">INPUT: <span id="hud-input-mode">KEYBOARD/TOUCH</span></div>
        <button id="btn-pause" class="ui-btn small">PAUSE</button>
      </div>
    </div>

    <!-- Main Menu Overlay -->
    <div id="menu-overlay" class="overlay">
      <div class="panel">
        <h1 class="title">FLIGHT COMMAND</h1>
        <p class="subtitle">MILESTONE 1: CORE ENGINE FOUNDATION</p>
        
        <div class="control-settings">
          <button id="btn-start" class="ui-btn primary">LAUNCH MISSION</button>
          <button id="btn-webcam-toggle" class="ui-btn secondary">ENABLE WEBCAM TRACKING</button>
          <p id="webcam-status" class="status-text">Webcam: Disabled (Consent Required)</p>
        </div>
      </div>
    </div>

    <!-- Pause Overlay -->
    <div id="pause-overlay" class="overlay hidden">
      <div class="panel">
        <h2>SYSTEM PAUSED</h2>
        <button id="btn-resume" class="ui-btn primary">RESUME</button>
        <button id="btn-restart" class="ui-btn secondary">ABORT & RESTART</button>
      </div>
    </div>

    <!-- Hidden Webcam Processing Elements -->
    <video id="webcam-video" autoplay playsinline muted class="hidden"></video>
    <canvas id="webcam-canvas" width="64" height="48" class="hidden"></canvas>
  </div>

  <script type="module">
    class InputManager {
      constructor(canvas) {
        this.canvas = canvas;
        this.moveX = 0;
        this.moveY = 0;
        this.isFiring = false;
        this.keys = {};
        this.pointerActive = false;
        this.pointerTarget = { x: null, y: null };

        this.webcamEnabled = false;
        this.webcamStream = null;
        this.videoEl = document.getElementById('webcam-video');
        this.procCanvas = document.getElementById('webcam-canvas');
        this.procCtx = this.procCanvas.getContext('2d', { willReadFrequently: true });
        this.prevFrame = null;

        this.webcamSensitivity = 2.2;
        this.webcamDeadZone = 0.08;
        this.webcamSmoothing = 0.25;
        this.smoothedCamX = 0;
        this.smoothedCamY = 0;

        this._bindEvents();
      }

      _bindEvents() {
        window.addEventListener('keydown', (e) => {
          this.keys[e.code] = true;
          if (e.code === 'Space') this.isFiring = true;
        });

        window.addEventListener('keyup', (e) => {
          this.keys[e.code] = false;
          if (e.code === 'Space') this.isFiring = false;
        });

        this.canvas.addEventListener('pointerdown', (e) => {
          this.pointerActive = true;
          this.isFiring = true;
          this._updatePointerPosition(e);
        });

        window.addEventListener('pointermove', (e) => {
          if (!this.pointerActive) return;
          this._updatePointerPosition(e);
        });

        window.addEventListener('pointerup', () => {
          this.pointerActive = false;
          this.isFiring = false;
          this.pointerTarget = { x: null, y: null };
        });
      }

      _updatePointerPosition(e) {
        const rect = this.canvas.getBoundingClientRect();
        this.pointerTarget.x = e.clientX - rect.left;
        this.pointerTarget.y = e.clientY - rect.top;
      }

      async enableWebcam() {
        if (!navigator.mediaDevices || !navigator.mediaDevices.getUserMedia) {
          throw new Error('Webcam API not supported in this browser.');
        }

        this.webcamStream = await navigator.mediaDevices.getUserMedia({
          video: { width: 160, height: 120, facingMode: 'user' },
          audio: false
        });

        this.videoEl.srcObject = this.webcamStream;
        await this.videoEl.play();
        this.prevFrame = null;
        this.webcamEnabled = true;
      }

      disableWebcam() {
        if (this.webcamStream) {
          this.webcamStream.getTracks().forEach((track) => track.stop());
          this.webcamStream = null;
        }
        this.webcamEnabled = false;
        this.prevFrame = null;
        this.smoothedCamX = 0;
        this.smoothedCamY = 0;
      }

      _processWebcamMotion() {
        if (!this.webcamEnabled || this.videoEl.readyState < 2) return;

        const w = this.procCanvas.width;
        const h = this.procCanvas.height;

        this.procCtx.save();
        this.procCtx.scale(-1, 1);
        this.procCtx.drawImage(this.videoEl, -w, 0, w, h);
        this.procCtx.restore();

        const frame = this.procCtx.getImageData(0, 0, w, h).data;

        if (!this.prevFrame) {
          this.prevFrame = new Uint8ClampedArray(frame);
          return;
        }

        let sumX = 0;
        let sumY = 0;
        let motionWeight = 0;

        for (let y = 0; y < h; y++) {
          for (let x = 0; x < w; x++) {
            const i = (y * w + x) * 4;
            const diff =
              Math.abs(frame[i] - this.prevFrame[i]) +
              Math.abs(frame[i + 1] - this.prevFrame[i + 1]) +
              Math.abs(frame[i + 2] - this.prevFrame[i + 2]);

            if (diff > 65) {
              sumX += (x / w) * 2 - 1;
              sumY += (y / h) * 2 - 1;
              motionWeight++;
            }
          }
        }

        this.prevFrame.set(frame);

        if (motionWeight > 12) {
          let rawX = (sumX / motionWeight) * this.webcamSensitivity;
          let rawY = (sumY / motionWeight) * this.webcamSensitivity;

          rawX = Math.abs(rawX) < this.webcamDeadZone ? 0 : Math.max(-1, Math.min(1, rawX));
          rawY = Math.abs(rawY) < this.webcamDeadZone ? 0 : Math.max(-1, Math.min(1, rawY));

          this.smoothedCamX += (rawX - this.smoothedCamX) * this.webcamSmoothing;
          this.smoothedCamY += (rawY - this.smoothedCamY) * this.webcamSmoothing;
        } else {
          this.smoothedCamX *= 0.85;
          this.smoothedCamY *= 0.85;
        }
      }

      update(playerEntity) {
        let kx = 0;
        let ky = 0;

        if (this.keys['ArrowLeft'] || this.keys['KeyA']) kx -= 1;
        if (this.keys['ArrowRight'] || this.keys['KeyD']) kx += 1;
        if (this.keys['ArrowUp'] || this.keys['KeyW']) ky -= 1;
        if (this.keys['ArrowDown'] || this.keys['KeyS']) ky += 1;

        if (kx !== 0 && ky !== 0) {
          const inv = 1 / Math.SQRT2;
          kx *= inv;
          ky *= inv;
        }

        if (this.webcamEnabled) {
          this._processWebcamMotion();
          this.moveX = kx !== 0 ? kx : this.smoothedCamX;
          this.moveY = ky !== 0 ? ky : this.smoothedCamY;
          this.isFiring = Boolean(this.keys['Space'] || this.pointerActive || true);
        } else if (this.pointerActive && this.pointerTarget.x !== null && playerEntity) {
          const dx = this.pointerTarget.x - playerEntity.x;
          const dy = this.pointerTarget.y - playerEntity.y;
          const dist = Math.hypot(dx, dy);
          if (dist > 6) {
            this.moveX = Math.max(-1, Math.min(1, dx / 40));
            this.moveY = Math.max(-1, Math.min(1, dy / 40));
          } else {
            this.moveX = 0;
            this.moveY = 0;
          }
        } else {
          this.moveX = kx;
          this.moveY = ky;
        }
      }
    }

    class EntityManager {
      constructor(width, height) {
        this.width = width;
        this.height = height;
        this.reset();
      }

      reset() {
        this.player = {
          x: this.width / 2,
          y: this.height * 0.82,
          radius: 18,
          speed: 440,
          fireCooldown: 0,
          fireRate: 0.16,
          hp: 100,
          maxHp: 100
        };

        this.projectiles = [];
        this.enemies = [];
        this.enemySpawnTimer = 0;
        this.score = 0;
      }

      resize(width, height) {
        this.width = width;
        this.height = height;
        if (this.player) {
          this.player.x = Math.max(24, Math.min(this.width - 24, this.player.x));
          this.player.y = Math.max(24, Math.min(this.height - 24, this.player.y));
        }
      }

      update(dt, input) {
        const p = this.player;

        p.x += input.moveX * p.speed * dt;
        p.y += input.moveY * p.speed * dt;

        p.x = Math.max(p.radius + 8, Math.min(this.width - p.radius - 8, p.x));
        p.y = Math.max(p.radius + 8, Math.min(this.height - p.radius - 8, p.y));

        p.fireCooldown = Math.max(0, p.fireCooldown - dt);
        if (input.isFiring && p.fireCooldown === 0) {
          this.projectiles.push({
            x: p.x,
            y: p.y - p.radius,
            vy: -780,
            radius: 4,
            fromPlayer: true
          });
          p.fireCooldown = p.fireRate;
        }

        for (let i = this.projectiles.length - 1; i >= 0; i--) {
          const proj = this.projectiles[i];
          proj.y += proj.vy * dt;
          if (proj.y < -20 || proj.y > this.height + 20) {
            this.projectiles.splice(i, 1);
          }
        }

        this.enemySpawnTimer -= dt;
        if (this.enemySpawnTimer <= 0) {
          this.enemies.push({
            x: 32 + Math.random() * (this.width - 64),
            y: -24,
            vy: 150 + Math.random() * 90,
            radius: 16,
            hp: 1
          });
          this.enemySpawnTimer = 0.95;
        }

        for (let i = this.enemies.length - 1; i >= 0; i--) {
          const enemy = this.enemies[i];
          enemy.y += enemy.vy * dt;

          if (enemy.y > this.height + 30) {
            this.enemies.splice(i, 1);
            continue;
          }

          for (let j = this.projectiles.length - 1; j >= 0; j--) {
            const proj = this.projectiles[j];
            if (!proj.fromPlayer) continue;

            const dist = Math.hypot(proj.x - enemy.x, proj.y - enemy.y);
            if (dist < proj.radius + enemy.radius) {
              this.projectiles.splice(j, 1);
              enemy.hp -= 1;
              if (enemy.hp <= 0) {
                this.enemies.splice(i, 1);
                this.score += 100;
              }
              break;
            }
          }
        }
      }

      render(ctx) {
        ctx.fillStyle = '#38bdf8';
        ctx.shadowColor = '#38bdf8';
        ctx.shadowBlur = 10;
        for (const proj of this.projectiles) {
          ctx.beginPath();
          ctx.roundRect(proj.x - 2, proj.y - 10, 4, 18, 2);
          ctx.fill();
        }

        ctx.fillStyle = '#f43f5e';
        ctx.shadowColor = '#f43f5e';
        ctx.shadowBlur = 12;
        for (const enemy of this.enemies) {
          ctx.beginPath();
          ctx.moveTo(enemy.x, enemy.y + enemy.radius);
          ctx.lineTo(enemy.x - enemy.radius, enemy.y - enemy.radius);
          ctx.lineTo(enemy.x + enemy.radius, enemy.y - enemy.radius);
          ctx.closePath();
          ctx.fill();
        }

        const p = this.player;
        ctx.save();
        ctx.translate(p.x, p.y);
        ctx.fillStyle = '#e0f2fe';
        ctx.shadowColor = '#0ea5e9';
        ctx.shadowBlur = 16;

        ctx.beginPath();
        ctx.moveTo(0, -22);
        ctx.lineTo(18, 16);
        ctx.lineTo(6, 10);
        ctx.lineTo(0, 18);
        ctx.lineTo(-6, 10);
        ctx.lineTo(-18, 16);
        ctx.closePath();
        ctx.fill();
        ctx.restore();

        ctx.shadowBlur = 0;
      }
    }

    class GameEngine {
      constructor(canvas) {
        this.canvas = canvas;
        this.ctx = canvas.getContext('2d');
        this.state = 'MENU';

        this.lastTimestamp = 0;
        this.rafId = null;

        this._handleResize();
        this.input = new InputManager(this.canvas);
        this.entities = new EntityManager(this.width, this.height);

        window.addEventListener('resize', () => this._handleResize());
      }

      _handleResize() {
        const dpr = Math.min(window.devicePixelRatio || 1, 2);
        this.width = window.innerWidth;
        this.height = window.innerHeight;

        this.canvas.width = this.width * dpr;
        this.canvas.height = this.height * dpr;
        this.ctx.setTransform(dpr, 0, 0, dpr, 0, 0);

        if (this.entities) {
          this.entities.resize(this.width, this.height);
        }
      }

      start() {
        this.entities.reset();
        this.state = 'PLAYING';
        this.lastTimestamp = performance.now();
        this._loop(this.lastTimestamp);
      }

      pause() {
        if (this.state === 'PLAYING') {
          this.state = 'PAUSED';
        }
      }

      resume() {
        if (this.state === 'PAUSED') {
          this.state = 'PLAYING';
          this.lastTimestamp = performance.now();
          this._loop(this.lastTimestamp);
        }
      }

      _loop(timestamp) {
        if (this.state !== 'PLAYING') return;

        const dt = Math.min((timestamp - this.lastTimestamp) / 1000, 0.05);
        this.lastTimestamp = timestamp;

        this.update(dt);
        this.render();

        this.rafId = requestAnimationFrame((ts) => this._loop(ts));
      }

      update(dt) {
        this.input.update(this.entities.player);
        this.entities.update(dt, this.input);

        const scoreEl = document.getElementById('hud-score');
        if (scoreEl) scoreEl.textContent = this.entities.score;
      }

      render() {
        this.ctx.clearRect(0, 0, this.width, this.height);
        this.entities.render(this.ctx);
      }
    }

    // Main Initiation
    const canvas = document.getElementById('gameCanvas');
    const engine = new GameEngine(canvas);

    const menuOverlay = document.getElementById('menu-overlay');
    const pauseOverlay = document.getElementById('pause-overlay');
    const hud = document.getElementById('hud');
    const webcamStatus = document.getElementById('webcam-status');
    const hudInputMode = document.getElementById('hud-input-mode');

    const btnStart = document.getElementById('btn-start');
    const btnWebcamToggle = document.getElementById('btn-webcam-toggle');
    const btnPause = document.getElementById('btn-pause');
    const btnResume = document.getElementById('btn-resume');
    const btnRestart = document.getElementById('btn-restart');

    btnStart.addEventListener('click', () => {
      menuOverlay.classList.add('hidden');
      hud.classList.remove('hidden');
      engine.start();
    });

    btnWebcamToggle.addEventListener('click', async () => {
      if (!engine.input.webcamEnabled) {
        webcamStatus.textContent = 'Webcam: Requesting permission...';
        try {
          await engine.input.enableWebcam();
          btnWebcamToggle.textContent = 'DISABLE WEBCAM TRACKING';
          webcamStatus.textContent = 'Webcam: Active (Calibrated & Ready)';
          hudInputMode.textContent = 'WEBCAM + KEYBOARD';
        } catch (err) {
          webcamStatus.textContent = `Webcam Unavailable: ${err.message}`;
          hudInputMode.textContent = 'KEYBOARD/TOUCH';
        }
      } else {
        engine.input.disableWebcam();
        btnWebcamToggle.textContent = 'ENABLE WEBCAM TRACKING';
        webcamStatus.textContent = 'Webcam: Disabled';
        hudInputMode.textContent = 'KEYBOARD/TOUCH';
      }
    });

    btnPause.addEventListener('click', () => {
      engine.pause();
      pauseOverlay.classList.remove('hidden');
    });

    btnResume.addEventListener('click', () => {
      pauseOverlay.classList.add('hidden');
      engine.resume();
    });

    btnRestart.addEventListener('click', () => {
      pauseOverlay.classList.add('hidden');
      engine.start();
    });
  </script>
</body>
</html>
