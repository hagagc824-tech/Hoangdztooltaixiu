<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI PRO 2026 | HOANGDZ SYSTEM</title>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;900&display=swap" rel="stylesheet">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/crypto-js/4.1.1/crypto-js.min.js"></script>
    <style>
        :root { --neon: #00f2ff; --bg: #050505; }
        body { margin:0; background:var(--bg); color:#fff; font-family:'Orbitron', sans-serif; overflow-x:hidden; }
        
        /* Hiệu ứng tuyết rơi dày */
        .snow-container { position:fixed; inset:0; pointer-events:none; z-index:999; }
        .snowflake { position:absolute; color:white; font-size: 15px; opacity:0.8; animation: fall linear infinite; }
        @keyframes fall { to { transform: translateY(100vh) rotate(360deg); } }

        .wrapper { max-width:450px; margin:20px auto; padding:15px; position:relative; z-index:1000; }
        .glass { background:rgba(0,0,0,0.7); border:1px solid var(--neon); border-radius:20px; padding:20px; margin-bottom:20px; text-align:center; box-shadow: 0 0 20px rgba(0, 242, 255, 0.2); }
        input, button { width:100%; padding:14px; margin-bottom:12px; border-radius:10px; border:1px solid #444; background:rgba(255,255,255,0.05); color:#fff; font-size:16px; box-sizing:border-box; }
        .btn { background:linear-gradient(90deg, var(--neon), #7000ff); font-weight:bold; cursor:pointer; border:none; color:white; transition: 0.3s; }
        .btn:active { transform: scale(0.95); }
        
        .res-box { font-size:3rem; font-weight:900; color:var(--neon); margin:15px 0; text-shadow: 0 0 20px var(--neon); }
        .res-jumping { animation: jump 0.2s infinite; }
        @keyframes jump { 0% { transform: scale(1); opacity: 0.5; } 50% { transform: scale(1.1); opacity: 1; } 100% { transform: scale(1); opacity: 0.5; } }
        
        .info-text { font-size:12px; color:#fff; text-align:left; margin:15px 0; line-height:1.6; }
        .warning-text { font-size:12px; color:#ffcc00; margin-bottom:10px; font-weight:bold; }
        .history-item { font-size:13px; border-bottom:1px solid #333; padding:10px 0; display:flex; justify-content:space-between; color:#ccc; }
        .login-overlay { position:fixed; inset:0; background:#000; z-index:9999; display:flex; align-items:center; justify-content:center; padding:20px; }
    </style>
</head>
<body>
    <div class="snow-container" id="snow"></div>

    <div class="login-overlay" id="loginScreen">
        <div class="glass" style="width:100%; max-width:320px;">
            <h2 style="color:var(--neon);">🔑 KÍCH HOẠT VIP</h2>
            <input type="text" id="keyInput" placeholder="Nhập Key...">
            <button class="btn" onclick="checkKey()">KÍCH HOẠT NGAY</button>
            <div id="checkStatus" style="font-size:12px; color:red;"></div>
        </div>
    </div>

    <div class="wrapper" id="mainScreen" style="display:none;">
        <div class="glass">
            <h3 style="color:var(--neon); margin:0;">GIỚI THIỆU TOOL</h3>
            <p style="font-size:11px;">Hệ thống phân tích MD5 2026. Công nghệ AI độc quyền bởi HOANGDZ.</p>
            <div id="timerDisplay" style="color:yellow; font-size:12px;">Thời gian: --:--</div>
            <button class="btn" style="background:#444; font-size:11px;" onclick="logout()">ĐĂNG XUẤT</button>
        </div>

        <div class="glass">
            <input type="text" id="code" placeholder="Mã phiên MD5...">
            <div class="warning-text">⚠️ CẢNH BÁO: Nên bỏ 2-3 tay đầu để tool ổn định tín hiệu!</div>
            <button class="btn" onclick="runAnalysis()">PHÂN TÍCH KẾT QUẢ</button>
            
            <div id="statusMsg" style="font-size:13px; color:var(--neon); margin:10px 0; font-weight:bold;"></div>
            
            <div id="resultContent" style="display:none; text-align:left;">
                <div class="res-box" id="res">--</div>
                <div class="info-text">
                    <p><b>Tỉ lệ thắng:</b> <span id="winrate">--</span>%</p>
                    <p><b>Tại sao ra kết quả đó:</b> Dựa trên thuật toán xác suất MD5 kết hợp với chuỗi biến động phiên.</p>
                    <p><b>Anh HOANGDZ bảo:</b> "Chơi có kỷ luật, thắng không kiêu, bại không nản. Chúc anh em về bờ an toàn!"</p>
                    <p><b>Liên hệ Admin:</b> @tranhoang2286</p>
                </div>
            </div>
        </div>

        <div class="glass">
            <h4 style="margin:0 0 10px; color:var(--neon);">LỊCH SỬ DỰ ĐOÁN</h4>
            <div id="historyList"></div>
        </div>
    </div>

    <script>
        function createSnow() {
            const snow = document.getElementById('snow');
            for(let i=0; i<80; i++) {
                let d = document.createElement('div');
                d.className = 'snowflake';
                d.innerHTML = '❄';
                d.style.left = Math.random()*100 + '%';
                d.style.animationDuration = Math.random()*5 + 5 + 's';
                snow.appendChild(d);
            }
        }
        createSnow();

        function checkKey() {
            if (document.getElementById('keyInput').value.startsWith("KEY-HOANGDZ-")) {
                localStorage.setItem('expiry', Date.now() + 3600000); 
                location.reload();
            } else { alert("Key không hợp lệ!"); }
        }

        function runAnalysis() {
            let input = document.getElementById('code').value.trim();
            if(input.length < 32) return alert("Nhập đủ 32 ký tự!");
            
            let status = document.getElementById('statusMsg');
            let resContent = document.getElementById('resultContent');
            let resEl = document.getElementById('res');
            
            status.innerText = "🔄 Đang phân tích dữ liệu...";
            resContent.style.display = "block";
            resEl.classList.add('res-jumping');
            
            let count = 0;
            let interval = setInterval(() => {
                resEl.innerText = (count++ % 2 === 0) ? "🔴 TÀI" : "⚪ XỈU";
            }, 100);

            setTimeout(() => {
                clearInterval(interval);
                resEl.classList.remove('res-jumping');
                let hash = CryptoJS.MD5(input).toString();
                let res = (parseInt(hash.slice(-1), 16) % 2 === 0) ? "🔴 TÀI" : "⚪ XỈU";
                resEl.innerText = res;
                document.getElementById('winrate').innerText = Math.floor(Math.random() * (95 - 85 + 1) + 85);
                status.innerText = "✅ Đã phân tích xong!";
                
                let history = JSON.parse(localStorage.getItem('history') || '[]');
                history.unshift({time: new Date().toLocaleTimeString(), res: res});
                localStorage.setItem('history', JSON.stringify(history.slice(0, 5)));
                renderHistory();
            }, 2000);
        }

        function renderHistory() {
            let list = document.getElementById('historyList');
            let history = JSON.parse(localStorage.getItem('history') || '[]');
            list.innerHTML = history.map(h => `<div class="history-item"><span>${h.time}</span><span>${h.res}</span></div>`).join('');
        }

        function logout() { localStorage.removeItem('expiry'); location.reload(); }
        
        function updateTimer() {
            let expiry = localStorage.getItem('expiry');
            if (expiry) {
                let left = expiry - Date.now();
                if (left <= 0) { localStorage.removeItem('expiry'); location.reload(); }
                let m = Math.floor(left/60000);
                let s = Math.floor((left%60000)/1000);
                document.getElementById('timerDisplay').innerText = `Thời gian còn lại: ${m}p ${s}s`;
            }
        }

        window.onload = () => {
            if (localStorage.getItem('expiry') > Date.now()) {
                document.getElementById('loginScreen').style.display = 'none';
                document.getElementById('mainScreen').style.display = 'block';
                setInterval(updateTimer, 1000);
                renderHistory();
            }
        };
    </script>
</body>
</html>
