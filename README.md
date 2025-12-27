<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>McD Private Panel</title>
    <style>
        /* CSS SEDERHANA & RESPONSIF */
        * { box-sizing: border-box; }
        body { 
            font-family: -apple-system, sans-serif; 
            background-color: #da291c; /* Merah McD */
            margin: 0; 
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
        }

        .card { 
            background: #fff; 
            width: 100%; 
            max-width: 400px; 
            border-radius: 20px; 
            padding: 30px; 
            box-shadow: 0 15px 35px rgba(0,0,0,0.3); 
            text-align: center;
        }

        h2 { 
            margin: 0 0 5px 0; 
            color: #da291c; 
            font-weight: 800; 
            font-size: 24px;
        }

        p { color: #666; font-size: 13px; margin-bottom: 25px; }

        /* Style Input Pilihan Menu */
        .form-group { text-align: left; margin-bottom: 15px; }
        label { font-size: 12px; font-weight: bold; color: #333; margin-left: 5px; }
        
        select { 
            width: 100%; 
            padding: 15px; 
            border-radius: 12px; 
            border: 2px solid #eee; 
            background: #f9f9f9; 
            font-size: 16px; 
            outline: none; 
            margin-top: 5px;
            -webkit-appearance: none; /* Hapus panah default di iPhone */
        }

        /* Tombol Eksekusi */
        .btn-inject { 
            background: #ffbc0d; /* Kuning McD */
            color: #000; 
            font-weight: 900; 
            border: none; 
            width: 100%; 
            padding: 18px; 
            border-radius: 12px; 
            font-size: 18px; 
            cursor: pointer; 
            transition: 0.2s;
            margin-top: 10px;
            box-shadow: 0 5px 0 #cc9a00;
        }

        .btn-inject:active { 
            transform: translateY(5px); 
            box-shadow: none; 
        }

        .footer { 
            margin-top: 25px; 
            color: rgba(255,255,255,0.6); 
            font-size: 11px; 
            text-align: center; 
        }
    </style>
</head>
<body>

<div class="card">
    <h2>MCD UNLOCKED</h2>
    <p>Script Polos Tanpa Lisensi</p>

    <div class="form-group">
        <label>PILIH MENU:</label>
        <select id="pilihanMenu">
            <option value="267611|5272">PAKET 1 (Contoh)</option>
            <option value="272395|5271">PAKET 2 (Contoh)</option>
            <option value="272400|5271">PAKET 3 (Contoh)</option>
        </select>
    </div>

    <button class="btn-inject" onclick="gasPol()">GAS INJECT</button>
</div>

<div class="footer">
    Status: <strong>No License / Free Source</strong><br>
    Engine: Android Intent:// v4
</div>

<script>
    function gasPol() {
        // 1. AMBIL DATA DARI PILIHAN
        var rawData = document.getElementById("pilihanMenu").value;
        var splitData = rawData.split("|");
        var offerID = splitData[0];
        var loyaltyID = splitData[1];

        // 2. SETTING TARGET
        // "com.mcdonalds.app" adalah ID aplikasi McD Indonesia di Playstore
        var targetPackage = "com.mcdonalds.app"; 
        
        // "partner" ini trik agar server mengira kita klik dari iklan Tiktok/Google
        var bypassKey = encodeURIComponent("Tiktok Live"); 

        // 3. RAKIT URL "INTENT"
        // Ini adalah perintah level sistem Android, bukan sekedar link browser.
        // Script ini akan memaksa OS mencari aplikasi McD dan membuka halaman redeem.
        
        var deepLinkPath = "offers/details?" + 
                           "offer_id=" + offerID + 
                           "&loyalty_id=" + loyaltyID + 
                           "&view=claim" + 
                           "&is_mass_code=1" + 
                           "&partner=" + bypassKey + 
                           "&action=redeem" + 
                           "&is_native=true";

        var androidIntent = "intent://gmalite/" + deepLinkPath + "#Intent;scheme=gmalite;package=" + targetPackage + ";end";

        // 4. EKSEKUSI
        // Langsung lempar user ke aplikasi
        window.location.href = androidIntent;
    }
</script>

</body>
</html>
