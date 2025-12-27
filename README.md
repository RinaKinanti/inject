<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>McD Internal Injector v2</title>
    <style>
        body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; background: #da291c; padding: 15px; margin: 0; color: white; display: flex; align-items: center; justify-content: center; min-height: 100vh; }
        .card { background: white; border-radius: 20px; padding: 25px; width: 100%; max-width: 400px; color: #333; box-shadow: 0 10px 25px rgba(0,0,0,0.3); }
        h2 { font-size: 20px; margin-bottom: 20px; text-align: center; color: #da291c; font-weight: 800; letter-spacing: -0.5px; }
        label { font-size: 12px; font-weight: bold; color: #666; margin-bottom: 5px; display: block; }
        select { width: 100%; padding: 15px; border-radius: 12px; font-size: 16px; margin-bottom: 15px; border: 2px solid #eee; outline: none; appearance: none; background-color: #f9f9f9; }
        .btn { width: 100%; padding: 16px; border-radius: 12px; font-size: 16px; font-weight: bold; color: #222; cursor: pointer; background: #ffbc0d; border: none; transition: transform 0.1s; }
        .btn:active { transform: scale(0.98); }
        .btn:disabled { background: #e0e0e0; color: #999; cursor: not-allowed; }
        .footer { font-size: 11px; text-align: center; margin-top: 20px; color: #ffdada; opacity: 0.8; }
        
        /* Loading Animation */
        .spinner { display: inline-block; width: 15px; height: 15px; border: 2px solid rgba(0,0,0,0.3); border-radius: 50%; border-top-color: #000; animation: spin 1s ease-in-out infinite; margin-right: 8px; vertical-align: middle; display: none; }
        @keyframes spin { to { transform: rotate(360deg); } }
        .loading .spinner { display: inline-block; }
    </style>
</head>
<body>

<div class="card">
    <h2>INJEKSI MENU</h2>
    
    <label>PILIH PAKET:</label>
    <select id="menu">
        <option value="267611|5272">Panas 1 (ID: 267611)</option>
        <option value="272395|5271">Cheeseburg + Fries (ID: 272395)</option>
        <option value="272400|5271">Ayam + McFloat + Fries (ID: 272400)</option>
        <option value="272404|5271">McFlurry + Fries (ID: 272404)</option>
        <option value="272469|5271">McNugget + Cola (ID: 272469)</option>
        <option value="272484|5271">Ayam + Nasi + Lemon Tea (ID: 272484)</option>
    </select>
    
    <button id="btnAction" class="btn" onclick="gas()">
        <span class="spinner"></span>
        <span id="btnText">INJECT KE APLIKASI</span>
    </button>

    <div class="footer">
        Status: Connected via Tiktok Live 109.4 Bridge<br>
        Patch: Native Redeem Force
    </div>
</div>

<script>
function gas() {
    // 1. Ambil Data
    const menu = document.getElementById('menu');
    const data = menu.value.split('|');
    const off = data[0];
    const loy = data[1];

    // UI Feedback (Tombol Loading)
    const btn = document.getElementById('btnAction');
    const btnText = document.getElementById('btnText');
    
    btn.classList.add('loading');
    btn.disabled = true;
    btnText.innerText = "MENCOBA INJECT...";

    // 2. Setup Parameter Bypass
    // Pastikan Partner ter-encode dengan benar untuk menghindari error server
    const partner = encodeURIComponent("Tiktok Live 109.4");
    
    // 3. Construct URL (Menggunakan Template Literal agar rapi)
    // Target Utama: Details View dengan Native Flag
    const primaryLink = `gmalite://offers/details?offer_id=${off}&loyalty_id=${loy}&view=claim&is_mass_code=1&partner=${partner}&action=redeem&is_native=true`;

    // Target Cadangan: Direct Redeem (Jika view details gagal)
    const backupLink = `gmalite://offers/redeem?offer_id=${off}&loyalty_id=${loy}&is_mass_code=1`;

    // 4. Eksekusi
    // Coba link utama
    window.location.href = primaryLink;

    // 5. Fallback Logic (Mukidi Style v2)
    // Gunakan timer untuk mencoba link cadangan jika aplikasi tidak terbuka dalam 1.5 detik
    setTimeout(() => {
        // Coba metode backup
        window.location.href = backupLink;
        
        // Reset tombol setelah mencoba backup
        setTimeout(() => {
            btn.classList.remove('loading');
            btn.disabled = false;
            btnText.innerText = "INJECT ULANG";
        }, 1000);
    }, 1500);
}
</script>

</body>
</html>
