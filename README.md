 <!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>If you want to play game then...</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <style>
    :root { --bg:#000; --green:#00ff00; --red:#ff0000; }
    * { box-sizing:border-box; }
    html, body {
      height:100%; margin:0;
      background:var(--bg); color:var(--green);
      font-family:monospace;
    }
    .layout { display:flex; height:100%; overflow:hidden; }
    .panel {
      flex:1; padding:20px; height:100%;
      overflow-y:auto; white-space:pre-wrap;
      font-size:18px; font-weight:bold;
    }
    .panel.right { border-left:2px solid #222; }
    .overlay {
      position:fixed; inset:0;
      background:rgba(0,0,0,0.9);
      display:flex; flex-direction:column;
      align-items:center; justify-content:center;
      z-index:9999; text-align:center; padding:20px;
    }
    .warning {
      color:red; font-size:44px; font-weight:bold;
      animation:blink 1s infinite; margin-bottom:20px;
    }
    @keyframes blink { 0%{opacity:1;} 50%{opacity:0;} 100%{opacity:1;} }
    .btn {
      background:red; color:#fff; border:none;
      font-size:18px; font-weight:bold;
      padding:10px 20px; cursor:pointer;
    }
    .code-header { color:#00ffff; margin-bottom:10px; }
    .line { display:block; margin:0 0 2px 0; }
    .hidden { display:none; }
  </style>
</head>
<body>
  <!-- Overlay -->
  <div id="overlay" class="overlay" aria-live="polite">
    <div id="overlayMsg" class="warning">⚠️ If you want to play game then... ⚠️</div>
    <button id="startBtn" class="btn" type="button">Click the button</button>
  </div>

  <!-- Main layout -->
  <div class="layout">
    <div id="terminalLeft" class="panel left" aria-label="Left terminal">
      <div class="code-header">// Fake exploit code running...
function hackSystem() {
  console.log("Injecting payload...");
  return true;
}</div>
    </div>
    <div id="terminalRight" class="panel right" aria-label="Right terminal"></div>
  </div>

  <script>
    (function () {
      'use strict';
      var overlay = document.getElementById('overlay');
      var overlayMsg = document.getElementById('overlayMsg');
      var startBtn = document.getElementById('startBtn');
      var left = document.getElementById('terminalLeft');
      var right = document.getElementById('terminalRight');

      // Left side logs (green)
      var leftLogs = [
        "[ACCESSING] Askari Net secure servers...",
        "[BREACH] HBL Banking System compromised...",
        "[ALERT] ATM PINs decrypted...",
        "[WARNING] Financial records exposed...",
        "[INFO] Credit card vault unlocked...",
        "[UPLOAD] Sending data to dark web...",
        "[TRACE] Location triangulated...",
        "[LOCKDOWN] Security bypass successful...",
        "[COMPLETE] All accounts compromised...",
        "[SCAN] WhatsApp chats intercepted...",
        "[INJECT] Malware deployed...",
        "[OVERRIDE] Firewall disabled...",
        "[CAPTURE] Camera access granted...",
        "[STEAL] Passwords extracted...",
        "[BREAK] VPN tunnel destroyed...",
        "[ALERT] Phone contacts cloned...",
        "[HACK] Social media accounts hijacked...",
        "[SPY] Microphone activated...",
        "[LEAK] Confidential files exposed...",
        "[INFECT] Trojan horse installed...",
        "[BREACH] Email inbox compromised...",
        "[TRACE] GPS location locked...",
        "[STEAL] Banking OTP intercepted...",
        "[ALERT] Cloud storage breached...",
        "[BREAK] Secure folder unlocked...",
        "[CAPTURE] Screenshot taken...",
        "[SPY] Browser history stolen...",
        "[BREACH] SIM card cloned...",
        "[STEAL] Crypto wallet accessed...",
        "[BREAK] Secure notes decrypted...",
        "[CAPTURE] Fingerprint data stolen...",
        "[SPY] Face ID bypassed...",
        "[BREACH] Government database pinged...",
        "[ALERT] Military server accessed...",
        "[STEAL] Classified documents leaked...",
        "[BREAK] Secure drive formatted...",
        "[CAPTURE] Hidden files revealed...",
        "[SPY] Secret chats mirrored...",
        "[BREACH] ATM network override...",
        "[ALERT] Payment gateway hijacked...",
        "[STEAL] Salary records exposed...",
        "[BREAK] Secure backup deleted...",
        "[CAPTURE] CCTV feed tapped...",
        "[SPY] Bluetooth devices tracked...",
        "[BREACH] WiFi router hacked...",
        "[ALERT] ISP logs erased...",
        "[STEAL] Call recordings uploaded...",
        "[BREAK] Antivirus disabled...",
        "[CAPTURE] System registry altered...",
        "[SPY] Hidden apps discovered...",
        "[BREACH] Secure shell cracked...",
        "[ALERT] Root access obtained...",
        "[STEAL] Encrypted keys stolen...",
        "[BREAK] Secure boot bypassed...",
        "[CAPTURE] Hidden partitions exposed...",
        "[SPY] Secret folders mirrored..."
      ];

      // Right side logs (red horror)
      var rightLogs = [
        ">>> ALERT: TikTok account hijacked",
        ">>> WARNING: Instagram photos leaked",
        ">>> NOTICE: Facebook messages mirrored",
        ">>> INFO: Snapchat streaks stolen",
        ">>> ALERT: YouTube channel compromised",
        ">>> SCAN: Netflix credentials exposed",
        ">>> ALERT: PUBG account hacked",
        ">>> WARNING: Fortnite skins stolen",
        ">>> INFO: Discord chats cloned",
        ">>> ALERT: Gmail inbox mirrored",
        ">>> NOTICE: Twitter feed hijacked",
        ">>> ALERT: LinkedIn profile breached",
        ">>> WARNING: Spotify playlists deleted",
        ">>> INFO: Amazon orders leaked",
        ">>> ALERT: PayPal account accessed",
        ">>> WARNING: Banking OTP intercepted",
        ">>> ALERT: Crypto wallet drained",
        ">>> INFO: Cloud storage mirrored",
        ">>> ALERT: Device reboot forced",
        ">>> WARNING: Secure notes exposed",
        ">>> ALERT: Hidden folders revealed",
        ">>> INFO: Bluetooth devices tracked",
        ">>> ALERT: WiFi router overridden",
        ">>> WARNING: ISP logs erased",
        ">>> ALERT: Antivirus disabled",
        ">>> INFO: Registry altered",
        ">>> ALERT: Root access obtained",
        ">>> WARNING: Secure boot bypassed",
        ">>> ALERT: Hidden partitions exposed",
        ">>> INFO: Secret folders mirrored",
        ">>> ALERT: CCTV feed tapped",
        ">>> WARNING: Camera activated",
        ">>> ALERT: Microphone listening",
        ">>> INFO: Passwords extracted",
        ">>> ALERT: OTP stolen",
        ">>> WARNING: Crypto keys leaked",
        ">>> ALERT: Government database pinged",
        ">>> INFO: Military server accessed",
        ">>> ALERT: Classified docs leaked",
        ">>> WARNING: Secure drive formatted",
        ">>> ALERT: Backup deleted",
        ">>> INFO: Hidden files revealed",
        ">>> ALERT: Secret chats mirrored",
        ">>> WARNING: ATM network override",
        ">>> ALERT: Payment gateway hijacked",
        ">>> INFO: Salary records exposed",
        ">>> ALERT: Secure shell cracked",
        ">>> WARNING: Root privileges gained",
        ">>> ALERT: System compromised"
      ];

      var leftIndex = 0;
      var rightIndex = 0;

      function appendLine(target, text, color) {
        var span = document.createElement('span');
        span.className = 'line';
        if (color) { span.style.color = color; }
        span.textContent = text;
        target.appendChild(span);
        target.scrollTop = target.scrollHeight;
      }

      startBtn.addEventListener('click', function () {
        overlayMsg.textContent = '💀 HACKED 💀';
        startBtn.classList.add('hidden');

        setTimeout(function () {
          overlay.classList.add('hidden');

          // Left logs (green)
          setInterval(function () {
            var line = leftLogs[leftIndex % leftLogs.length];
            appendLine(left, line, '#00ff00');
            leftIndex++;
          }, 400);

          // Right logs (red horror)
          setInterval(function () {
            var line = rightLogs[rightIndex % rightLogs.length];
            appendLine(right, line, '#ff0000');
            rightIndex++;
          }, 300);
        }, 2000);
      });
    })();
  </script>
</body>
</html>
