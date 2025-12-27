<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>McD Internal Injector v3</title>
    <style>
        /* Menggunakan style yang sama dari file asli Anda */
        body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif; background-color: #da291c; padding: 20px; margin: 0; color: #333; display: flex; flex-direction: column; align-items: center; justify-content: center; min-height: 100vh; }
        .card { background: white; border-radius: 20px; padding: 25px; width: 100%; max-width: 380px; box-shadow: 0 10px 30px rgba(0,0,0,0.25); text-align: center; }
        h2 { font-size: 22px; margin: 0 0 20px 0; color: #da291c; font-weight: 800; text-transform: uppercase; letter-spacing: -0.5px; }
        label { display: block; text-align: left; font-size: 12px; font-weight: bold; color: #666; margin-bottom: 8px; margin-left: 5px; }
        select { width: 100%; padding: 15px; border-radius: 12px; font-size: 16px; margin-bottom: 20px; border: 2px solid #eee; outline: none; background-color: #f8f8f8; -webkit-appearance: none; appearance: none; cursor: pointer; }
        .btn { width: 100%; padding: 18px; border-radius: 12px; font-size: 16px; margin-top: 5px; border: none; outline: none; background: #ffbc0d; font-weight: 900; color: #222; cursor: pointer; transition: all 0.2s; box-shadow: 0 4px 0 #e0a800; }
        .btn:active { transform: translateY(4px); box-shadow: none; }
        .btn:disabled { background: #ccc; box-shadow: none; cursor: not-allowed; color: #666; }
        .footer { font-size: 11px; text-align: center; margin-top: 25px; color: rgba(255, 255, 255, 0.7); line-height: 1.5; }
        .spinner { display: none; width: 16px; height: 16px; border: 3px solid rgba(0,0,0,0.1); border-radius: 50%; border-top-color: #000; animation: spin 0.8s ease-in-out infinite; vertical-align: middle; margin-right: 8px; }
        @keyframes spin { to { transform: rotate(360deg); } }
        .loading .spinner { display: inline-block; }
    </style>
</head>
<body>

<div class="card">
    <h2>PILIH MENU INJEKSI</h2>
    
    <label>DAFTAR PAKET TERSEDIA:</label>
    <select id="menu">
        <option value="267611|5272">Panas 1 (Cek Validitas)</option>
        <option value="272395|5271">Cheeseburger + Fries</option>
        <option value="272400|5271">Ayam + McFloat + Fries</option>
        <option value="272404|5271">McFlurry + Fries</option>
        <option value="272469|5271">McNugget + Cola</option>
        <option value="272484|5271">Ayam + Nasi + Lemon Tea</option>
    </select>
    
    <button id="btnAction" class="btn" onclick="gas()">
        <span class="spinner"></span>
        <span id="btnText">BUKA DI APLIKASI</span>
    </button>
</div>

<div class="footer">
    Status: <strong>Force Intent Mode</strong><br>
    Target: com.mcdonalds.app<br>
    <small>v3.0 Android Intent Patch</small>
</div>

<script>
function gas() {
    // 1. Ambil Data
    const menu = document.getElementById('menu');
    const btn = document.getElementById('btnAction');
    const btnText = document.getElementById('btnText');
    
    const val = menu.value.split('|');
    const offerId = val[0];
    const loyaltyId = val[1];

    // 2. UI Feedback
    btn.classList.add('loading');
    btn.disabled = true;
    btnText.innerText = "MEMBUKA APLIKASI...";

    // 3. Susun URL Intent (Sangat Penting)
    // Format ini memberitahu Android: "Cari aplikasi McD, kalau gak ada, buka Play Store"
    // Parameter Bypass "partner" tetap disertakan
    const partner = encodeURIComponent("Tiktok Live 109.4");
    
    // Schema gmalite untuk Deep Link
    const scheme = "gmalite"; 
    const path = `offers/details?offer_id=${offerId}&loyalty_id=${loyaltyId}&view=claim&is_mass_code=1&partner=${partner}&action=redeem&is_native=true`;
    
    // Target Package Name (Ini ID Aplikasi McD Global di PlayStore)
    const package = "com.mcdonalds.app"; 

    // Konstruksi String Intent Android
    // Syntax: intent://[PATH]#Intent;scheme=[SCHEME];package=[PACKAGE];end
    const intentUrl = `intent://${path}#Intent;scheme=${scheme};package=${package};S.browser_fallback_url=https://play.google.com/store/apps/details?id=${package};end`;

    // 4. Eksekusi
    // Menggunakan timeout kecil agar UI sempat berubah sebelum browser pindah aplikasi
    setTimeout(() => {
        window.location.href = intentUrl;
        
        // Reset tombol jika user kembali ke browser
        setTimeout(() => {
            btn.classList.remove('loading');
            btn.disabled = false;
            btnText.innerText = "COBA LAGI";
        }, 2000);
    }, 500);
}
</script>

</body>
</html>
