<!DOCTYPE html>
<html lang="id">
<head>
    <title>Akses Terkunci</title>
    <style>
        body { font-family: sans-serif; text-align: center; padding: 50px; }
        .box { border: 1px solid #ccc; padding: 20px; display: inline-block; border-radius: 8px; }
        input { padding: 10px; width: 250px; margin-bottom: 10px; }
        button { padding: 10px 20px; background: blue; color: white; border: none; cursor: pointer; }
    </style>
</head>
<body>

    <div class="box">
        <h2>Masukkan Key Akses</h2>
        <p>ID Pelacakan: <span id="display-id">Memuat...</span></p>
        
        <input type="text" id="input-key" placeholder="Masukkan Kode (Contoh: MKD-...)">
        <br>
        <button onclick="verifikasi()">Buka Akses</button>
        <p id="pesan"></p>
    </div>

    <script>
        // 1. Mengambil 'ko_click_id' dari URL
        const urlParams = new URLSearchParams(window.location.search);
        const clickId = urlParams.get('ko_click_id');
        
        // Tampilkan ID di layar
        document.getElementById('display-id').innerText = clickId ? clickId : "Tidak ada ID";

        function verifikasi() {
            const keyInput = document.getElementById('input-key').value;
            const keyBenar = "MKD-HVRTYV-TF98PH"; // Key yang Anda tentukan

            if (keyInput === keyBenar) {
                document.getElementById('pesan').innerText = "Akses Diterima! Mengalihkan...";
                document.getElementById('pesan').style.color = "green";
                // Arahkan ke halaman tujuan (misal Google)
                setTimeout(() => {
                    window.location.href = "https://google.com?id=" + clickId;
                }, 2000);
            } else {
                document.getElementById('pesan').innerText = "Key Salah atau Kadaluwarsa!";
                document.getElementById('pesan').style.color = "red";
            }
        }
    </script>
</body>
</html>
