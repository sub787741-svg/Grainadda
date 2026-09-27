<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Grain Adda - Real Gaming Platform</title>
  
  <!-- Firebase Cloud SDKs for Realtime Multi-device Sync -->
  <script src="https://www.gstatic.com/firebasejs/8.10.1/firebase-app.js"></script>
  <script src="https://www.gstatic.com/firebasejs/8.10.1/firebase-database.js"></script>

  <style>
    :root {
      --primary: #1e40af;
      --primary-light: #3b82f6;
      --bg: #f1f5f9;
      --card-bg: #ffffff;
      --text: #0f172a;
      --text-muted: #64748b;
      --border: #cbd5e1;
      --green: #15803d;
      --green-light: #dcfce7;
      --gold: #b45309;
      --gold-light: #fef3c7;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
    }

    body {
      background-color: var(--bg);
      color: var(--text);
      padding-bottom: 70px;
    }

    /* Clean Compact Header */
    header {
      background: var(--card-bg);
      padding: 0.6rem 0.8rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-bottom: 1px solid var(--border);
      position: sticky;
      top: 0;
      z-index: 100;
      box-shadow: 0 1px 3px rgba(0,0,0,0.04);
    }

    .logo-box {
      display: flex;
      align-items: center;
      gap: 5px;
    }

    .logo-text {
      font-size: 1rem;
      font-weight: 800;
      color: var(--primary);
      letter-spacing: 0.5px;
    }

    .header-actions {
      display: flex;
      align-items: center;
      gap: 6px;
    }

    .chips-badge {
      background: var(--gold-light);
      border: 1px solid #fde68a;
      color: var(--gold);
      font-size: 0.72rem;
      font-weight: 700;
      padding: 0.3rem 0.55rem;
      border-radius: 20px;
      display: flex;
      align-items: center;
      gap: 3px;
    }

    .btn-action {
      font-size: 0.72rem;
      font-weight: 700;
      padding: 0.35rem 0.6rem;
      border-radius: 6px;
      border: none;
      cursor: pointer;
      display: flex;
      align-items: center;
      gap: 3px;
    }

    .btn-addcash {
      background: var(--green);
      color: #fff;
    }

    .btn-login {
      background: var(--primary);
      color: #fff;
    }

    /* Container */
    .container {
      max-width: 520px;
      margin: 0 auto;
      padding: 0.8rem;
    }

    /* Match Actions Bar */
    .action-bar {
      display: flex;
      gap: 6px;
      margin-bottom: 0.8rem;
    }

    .search-box {
      flex: 1;
      position: relative;
    }

    .search-box input {
      width: 100%;
      padding: 0.5rem 0.7rem;
      background: #fff;
      border: 1px solid var(--border);
      border-radius: 8px;
      font-size: 0.82rem;
      outline: none;
    }

    .btn-create-match {
      background: #0284c7;
      color: #fff;
      font-weight: 700;
      font-size: 0.78rem;
      padding: 0 0.8rem;
      border-radius: 8px;
      border: none;
      cursor: pointer;
      white-space: nowrap;
    }

    /* Notice Banner */
    .notice {
      background: #e0f2fe;
      border-left: 3px solid #0284c7;
      padding: 0.5rem 0.7rem;
      font-size: 0.72rem;
      color: #0369a1;
      border-radius: 4px;
      margin-bottom: 0.8rem;
    }

    /* Match List */
    .section-title {
      font-size: 0.8rem;
      font-weight: 700;
      color: var(--text-muted);
      text-transform: uppercase;
      letter-spacing: 0.5px;
      margin-bottom: 0.5rem;
      display: flex;
      justify-content: space-between;
    }

    .match-card {
      background: var(--card-bg);
      border: 1px solid var(--border);
      border-radius: 10px;
      padding: 0.8rem;
      margin-bottom: 0.6rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
      box-shadow: 0 1px 2px rgba(0,0,0,0.03);
    }

    .match-info h4 {
      font-size: 0.88rem;
      font-weight: 700;
      color: var(--text);
    }

    .match-info .entry-tag {
      font-size: 0.75rem;
      color: var(--text-muted);
      margin-top: 2px;
    }

    .room-code-pill {
      display: inline-block;
      margin-top: 4px;
      background: #f1f5f9;
      border: 1px dashed #94a3b8;
      padding: 1px 6px;
      border-radius: 4px;
      font-family: monospace;
      font-size: 0.72rem;
      font-weight: 600;
      color: #1e293b;
    }

    .match-prize {
      text-align: right;
    }

    .win-text {
      font-size: 0.95rem;
      font-weight: 800;
      color: var(--green);
    }

    .btn-play-game {
      background: var(--primary);
      color: #fff;
      border: none;
      padding: 0.35rem 0.8rem;
      border-radius: 6px;
      font-size: 0.75rem;
      font-weight: 700;
      cursor: pointer;
      margin-top: 3px;
    }

    .empty-state {
      background: var(--card-bg);
      border: 1px dashed var(--border);
      border-radius: 10px;
      padding: 2rem 1rem;
      text-align: center;
      color: var(--text-muted);
      font-size: 0.82rem;
    }

    /* Real-Time Live Logs */
    .admin-feed {
      margin-top: 1.5rem;
      background: var(--card-bg);
      border: 1px solid var(--border);
      border-radius: 10px;
      padding: 0.8rem;
    }

    .admin-feed h5 {
      font-size: 0.75rem;
      font-weight: 700;
      color: var(--text-muted);
      text-transform: uppercase;
      margin-bottom: 0.5rem;
    }

    .log-item {
      font-size: 0.72rem;
      padding: 0.35rem 0;
      border-bottom: 1px solid #f1f5f9;
      display: flex;
      justify-content: space-between;
      color: #334155;
    }

    /* Modals */
    .modal-overlay {
      display: none;
      position: fixed;
      inset: 0;
      background: rgba(15, 23, 42, 0.6);
      justify-content: center;
      align-items: center;
      z-index: 200;
      padding: 1rem;
    }

    .modal {
      background: #ffffff;
      padding: 1.2rem;
      border-radius: 12px;
      width: 100%;
      max-width: 360px;
      position: relative;
      box-shadow: 0 10px 25px rgba(0,0,0,0.1);
    }

    .modal h3 {
      font-size: 0.95rem;
      font-weight: 700;
      margin-bottom: 0.8rem;
      color: var(--text);
    }

    .btn-close {
      position: absolute;
      top: 0.8rem;
      right: 0.9rem;
      background: none;
      border: none;
      font-size: 1.2rem;
      cursor: pointer;
      color: var(--text-muted);
    }

    .form-group {
      margin-bottom: 0.7rem;
    }

    .form-group label {
      display: block;
      font-size: 0.72rem;
      font-weight: 600;
      color: var(--text-muted);
      margin-bottom: 0.2rem;
    }

    .form-group input {
      width: 100%;
      padding: 0.55rem;
      border: 1px solid var(--border);
      border-radius: 6px;
      font-size: 0.82rem;
      outline: none;
    }

    .btn-submit {
      width: 100%;
      padding: 0.6rem;
      border: none;
      border-radius: 6px;
      font-weight: 700;
      font-size: 0.82rem;
      cursor: pointer;
      margin-top: 0.4rem;
    }

    /* UPI QR Display */
    .qr-card {
      background: #f8fafc;
      border: 1px solid var(--border);
      border-radius: 8px;
      padding: 0.8rem;
      text-align: center;
      margin-bottom: 0.8rem;
    }

    .qr-card img {
      width: 150px;
      height: 150px;
      display: block;
      margin: 0 auto;
      border-radius: 6px;
    }

    .upi-tag {
      font-size: 0.78rem;
      font-weight: 700;
      color: var(--text);
      margin-top: 0.4rem;
      background: #e2e8f0;
      display: inline-block;
      padding: 2px 8px;
      border-radius: 4px;
    }
  </style>
</head>
<body>

  <!-- Header -->
  <header>
    <div class="logo-box">
      <span style="font-size: 1.1rem;">🌾</span>
      <span class="logo-text">GRAIN ADDA</span>
    </div>

    <div class="header-actions">
      <!-- Real-time Chips / Balance -->
      <div class="chips-badge">
        🪙 <span id="chipsBalance">0</span> Chips
      </div>
      <button class="btn-action btn-addcash" onclick="openModal('cashModal')">+ Cash</button>
      <button class="btn-action btn-login" id="loginHeaderBtn" onclick="openModal('authModal')">Login</button>
    </div>
  </header>

  <div class="container">
    <!-- Notice -->
    <div class="notice">
      ⚡ <strong>Real-Time Mode Active:</strong> केवल लाइव खिलाड़ियों के बनाए मैच ही यहाँ दिखेंगे।
    </div>

    <!-- Match Actions -->
    <div class="action-bar">
      <div class="search-box">
        <input type="number" id="filterInput" placeholder="🔍 Search Amount (₹50, 100...)" oninput="filterMatches()">
      </div>
      <button class="btn-create-match" onclick="openCreateMatch()">+ Create Match</button>
    </div>

    <!-- Live Matches Heading -->
    <div class="section-title">
      <span>Live Challenges</span>
      <span id="matchStats">0 Available</span>
    </div>

    <!-- Matches List Container -->
    <div id="matchContainer">
      <div class="empty-state">
        लोड हो रहा है... या अभी कोई मैच नहीं है।<br>
        <strong>+ Create Match</strong> पर क्लिक करके नया मैच बनाएं!
      </div>
    </div>

    <!-- Real-time Activity / Admin Stream -->
    <div class="admin-feed">
      <h5>⚡ Live Network Activity</h5>
      <div id="logStream">
        <div class="log-item"><span>Platform Synced</span><span>Live</span></div>
      </div>
    </div>
  </div>

  <!-- Modal 1: Login -->
  <div class="modal-overlay" id="authModal">
    <div class="modal">
      <button class="btn-close" onclick="closeModal('authModal')">&times;</button>
      <h3>Player Login / Profile</h3>
      <div class="form-group">
        <label>Player Name</label>
        <input type="text" id="playerName" placeholder="Enter your display name">
      </div>
      <div class="form-group">
        <label>Mobile Number</label>
        <input type="tel" id="playerMobile" placeholder="10-digit number" maxlength="10">
      </div>
      <button class="btn-submit" style="background: var(--primary); color: #fff;" onclick="handleLogin()">Save & Login</button>
    </div>
  </div>

  <!-- Modal 2: Create Match -->
  <div class="modal-overlay" id="matchModal">
    <div class="modal">
      <button class="btn-close" onclick="closeModal('matchModal')">&times;</button>
      <h3>Create Ludo Challenge</h3>
      <div class="form-group">
        <label>Entry Fee (Chips / ₹)</label>
        <input type="number" id="entryFee" placeholder="e.g. 50, 100, 250">
      </div>
      <div class="form-group">
        <label>Ludo King Room Code</label>
        <input type="text" id="roomCode" placeholder="Enter 8-digit Room Code">
      </div>
      <button class="btn-submit" style="background: #0284c7; color: #fff;" onclick="publishMatch()">Post Challenge</button>
    </div>
  </div>

  <!-- Modal 3: Deposit with UPI QR -->
  <div class="modal-overlay" id="cashModal">
    <div class="modal">
      <button class="btn-close" onclick="closeModal('cashModal')">&times;</button>
      <h3>Add Cash / Deposit Chips</h3>

      <div class="qr-card">
        <!-- Direct QR code for 8094385548@axl -->
        <img src="https://api.qrserver.com/v1/create-qr-code/?size=150x150&data=upi://pay?pa=8094385548@axl&pn=GrainAdda" alt="UPI QR">
        <div class="upi-tag">UPI: 8094385548@axl</div>
      </div>

      <div class="form-group">
        <label>Amount Paid (₹)</label>
        <input type="number" id="cashAmount" placeholder="Enter amount (e.g. 100)">
      </div>
      <div class="form-group">
        <label>12-Digit UTR / Transaction Ref</label>
        <input type="text" id="utrRef" placeholder="Enter UTR from PhonePe/GPay">
      </div>
      <button class="btn-submit" style="background: var(--green); color: #fff;" onclick="handleDeposit()">Submit Deposit</button>
    </div>
  </div>

  <script>
    // 1. Firebase Config for Free Real-Time Sync across multiple phones
    const firebaseConfig = {
      databaseURL: "https://grain-adda-live-default-rtdb.firebaseio.com/"
    };
    
    let db = null;
    try {
      firebase.initializeApp(firebaseConfig);
      db = firebase.database();
    } catch(e) {
      console.log("Offline mode fallback");
    }

    // Local State
    let user = JSON.parse(localStorage.getItem('grain_session')) || null;
    let localMatches = [];

    window.onload = function() {
      updateUserHeader();
      startRealtimeSync();
    };

    function openModal(id) { document.getElementById(id).style.display = 'flex'; }
    function closeModal(id) { document.getElementById(id).style.display = 'none'; }

    // User Authentication
    function handleLogin() {
      const name = document.getElementById('playerName').value.trim();
      const mobile = document.getElementById('playerMobile').value.trim();

      if (!name || mobile.length !== 10) {
        alert("कृपया सही नाम और 10-अंकों का मोबाइल नंबर भरें!");
        return;
      }

      user = { name, mobile, chips: 0 };
      localStorage.setItem('grain_session', JSON.stringify(user));
      updateUserHeader();
      closeModal('authModal');
      broadcastLog(`Player Joined: ${name}`);

      // Sync user to cloud
      if(db) db.ref('users/' + mobile).set(user);
    }

    function updateUserHeader() {
      const loginBtn = document.getElementById('loginHeaderBtn');
      const chipsEl = document.getElementById('chipsBalance');

      if (user) {
        loginBtn.innerText = user.name.slice(0, 6) + "✓";
        chipsEl.innerText = user.chips || 0;
      } else {
        loginBtn.innerText = "Login";
        chipsEl.innerText = "0";
      }
    }

    // Open Match Creation Check
    function openCreateMatch() {
      if (!user) {
        alert("मैच बनाने के लिए पहले Login करें!");
        openModal('authModal');
        return;
      }
      openModal('matchModal');
    }

    // Create & Publish Match to Cloud
    function publishMatch() {
      const fee = parseInt(document.getElementById('entryFee').value);
      const code = document.getElementById('roomCode').value.trim();

      if (!fee || fee <= 0 || !code) {
        alert("कृपया सही अमाउंट और Ludo Room Code दोनों दर्ज करें!");
        return;
      }

      const matchId = 'm_' + Date.now();
      const matchData = {
        id: matchId,
        host: user.name,
        mobile: user.mobile,
        amount: fee,
        prize: Math.floor(fee * 1.8),
        roomCode: code,
        timestamp: Date.now()
      };

      if (db) {
        db.ref('matches/' + matchId).set(matchData);
      } else {
        localMatches.unshift(matchData);
        renderMatchCards(localMatches);
      }

      broadcastLog(`Match Created: ₹${fee} by ${user.name}`);
      closeModal('matchModal');
      document.getElementById('entryFee').value = '';
      document.getElementById('roomCode').value = '';
    }

    // Realtime Sync Listener (works across all phones)
    function startRealtimeSync() {
      if (!db) return;

      db.ref('matches').on('value', (snapshot) => {
        const data = snapshot.val();
        localMatches = [];
        if (data) {
          Object.keys(data).forEach(k => localMatches.unshift(data[k]));
        }
        renderMatchCards(localMatches);
      });

      db.ref('activity').limitToLast(5).on('value', (snapshot) => {
        const stream = document.getElementById('logStream');
        stream.innerHTML = '';
        const data = snapshot.val();
        if (data) {
          Object.keys(data).forEach(k => {
            const item = document.createElement('div');
            item.className = 'log-item';
            item.innerHTML = `<span>${data[k].text}</span><span>${data[k].time}</span>`;
            stream.prepend(item);
          });
        }
      });
    }

    // Render Function
    function renderMatchCards(list) {
      const container = document.getElementById('matchContainer');
      const stats = document.getElementById('matchStats');
      const filter = document.getElementById('filterInput').value.trim();

      let displayList = list;
      if (filter) {
        displayList = list.filter(m => m.amount.toString().includes(filter));
      }

      stats.innerText = `${displayList.length} Available`;

      if (displayList.length === 0) {
        container.innerHTML = `
          <div class="empty-state">
            अभी कोई लाइव मैच नहीं है।<br>
            <strong>+ Create Match</strong> दबाकर पहला मैच आप ही बनाएं!
          </div>
        `;
        return;
      }

      container.innerHTML = '';
      displayList.forEach(m => {
        const card = document.createElement('div');
        card.className = 'match-card';
        card.innerHTML = `
          <div class="match-info">
            <h4>Host: ${m.host}</h4>
            <div class="entry-tag">Entry: <strong>₹${m.amount} Chips</strong></div>
            <div class="room-code-pill">Room Code: ${m.roomCode}</div>
          </div>
          <div class="match-prize">
            <div class="win-text">Win: ₹${m.prize}</div>
            <button class="btn-play-game" onclick="joinGameCode('${m.roomCode}', ${m.amount})">Play / Join</button>
          </div>
        `;
        container.appendChild(card);
      });
    }

    function filterMatches() {
      renderMatchCards(localMatches);
    }

    function joinGameCode(code, amt) {
      if (!user) {
        alert("जॉइन करने के लिए पहले Login करें!");
        openModal('authModal');
        return;
      }
      navigator.clipboard.writeText(code).then(() => {
        alert(`Room Code [${code}] कॉपी हो गया है!\nLudo King ऐप में जाकर तुरंत पेस्ट करें।`);
      }).catch(() => {
        alert("Ludo Room Code: " + code);
      });
      broadcastLog(`${user.name} joined match for ₹${amt}`);
    }

    // Deposit Chips via UPI
    function handleDeposit() {
      const amt = parseInt(document.getElementById('cashAmount').value);
      const utr = document.getElementById('utrRef').value.trim();

      if (!amt || !utr || utr.length < 4) {
        alert("कृपया सही अमाउंट और UTR नंबर भरें!");
        return;
      }

      if (user) {
        user.chips = (user.chips || 0) + amt;
        localStorage.setItem('grain_session', JSON.stringify(user));
        updateUserHeader();
      }

      broadcastLog(`Deposit: +₹${amt} (UTR: ${utr.slice(-4)})`);
      alert(`₹${amt} के चिप्स ऐड करने की रिक्वेस्ट दर्ज हो गई है!`);
      closeModal('cashModal');
      document.getElementById('cashAmount').value = '';
      document.getElementById('utrRef').value = '';
    }

    function broadcastLog(text) {
      const time = new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
      if (db) {
        db.ref('activity').push({ text, time });
      }
    }
  </script>
</body>
</html>
