# WCK-SHU.github.io
GET FREE FOOD AND RESOURCE 
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>WORLD CENTRAL KITCHEN - SETON HALL</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif; }
    .map-bg {
      background-color: #f1f5f9;
      background-image: radial-gradient(#cbd5e1 1.5px, transparent 1.5px);
      background-size: 14px 14px;
    }
  </style>
</head>
<body class="bg-gray-100 flex flex-col h-screen max-w-md mx-auto border-x border-gray-300 shadow-xl">

  <!-- Header -->
  <header class="bg-orange-600 text-white p-3.5 text-center shadow-md flex-none">
    <h1 class="text-xl font-bold tracking-wide">WORLD CENTRAL KITCHEN</h1>
    <p class="text-xs text-orange-200 font-semibold tracking-wider">SETON HALL UNIVERSITY CHAPTER</p>
  </header>

  <!-- Survey Link Banner -->
  <a href="https://docs.google.com/forms/d/e/1FAIpQLSfy2r6Tf9DsBunALJIVM5gMCTE5MtBpitsIHqEyqEZGeyCiUg/viewform?usp=header" target="_blank" rel="noopener noreferrer" class="bg-blue-600 text-white text-xs text-center py-2 px-3 font-bold flex items-center justify-center gap-1 hover:bg-blue-700 transition flex-none">
    📋 Take Our Campus Food Security Survey ➔
  </a>

  <!-- Notification Banner (Simulated Push) -->
  <div id="pushBanner" class="hidden bg-amber-500 text-white p-2.5 text-xs font-bold text-center shadow-inner flex-none flex justify-between items-center px-4 animate-pulse">
    <span id="pushBannerText">🚨 NEW FREE FOOD ALERT AVAILABLE!</span>
    <button onclick="dismissBanner()" class="text-white text-sm font-black ml-2">✕</button>
  </div>

  <!-- Content Panels -->
  <main class="flex-1 overflow-y-auto p-4 space-y-4" id="mainContent">

    <!-- TAB 1: FEED & MAP -->
    <div id="tab-feed" class="tab-pane space-y-4">
      
      <!-- Interactive Campus Map -->
      <div class="bg-white rounded-lg p-3 border shadow-sm">
        <h2 class="text-sm font-bold text-gray-700 mb-2 flex justify-between items-center">
          <span>🗺️ Seton Hall Campus Map</span>
          <span class="text-[11px] font-normal text-gray-500">Tap pins for details</span>
        </h2>
        <div class="map-bg h-48 rounded-md relative border overflow-hidden flex items-center justify-center">
          <!-- SHU Campus Labels -->
          <div class="absolute text-[10px] text-gray-400 font-bold uppercase top-2 left-2 pointer-events-none">Walsh Gym</div>
          <div class="absolute text-[10px] text-gray-400 font-bold uppercase bottom-2 right-2 pointer-events-none">Jubilee Hall</div>
          <div class="absolute text-[10px] text-gray-400 font-bold uppercase top-1/2 left-3 pointer-events-none">Student Center</div>
          <div class="absolute text-[10px] text-gray-400 font-bold uppercase top-1/3 right-4 pointer-events-none">Library</div>
          
          <!-- Map Pins Container -->
          <div id="mapPinsContainer" class="absolute inset-0"></div>
        </div>
      </div>

      <!-- Live Food Feed -->
      <div>
        <div class="flex justify-between items-center mb-2">
          <h2 class="text-md font-bold text-gray-800">Active Free Food Alerts</h2>
          <span id="activeCount" class="text-xs font-semibold bg-orange-100 text-orange-800 px-2 py-0.5 rounded-full">0 Active</span>
        </div>
        <div id="eventsFeed" class="space-y-3"></div>
      </div>
    </div>

    <!-- TAB 2: HEADS UP (Submit) -->
    <div id="tab-headsup" class="tab-pane hidden space-y-3">
      <h2 class="text-lg font-bold text-gray-800">Campus Heads-Up Tip Line</h2>
      <p class="text-xs text-gray-600">Spotted extra free food after a meeting or event? Share it with students & faculty!</p>

      <form id="userForm" class="space-y-3 bg-white p-4 rounded-lg border shadow-sm">
        <div>
          <label class="block text-xs font-bold text-gray-700 mb-1">Room / Location:</label>
          <input type="text" id="userLocation" required placeholder="e.g. University Center Lobby" class="w-full text-sm border p-2 rounded focus:ring-2 focus:ring-orange-500 outline-none">
        </div>
        <div>
          <label class="block text-xs font-bold text-gray-700 mb-1">Food Description:</label>
          <input type="text" id="userFood" required placeholder="e.g. Half tray of pasta, salad, cookies" class="w-full text-sm border p-2 rounded focus:ring-2 focus:ring-orange-500 outline-none">
        </div>
        <div>
          <label class="block text-xs font-bold text-gray-700 mb-1">Minutes Event Lasts (Approx):</label>
          <input type="number" id="userDuration" placeholder="30" min="5" max="300" class="w-full text-sm border p-2 rounded focus:ring-2 focus:ring-orange-500 outline-none">
        </div>
        <button type="submit" class="w-full bg-green-700 text-white text-sm font-bold py-2.5 rounded hover:bg-green-800 transition">Post Campus Tip</button>
      </form>
    </div>

    <!-- TAB 3: ADMIN BROADCAST -->
    <div id="tab-admin" class="tab-pane hidden space-y-3">
      <h2 class="text-lg font-bold text-gray-800">Instant Admin Broadcast</h2>
      <p class="text-xs text-gray-600">Broadcast food availability immediately to the campus community.</p>

      <form id="adminForm" class="space-y-3 bg-white p-4 rounded-lg border shadow-sm">
        <div>
          <label class="block text-xs font-bold text-gray-700 mb-1">Location & Room Number:</label>
          <input type="text" id="adminLocation" required placeholder="e.g. Jubilee Hall Rm 112" class="w-full text-sm border p-2 rounded focus:ring-2 focus:ring-orange-500 outline-none">
        </div>
        <div>
          <label class="block text-xs font-bold text-gray-700 mb-1">Food Offered:</label>
          <input type="text" id="adminFood" required placeholder="e.g. Boxed lunches & beverages" class="w-full text-sm border p-2 rounded focus:ring-2 focus:ring-orange-500 outline-none">
        </div>
        <div>
          <label class="block text-xs font-bold text-gray-700 mb-1">Minutes Until Event Officially Ends:</label>
          <input type="number" id="adminDuration" required placeholder="40" min="1" max="240" class="w-full text-sm border p-2 rounded focus:ring-2 focus:ring-orange-500 outline-none">
        </div>
        <button type="submit" class="w-full bg-orange-600 text-white text-sm font-bold py-2.5 rounded hover:bg-orange-700 transition">Broadcast Alert Immediately</button>
      </form>
    </div>

    <!-- TAB 4: PRESCHEDULE (Password Protected - Passcode: 18340) -->
    <div id="tab-preschedule" class="tab-pane hidden space-y-3">
      
      <!-- Lock Screen View -->
      <div id="prescheduleLockView" class="bg-white p-5 rounded-lg border shadow-sm text-center space-y-3">
        <div class="text-3xl">🔒</div>
        <h2 class="text-base font-bold text-gray-800">Restricted Access</h2>
        <p class="text-xs text-gray-600">Enter manager passcode to access prescheduled events management.</p>
        
        <form id="lockForm" class="space-y-3 max-w-xs mx-auto">
          <input type="password" id="passcodeInput" maxlength="10" placeholder="Enter Passcode" class="w-full text-center text-lg tracking-widest border p-2 rounded focus:ring-2 focus:ring-orange-500 outline-none">
          <p id="lockError" class="text-xs text-red-600 hidden font-bold">Incorrect Passcode. Access Denied.</p>
          <button type="submit" class="w-full bg-slate-800 text-white text-sm font-bold py-2 rounded hover:bg-slate-900 transition">Unlock Panel</button>
        </form>
      </div>

      <!-- Unlocked Preschedule Manager View -->
      <div id="prescheduleUnlockedView" class="hidden space-y-4">
        <div class="flex justify-between items-center border-b pb-2">
          <div>
            <h2 class="text-base font-bold text-gray-800">Preschedule Food Event</h2>
            <p class="text-[11px] text-gray-500">Alerts launch automatically 10m before event ends.</p>
          </div>
          <button onclick="lockPreschedule()" class="text-xs bg-gray-200 text-gray-700 px-2.5 py-1 rounded font-semibold hover:bg-gray-300">Lock 🔒</button>
        </div>

        <form id="prescheduleForm" class="space-y-3 bg-white p-4 rounded-lg border shadow-sm">
          <div>
            <label class="block text-xs font-bold text-gray-700 mb-1">Location & Room Number:</label>
            <input type="text" id="preLocation" required placeholder="e.g. McNulty Hall Rm 101" class="w-full text-sm border p-2 rounded focus:ring-2 focus:ring-orange-500 outline-none">
          </div>
          <div>
            <label class="block text-xs font-bold text-gray-700 mb-1">Food Description:</label>
            <input type="text" id="preFood" required placeholder="e.g. Catering Tray Sandwiches & Dessert" class="w-full text-sm border p-2 rounded focus:ring-2 focus:ring-orange-500 outline-none">
          </div>
          <div>
            <label class="block text-xs font-bold text-gray-700 mb-1">Event End Date & Time:</label>
            <input type="datetime-local" id="preEndTime" required class="w-full text-sm border p-2 rounded focus:ring-2 focus:ring-orange-500 outline-none">
          </div>

          <div class="bg-amber-50 p-2.5 rounded border border-amber-200 text-[11px] text-amber-800 space-y-1">
            <p class="font-bold">⏱️ Preschedule Timing Rules:</p>
            <p>• Alert launches public notification exactly <strong>10 minutes before</strong> official end time.</p>
            <p>• Countdown stays active for <strong>50 minutes after</strong> official end time before removal.</p>
          </div>

          <button type="submit" class="w-full bg-orange-600 text-white text-sm font-bold py-2.5 rounded hover:bg-orange-700 transition">Save Prescheduled Event</button>
        </form>

        <!-- Prescheduled Queue List -->
        <div>
          <h3 class="text-sm font-bold text-gray-800 mb-2">Prescheduled Event Queue</h3>
          <div id="prescheduleQueue" class="space-y-2"></div>
        </div>
      </div>

    </div>

    <!-- TAB 5: HOTLINES & RESOURCES -->
    <div id="tab-hotline" class="tab-pane hidden space-y-3">
      <h2 class="text-lg font-bold text-gray-800">Emergency & Campus Hotlines</h2>

      <div class="bg-white p-3.5 rounded-lg border shadow-sm space-y-1">
        <h3 class="text-sm font-bold text-blue-800">🍞 Campus Food Pantry</h3>
        <p class="text-xs text-gray-600">Boland Hall Annex | Mon-Fri 10:00 AM - 4:00 PM</p>
        <p class="text-[11px] text-gray-500">Free grocer and essential hygiene supplies for SHU students.</p>
      </div>

      <div class="bg-white p-3.5 rounded-lg border shadow-sm space-y-1">
        <h3 class="text-sm font-bold text-blue-800">🏠 Emergency Housing Security</h3>
        <p class="text-xs text-gray-600">Dean of Students Office: (973) 761-9000</p>
        <p class="text-xs text-gray-600">24/7 Housing Crisis Helpline: Call 211</p>
      </div>

      <div class="bg-white p-3.5 rounded-lg border shadow-sm space-y-1 border-l-4 border-l-red-500">
        <h3 class="text-sm font-bold text-red-700">🛡️ ICE & Legal Emergency Resources</h3>
        <p class="text-xs text-gray-600">Know Your Rights: You have the right to remain silent and request an attorney.</p>
        <a href="tel:18003755283" class="inline-block mt-1 text-xs font-bold text-red-600 underline hover:text-red-800">Call Legal Support Emergency Line (1-800-375-5283)</a>
      </div>
    </div>

  </main>

  <!-- Bottom Navigation Bar -->
  <nav class="bg-white border-t flex justify-around p-2 text-center text-[11px] text-gray-500 flex-none">
    <button onclick="switchTab('feed')" id="nav-feed" class="flex-1 py-1 text-orange-600 font-bold">
      🔔 Alerts
    </button>
    <button onclick="switchTab('headsup')" id="nav-headsup" class="flex-1 py-1">
      💡 Tip Line
    </button>
    <button onclick="switchTab('admin')" id="nav-admin" class="flex-1 py-1">
      📣 Admin
    </button>
    <button onclick="switchTab('preschedule')" id="nav-preschedule" class="flex-1 py-1">
      📅 Schedule
    </button>
    <button onclick="switchTab('hotline')" id="nav-hotline" class="flex-1 py-1">
      ☎️ Hotlines
    </button>
  </nav>

  <!-- JavaScript Application Logic -->
  <script>
    // System Password
    const MANAGER_PASSWORD = "18340";
    let isUnlocked = false;

    // Primary State Storage
    let events = [
      {
        id: 'default-1',
        location: 'Student Center - Rm 201',
        food: 'Pizza Boxes & Cold Drinks',
        endTime: Date.now() + (15 * 60 * 1000), // 15 mins left until event ends
        source: 'Official WCK-SHU',
        top: '45%',
        left: '25%',
        notified: false
      }
    ];

    let prescheduledEvents = [];

    // Tab Switcher
    function switchTab(tabId) {
      document.querySelectorAll('.tab-pane').forEach(el => el.classList.add('hidden'));
      document.getElementById('tab-' + tabId).classList.remove('hidden');

      document.querySelectorAll('nav button').forEach(btn => {
        btn.classList.remove('text-orange-600', 'font-bold');
        btn.classList.add('text-gray-500');
      });
      document.getElementById('nav-' + tabId).classList.add('text-orange-600', 'font-bold');

      if (tabId === 'preschedule') {
        updatePrescheduleUI();
      }
    }

    // Password Lock Handling
    document.getElementById('lockForm').addEventListener('submit', (e) => {
      e.preventDefault();
      const val = document.getElementById('passcodeInput').value;
      if (val === MANAGER_PASSWORD) {
        isUnlocked = true;
        document.getElementById('lockError').classList.add('hidden');
        document.getElementById('passcodeInput').value = '';
        updatePrescheduleUI();
      } else {
        document.getElementById('lockError').classList.remove('hidden');
      }
    });

    function lockPreschedule() {
      isUnlocked = false;
      updatePrescheduleUI();
    }

    function updatePrescheduleUI() {
      if (isUnlocked) {
        document.getElementById('prescheduleLockView').classList.add('hidden');
        document.getElementById('prescheduleUnlockedView').classList.remove('hidden');
        renderPrescheduleQueue();
      } else {
        document.getElementById('prescheduleLockView').classList.remove('hidden');
        document.getElementById('prescheduleUnlockedView').classList.add('hidden');
      }
    }

    // Preschedule Form Submission
    document.getElementById('prescheduleForm').addEventListener('submit', (e) => {
      e.preventDefault();
      const loc = document.getElementById('preLocation').value;
      const food = document.getElementById('preFood').value;
      const endTimeVal = document.getElementById('preEndTime').value;

      const endMs = new Date(endTimeVal).getTime();
      if (isNaN(endMs) || endMs <= Date.now()) {
        alert('Please choose a valid future date and time for the event end.');
        return;
      }

      const item = {
        id: 'pre-' + Date.now(),
        location: loc,
        food: food,
        endTime: endMs,
        source: 'Prescheduled WCK',
        top: Math.floor(Math.random() * 55 + 20) + '%',
        left: Math.floor(Math.random() * 55 + 20) + '%'
      };

      prescheduledEvents.push(item);
      e.target.reset();
      renderPrescheduleQueue();
      alert('Event scheduled! Notification will go live 10 minutes before the event ends.');
    });

    // Admin Immediate Broadcast
    document.getElementById('adminForm').addEventListener('submit', (e) => {
      e.preventDefault();
      const loc = document.getElementById('adminLocation').value;
      const food = document.getElementById('adminFood').value;
      const duration = parseInt(document.getElementById('adminDuration').value) || 30;

      const newEvt = {
        id: 'adm-' + Date.now(),
        location: loc,
        food: food,
        endTime: Date.now() + (duration * 60 * 1000),
        source: 'Official WCK-SHU',
        top: Math.floor(Math.random() * 55 + 20) + '%',
        left: Math.floor(Math.random() * 55 + 20) + '%',
        notified: true
      };

      events.unshift(newEvt);
      e.target.reset();
      triggerPushBanner(`🚨 FREE FOOD ALERT: ${food} at ${loc}!`);
      switchTab('feed');
      render();
    });

    // User Tip Submission
    document.getElementById('userForm').addEventListener('submit', (e) => {
      e.preventDefault();
      const loc = document.getElementById('userLocation').value;
      const food = document.getElementById('userFood').value;
      const duration = parseInt(document.getElementById('userDuration').value) || 30;

      const newEvt = {
        id: 'usr-' + Date.now(),
        location: loc,
        food: food,
        endTime: Date.now() + (duration * 60 * 1000),
        source: 'Student Tip',
        top: Math.floor(Math.random() * 55 + 20) + '%',
        left: Math.floor(Math.random() * 55 + 20) + '%',
        notified: true
      };

      events.unshift(newEvt);
      e.target.reset();
      triggerPushBanner(`💡 STUDENT TIP: Free food spotted at ${loc}!`);
      switchTab('feed');
      render();
    });

    function triggerPushBanner(msg) {
      const banner = document.getElementById('pushBanner');
      document.getElementById('pushBannerText').innerText = msg;
      banner.classList.remove('hidden');
    }

    function dismissBanner() {
      document.getElementById('pushBanner').classList.add('hidden');
    }

    // Render Prescheduled Queue
    function renderPrescheduleQueue() {
      const qEl = document.getElementById('prescheduleQueue');
      if (!qEl) return;
      qEl.innerHTML = '';

      if (prescheduledEvents.length === 0) {
        qEl.innerHTML = '<p class="text-xs text-gray-500 italic">No events currently in the prescheduled queue.</p>';
        return;
      }

      prescheduledEvents.forEach((item, index) => {
        const triggerTime = new Date(item.endTime - (10 * 60 * 1000));
        const div = document.createElement('div');
        div.className = 'bg-white p-3 rounded border text-xs flex justify-between items-center shadow-sm';
        div.innerHTML = `
          <div>
            <p class="font-bold text-gray-800">${item.location}</p>
            <p class="text-gray-600">🍱 ${item.food}</p>
            <p class="text-[10px] text-amber-700 mt-1">Alert Launch: ${triggerTime.toLocaleDateString()} ${triggerTime.toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'})}</p>
          </div>
          <button onclick="removePrescheduled(${index})" class="text-red-600 font-bold px-2 py-1 hover:bg-red-50 rounded">Cancel</button>
        `;
        qEl.appendChild(div);
      });
    }

    function removePrescheduled(idx) {
      prescheduledEvents.splice(idx, 1);
      renderPrescheduleQueue();
    }

    // Main Processing & Rendering Engine
    function render() {
      const now = Date.now();

      // Check Prescheduled Queue for T-10 minute alert launch
      for (let i = prescheduledEvents.length - 1; i >= 0; i--) {
        const item = prescheduledEvents[i];
        const triggerTimeMs = item.endTime - (10 * 60 * 1000); // 10 minutes before event ends

        if (now >= triggerTimeMs) {
          // Promote to active live alert
          events.unshift({
            ...item,
            notified: true
          });
          triggerPushBanner(`🚨 PRESCHEDULED ALERT: Free ${item.food} available at ${item.location}!`);
          prescheduledEvents.splice(i, 1);
          if (isUnlocked) renderPrescheduleQueue();
        }
      }

      const feedEl = document.getElementById('eventsFeed');
      const pinsEl = document.getElementById('mapPinsContainer');
      const activeCountEl = document.getElementById('activeCount');

      feedEl.innerHTML = '';
      pinsEl.innerHTML = '';

      let activeCount = 0;

      events.forEach(evt => {
        // Countdown rule: Runs 50 minutes past official event end time
        const removalTimeMs = evt.endTime + (50 * 60 * 1000);
        const diffMs = removalTimeMs - now;

        if (diffMs <= 0) return; // Expired & removed

        activeCount++;

        const minsLeft = Math.floor(diffMs / 60000);
        const secsLeft = Math.floor((diffMs % 60000) / 1000);

        const eventEnded = now > evt.endTime;
        const inPostWindow = eventEnded && now <= removalTimeMs;

        // Card UI
        const card = document.createElement('div');
        card.className = `p-3 rounded-lg border shadow-sm transition bg-white ${inPostWindow ? 'border-amber-400 bg-amber-50/50' : 'border-gray-200'}`;
        card.innerHTML = `
          <div class="flex justify-between items-start">
            <h3 class="font-bold text-sm text-gray-900">${evt.location}</h3>
            <span class="text-[10px] bg-gray-200 px-1.5 py-0.5 rounded text-gray-700 font-medium">${evt.source}</span>
          </div>
          <p class="text-xs text-gray-700 mt-1">🍱 ${evt.food}</p>
          <div class="mt-2 p-2 rounded ${inPostWindow ? 'bg-amber-100/70 border border-amber-300' : 'bg-orange-50 border border-orange-200'} flex justify-between items-center text-xs">
            <span class="font-semibold ${inPostWindow ? 'text-amber-900' : 'text-orange-800'}">
              ${inPostWindow ? '⌛ Post-Event Food Grab Window:' : '⏱️ Active Food Availability:'}
            </span>
            <span class="font-bold ${inPostWindow ? 'text-amber-700' : 'text-orange-600'}">${minsLeft}m ${secsLeft < 10 ? '0' : ''}${secsLeft}s</span>
          </div>
        `;
        feedEl.appendChild(card);

        // Map Pin UI
        const pin = document.createElement('div');
        pin.className = "absolute text-xl cursor-pointer transform -translate-x-1/2 -translate-y-1/2 transition hover:scale-125";
        pin.style.top = evt.top;
        pin.style.left = evt.left;
        pin.innerHTML = "📍";
        pin.title = `${evt.location} - ${evt.food}`;
        pin.onclick = () => alert(`📍 LOCATION: ${evt.location}\n🍱 FOOD: ${evt.food}\n📣 SOURCE: ${evt.source}\n⏱️ TIME REMAINING: ${minsLeft}m ${secsLeft}s`);
        pinsEl.appendChild(pin);
      });

      activeCountEl.innerText = `${activeCount} Active`;

      if (activeCount === 0) {
        feedEl.innerHTML = '<div class="p-4 text-center text-xs text-gray-500 bg-white rounded-lg border">No active free food alerts currently listed. Stay tuned!</div>';
      }
    }

    // Initialize 1-second interval loop
    setInterval(render, 1000);
    render();
  </script>
</body>
</html>
