<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Apex Gaming & Exchange Control Panel</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@400;600&display=swap" rel="stylesheet">
  <style>
    body { font-family: 'Outfit', sans-serif; background: #0b0f19; }
    .mono { font-family: 'JetBrains Mono', monospace; }
    .gold-gradient {
      background: linear-gradient(135deg, #f59e0b 0%, #fbbf24 50%, #d97706 100%);
    }
    .hero-gradient {
      background: radial-gradient(circle at 10% 20%, rgba(30, 58, 138, 0.8) 0%, rgba(15, 23, 42, 0.95) 50%, rgba(11, 15, 25, 1) 100%);
    }
    .glass-card {
      background: rgba(17, 24, 39, 0.7);
      backdrop-filter: blur(12px);
      border: 1px solid rgba(255, 255, 255, 0.08);
    }
    .custom-scrollbar::-webkit-scrollbar { width: 5px; height: 5px; }
    .custom-scrollbar::-webkit-scrollbar-track { background: #0f172a; }
    .custom-scrollbar::-webkit-scrollbar-thumb { background: #334155; border-radius: 4px; }
    .custom-scrollbar::-webkit-scrollbar-thumb:hover { background: #f59e0b; }
  </style>
</head>
<body class="text-slate-100 min-h-screen flex flex-col selection:bg-amber-500 selection:text-black">

  <div id="app" class="flex flex-col min-h-screen">
    
    <!-- Top Glowing / Shining Banner -->
    <header class="hero-gradient border-b border-amber-500/30 px-6 py-4 sticky top-0 z-50 shadow-2xl relative overflow-hidden">
      <div class="absolute -top-10 -left-10 w-48 h-48 bg-amber-500/20 rounded-full blur-3xl pointer-events-none"></div>
      <div class="absolute top-0 right-1/4 w-60 h-20 bg-cyan-500/20 rounded-full blur-3xl pointer-events-none"></div>

      <div class="max-w-7xl mx-auto flex flex-wrap justify-between items-center gap-4 relative z-10">
        <div class="flex items-center gap-4">
          <div class="w-12 h-12 rounded-xl gold-gradient flex items-center justify-center shadow-lg shadow-amber-500/30 ring-2 ring-amber-300/50">
            <i class="fa-solid fa-crown text-slate-950 text-2xl"></i>
          </div>
          <div>
            <div class="flex items-center gap-2">
              <h1 class="text-2xl font-extrabold tracking-wider bg-clip-text text-transparent bg-gradient-to-r from-amber-300 via-amber-100 to-amber-500">
                ROYAL APEX MASTER PANEL
              </h1>
              <span class="text-[10px] bg-emerald-500/20 text-emerald-400 border border-emerald-500/40 px-2 py-0.5 rounded-full font-bold uppercase tracking-widest animate-pulse">
                ● Live Seamless Sync
              </span>
            </div>
            <p class="text-xs text-slate-300 font-medium">एडवांस्ड रिस्क मैनेजमेंट, लाइव गेम्स इंटीग्रेशन और ऑटो-वॉलेट सिंक इंजन</p>
          </div>
        </div>

        <!-- Quick Summary Stats on Top -->
        <div class="flex items-center gap-3">
          <div class="glass-card px-4 py-2 rounded-xl border border-amber-500/30">
            <span class="text-[11px] text-slate-400 block font-medium">सुपर एडमिन पूल फंड</span>
            <span class="text-xl font-black text-amber-400 mono">₹{{ adminBalance.toLocaleString() }}</span>
          </div>
          <div class="glass-card px-4 py-2 rounded-xl border border-red-500/30">
            <span class="text-[11px] text-slate-400 block font-medium">लाइव रिस्क / एक्सपोज़र</span>
            <span class="text-xl font-black text-rose-400 mono">₹{{ totalExposure.toLocaleString() }}</span>
          </div>
          <div class="glass-card px-4 py-2 rounded-xl border border-emerald-500/30">
            <span class="text-[11px] text-slate-400 block font-medium">नेट हाउस प्रॉफ़िट (P&L)</span>
            <span class="text-xl font-black text-emerald-400 mono">+₹{{ totalProfitLoss.toLocaleString() }}</span>
          </div>
        </div>
      </div>
    </header>

    <!-- Navigation Tabs -->
    <div class="bg-slate-900/90 border-b border-slate-800 px-6 py-2.5">
      <div class="max-w-7xl mx-auto flex flex-wrap gap-2">
        <button @click="currentTab = 'dashboard'" :class="currentTab === 'dashboard' ? 'gold-gradient text-slate-950 font-bold shadow-md' : 'text-slate-400 hover:text-white bg-slate-800/60'" class="px-4 py-2 rounded-lg text-sm transition flex items-center gap-2">
          <i class="fa-solid fa-chart-pie"></i> डैशबोर्ड और डाउनलाइन
        </button>
        <button @click="currentTab = 'games'" :class="currentTab === 'games' ? 'gold-gradient text-slate-950 font-bold shadow-md' : 'text-slate-400 hover:text-white bg-slate-800/60'" class="px-4 py-2 rounded-lg text-sm transition flex items-center gap-2">
          <i class="fa-solid fa-gamepad text-emerald-400"></i> गेम इंटीग्रेशन व लॉबी (Live Connect)
        </button>
        <button @click="currentTab = 'settlement'" :class="currentTab === 'settlement' ? 'gold-gradient text-slate-950 font-bold shadow-md' : 'text-slate-400 hover:text-white bg-slate-800/60'" class="px-4 py-2 rounded-lg text-sm transition flex items-center gap-2">
          <i class="fa-solid fa-calculator"></i> वीकली सेटलमेंट और P&L
        </button>
        <button @click="currentTab = 'livebets'" :class="currentTab === 'livebets' ? 'gold-gradient text-slate-950 font-bold shadow-md' : 'text-slate-400 hover:text-white bg-slate-800/60'" class="px-4 py-2 rounded-lg text-sm transition flex items-center gap-2">
          <i class="fa-solid fa-satellite-dish"></i> लाइव बेट्स रडार
        </button>
      </div>
    </div>

    <!-- Main Workspace -->
    <main class="max-w-7xl mx-auto w-full p-6 flex-1 space-y-6">

      <!-- TAB 1: DASHBOARD & ACCOUNTS -->
      <div v-if="currentTab === 'dashboard'" class="grid grid-cols-1 lg:grid-cols-3 gap-6">

        <!-- Left Controls -->
        <div class="space-y-6">
          
          <!-- ID Generator Card -->
          <div class="glass-card rounded-2xl p-5 shadow-xl border border-slate-700/60">
            <div class="flex items-center gap-2 border-b border-slate-700/80 pb-3 mb-4">
              <i class="fa-solid fa-id-card-clip text-amber-400 text-lg"></i>
              <h2 class="text-base font-bold text-white">नई डाउनलाइन ID बनाएं</h2>
            </div>
            
            <form @submit.prevent="createAccount" class="space-y-3">
              <div>
                <label class="text-xs text-slate-400 block mb-1">यूज़रनेम / क्लाइंट कोड</label>
                <input v-model="form.username" type="text" placeholder="e.g. Master_Jaipur_99" required
                  class="w-full bg-slate-900 border border-slate-700 rounded-xl px-3 py-2 text-sm text-slate-200 focus:outline-none focus:border-amber-400 transition">
              </div>
              <div>
                <label class="text-xs text-slate-400 block mb-1">पासवर्ड</label>
                <input v-model="form.password" type="password" placeholder="••••••••" required
                  class="w-full bg-slate-900 border border-slate-700 rounded-xl px-3 py-2 text-sm text-slate-200 focus:outline-none focus:border-amber-400 transition">
              </div>
              <div class="grid grid-cols-2 gap-3">
                <div>
                  <label class="text-xs text-slate-400 block mb-1">रोल पदानुक्रम</label>
                  <select v-model="form.role" class="w-full bg-slate-900 border border-slate-700 rounded-xl px-3 py-2 text-sm text-slate-200 focus:outline-none focus:border-amber-400">
                    <option value="Super Master">Super Master</option>
                    <option value="Master">Master</option>
                    <option value="Client">Client / User</option>
                  </select>
                </div>
                <div>
                  <label class="text-xs text-slate-400 block mb-1">शेयरिंग / पार्टनरशिप %</label>
                  <input v-model.number="form.sharePercent" type="number" min="0" max="100" placeholder="%"
                    class="w-full bg-slate-900 border border-slate-700 rounded-xl px-3 py-2 text-sm text-slate-200 focus:outline-none focus:border-amber-400">
                </div>
              </div>
              <div class="grid grid-cols-2 gap-3">
                <div>
                  <label class="text-xs text-slate-400 block mb-1">क्रेडिट लिमिट (₹)</label>
                  <input v-model.number="form.creditLimit" type="number" placeholder="50,000"
                    class="w-full bg-slate-900 border border-slate-700 rounded-xl px-3 py-2 text-sm text-slate-200 focus:outline-none focus:border-amber-400">
                </div>
                <div>
                  <label class="text-xs text-slate-400 block mb-1">मैक्स बेट लिमिट (₹)</label>
                  <input v-model.number="form.maxBetLimit" type="number" placeholder="10,000"
                    class="w-full bg-slate-900 border border-slate-700 rounded-xl px-3 py-2 text-sm text-slate-200 focus:outline-none focus:border-amber-400">
                </div>
              </div>
              <button type="submit" class="w-full gold-gradient hover:brightness-110 text-slate-950 font-extrabold py-2.5 rounded-xl text-sm transition shadow-lg shadow-amber-500/20 mt-2">
                आईडी एक्टिवेट करें
              </button>
            </form>
          </div>

          <!-- Quick Chip Transfer -->
          <div class="glass-card rounded-2xl p-5 shadow-xl border border-slate-700/60">
            <div class="flex items-center gap-2 border-b border-slate-700/80 pb-3 mb-4">
              <i class="fa-solid fa-bolt text-emerald-400 text-lg"></i>
              <h2 class="text-base font-bold text-white">फास्ट क्रेडिट / चिप ट्रांसफर</h2>
            </div>
            
            <form @submit.prevent="transferChips" class="space-y-3">
              <div>
                <label class="text-xs text-slate-400 block mb-1">खाता सेलेक्ट करें</label>
                <select v-model="transfer.userId" required class="w-full bg-slate-900 border border-slate-700 rounded-xl px-3 py-2 text-sm text-slate-200 focus:outline-none focus:border-amber-400">
                  <option value="" disabled>-- खाता चुनें --</option>
                  <option v-for="user in accounts" :key="user.id" :value="user.id">
                    {{ user.username }} ({{ user.role }}) - बैलेंस: ₹{{ user.balance.toLocaleString() }}
                  </option>
                </select>
              </div>
              <div class="grid grid-cols-2 gap-3">
                <div>
                  <label class="text-xs text-slate-400 block mb-1">चिप्स रकम (₹)</label>
                  <input v-model.number="transfer.amount" type="number" min="1" placeholder="₹ Amount" required
                    class="w-full bg-slate-900 border border-slate-700 rounded-xl px-3 py-2 text-sm text-slate-200 focus:outline-none focus:border-amber-400">
                </div>
                <div>
                  <label class="text-xs text-slate-400 block mb-1">एक्शन</label>
                  <select v-model="transfer.type" class="w-full bg-slate-900 border border-slate-700 rounded-xl px-3 py-2 text-sm text-slate-200 focus:outline-none focus:border-amber-400">
                    <option value="deposit">डिपॉज़िट (+)</option>
                    <option value="withdraw">विथड्रॉ (-)</option>
                  </select>
                </div>
              </div>
              <button type="submit" class="w-full bg-emerald-600 hover:bg-emerald-500 text-white font-bold py-2.5 rounded-xl text-sm transition shadow-lg shadow-emerald-600/20">
                तुरंत प्रोसेस करें
              </button>
            </form>
          </div>

        </div>

        <!-- Right Side: Accounts Table & Quick Search -->
        <div class="lg:col-span-2 space-y-6">
          <div class="glass-card rounded-2xl p-5 shadow-xl border border-slate-700/60">
            <div class="flex flex-wrap justify-between items-center gap-3 border-b border-slate-700/80 pb-4 mb-4">
              <div>
                <h2 class="text-base font-bold text-white flex items-center gap-2">
                  <i class="fa-solid fa-users text-amber-400"></i> डाउनलाइन व क्लाइंट नेटवर्क
                </h2>
                <span class="text-xs text-slate-400">कुल सक्रिय आईडी: {{ accounts.length }} | फ़िल्टर और रिस्क लिमिट्स</span>
              </div>
              <div class="flex items-center gap-2">
                <input v-model="searchQuery" type="text" placeholder="सर्च आईडी..." 
                  class="bg-slate-900 border border-slate-700 rounded-lg px-3 py-1.5 text-xs text-slate-200 focus:outline-none focus:border-amber-400">
              </div>
            </div>

            <!-- Table -->
            <div class="overflow-x-auto custom-scrollbar">
              <table class="w-full text-left text-sm">
                <thead class="bg-slate-950/80 text-slate-400 text-xs uppercase tracking-wider">
                  <tr>
                    <th class="py-3 px-3">अकाउंट आईडी</th>
                    <th class="py-3 px-3">रोल / शेयर %</th>
                    <th class="py-3 px-3">बैलेंस</th>
                    <th class="py-3 px-3">एक्सपोज़र</th>
                    <th class="py-3 px-3">बेट लॉक</th>
                    <th class="py-3 px-3">स्टेटस</th>
                    <th class="py-3 px-3 text-center">एक्शन</th>
                  </tr>
                </thead>
                <tbody class="divide-y divide-slate-800">
                  <tr v-for="user in filteredAccounts" :key="user.id" class="hover:bg-slate-800/40 transition">
                    <td class="py-3 px-3 font-bold text-amber-300">
                      {{ user.username }}
                      <span class="text-[10px] text-slate-500 block">ID: #{{ user.id }}</span>
                    </td>
                    <td class="py-3 px-3">
                      <span class="bg-slate-800 border border-slate-700 text-slate-300 text-xs px-2 py-0.5 rounded font-medium">
                        {{ user.role }}
                      </span>
                      <span class="text-[11px] text-amber-400/80 block mt-0.5 font-bold">{{ user.sharePercent }}% शेयर</span>
                    </td>
                    <td class="py-3 px-3 font-semibold text-emerald-400 mono">₹{{ user.balance.toLocaleString() }}</td>
                    <td class="py-3 px-3 font-semibold text-rose-400 mono">₹{{ user.exposure.toLocaleString() }}</td>
                    <td class="py-3 px-3">
                      <button @click="toggleBetLock(user)" :class="user.betLocked ? 'bg-rose-500/20 text-rose-400 border border-rose-500/40' : 'bg-slate-800 text-slate-400 border border-slate-700'" class="text-[11px] px-2 py-1 rounded font-medium transition">
                        <i :class="user.betLocked ? 'fa-solid fa-lock' : 'fa-solid fa-unlock'"></i> {{ user.betLocked ? 'Locked' : 'Open' }}
                      </button>
                    </td>
                    <td class="py-3 px-3">
                      <span :class="user.status === 'Active' ? 'bg-emerald-950 text-emerald-400 border border-emerald-800' : 'bg-rose-950 text-rose-400 border border-rose-800'" class="text-xs px-2 py-0.5 rounded font-medium">
                        {{ user.status }}
                      </span>
                    </td>
                    <td class="py-3 px-3 text-center space-x-1">
                      <button @click="toggleAccountStatus(user)" class="text-xs bg-slate-800 hover:bg-slate-700 px-2.5 py-1 rounded border border-slate-700 transition">
                        {{ user.status === 'Active' ? 'सस्पेंड' : 'एक्टिव' }}
                      </button>
                      <button @click="openGameAsUser(user)" class="text-xs bg-emerald-500/20 text-emerald-300 hover:bg-emerald-500/30 border border-emerald-500/40 px-2.5 py-1 rounded transition">
                        गेम खेलें
                      </button>
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>

          <!-- Live Ledger Stream -->
          <div class="glass-card rounded-2xl p-5 shadow-xl border border-slate-700/60">
            <h2 class="text-base font-bold text-white flex items-center gap-2 border-b border-slate-700/80 pb-3 mb-4">
              <i class="fa-solid fa-receipt text-cyan-400"></i> रियल-टाइम वॉलेट ऑडिट लेज़र (Live Sync Feed)
            </h2>
            <div class="overflow-x-auto max-h-56 overflow-y-auto custom-scrollbar">
              <table class="w-full text-left text-xs">
                <thead class="bg-slate-950 text-slate-400 uppercase sticky top-0">
                  <tr>
                    <th class="py-2 px-3">टाइम</th>
                    <th class="py-2 px-3">खाता</th>
                    <th class="py-2 px-3">ट्रांजेक्शन प्रकार</th>
                    <th class="py-2 px-3">रकम</th>
                    <th class="py-2 px-3">रिमार्क्स</th>
                  </tr>
                </thead>
                <tbody class="divide-y divide-slate-800">
                  <tr v-for="log in ledgerLogs" :key="log.id">
                    <td class="py-2 px-3 text-slate-400 mono">{{ log.time }}</td>
                    <td class="py-2 px-3 font-semibold text-slate-200">{{ log.username }}</td>
                    <td class="py-2 px-3">
                      <span :class="log.type.includes('डिपॉज़िट') || log.type.includes('जीता') ? 'text-emerald-400' : (log.type.includes('विथड्रॉ') ? 'text-amber-400' : 'text-rose-400')" class="font-bold">
                        {{ log.type }}
                      </span>
                    </td>
                    <td class="py-2 px-3 font-bold mono">₹{{ log.amount.toLocaleString() }}</td>
                    <td class="py-2 px-3 text-slate-400">{{ log.remarks }}</td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>

      </div>

      <!-- TAB 2: GAME INTEGRATION & LIVE ARENA -->
      <div v-if="currentTab === 'games'" class="space-y-6">
        
        <!-- Add New Game by Link Section -->
        <div class="glass-card rounded-2xl p-5 shadow-xl border border-slate-700/60">
          <div class="flex items-center gap-2 border-b border-slate-700/80 pb-3 mb-4">
            <i class="fa-solid fa-link text-amber-400 text-lg"></i>
            <div>
              <h2 class="text-base font-bold text-white">नया गेम लिंक / URL जोड़ें (Add Game Link)</h2>
              <p class="text-xs text-slate-400">किसी भी वेब-बेस्ड गेम (HTML5, iFrame URL, कसीनो लिंक) को सीधे पैनल में मैप करें</p>
            </div>
          </div>
          <form @submit.prevent="addGameByLink" class="grid grid-cols-1 md:grid-cols-4 gap-4">
            <div>
              <label class="text-xs text-slate-400 block mb-1">गेम का नाम</label>
              <input v-model="newGame.name" type="text" placeholder="e.g. Aviator Pro, Live Teen Patti" required
                class="w-full bg-slate-900 border border-slate-700 rounded-xl px-3 py-2 text-sm text-slate-200 focus:outline-none focus:border-amber-400 transition">
            </div>
            <div>
              <label class="text-xs text-slate-400 block mb-1">कैटेगरी</label>
              <select v-model="newGame.category" class="w-full bg-slate-900 border border-slate-700 rounded-xl px-3 py-2 text-sm text-slate-200 focus:outline-none focus:border-amber-400">
                <option value="Live Casino">Live Casino</option>
                <option value="Sports Exchange">Sports Exchange</option>
                <option value="Crash Game">Crash Game / Aviator</option>
                <option value="Card Game">Card Game (Teen Patti/Andar Bahar)</option>
              </select>
            </div>
            <div>
              <label class="text-xs text-slate-400 block mb-1">गेम का URL / लिंक</label>
              <input v-model="newGame.url" type="url" placeholder="https://example-game.com/play" required
                class="w-full bg-slate-900 border border-slate-700 rounded-xl px-3 py-2 text-sm text-slate-200 focus:outline-none focus:border-amber-400 transition">
            </div>
            <div class="flex items-end">
              <button type="submit" class="w-full gold-gradient hover:brightness-110 text-slate-950 font-bold py-2.5 rounded-xl text-sm transition shadow-lg shadow-amber-500/20">
                <i class="fa-solid fa-plus mr-1"></i> गेम ऐड करें
              </button>
            </div>
          </form>
        </div>

        <!-- Integrated Games Lobby -->
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
          <div v-for="game in integratedGames" :key="game.id" class="glass-card rounded-2xl p-5 border border-slate-700/60 relative overflow-hidden flex flex-col justify-between">
            <div>
              <div class="flex justify-between items-start mb-3">
                <span class="text-xs bg-slate-800 text-amber-400 border border-slate-700 px-2.5 py-1 rounded-full font-semibold">
                  {{ game.category }}
                </span>
                <span :class="game.status === 'Live' ? 'text-emerald-400 bg-emerald-500/10 border-emerald-500/30' : 'text-slate-400 bg-slate-800 border-slate-700'" class="text-xs border px-2 py-0.5 rounded-full font-bold">
                  ● {{ game.status }}
                </span>
              </div>
              <h3 class="text-lg font-bold text-white mb-1">{{ game.name }}</h3>
              <p class="text-xs text-slate-400 truncate mb-4 font-mono">{{ game.url }}</p>
            </div>

            <div class="space-y-3 pt-3 border-t border-slate-800">
              <div class="flex justify-between text-xs text-slate-400">
                <span>एक्टिव खिलाड़ी: <strong class="text-white">{{ game.activePlayers }}</strong></span>
                <span>टर्नओवर: <strong class="text-emerald-400 mono">₹{{ game.turnover.toLocaleString() }}</strong></span>
              </div>
              <button @click="launchGameModal(game)" class="w-full bg-gradient-to-r from-emerald-600 to-teal-600 hover:from-emerald-500 hover:to-teal-500 text-white font-bold py-2 rounded-xl text-xs transition shadow-lg">
                <i class="fa-solid fa-play mr-1"></i> लाइव सिम्युलेटर खोलें (Auto Sync)
              </button>
            </div>
          </div>
        </div>

        <!-- Live Interactive Game Frame & Seamless Sync Test -->
        <div v-if="activeGameSession" class="glass-card rounded-2xl p-6 border-2 border-amber-500/50 relative shadow-2xl">
          <div class="flex flex-wrap justify-between items-center border-b border-slate-700/80 pb-4 mb-4 gap-2">
            <div class="flex items-center gap-3">
              <div class="w-3 h-3 rounded-full bg-emerald-400 animate-ping"></div>
              <div>
                <h3 class="text-lg font-extrabold text-amber-400">{{ activeGameSession.name }}</h3>
                <span class="text-xs text-slate-300">एक्टिव खिलाड़ी: <strong>{{ activeUserForGame.username }}</strong> | वॉलेट बैलेंस: <strong class="text-emerald-400 mono">₹{{ activeUserForGame.balance.toLocaleString() }}</strong></span>
              </div>
            </div>
            <button @click="activeGameSession = null" class="bg-rose-600/80 hover:bg-rose-500 text-white text-xs px-3 py-1.5 rounded-lg transition font-bold">
              बंद करें (Close Arena)
            </button>
          </div>

          <!-- Game Simulation & Real-time Bet Engine -->
          <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
            <div class="lg:col-span-2 bg-slate-950 rounded-xl border border-slate-800 p-4 min-h-[350px] flex flex-col justify-between relative overflow-hidden">
              <div class="text-center my-auto space-y-3">
                <i class="fa-solid fa-dice text-6xl text-amber-400 animate-bounce"></i>
                <h4 class="text-xl font-bold text-white">{{ activeGameSession.name }} Live Window</h4>
                <p class="text-xs text-slate-400 max-w-md mx-auto">
                  यह गेम पैनल के साथ <strong>Seamless Wallet API</strong> द्वारा रियल-टाइम जुड़ा हुआ है। यहाँ लगाया गया कोई भी दांव सीधे पैनल के मुख्य वॉलेट और लेज़र से ऑटोमैटिक कटेगा और जुड़ेगा।
                </p>
                <div class="inline-block bg-slate-900 border border-slate-700 px-4 py-2 rounded-xl text-xs mono text-cyan-300">
                  Target URL: {{ activeGameSession.url }}
                </div>
              </div>
              <div class="text-xs text-slate-500 flex justify-between border-t border-slate-800/80 pt-2">
                <span>Webhook Engine: Active (200 OK)</span>
                <span>Latency: 24ms</span>
              </div>
            </div>

            <!-- In-Game Real-Time Betting Terminal -->
            <div class="bg-slate-900/90 rounded-xl border border-slate-800 p-5 space-y-4 flex flex-col justify-between">
              <div>
                <h4 class="text-sm font-bold text-white border-b border-slate-800 pb-2 mb-3">
                  गेम एक्शन सिमुलेटर (Test Seamless Sync)
                </h4>
                <div class="space-y-3">
                  <div>
                    <label class="text-xs text-slate-400 block mb-1">दांव रकम (Stake)</label>
                    <div class="grid grid-cols-3 gap-2">
                      <button @click="inGameStake = 500" :class="inGameStake === 500 ? 'bg-amber-500 text-slate-950 font-bold' : 'bg-slate-800 text-slate-300'" class="py-1 rounded text-xs">₹500</button>
                      <button @click="inGameStake = 1000" :class="inGameStake === 1000 ? 'bg-amber-500 text-slate-950 font-bold' : 'bg-slate-800 text-slate-300'" class="py-1 rounded text-xs">₹1,000</button>
                      <button @click="inGameStake = 5000" :class="inGameStake === 5000 ? 'bg-amber-500 text-slate-950 font-bold' : 'bg-slate-800 text-slate-300'" class="py-1 rounded text-xs">₹5,000</button>
                    </div>
                  </div>
                  <div>
                    <label class="text-xs text-slate-400 block mb-1">मैनुअल रकम (₹)</label>
                    <input v-model.number="inGameStake" type="number" min="100" class="w-full bg-slate-950 border border-slate-700 rounded-lg px-3 py-1.5 text-xs text-slate-200 mono">
                  </div>
                </div>
              </div>

              <div class="space-y-2">
                <button @click="processLiveGameResult('win')" class="w-full bg-emerald-600 hover:bg-emerald-500 text-white font-bold py-2.5 rounded-xl text-xs transition shadow-lg flex items-center justify-center gap-2">
                  <i class="fa-solid fa-trophy"></i> खिलाड़ी जीता (Win Bet - 2x Return)
                </button>
                <button @click="processLiveGameResult('loss')" class="w-full bg-rose-600 hover:bg-rose-500 text-white font-bold py-2.5 rounded-xl text-xs transition shadow-lg flex items-center justify-center gap-2">
                  <i class="fa-solid fa-skull"></i> खिलाड़ी हारा (Loss Bet - House Wins)
                </button>
              </div>
            </div>
          </div>
        </div>

      </div>

      <!-- TAB 3: SETTLEMENT & P&L SHEET -->
      <div v-if="currentTab === 'settlement'" class="space-y-6">
        <div class="glass-card rounded-2xl p-6 shadow-xl border border-slate-700/60">
          <div class="flex justify-between items-center border-b border-slate-700/80 pb-4 mb-4">
            <div>
              <h2 class="text-lg font-bold text-white flex items-center gap-2">
                <i class="fa-solid fa-scale-balanced text-amber-400"></i> वीकली सेटलमेंट और कमीशन शीट (Weekly Settlement)
              </h2>
              <p class="text-xs text-slate-400">सभी डाउनलाइंस का लेन-देन, ग्रॉस लॉस, और कमीशन शेयरिंग हिसाब</p>
            </div>
            <button @click="settleAllWeeks" class="gold-gradient text-slate-950 font-bold px-4 py-2 rounded-xl text-xs shadow-lg">
              सभी खाते सेटल करें
            </button>
          </div>

          <div class="overflow-x-auto">
            <table class="w-full text-left text-sm">
              <thead class="bg-slate-950 text-slate-400 text-xs uppercase">
                <tr>
                  <th class="py-3 px-4">पार्टनर / आईडी</th>
                  <th class="py-3 px-4">शेयरिंग %</th>
                  <th class="py-3 px-4">टोटल टर्नओवर</th>
                  <th class="py-3 px-4">क्लाइंट P&L</th>
                  <th class="py-3 px-4">पार्टनर हिस्सा</th>
                  <th class="py-3 px-4">एडमिन नेट प्रॉफ़िट</th>
                  <th class="py-3 px-4 text-center">सेटलमेंट स्थिति</th>
                </tr>
              </thead>
              <tbody class="divide-y divide-slate-800">
                <tr v-for="user in accounts" :key="user.id">
                  <td class="py-3 px-4 font-bold text-amber-300">{{ user.username }} ({{ user.role }})</td>
                  <td class="py-3 px-4 font-semibold">{{ user.sharePercent }}%</td>
                  <td class="py-3 px-4 mono">₹{{ (user.turnover || 85000).toLocaleString() }}</td>
                  <td class="py-3 px-4 mono" :class="user.pnl >= 0 ? 'text-emerald-400' : 'text-rose-400'">
                    {{ user.pnl >= 0 ? '+' : '' }}₹{{ (user.pnl || -12500).toLocaleString() }}
                  </td>
                  <td class="py-3 px-4 mono text-cyan-400">₹{{ Math.abs(Math.round(((user.pnl || -12500) * user.sharePercent) / 100)).toLocaleString() }}</td>
                  <td class="py-3 px-4 mono text-emerald-400 font-bold">₹{{ Math.abs(Math.round(((user.pnl || -12500) * (100 - user.sharePercent)) / 100)).toLocaleString() }}</td>
                  <td class="py-3 px-4 text-center">
                    <span class="bg-amber-500/20 text-amber-400 border border-amber-500/40 text-xs px-2.5 py-1 rounded-full font-semibold">
                      पेंडिंग (Due Mon)
                    </span>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>

      <!-- TAB 4: LIVE BETS RADAR -->
      <div v-if="currentTab === 'livebets'" class="space-y-6">
        <div class="glass-card rounded-2xl p-6 shadow-xl border border-slate-700/60">
          <div class="flex justify-between items-center border-b border-slate-700/80 pb-4 mb-4">
            <div>
              <h2 class="text-lg font-bold text-white flex items-center gap-2">
                <i class="fa-solid fa-radar text-rose-400"></i> लाइव मार्केट्स व हाई-रिस्क बेट्स रडार
              </h2>
              <p class="text-xs text-slate-400">लाइव रनिंग मैचेस, ऑड्स फ्लक्चुएशन और ओवर-एक्सपोज़र अलर्ट्स</p>
            </div>
            <span class="text-xs bg-rose-500/20 text-rose-400 border border-rose-500/40 px-3 py-1.5 rounded-full font-bold">
              लाइव एक्टिव बेट्स: {{ activeBets.length }}
            </span>
          </div>

          <div class="overflow-x-auto">
            <table class="w-full text-left text-sm">
              <thead class="bg-slate-950 text-slate-400 text-xs uppercase">
                <tr>
                  <th class="py-3 px-4">मार्केट / गेम</th>
                  <th class="py-3 px-4">यूज़रनेम</th>
                  <th class="py-3 px-4">बेट प्रकार</th>
                  <th class="py-3 px-4">ऑड्स (Odds)</th>
                  <th class="py-3 px-4">स्टेक रकम</th>
                  <th class="py-3 px-4">पोटेंशियल लॉस (Risk)</th>
                  <th class="py-3 px-4 text-center">कंट्रोल</th>
                </tr>
              </thead>
              <tbody class="divide-y divide-slate-800">
                <tr v-for="bet in activeBets" :key="bet.id" class="hover:bg-slate-800/40">
                  <td class="py-3 px-4 font-bold text-white flex items-center gap-2">
                    <span class="w-2 h-2 rounded-full bg-emerald-400 animate-ping"></span>
                    {{ bet.market }}
                  </td>
                  <td class="py-3 px-4 text-amber-300 font-semibold">{{ bet.username }}</td>
                  <td class="py-3 px-4">
                    <span :class="bet.type === 'Back' ? 'bg-sky-500/20 text-sky-400' : 'bg-pink-500/20 text-pink-400'" class="px-2 py-0.5 rounded text-xs font-bold uppercase">
                      {{ bet.type }}
                    </span>
                  </td>
                  <td class="py-3 px-4 font-bold mono text-amber-400">{{ bet.odds }}</td>
                  <td class="py-3 px-4 font-semibold mono">₹{{ bet.stake.toLocaleString() }}</td>
                  <td class="py-3 px-4 font-bold mono text-rose-400">₹{{ bet.potentialLoss.toLocaleString() }}</td>
                  <td class="py-3 px-4 text-center">
                    <button @click="voidBet(bet.id)" class="text-xs bg-rose-600/80 hover:bg-rose-500 text-white px-2.5 py-1 rounded transition font-medium">
                      वॉयड (रद्द) करें
                    </button>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>

    </main>

  </div>

  <script>
    const { createApp, ref, computed } = Vue;

    createApp({
      setup() {
        const currentTab = ref('dashboard');
        const adminBalance = ref(1500000);
        const totalProfitLoss = ref(385400);
        const searchQuery = ref('');

        const accounts = ref([
          { id: 101, username: 'Royal_Super_Delhi', role: 'Super Master', sharePercent: 85, balance: 250000, exposure: 45000, creditLimit: 500000, maxBetLimit: 50000, status: 'Active', betLocked: false, turnover: 420000, pnl: -65000 },
          { id: 102, username: 'Jaipur_Master_01', role: 'Master', sharePercent: 70, balance: 85000, exposure: 12000, creditLimit: 200000, maxBetLimit: 25000, status: 'Active', betLocked: false, turnover: 195000, pnl: -28000 },
          { id: 103, username: 'Player_Vikram_VIP', role: 'Client', sharePercent: 0, balance: 18500, exposure: 3500, creditLimit: 50000, maxBetLimit: 10000, status: 'Active', betLocked: false, turnover: 45000, pnl: -4500 },
          { id: 104, username: 'Player_Amit_Pro', role: 'Client', sharePercent: 0, balance: 4200, exposure: 0, creditLimit: 20000, maxBetLimit: 5000, status: 'Suspended', betLocked: true, turnover: 12000, pnl: 2100 }
        ]);

        const integratedGames = ref([
          { id: 1, name: 'Live Lightning Roulette', category: 'Live Casino', url: 'https://games.provider.com/roulette/launch', status: 'Live', activePlayers: 18, turnover: 145000 },
          { id: 2, name: 'Aviator Super Flight', category: 'Crash Game', url: 'https://spribe.provider.com/aviator/play', status: 'Live', activePlayers: 42, turnover: 380000 },
          { id: 3, name: 'Cricket Exchange Live Odds', category: 'Sports Exchange', url: 'https://betfair-feed.provider.com/cricket', status: 'Live', activePlayers: 64, turnover: 820000 }
        ]);

        const newGame = ref({ name: '', category: 'Live Casino', url: '' });
        const activeGameSession = ref(null);
        const activeUserForGame = ref(accounts.value[2]); // Default: Player_Vikram_VIP
        const inGameStake = ref(1000);

        const activeBets = ref([
          { id: 1, market: 'IND vs AUS - Match Odds', username: 'Player_Vikram_VIP', type: 'Back', odds: 1.85, stake: 2000, potentialLoss: 1700 },
          { id: 2, market: 'Roulette Live - Red/Black', username: 'Jaipur_Master_01', type: 'Lay', odds: 2.00, stake: 5000, potentialLoss: 5000 },
          { id: 3, market: 'IPL 2026 Winner - Winner', username: 'Royal_Super_Delhi', type: 'Back', odds: 3.50, stake: 10000, potentialLoss: 25000 }
        ]);

        const ledgerLogs = ref([
          { id: 1, time: new Date().toLocaleTimeString(), username: 'Royal_Super_Delhi', type: 'चिप्स डिपॉज़िट', amount: 250000, remarks: 'सुपर एडमिन द्वारा पार्टनर क्रेडिट अलॉट' },
          { id: 2, time: new Date().toLocaleTimeString(), username: 'Jaipur_Master_01', type: 'चिप्स डिपॉज़िट', amount: 85000, remarks: 'मास्टर डाउनलाइन अलॉटमेंट' }
        ]);

        const form = ref({ username: '', password: '', role: 'Master', sharePercent: 80, creditLimit: 100000, maxBetLimit: 15000 });
        const transfer = ref({ userId: '', amount: null, type: 'deposit' });

        const totalExposure = computed(() => accounts.value.reduce((sum, a) => sum + a.exposure, 0));
        const filteredAccounts = computed(() => {
          if (!searchQuery.value) return accounts.value;
          return accounts.value.filter(a => a.username.toLowerCase().includes(searchQuery.value.toLowerCase()));
        });

        const createAccount = () => {
          const newId = 100 + accounts.value.length + 1;
          accounts.value.push({
            id: newId,
            username: form.value.username,
            role: form.value.role,
            sharePercent: form.value.sharePercent || 0,
            balance: 0,
            exposure: 0,
            creditLimit: form.value.creditLimit,
            maxBetLimit: form.value.maxBetLimit,
            status: 'Active',
            betLocked: false,
            turnover: 0,
            pnl: 0
          });

          ledgerLogs.value.unshift({
            id: Date.now(),
            time: new Date().toLocaleTimeString(),
            username: form.value.username,
            type: 'नई आईडी एक्टिवेट',
            amount: 0,
            remarks: `${form.value.role} बनाया गया (${form.value.sharePercent}% शेयर)`
          });

          alert(`सफलतापूर्वक नई आईडी ${form.value.username} बन गई!`);
          form.value.username = '';
          form.value.password = '';
        };

        const transferChips = () => {
          const target = accounts.value.find(a => a.id === transfer.value.userId);
          if (!target) return;
          const amt = transfer.value.amount;

          if (transfer.value.type === 'deposit') {
            if (adminBalance.value < amt) return alert('एडमिन पूल में पर्याप्त बैलेंस नहीं है!');
            adminBalance.value -= amt;
            target.balance += amt;
            ledgerLogs.value.unshift({
              id: Date.now(),
              time: new Date().toLocaleTimeString(),
              username: target.username,
              type: 'चिप्स डिपॉज़िट (+)',
              amount: amt,
              remarks: 'पैनल क्रेडिट लोड'
            });
          } else {
            if (target.balance < amt) return alert('क्लाइंट बैलेंस कम है!');
            target.balance -= amt;
            adminBalance.value += amt;
            ledgerLogs.value.unshift({
              id: Date.now(),
              time: new Date().toLocaleTimeString(),
              username: target.username,
              type: 'चिप्स विथड्रॉ (-)',
              amount: amt,
              remarks: 'पैनल से चिप्स विथड्रॉ'
            });
          }
          transfer.value.amount = null;
        };

        const addGameByLink = () => {
          if (!newGame.value.name || !newGame.value.url) return;
          integratedGames.value.push({
            id: integratedGames.value.length + 1,
            name: newGame.value.name,
            category: newGame.value.category,
            url: newGame.value.url,
            status: 'Live',
            activePlayers: 1,
            turnover: 0
          });
          alert(`${newGame.value.name} सफलतापूर्वक पैनल में जुड़ गया है!`);
          newGame.value.name = '';
          newGame.value.url = '';
        };

        const openGameAsUser = (user) => {
          activeUserForGame.value = user;
          currentTab.value = 'games';
          activeGameSession.value = integratedGames.value[0];
        };

        const launchGameModal = (game) => {
          activeGameSession.value = game;
        };

        const processLiveGameResult = (outcome) => {
          const u = activeUserForGame.value;
          const stake = inGameStake.value;

          if (u.betLocked) return alert('इस यूज़र की बेटिंग लॉक है!');
          if (u.balance < stake) return alert('वॉलेट में बैलेंस कम है!');

          if (outcome === 'loss') {
            u.balance -= stake;
            u.pnl -= stake;
            u.turnover += stake;
            totalProfitLoss.value += stake;
            activeGameSession.value.turnover += stake;

            ledgerLogs.value.unshift({
              id: Date.now(),
              time: new Date().toLocaleTimeString(),
              username: u.username,
              type: 'गेम बेट हारी (-)',
              amount: stake,
              remarks: `${activeGameSession.value.name} में बेट हारी (House Profit)`
            });
            alert(`बेट रिजल्ट: खिलाड़ी हार गया! ₹${stake} सीधे कटकर पैनल के हाउस प्रॉफ़िट में जुड़ गए।`);
          } else {
            const winAmt = stake; // 1:1 net win
            u.balance += winAmt;
            u.pnl += winAmt;
            u.turnover += stake;
            totalProfitLoss.value -= winAmt;
            activeGameSession.value.turnover += stake;

            ledgerLogs.value.unshift({
              id: Date.now(),
              time: new Date().toLocaleTimeString(),
              username: u.username,
              type: 'गेम बेट जीता (+)',
              amount: winAmt,
              remarks: `${activeGameSession.value.name} में 2x पेआउट जीता`
            });
            alert(`बेट रिजल्ट: खिलाड़ी ₹${winAmt} जीत गया! बैलेंस तुरंत ऑटो-अपडेट हो गया।`);
          }
        };

        const toggleAccountStatus = (user) => { user.status = user.status === 'Active' ? 'Suspended' : 'Active'; };
        const toggleBetLock = (user) => { user.betLocked = !user.betLocked; };
        const voidBet = (betId) => {
          activeBets.value = activeBets.value.filter(b => b.id !== betId);
          alert('बेट को सफलतापूर्वक वॉयड (रद्द) कर दिया गया!');
        };
        const settleAllWeeks = () => { alert('वीकली सेटलमेंट सफलता से पूर्ण हुआ! सभी लेज़र अपडेट हो गए हैं।'); };

        return {
          currentTab,
          adminBalance,
          totalProfitLoss,
          totalExposure,
          searchQuery,
          accounts,
          filteredAccounts,
          integratedGames,
          newGame,
          activeGameSession,
          activeUserForGame,
          inGameStake,
          activeBets,
          ledgerLogs,
          form,
          transfer,
          createAccount,
          transferChips,
          addGameByLink,
          openGameAsUser,
          launchGameModal,
          processLiveGameResult,
          toggleAccountStatus,
          toggleBetLock,
          voidBet,
          settleAllWeeks
        };
      }
    }).mount('#app');
  </script>
</body>
</html>
