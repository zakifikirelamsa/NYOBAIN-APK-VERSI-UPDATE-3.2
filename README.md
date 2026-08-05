# NYOBAIN-APK-VERSI-UPDATE-3.2
versi 3.2
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>⚠️ PERINGATAN!</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background-color: #000;
            font-family: 'Courier New', Courier, monospace;
            overflow: hidden;
            height: 100vh;
        }

        /* ===== LOADING SCREEN ===== */
        #loadingScreen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 9999;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            transition: opacity 0.8s ease, visibility 0.8s ease;
            background: #0a0a0a;
        }

        #loadingScreen.hide {
            opacity: 0;
            visibility: hidden;
            pointer-events: none;
        }

        #loadingVideo {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            object-fit: cover;
            opacity: 0.3;
            z-index: 0;
        }

        .loader-content {
            position: relative;
            z-index: 1;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .loader-skull {
            font-size: 80px;
            animation: spinSkull 1.5s linear infinite;
            filter: drop-shadow(0 0 30px rgba(255, 255, 255, 0.3));
        }

        @keyframes spinSkull {
            0% { transform: rotate(0deg) scale(1); }
            50% { transform: rotate(180deg) scale(1.1); filter: drop-shadow(0 0 50px rgba(255, 255, 255, 0.8)); }
            100% { transform: rotate(360deg) scale(1); }
        }

        .loader-text {
            color: #fff;
            font-size: 14px;
            letter-spacing: 3px;
            margin-top: 20px;
            opacity: 0.7;
            animation: blinkText 1s infinite alternate;
        }

        .progress-wrapper {
            width: 300px;
            margin-top: 20px;
        }

        .progress-bar-bg {
            width: 100%;
            height: 6px;
            background: #1a1a1a;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: inset 0 0 10px rgba(255,255,255,0.05);
        }

        .progress-bar-fill {
            width: 0%;
            height: 100%;
            background: linear-gradient(90deg, #ff0000, #ff6600, #ffcc00);
            border-radius: 10px;
            transition: width 0.1s linear;
            box-shadow: 0 0 20px rgba(255, 0, 0, 0.5);
            animation: glowProgress 0.5s infinite alternate;
        }

        @keyframes glowProgress {
            0% { box-shadow: 0 0 10px rgba(255, 0, 0, 0.3); }
            100% { box-shadow: 0 0 30px rgba(255, 100, 0, 0.8); }
        }

        .progress-text {
            color: #888;
            font-size: 12px;
            text-align: right;
            margin-top: 5px;
            letter-spacing: 1px;
        }

        .progress-text span {
            color: #fff;
            font-weight: bold;
        }

        /* ===== MAIN CONTENT ===== */
        #mainContent {
            display: none;
            position: relative;
            width: 100vw;
            height: 100vh;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            gap: 15px;
            padding: 20px;
        }

        #mainContent.show {
            display: flex;
            animation: fadeIn 1s ease;
        }

        @keyframes fadeIn {
            0% { opacity: 0; transform: scale(0.9); }
            100% { opacity: 1; transform: scale(1); }
        }

        #bgVideo {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            object-fit: cover;
            z-index: 0;
            opacity: 0.4;
        }

        /* ===== EFEK API & BINTANG ===== */
        #fireEffect {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 0;
            pointer-events: none;
            display: none;
        }

        #fireEffect.active {
            display: block;
        }

        .container {
            position: relative;
            z-index: 1;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 12px;
            width: 100%;
            max-width: 500px;
        }

        .glitch-box {
            position: relative;
            filter: drop-shadow(0 0 15px rgba(255, 255, 255, 0.8)) 
                    drop-shadow(0 0 30px rgba(255, 255, 255, 0.4));
            animation: pulse 1.5s infinite alternate ease-in-out;
        }

        @keyframes pulse {
            0% { transform: scale(0.98); filter: drop-shadow(0 0 10px rgba(255, 255, 255, 0.6)); }
            100% { transform: scale(1.02); filter: drop-shadow(0 0 25px rgba(255, 255, 255, 1)); }
        }

        canvas#skullCanvas {
            display: block;
            cursor: pointer;
            width: 200px;
            height: auto;
        }

        .warning-text {
            text-align: center;
            animation: blinkText 0.8s infinite alternate;
        }

        .warning-text h1 {
            color: #ff0000;
            font-size: 28px;
            font-weight: 900;
            text-shadow: 0 0 20px rgba(255, 0, 0, 0.8), 0 0 60px rgba(255, 0, 0, 0.4);
            letter-spacing: 4px;
        }

        .warning-text p {
            color: #fff;
            font-size: 11px;
            margin-top: 5px;
            letter-spacing: 2px;
            opacity: 0.8;
        }

        @keyframes blinkText {
            0% { opacity: 0.6; }
            100% { opacity: 1; }
        }

        /* ===== FORM PESAN ===== */
        .message-box {
            background: rgba(0, 0, 0, 0.85);
            border: 1px solid rgba(255, 255, 255, 0.15);
            border-radius: 10px;
            padding: 15px;
            width: 100%;
            backdrop-filter: blur(10px);
        }

        .message-box label {
            color: #fff;
            font-size: 11px;
            letter-spacing: 1px;
            display: block;
            margin-bottom: 4px;
        }

        /* ===== INPUT NOMOR ===== */
        .nomor-input-group {
            display: flex;
            gap: 8px;
            margin-bottom: 12px;
        }

        .nomor-input-group input {
            flex: 1;
            padding: 10px 12px;
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 5px;
            color: #00ff88;
            font-size: 14px;
            font-family: inherit;
            letter-spacing: 1px;
        }

        .nomor-input-group input:focus {
            outline: none;
            border-color: #00ff88;
            box-shadow: 0 0 20px rgba(0, 255, 136, 0.1);
        }

        .nomor-input-group input::placeholder {
            color: #555;
            font-size: 12px;
        }

        .nomor-input-group .btn-set {
            padding: 10px 20px;
            background: #00ff88;
            color: #000;
            border: none;
            border-radius: 5px;
            font-weight: bold;
            cursor: pointer;
            font-size: 12px;
            transition: 0.3s;
            white-space: nowrap;
        }

        .nomor-input-group .btn-set:hover {
            box-shadow: 0 0 30px rgba(0, 255, 136, 0.4);
            transform: scale(1.05);
        }

        .nomor-display {
            color: #00ff88;
            font-size: 18px;
            font-weight: bold;
            text-align: center;
            padding: 8px;
            background: rgba(0, 255, 136, 0.08);
            border-radius: 5px;
            margin-bottom: 12px;
            border: 1px solid rgba(0, 255, 136, 0.2);
            cursor: pointer;
            transition: 0.3s;
            word-break: break-all;
        }

        .nomor-display:hover {
            background: rgba(0, 255, 136, 0.15);
            box-shadow: 0 0 20px rgba(0, 255, 136, 0.1);
        }

        .message-box textarea {
            width: 100%;
            height: 80px;
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 5px;
            color: #fff;
            padding: 10px;
            font-size: 13px;
            resize: none;
            font-family: inherit;
        }

        .message-box textarea:focus {
            outline: none;
            border-color: #00ff88;
            box-shadow: 0 0 20px rgba(0, 255, 136, 0.1);
        }

        .message-box .char-count {
            color: #888;
            font-size: 10px;
            text-align: right;
            margin-top: 3px;
        }

        .message-box .char-count span {
            color: #fff;
        }

        .message-box .char-count.danger span {
            color: #ff0000;
        }

        .btn-group {
            display: flex;
            gap: 8px;
            margin-top: 12px;
            flex-wrap: wrap;
            justify-content: center;
        }

        .btn-group button {
            padding: 8px 16px;
            font-size: 11px;
            font-weight: bold;
            letter-spacing: 1px;
            text-transform: uppercase;
            border: 2px solid #fff;
            background: transparent;
            color: #fff;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 0 15px rgba(255, 255, 255, 0.1);
            border-radius: 5px;
            flex: 1;
            min-width: 80px;
        }

        .btn-random {
            border-color: #ff8800;
            color: #ff8800;
        }

        .btn-random:hover {
            background: #ff8800;
            color: #000;
            box-shadow: 0 0 30px rgba(255, 136, 0, 0.6);
            transform: scale(1.05);
        }

        .btn-kirim {
            border-color: #00ff88;
            color: #00ff88;
        }

        .btn-kirim:hover {
            background: #00ff88;
            color: #000;
            box-shadow: 0 0 30px rgba(0, 255, 136, 0.6);
            transform: scale(1.05);
        }

        .btn-kirim:disabled {
            opacity: 0.3;
            cursor: not-allowed;
            transform: none !important;
        }

        .btn-keluar {
            border-color: #ff0033;
            color: #ff0033;
        }

        .btn-keluar:hover {
            background: #ff0033;
            color: #fff;
            box-shadow: 0 0 30px rgba(255, 0, 51, 0.6);
            transform: scale(1.05);
        }

        .status-text {
            color: #888;
            font-size: 10px;
            margin-top: 5px;
            letter-spacing: 1px;
            text-align: center;
        }

        .status-text.success {
            color: #00ff88;
        }

        .status-text.error {
            color: #ff0033;
        }

        .glitch-trigger {
            color: #555;
            font-size: 9px;
            letter-spacing: 1px;
            opacity: 0.5;
        }

        /* ===== RESPONSIVE ===== */
        @media (max-width: 480px) {
            .warning-text h1 { font-size: 22px; }
            canvas#skullCanvas { width: 150px; }
            .nomor-input-group { flex-direction: column; }
            .nomor-input-group .btn-set { width: 100%; }
            .nomor-display { font-size: 15px; }
            .btn-group button { font-size: 10px; padding: 8px 12px; }
        }
    </style>
</head>
<body>

    <!-- ===== LOADING SCREEN ===== -->
    <div id="loadingScreen">
        <video id="loadingVideo" autoplay muted loop>
            <source src="https://cdn.coverr.co/videos/coverr-typing-on-laptop-1572/1080p.mp4" type="video/mp4">
        </video>
        <div class="loader-content">
            <div class="loader-skull">💀</div>
            <div class="loader-text">⚡ MEMUAT SISTEM ⚡</div>
            <div class="progress-wrapper">
                <div class="progress-bar-bg">
                    <div class="progress-bar-fill" id="progressFill"></div>
                </div>
                <div class="progress-text">
                    <span id="progressPercent">0</span>%
                </div>
            </div>
        </div>
    </div>

    <!-- ===== MAIN CONTENT ===== -->
    <div id="mainContent">
        <video id="bgVideo" autoplay muted loop>
            <source src="https://cdn.coverr.co/videos/coverr-typing-on-laptop-1572/1080p.mp4" type="video/mp4">
        </video>

        <div id="fireEffect">
            <canvas id="fireCanvas"></canvas>
        </div>

        <div class="container">
            <div class="glitch-box" id="glitchBox">
                <canvas id="skullCanvas" width="400" height="500"></canvas>
            </div>

            <div class="warning-text">
                <h1>⚠️ PERINGATAN!!!</h1>
                <p>SEBELUM MEMAKAI APLIKASI, WAJIB BACA TERLEBIH DAHULU!</p>
            </div>

            <!-- ===== FORM PESAN ===== -->
            <div class="message-box">
                <label>📱 NOMOR WHATSAPP TUJUAN:</label>
                
                <!-- Input Manual Nomor -->
                <div class="nomor-input-group">
                    <input type="text" id="nomorInput" placeholder="Contoh: 6281234567890 atau 081234567890">
                    <button class="btn-set" onclick="setNomorManual()">SET</button>
                </div>

                <!-- Display Nomor Aktif -->
                <div class="nomor-display" id="nomorDisplay" onclick="copyNomor()">
                    +62 812-3456-7890
                </div>

                <label>💬 PESAN (maks 200 karakter):</label>
                <textarea id="pesanInput" placeholder="Tulis pesanmu di sini..." maxlength="200"></textarea>
                <div class="char-count" id="charCount">
                    <span id="charCountNum">0</span> / 200 karakter
                </div>

                <div class="btn-group">
                    <button class="btn-random" onclick="randomNomor()">🎲 RANDOM</button>
                    <button class="btn-kirim" id="btnKirim" onclick="kirimPesan()">📤 KIRIM</button>
                    <button class="btn-keluar" onclick="keluar()">❌ KELUAR</button>
                </div>

                <div class="status-text" id="statusText">Klik Random atau masukkan nomor sendiri</div>
            </div>

            <div class="glitch-trigger">✦ efek glitch otomatis setiap 5 detik ✦</div>
        </div>
    </div>

    <script>
        // ===== VARIABEL GLOBAL =====
        let currentNomor = '+62 812-3456-7890';
        let isFireActive = false;

        // ===== LOADING PROGRESS =====
        let progress = 0;
        const progressFill = document.getElementById('progressFill');
        const progressPercent = document.getElementById('progressPercent');
        const loadingScreen = document.getElementById('loadingScreen');
        const mainContent = document.getElementById('mainContent');

        // ===== PLAY SUARA =====
        function playBeepSound() {
            try {
                const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
                const oscillator = audioCtx.createOscillator();
                const gainNode = audioCtx.createGain();
                oscillator.connect(gainNode);
                gainNode.connect(audioCtx.destination);
                oscillator.type = 'sine';
                oscillator.frequency.value = 880;
                gainNode.gain.value = 0.3;
                oscillator.start();
                oscillator.stop(audioCtx.currentTime + 0.3);
                setTimeout(() => {
                    const osc2 = audioCtx.createOscillator();
                    const gain2 = audioCtx.createGain();
                    osc2.connect(gain2);
                    gain2.connect(audioCtx.destination);
                    osc2.type = 'sine';
                    osc2.frequency.value = 1100;
                    gain2.gain.value = 0.2;
                    osc2.start();
                    osc2.stop(audioCtx.currentTime + 0.2);
                }, 300);
            } catch (e) {}
        }

        function playErrorSound() {
            try {
                const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
                const oscillator = audioCtx.createOscillator();
                const gainNode = audioCtx.createGain();
                oscillator.connect(gainNode);
                gainNode.connect(audioCtx.destination);
                oscillator.type = 'sawtooth';
                oscillator.frequency.value = 200;
                gainNode.gain.value = 0.2;
                oscillator.start();
                oscillator.stop(audioCtx.currentTime + 0.5);
            } catch (e) {}
        }

        function playSuccessSound() {
            try {
                const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
                const notes = [523, 659, 784];
                notes.forEach((freq, i) => {
                    setTimeout(() => {
                        const osc = audioCtx.createOscillator();
                        const gain = audioCtx.createGain();
                        osc.connect(gain);
                        gain.connect(audioCtx.destination);
                        osc.type = 'sine';
                        osc.frequency.value = freq;
                        gain.gain.value = 0.15;
                        osc.start();
                        osc.stop(audioCtx.currentTime + 0.15);
                    }, i * 150);
                });
            } catch (e) {}
        }

        function simulateLoading() {
            const interval = setInterval(() => {
                const increment = Math.floor(Math.random() * 4) + 2;
                progress = Math.min(progress + increment, 100);
                progressFill.style.width = progress + '%';
                progressPercent.textContent = progress;
                if (progress >= 100) {
                    clearInterval(interval);
                    playBeepSound();
                    setTimeout(() => {
                        loadingScreen.classList.add('hide');
                        mainContent.classList.add('show');
                        initFireCanvas();
                        setTimeout(triggerGlitch, 500);
                    }, 500);
                }
            }, 120);
        }

        window.addEventListener('load', () => {
            setTimeout(simulateLoading, 500);
        });

        // ===== GAMBAR SKULL =====
        const canvas = document.getElementById('skullCanvas');
        const ctx = canvas.getContext('2d');
        const glitchBox = document.getElementById('glitchBox');

        function drawSkull() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            ctx.save();
            ctx.strokeStyle = '#ffffff';
            ctx.fillStyle = '#ffffff';
            ctx.lineWidth = 4;
            ctx.lineJoin = 'round';
            ctx.shadowColor = '#ffffff';
            ctx.shadowBlur = 15;
            const cx = canvas.width / 2;
            const cy = canvas.height / 2 + 20;
            ctx.beginPath();
            ctx.moveTo(cx - 40, cy - 50);
            ctx.bezierCurveTo(cx - 70, cy - 120, cx - 80, cy - 180, cx - 50, cy - 220);
            ctx.bezierCurveTo(cx - 30, cy - 170, cx - 40, cy - 100, cx - 20, cy - 50);
            ctx.stroke();
            ctx.fill();
            ctx.beginPath();
            ctx.moveTo(cx + 40, cy - 50);
            ctx.bezierCurveTo(cx + 70, cy - 120, cx + 80, cy - 180, cx + 50, cy - 220);
            ctx.bezierCurveTo(cx + 30, cy - 170, cx + 40, cy - 100, cx + 20, cy - 50);
            ctx.stroke();
            ctx.fill();
            ctx.beginPath();
            ctx.arc(cx, cy - 20, 50, Math.PI * 0.85, Math.PI * 0.15, false);
            ctx.lineTo(cx + 35, cy + 30);
            ctx.lineTo(cx - 35, cy + 30);
            ctx.closePath();
            ctx.stroke();
            ctx.globalCompositeOperation = 'destination-out';
            ctx.beginPath();
            ctx.ellipse(cx - 20, cy - 15, 12, 18, Math.PI / 12, 0, Math.PI * 2);
            ctx.fill();
            ctx.beginPath();
            ctx.ellipse(cx + 20, cy - 15, 12, 18, -Math.PI / 12, 0, Math.PI * 2);
            ctx.fill();
            ctx.beginPath();
            ctx.moveTo(cx, cy + 5);
            ctx.lineTo(cx - 6, cy + 20);
            ctx.lineTo(cx + 6, cy + 20);
            ctx.closePath();
            ctx.fill();
            ctx.restore();
            ctx.save();
            ctx.fillStyle = '#ffffff';
            ctx.shadowColor = '#ffffff';
            ctx.shadowBlur = 10;
            ctx.beginPath();
            ctx.arc(cx, cy + 90, 18, 0, Math.PI * 2);
            ctx.fill();
            ctx.beginPath();
            ctx.rect(cx - 12, cy + 105, 24, 15);
            ctx.fill();
            ctx.restore();
        }

        // ===== EFEK GLITCH =====
        function triggerGlitch() {
            let count = 0;
            const interval = setInterval(() => {
                const offsetX = (Math.random() - 0.5) * 30;
                const offsetY = (Math.random() - 0.5) * 30;
                glitchBox.style.transform = `translate(${offsetX}px, ${offsetY}px) scale(${0.9 + Math.random() * 0.3})`;
                glitchBox.style.filter = Math.random() > 0.5 ? 'invert(1)' : 'none';
                count++;
                if (count > 15) {
                    clearInterval(interval);
                    glitchBox.style.transform = 'none';
                    glitchBox.style.filter = 'none';
                }
            }, 40);
        }

        setInterval(triggerGlitch, 5000);
        canvas.addEventListener('click', triggerGlitch);

        // ===== FORMAT NOMOR =====
        function formatNomor(nomor) {
            // Hapus semua karakter non-digit
            let clean = nomor.replace(/\D/g, '');
            
            // Kalau mulai dengan 0, ganti jadi 62
            if (clean.startsWith('0')) {
                clean = '62' + clean.substring(1);
            }
            
            // Kalau tidak mulai dengan 62, tambahkan 62
            if (!clean.startsWith('62')) {
                clean = '62' + clean;
            }
            
            // Format: +62 XXX-XXXX-XXXX
            if (clean.length >= 12) {
                const prefix = clean.substring(0, 3);
                const part1 = clean.substring(3, 6);
                const part2 = clean.substring(6, 10);
                const part3 = clean.substring(10, 14);
                return `+${prefix} ${part1}-${part2}-${part3}`;
            }
            
            return `+${clean}`;
        }

        function cleanNomor(nomor) {
            return nomor.replace(/\D/g, '');
        }

        // ===== SET NOMOR MANUAL =====
        function setNomorManual() {
            const input = document.getElementById('nomorInput');
            const rawNomor = input.value.trim();
            const statusText = document.getElementById('statusText');

            if (!rawNomor) {
                statusText.textContent = '⚠️ Masukkan nomor terlebih dahulu!';
                statusText.className = 'status-text error';
                playErrorSound();
                return;
            }

            // Format nomor
            const formatted = formatNomor(rawNomor);
            const clean = cleanNomor(rawNomor);

            // Validasi minimal 10 digit
            if (clean.length < 10) {
                statusText.textContent = '⚠️ Nomor terlalu pendek! Minimal 10 digit.';
                statusText.className = 'status-text error';
                playErrorSound();
                return;
            }

            currentNomor = formatted;
            document.getElementById('nomorDisplay').textContent = formatted;
            document.getElementById('nomorInput').value = formatted;
            statusText.textContent = '✅ Nomor berhasil diubah!';
            statusText.className = 'status-text success';
            document.getElementById('btnKirim').disabled = false;
            playBeepSound();
        }

        // Enter key untuk input nomor
        document.getElementById('nomorInput').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                setNomorManual();
            }
        });

        // ===== RANDOM NOMOR =====
        function randomNomor() {
            const prefix = ['812', '813', '814', '815', '816', '817', '818', '819', '811', '821', '822', '823', '852', '853'];
            const pilihPrefix = prefix[Math.floor(Math.random() * prefix.length)];
            const nomor1 = Math.floor(Math.random() * 1000).toString().padStart(3, '0');
            const nomor2 = Math.floor(Math.random() * 10000).toString().padStart(4, '0');
            
            currentNomor = `+62 ${pilihPrefix}-${nomor1}-${nomor2}`;
            document.getElementById('nomorDisplay').textContent = currentNomor;
            document.getElementById('nomorInput').value = currentNomor;
            document.getElementById('statusText').textContent = '🎲 Nomor random siap!';
            document.getElementById('statusText').className = 'status-text success';
            document.getElementById('btnKirim').disabled = false;
            playBeepSound();
        }

        function copyNomor() {
            const nomorClean = currentNomor.replace(/[^0-9]/g, '');
            if (navigator.clipboard) {
                navigator.clipboard.writeText(nomorClean).then(() => {
                    document.getElementById('statusText').textContent = '📋 Nomor disalin!';
                    document.getElementById('statusText').className = 'status-text success';
                });
            }
        }

        // ===== CHAR COUNTER =====
        const pesanInput = document.getElementById('pesanInput');
        const charCountNum = document.getElementById('charCountNum');
        const charCount = document.getElementById('charCount');

        pesanInput.addEventListener('input', function() {
            const length = this.value.length;
            charCountNum.textContent = length;
            charCount.className = length > 180 ? 'char-count danger' : 'char-count';
        });

        // ===== KIRIM PESAN =====
        function kirimPesan() {
            const pesan = pesanInput.value.trim();
            const statusText = document.getElementById('statusText');
            const btnKirim = document.getElementById('btnKirim');

            if (!currentNomor || currentNomor === '+62 812-3456-7890') {
                statusText.textContent = '⚠️ Masukkan nomor dulu! (Random atau Manual)';
                statusText.className = 'status-text error';
                playErrorSound();
                return;
            }

            if (pesan.length === 0) {
                statusText.textContent = '⚠️ Tulis pesan dulu!';
                statusText.className = 'status-text error';
                playErrorSound();
                return;
            }

            if (pesan.length > 200) {
                statusText.textContent = '⚠️ Pesan terlalu panjang! Maks 200 karakter.';
                statusText.className = 'status-text error';
                playErrorSound();
                return;
            }

            playSuccessSound();
            const nomorClean = currentNomor.replace(/[^0-9]/g, '');
            const url = `https://api.whatsapp.com/send?phone=${nomorClean}&text=${encodeURIComponent(pesan)}`;
            
            statusText.textContent = '📤 Membuka WhatsApp...';
            statusText.className = 'status-text success';
            btnKirim.disabled = true;

            activateFireEffect();
            window.open(url, '_blank');

            setTimeout(() => {
                statusText.textContent = '✅ Pesan terkirim! Klik Random atau SET untuk kirim lagi.';
                btnKirim.disabled = false;
            }, 3000);
        }

        // ===== EFEK API & BINTANG =====
        function activateFireEffect() {
            if (isFireActive) return;
            isFireActive = true;
            document.getElementById('fireEffect').classList.add('active');
            document.getElementById('bgVideo').style.opacity = '0.2';
        }

        function initFireCanvas() {
            const fireCanvas = document.getElementById('fireCanvas');
            const ctxFire = fireCanvas.getContext('2d');
            fireCanvas.width = window.innerWidth;
            fireCanvas.height = window.innerHeight;

            const particles = [];
            const stars = [];

            for (let i = 0; i < 50; i++) {
                stars.push({
                    x: Math.random() * fireCanvas.width,
                    y: Math.random() * fireCanvas.height,
                    size: Math.random() * 2 + 1,
                    speed: Math.random() * 3 + 1,
                    angle: Math.random() * Math.PI * 2,
                    life: Math.random() * 100 + 50
                });
            }

            for (let i = 0; i < 80; i++) {
                particles.push({
                    x: fireCanvas.width / 2 + (Math.random() - 0.5) * 200,
                    y: fireCanvas.height - Math.random() * 100,
                    size: Math.random() * 8 + 3,
                    speedY: Math.random() * 3 + 1,
                    speedX: (Math.random() - 0.5) * 2,
                    life: Math.random() * 80 + 40,
                    maxLife: 80,
                    color: `hsl(${Math.random() * 40 + 10}, 100%, ${Math.random() * 30 + 30}%)`
                });
            }

            function drawFire() {
                ctxFire.clearRect(0, 0, fireCanvas.width, fireCanvas.height);

                stars.forEach(star => {
                    star.x += Math.cos(star.angle) * star.speed;
                    star.y += Math.sin(star.angle) * star.speed;
                    star.life -= 0.5;
                    if (star.life <= 0) {
                        star.x = Math.random() * fireCanvas.width;
                        star.y = -20;
                        star.life = Math.random() * 100 + 50;
                        star.speed = Math.random() * 3 + 1;
                    }
                    ctxFire.beginPath();
                    ctxFire.arc(star.x, star.y, star.size, 0, Math.PI * 2);
                    ctxFire.fillStyle = `rgba(255, 255, 255, ${star.life / 150})`;
                    ctxFire.fill();
                    ctxFire.beginPath();
                    ctxFire.moveTo(star.x, star.y);
                    ctxFire.lineTo(star.x - Math.cos(star.angle) * 20, star.y - Math.sin(star.angle) * 20);
                    ctxFire.strokeStyle = `rgba(255, 255, 255, ${star.life / 200})`;
                    ctxFire.lineWidth = 1;
                    ctxFire.stroke();
                });

                particles.forEach(p => {
                    p.x += p.speedX + (Math.random() - 0.5) * 0.5;
                    p.y -= p.speedY;
                    p.life -= 1;
                    p.size *= 0.99;
                    if (p.life <= 0 || p.size < 0.5) {
                        p.x = fireCanvas.width / 2 + (Math.random() - 0.5) * 250;
                        p.y = fireCanvas.height - Math.random() * 50;
                        p.size = Math.random() * 8 + 3;
                        p.life = Math.random() * 80 + 40;
                        p.speedY = Math.random() * 3 + 1;
                        p.color = `hsl(${Math.random() * 40 + 10}, 100%, ${Math.random() * 30 + 30}%)`;
                    }
                    const gradient = ctxFire.createRadialGradient(p.x, p.y, 0, p.x, p.y, p.size * 2);
                    gradient.addColorStop(0, p.color);
                    gradient.addColorStop(1, 'rgba(255, 0, 0, 0)');
                    ctxFire.beginPath();
                    ctxFire.arc(p.x, p.y, p.size * 2, 0, Math.PI * 2);
                    ctxFire.fillStyle = gradient;
                    ctxFire.fill();
                    ctxFire.beginPath();
                    ctxFire.arc(p.x, p.y, p.size, 0, Math.PI * 2);
                    ctxFire.fillStyle = `rgba(255
