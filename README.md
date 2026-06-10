# ANNISA-ZAKIYAH-
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Yuk, Baca Al-Qur'an Hari Ini</title>
    <style>
        /* --- CSS STYLING --- */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: #f7f9fa; /* Abu-abu sangat terang & bersih */
            color: #333333; /* Abu-abu gelap untuk keterbacaan teks */
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            overflow: hidden; /* Mencegah scrollbar muncul saat tombol kabur */
            padding: 20px;
        }

        .container {
            background: #ffffff; /* Putih bersih */
            max-width: 480px;
            width: 100%;
            border-radius: 24px;
            padding: 40px 30px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.05);
            text-align: center;
            border: 1px solid #e3e8ec;
            position: relative;
        }

        /* Stiker / Dekorasi Pendukung Tema */
        .sticker-bg {
            font-size: 2.2rem;
            position: absolute;
            opacity: 0.15;
            user-select: none;
        }
        .st-left { top: 20px; left: 20px; }
        .st-right { bottom: 20px; right: 20px; }

        .sticker-main {
            font-size: 5rem;
            margin-bottom: 20px;
            display: inline-block;
            animation: slowFloat 3s infinite ease-in-out;
            user-select: none;
        }

        @keyframes slowFloat {
            0%, 100% { transform: translateY(0) scale(1); }
            50% { transform: translateY(-8px) scale(1.03); }
        }

        h1 {
            font-size: 1.6rem;
            color: #2c3e50;
            margin-bottom: 12px;
            line-height: 1.4;
        }

        p.quote-ajakan {
            font-size: 1rem;
            color: #626d78;
            margin-bottom: 35px;
            line-height: 1.6;
        }

        /* Area Penempatan Tombol */
        .btn-wrapper {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 20px;
            height: 55px;
            position: relative;
        }

        button {
            padding: 12px 35px;
            font-size: 1rem;
            font-weight: 600;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: transform 0.2s, background-color 0.3s;
        }

        .btn-ya {
            background-color: #2c3e50; /* Abu-abu slate gelap premium */
            color: #ffffff;
            box-shadow: 0 4px 15px rgba(44, 62, 80, 0.2);
        }

        .btn-ya:hover {
            background-color: #1a252f;
            transform: scale(1.05);
        }

        .btn-tidak {
            background-color: #ffffff;
            color: #7f8c8d;
            border: 2px solid #bdc3c7;
            position: absolute;
            transition: all 0.15s ease; /* Transisi perpindahan posisi yang halus */
        }

        /* Set posisi awal tombol Tidak berdampingan di kanan tombol Ya */
        #btnTidak {
            left: 56%;
        }
        #btnYa {
            margin-right: 120px;
        }

        /* Kotak Pesan Keberkahan Al-Qur'an */
        .message-box {
            display: none;
            background-color: #f8f9fa;
            border-left: 4px solid #7f8c8d;
            padding: 22px;
            border-radius: 12px;
            margin-top: 30px;
            animation: popUp 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards;
        }

        @keyframes popUp {
            from { opacity: 0; transform: scale(0.9) translateY(15px); }
            to { opacity: 1; transform: scale(1) translateY(0); }
        }

        .message-title {
            font-size: 1.2rem;
            font-weight: bold;
            color: #2c3e50;
            margin-bottom: 8px;
        }

        .message-body {
            font-size: 0.95rem;
            color: #555555;
            line-height: 1.6;
            font-style: italic;
        }
    </style>
</head>
<body>

    <div class="container" id="mainCard">
        <!-- Stiker Sudut Bernuansa Islami Romantis & Damai -->
        <div class="sticker-bg st-left">✨</div>
        <div class="sticker-bg st-right">🌙</div>

        <!-- Stiker Utama Mushaf Al-Qur'an -->
        <div class="sticker-main" id="mainSticker">📖</div>

        <h1 id="mainTitle">Sudahkah Kita Membaca Al-Qur'an Hari Ini?</h1>
        <p class="quote-ajakan" id="subTitle">
            "Bacalah Al-Qur'an, karena sesungguhnya ia akan datang pada hari kiamat sebagai pemberi syafaat bagi pembacanya." (HR. Muslim) <br><br>
            Luangkan waktu 5 menit saja sekarang, yuk?
        </p>

        <!-- Area Tombol Interaktif -->
        <div class="btn-wrapper" id="buttonArea">
            <button class="btn-ya" id="btnYa" onclick="aksiYa()">Ya, Tentu!</button>
            <button class="btn-tidak" id="btnTidak" onmouseover="hindariTombol()" onclick="hindariTombol()">Tidak</button>
        </div>

        <!-- Kotak Respon Positif -->
        <div class="message-box" id="successBox">
            <div class="message-title">Masha Allah, Pilihan yang Indah! 🤍</div>
            <div class="message-body">
                "Al-Qur'an adalah penenang jiwa yang gundah, penerang jalan yang gelap, dan sumber keberkahan di setiap detik kehidupan kita. Selamat membaca, semoga setiap huruf yang kamu lunturkan menjadi ladang pahala tak terputus. Aamiin."
            </div>
        </div>
    </div>

    <script>
        /* --- JAVASCRIPT INTERAKTIF --- */

        function hindariTombol() {
            const btnTidak = document.getElementById('btnTidak');
            const card = document.getElementById('mainCard');
            
            // Mengambil ukuran absolut dari card kontainer utama
            const cardRect = card.getBoundingClientRect();
            const btnRect = btnTidak.getBoundingClientRect();

            // Menghitung batas koordinat maksimal di dalam kartu putih agar tombol tidak keluar jalur
            // Diberi kelonggaran margin batin (padding) sebesar 35px demi estetika
            const maxX = cardRect.width - btnRect.width - 35;
            const maxY = cardRect.height - btnRect.height - 35;

            // Menghasilkan titik koordinat baru secara acak matematika
            const acakX = Math.floor(Math.random() * (maxX - 35)) + 35;
            const acakY = Math.floor(Math.random() * (maxY - 35)) + 35;

            // Memindahkan posisi tombol Tidak secara instan/halus
            btnTidak.style.position = 'absolute';
            btnKeepLeft = btnTidak.style.left = acakX + 'px';
            btnKeepTop = btnTidak.style.top = acakY + 'px';
        }

        function aksiYa() {
            const successBox = document.getElementById('successBox');
            const btnTidak = document.getElementById('btnTidak');
            const btnYa = document.getElementById('btnYa');
            const mainSticker = document.getElementById('mainSticker');
            const mainTitle = document.getElementById('mainTitle');
            const subTitle = document.getElementById('subTitle');

            // 1. Munculkan kotak pesan keberkahan
            successBox.style.display = 'block';

            // 2. Hilangkan tombol "Tidak" secara permanen
            btnTidak.style.display = 'none';

            // 3. Ubah perilaku & teks tombol "Ya" agar menetap di tengah
            btnYa.style.margin = '0'; 
            btnYa.disabled = true; // Kunci tombol agar tidak bisa diklik berulang kali
            btnYa.innerText = "Alhamdulillah ✨";

            // 4. Transformasikan tampilan stiker dan teks menjadi atmosfer penuh kegembiraan religi
            mainSticker.innerText = "🕌✨";
            mainTitle.innerText = "Niat Baik Telah Bulat!";
            subTitle.innerText = "Ambil wudhu terbaikmu, buka mushaf atau aplikasimu, dan mulailah dengan ta'awudz.";
        }
    </script>

</body>
</html>
