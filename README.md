# Flag-Coachboard
Sacristans Flag Trainigsplaner 
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Sacristans Flag Coachboard</title>
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@3.3.2/dist/tailwind.min.css" rel="stylesheet">
</head>
<body class="bg-gray-100 font-sans">

  <!-- Header -->
  <header class="bg-red-600 text-white p-4 text-center text-2xl font-bold">
    Sacristans Flag Coachboard
  </header>

  <!-- Navigation Tabs -->
  <div class="flex justify-center mt-4 space-x-4">
    <button class="tab-btn bg-white px-4 py-2 rounded shadow" data-tab="playbooks">Playbooks</button>
    <button class="tab-btn bg-white px-4 py-2 rounded shadow" data-tab="trainings">Trainingspläne</button>
    <button class="tab-btn bg-white px-4 py-2 rounded shadow" data-tab="videos">Videos & Links</button>
  </div>

  <!-- Content -->
  <div class="mt-6 max-w-5xl mx-auto">
    <!-- Playbooks -->
    <div class="tab-content hidden" id="playbooks">
      <h2 class="text-xl font-semibold mb-4">Playbooks Übersicht</h2>
      <table class="table-auto w-full bg-white shadow rounded">
        <thead>
          <tr class="bg-red-200">
            <th class="px-4 py-2">Play</th>
            <th class="px-4 py-2">Beschreibung</th>
            <th class="px-4 py-2">Level</th>
          </tr>
        </thead>
        <tbody id="playbook-table">
          <!-- Dynamische Inhalte per JS -->
        </tbody>
      </table>
    </div>

    <!-- Trainingspläne -->
    <div class="tab-content hidden" id="trainings">
      <h2 class="text-xl font-semibold mb-4">Trainingsplan</h2>
      <input type="text" id="search-input" placeholder="Suche Trainingsinhalt..." class="mb-4 p-2 border rounded w-full">
      <table class="table-auto w-full bg-white shadow rounded">
        <thead>
          <tr class="bg-green-200">
            <th class="px-4 py-2">Datum</th>
            <th class="px-4 py-2">Thema</th>
            <th class="px-4 py-2">Beschreibung</th>
          </tr>
        </thead>
        <tbody id="training-table">
          <!-- Dynamische Inhalte per JS -->
        </tbody>
      </table>
    </div>

    <!-- Videos & Links -->
    <div class="tab-content hidden" id="videos">
      <h2 class="text-xl font-semibold mb-4">Videos & Ressourcen</h2>
      <ul id="video-list" class="list-disc pl-5">
        <!-- Dynamische Inhalte per JS -->
      </ul>
    </div>
  </div>

  <script>
    // Sample Data
    const playbooks = [
      { play: 'Slant Right', desc: 'Kurzer Pass auf X-Receiver', level: 'U13' },
      { play: 'Screen Pass', desc: 'Schneller Pass auf S-Receiver', level: 'U13' },
      { play: 'Triangle Read', desc: 'Quarterback liest 3 Optionen', level: 'U13' },
    ];

    const trainings = [
      { date: '2025-10-23', topic: 'Schnelligkeit', desc: 'Sprintübungen & Agility-Leiter' },
      { date: '2025-10-24', topic: 'Pässe', desc: 'Kurzpassübungen auf X, Y, S' },
      { date: '2025-10-25', topic: 'Defense', desc: 'Flag Pulling & Coverage Drill' },
    ];

    const videos = [
      { title: 'Slant Route Tutorial', link: 'https://www.youtube.com/watch?v=abc123' },
      { title: 'Triangle Read Erklärung', link: 'https://www.youtube.com/watch?v=def456' },
      { title: 'Agility Training', link: 'https://www.youtube.com/watch?v=ghi789' },
    ];

    // Populate Playbooks
    const playbookTable = document.getElementById('playbook-table');
    playbooks.forEach(p => {
      const row = document.createElement('tr');
      row.innerHTML = `<td class="border px-4 py-2">${p.play}</td>
                       <td class="border px-4 py-2">${p.desc}</td>
                       <td class="border px-4 py-2">${p.level}</td>`;
      playbookTable.appendChild(row);
    });

    // Populate Trainings
    const trainingTable = document.getElementById('training-table');
    trainings.forEach(t => {
      const row = document.createElement('tr');
      row.innerHTML = `<td class="border px-4 py-2">${t.date}</td>
                       <td class="border px-4 py-2">${t.topic}</td>
                       <td class="border px-4 py-2">${t.desc}</td>`;
      trainingTable.appendChild(row);
    });

    // Populate Videos
    const videoList = document.getElementById('video-list');
    videos.forEach(v => {
      const li = document.createElement('li');
      li.innerHTML = `<a href="${v.link}" target="_blank" class="text-blue-600 underline">${v.title}</a>`;
      videoList.appendChild(li);
    });

    // Tab Switching
    const tabBtns = document.querySelectorAll('.tab-btn');
    const tabContents = document.querySelectorAll('.tab-content');
    tabBtns.forEach(btn => {
      btn.addEventListener('click', () => {
        tabContents.forEach(c => c.classList.add('hidden'));
        document.getElementById(btn.dataset.tab).classList.remove('hidden');
      });
    });

    // Search Funktion
    const searchInput = document.getElementById('search-input');
    searchInput.addEventListener('input', () => {
      const filter = searchInput.value.toLowerCase();
      trainingTable.querySelectorAll('tr').forEach(row => {
        const topic = row.cells[1].textContent.toLowerCase();
        const desc = row.cells[2].textContent.toLowerCase();
        row.style.display = (topic.includes(filter) || desc.includes(filter)) ? '' : 'none';
      });
    });

    // Zeige standardmäßig Playbooks
    document.getElementById('playbooks').classList.remove('hidden');
  </script>

</body>
</html>
