<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>McD Internal Injector</title>
    <style>
        /* CSS Reset & Basic Style */
        body { 
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif; 
            background-color: #da291c; /* McD Red */
            padding: 20px; 
            margin: 0; 
            color: #333;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
        }

        /* Card Container - Mirip Mukidi */
        .card { 
            background: white; 
            border-radius: 20px; 
            padding: 25px; 
            width: 100%; 
            max-width: 380px; 
            box-shadow: 0 10px 30px rgba(0,0,0,0.25); 
            text-align: center;
        }

        /* Typography */
        h2 { 
            font-size: 22px; 
            margin: 0 0 20px 0; 
            color: #da291c; 
            font-weight: 800;
            text-transform: uppercase;
            letter-spacing: -0.5px;
        }

        /* Form Elements */
        label {
            display: block;
            text-align: left;
            font-size: 12px;
            font-weight: bold;
            color: #666;
            margin-bottom: 8px;
            margin-left: 5px;
        }

        select { 
            width: 100%; 
            padding: 15px; 
            border-radius: 12px; 
            font-size: 16px; 
            margin-bottom: 20px; 
            border: 2px solid #eee; 
            outline: none; 
            background-color: #f8f8f8;
            -webkit-appearance: none;
            appearance: none;
            cursor: pointer;
        }

        /* Button Style - McD Yellow */
        .btn { 
            width: 100%; 
            padding: 18px; 
            border-radius: 12px; 
            font-size: 16px; 
            margin-top: 5px; 
            border: none; 
            outline: none;
            background: #ffbc0d; 
            font-weight: 900; 
            color: #222; 
            cursor: pointer; 
            transition: all 0.2s;
            box-shadow: 0 4px 0 #e0a800;
        }

        .btn:active {
            transform: translateY(4px);
            box-shadow: none;
        }

        .btn:disabled {
            background: #ccc;
            box-shadow: none;
            cursor: not-allowed;
            color: #666;
        }

        /* Footer Info */
        .footer { 
            font-size: 11px; 
            text-align: center; 
            margin-top: 25px; 
            color: rgba(255, 255, 255, 0.7); 
            line-height: 1.5;
        }

        /* Loading Spinner Animation */
        .spinner {
            display: none;
            width: 16px;
            height: 16px;
            border: 3px solid rgba(0,0,0,0.1);
            border-radius: 50%;
            border-top-color: #000;
            animation: spin 0.8s ease-in-out infinite;
            vertical-align: middle;
            margin-right: 8px;
        }
        
        @keyframes spin { to { transform: rotate(360deg); } }
        .loading .spinner { display: inline-block; }

    </style>
</head>
<body>

<div class="card">
    <h2>PILIH MENU INJEKSI</h2>
    
    <label>DAFTAR PAKET TERSEDIA:</label>
    <select id="menu">
        <option value="267611|5272">Panas 1 (Hemat)</option>
        <option value="272395|5271">Cheeseburger + Fries</option>
        <option value="272400|5271">Ayam + McFloat + Fries</option>
        <option value="272404|5271">McFlurry + Fries</option>
        <option value="272469|5271">McNugget + Cola</option>
        <option value="272484|5271">Ayam + Nasi + Lemon Tea</option>
    </select>
    
    <button id="btnAction" class="btn" onclick="gas()">
        <span class="spinner"></span>
        <span id="btnText">INJECT KE APLIKASI</span>
    </button>
</div>

<div class="footer">
    Status: <strong>Connected</strong><br>
    Server: Tiktok Live 109.4 Bridge<br>
    <small>v2.4 Native Redeem Patch</small>
</div>

<script>
function gas() {
    // 1. Ambil elemen UI
    const menu = document.getElementById('menu');
    const btn = document.getElementById('btnAction');
    const btnText = document.getElementById('btnText');
    
    // 2. Parse Data
    const val = menu.value.split('|');
    const offerId = val[0];
    const loyaltyId = val[1];

    // 3. Efek Loading (UX)
    btn.classList.add('loading');
    btn.disabled = true;
    btnText.innerText = "MENCOBA MENGHUBUNGKAN...";

    // 4. Konfigurasi Link (Bypass Logic)
    // Menggunakan partner tiktok agar server tidak menolak request
    const partner = encodeURIComponent("Tiktok Live 109.4");
    
    // Link Utama: Langsung ke tampilan klaim (Native View)
    const deepLinkMain = `gmalite://offers/details?offer_id=${offerId}&loyalty_id=${loyaltyId}&
