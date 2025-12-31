<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chúc Mừng Năm Mới Bính Ngọ 2026</title>
    <style>
        body, html {
            margin: 0;
            padding: 0;
            width: 100%;
            height: 100%;
            overflow: hidden;
            background: #000;
            font-family: 'Segoe UI', Arial, sans-serif;
        }

        canvas {
            display: block;
            position: absolute;
            top: 0;
            left: 0;
            z-index: 1;
        }

        /* Lớp phủ nội dung */
        .container {
            position: relative;
            z-index: 10;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100vh;
            text-align: center;
            color: #fff;
            pointer-events: none;
        }

        /* Tiêu đề năm mới */
        .header-text {
            font-size: 3rem;
            color: #ffd700;
            text-shadow: 0 0 20px #ff0000, 0 0 30px #ffcc00;
            margin-bottom: 20px;
            font-weight: bold;
            text-transform: uppercase;
        }

        /* Đồng hồ đếm ngược */
        .countdown-wrapper {
            display: flex;
            gap: 20px;
            background: rgba(0, 0, 0, 0.5);
            padding: 20px 40px;
            border-radius: 50px;
            border: 2px solid #ffd700;
            box-shadow: 0 0 30px rgba(255, 215, 0, 0.4);
        }

        .time-box {
            display: flex;
            flex-direction: column;
        }

        .time-value {
            font-size: 3.5rem;
            font-weight: 900;
            color: #fff;
            line-height: 1;
        }

        .time-label {
            font-size: 0.9rem;
            color: #ff3333;
            text-transform: uppercase;
            font-weight: bold;
        }

        /* Lời chúc */
        .wish-text {
            margin-top: 30px;
            font-size: 2.5rem;
            color: #ff3333;
            font-weight: bold;
            text-shadow: 2px 2px 5px #fff;
            animation: pulse 1.5s infinite alternate;
        }

        @keyframes pulse {
            from { transform: scale(1); opacity: 0.8; }
            to { transform: scale(1.1); opacity: 1; }
        }

        /* Hiệu ứng ngựa chạy */
        .horse-container {
            position: absolute;
            bottom: 20px;
            width: 100%;
            z-index: 5;
        }

        .horse {
            position: absolute;
            font-size: 60px;
            animation: gallop 8s linear infinite;
        }

        @keyframes gallop {
            from { left: -100px; }
            to { left: 110%; }
        }

        /* Lồng đèn */
        .lantern {
            position: absolute;
            top: -10px;
            width: 50px;
            height: 70px;
            background: #ff0000;
            border-radius: 20px;
            box-shadow: 0 0 20px #ff0000;
            animation: swing 2s ease-in-out infinite;
            transform-origin: top center;
            z-index: 15;
        }
        .lantern::after { content: "🧧"; font-size: 25px; display: flex; justify-content: center; margin-top: 15px; }

        @keyframes swing {
            0%, 100% { transform: rotate(-15deg); }
            50% { transform: rotate(15deg); }
        }
    </style>
</head>
<body>

    <div class="lantern" style="left: 5%;"></div>
    <div class="lantern" style="left: 15%;"></div>
    <div class="lantern" style="right: 5%;"></div>
    <div class="lantern" style="right: 15%;"></div>

    <div class="container">
        <div class="header-text">Đếm ngược đến Xuân Bính Ngọ 2026</div>
        
        <div class="countdown-wrapper" id="timer">
            <div class="time-box"><span class="time-value" id="days">00</span><span class="time-label">Ngày</span></div>
            <div class="time-box"><span class="time-value" id="hours">00</span><span class="time-label">Giờ</span></div>
            <div class="time-box"><span class="time-value" id="mins">00</span><span class="time-label">Phút</span></div>
            <div class="time-box"><span class="time-value" id="secs">00</span><span class="time-label">Giây</span></div>
        </div>

        <div class="wish-text">MÃ ĐÁO THÀNH CÔNG - VẠN SỰ NHƯ Ý</div>
    </div>

    <div class="horse" style="bottom: 80px; animation-duration: 10s;">🐎</div>
    <div class="horse" style="bottom: 40px; animation-duration: 7s;">🏇</div>

    <canvas id="fireworks"></canvas>

    <script>
        // Cài đặt ngày đích: 1/1/2026
        const countdownDate = new Date("Jan 1, 2026 00:00:00").getTime();

        function updateTimer() {
            const now = new Date().getTime();
            const distance = countdownDate - now;

            const d = Math.floor(distance / (1000 * 60 * 60 * 24));
            const h = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
            const m = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
            const s = Math.floor((distance % (1000 * 60)) / 1000);

            document.getElementById("days").innerText = d < 10 ? "0" + d : d;
            document.getElementById("hours").innerText = h < 10 ? "0" + h : h;
            document.getElementById("mins").innerText = m < 10 ? "0" + m : m;
            document.getElementById("secs").innerText = s < 10 ? "0" + s : s;

            if (distance < 0) {
                clearInterval(timerInterval);
                document.querySelector(".header-text").innerHTML = "CHÚC MƯNG NĂM MỚI 2026!";
                document.getElementById("timer").style.display = "none";
            }
        }

        const timerInterval = setInterval(updateTimer, 1000);
        updateTimer();
        // --- CODE PHÁO HOA ---
        const canvas = document.getElementById('fireworks');
        const ctx = canvas.getContext('2d');
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        class Particle {
            constructor(x, y, color) {
                this.x = x;
                this.y = y;
                this.color = color;
                this.radius = Math.random() * 2 + 1;
                this.velocity = {
                    x: (Math.random() - 0.5) * 10,
                    y: (Math.random() - 0.5) * 10
                };
                this.opacity = 1;
            }
            draw() {
                ctx.save();
                ctx.globalAlpha = this.opacity;
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
                ctx.fillStyle = this.color;
                ctx.shadowBlur = 10;
                ctx.shadowColor = this.color;
                ctx.fill();
                ctx.restore();
            }
            update() {
                this.x += this.velocity.x;
                this.y += this.velocity.y;
                this.velocity.y += 0.05; // Trọng lực
                this.opacity -= 0.01;
            }
        }

        let particles = [];
        const colors = ['#ff0000', '#ffd700', '#00ff00', '#00ffff', '#ff00ff', '#ffffff', '#ff9900', '#ffff00'];

        function explode(x, y) {
            const color = colors[Math.floor(Math.random() * colors.length)];
            for (let i = 0; i < 100; i++) {
                particles.push(new Particle(x, y, color));
            }
        }

        function animate() {
            ctx.fillStyle = 'rgba(0, 0, 0, 0.15)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            if (Math.random() < 0.08) {
                explode(Math.random() * canvas.width, Math.random() * canvas.height * 0.7);
            }

            particles.forEach((p, i) => {
                if (p.opacity > 0) {
                    p.update();
                    p.draw();
                } else {
                    particles.splice(i, 1);
                }
            });
            requestAnimationFrame(animate);
        }

        animate();

        window.addEventListener('resize', () => {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        });
    </script>
</body>
</html>
