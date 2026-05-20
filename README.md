<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Zoom Management Dashboard</title>

  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: Arial, sans-serif;
    }

    body {
      background: #f3f4f6;
      display: flex;
      min-height: 100vh;
    }

    .sidebar {
      width: 250px;
      background: #111827;
      color: white;
      padding: 20px;
    }

    .sidebar h2 {
      margin-bottom: 30px;
      font-size: 22px;
    }

    .sidebar ul {
      list-style: none;
    }

    .sidebar li {
      padding: 12px;
      border-radius: 8px;
      margin-bottom: 10px;
      cursor: pointer;
      transition: 0.3s;
    }

    .sidebar li:hover {
      background: #2563eb;
    }

    .main {
      flex: 1;
      padding: 20px;
    }

    .header {
      background: white;
      padding: 20px;
      border-radius: 15px;
      margin-bottom: 20px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.08);
    }

    .header h1 {
      color: #111827;
    }

    .cards {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
      gap: 20px;
      margin-bottom: 20px;
    }

    .card {
      background: white;
      padding: 20px;
      border-radius: 15px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.08);
    }

    .card h3 {
      margin-bottom: 10px;
      color: #6b7280;
      font-size: 16px;
    }

    .card p {
      font-size: 30px;
      font-weight: bold;
      color: #2563eb;
    }

    .section {
      background: white;
      padding: 20px;
      border-radius: 15px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.08);
      margin-bottom: 20px;
    }

    .section h2 {
      margin-bottom: 20px;
    }

    table {
      width: 100%;
      border-collapse: collapse;
    }

    th {
      background: #2563eb;
      color: white;
      padding: 12px;
      text-align: left;
    }

    td {
      padding: 12px;
      border-bottom: 1px solid #ddd;
    }

    tr:hover {
      background: #f9fafb;
    }

    .calendar {
      display: grid;
      grid-template-columns: repeat(7, 1fr);
      gap: 10px;
    }

    .day {
      background: #f9fafb;
      padding: 15px;
      border-radius: 10px;
      min-height: 90px;
      position: relative;
    }

    .event {
      background: #2563eb;
      color: white;
      padding: 5px;
      border-radius: 5px;
      font-size: 12px;
      margin-top: 5px;
    }

    .form-group {
      margin-bottom: 15px;
    }

    input {
      width: 100%;
      padding: 12px;
      border: 1px solid #ddd;
      border-radius: 8px;
    }

    button {
      background: #2563eb;
      color: white;
      border: none;
      padding: 12px 20px;
      border-radius: 8px;
      cursor: pointer;
      transition: 0.3s;
    }

    button:hover {
      background: #1d4ed8;
    }

    @media(max-width: 768px) {
      body {
        flex-direction: column;
      }

      .sidebar {
        width: 100%;
      }
    }
  </style>
</head>
<body>

  <div class="sidebar">
    <h2>Zoom Dashboard</h2>

    <ul>
      <li>Dashboard</li>
      <li>Peminjaman Zoom</li>
      <li>Pendampingan</li>
      <li>Kalender Agenda</li>
      <li>Laporan</li>
      <li>Pengaturan</li>
    </ul>
  </div>

  <div class="main">

    <div class="header">
      <h1>Sistem Peminjaman & Pendampingan Zoom</h1>
      <p>Monitoring agenda Zoom Meeting Instansi</p>
    </div>

    <div class="cards">
      <div class="card">
        <h3>Total Permintaan</h3>
        <p id="totalRequest">3</p>
      </div>

      <div class="card">
        <h3>Total Pendampingan</h3>
        <p>2</p>
      </div>

      <div class="card">
        <h3>Akun Zoom Aktif</h3>
        <p>5</p>
      </div>

      <div class="card">
        <h3>Kegiatan Hari Ini</h3>
        <p>4</p>
      </div>
    </div>

    <div class="section">
      <h2>Tambah Agenda Zoom</h2>

      <div class="form-group">
        <input type="text" id="kegiatan" placeholder="Nama Kegiatan">
      </div>

      <div class="form-group">
        <input type="date" id="tanggal">
      </div>

      <div class="form-group">
        <input type="text" id="akun" placeholder="Akun Zoom">
      </div>

      <div class="form-group">
        <input type="text" id="petugas" placeholder="Petugas Pendamping">
      </div>

      <button onclick="tambahAgenda()">Tambah Agenda</button>
    </div>

    <div class="section">
      <h2>Data Agenda Kegiatan</h2>

      <table>
        <thead>
          <tr>
            <th>No</th>
            <th>Kegiatan</th>
            <th>Tanggal</th>
            <th>Akun Zoom</th>
            <th>Petugas</th>
          </tr>
        </thead>

        <tbody id="tableBody">
        </tbody>
      </table>
    </div>

    <div class="section">
      <h2>Kalender Agenda</h2>

      <div class="calendar">
        <div class="day">1</div>
        <div class="day">2</div>
        <div class="day">3</div>
        <div class="day">4</div>
        <div class="day">5</div>
        <div class="day">6</div>

        <div class="day">
          7
          <div class="event">Rapat Nasional</div>
        </div>

        <div class="day">8</div>
        <div class="day">9</div>
        <div class="day">10</div>
        <div class="day">11</div>
        <div class="day">12</div>
        <div class="day">13</div>

        <div class="day">
          14
          <div class="event">Webinar Pendidikan</div>
        </div>
      </div>
    </div>

  </div>

  <script>
    let dataAgenda = [
      {
        kegiatan: 'Rapat Koordinasi Nasional',
        tanggal: '2026-05-20',
        akun: 'zoom1@instansi.go.id',
        petugas: 'Admin Zoom'
      },
      {
        kegiatan: 'Webinar Pendidikan',
        tanggal: '2026-05-21',
        akun: 'zoom2@instansi.go.id',
        petugas: 'Operator Webinar'
      },
      {
        kegiatan: 'Sosialisasi Program',
        tanggal: '2026-05-22',
        akun: 'zoom3@instansi.go.id',
        petugas: 'Tim IT'
      }
    ];

    function renderTable() {
      const tableBody = document.getElementById('tableBody');
      tableBody.innerHTML = '';

      dataAgenda.forEach((item, index) => {
        tableBody.innerHTML += `
          <tr>
            <td>${index + 1}</td>
            <td>${item.kegiatan}</td>
            <td>${item.tanggal}</td>
            <td>${item.akun}</td>
            <td>${item.petugas}</td>
          </tr>
        `;
      });

      document.getElementById('totalRequest').innerText = dataAgenda.length;
    }

    function tambahAgenda() {
      const kegiatan = document.getElementById('kegiatan').value;
      const tanggal = document.getElementById('tanggal').value;
      const akun = document.getElementById('akun').value;
      const petugas = document.getElementById('petugas').value;

      if (!kegiatan || !tanggal || !akun || !petugas) {
        alert('Semua field wajib diisi');
        return;
      }

      dataAgenda.push({
        kegiatan,
        tanggal,
        akun,
        petugas
      });

      renderTable();

      document.getElementById('kegiatan').value = '';
      document.getElementById('tanggal').value = '';
      document.getElementById('akun').value = '';
      document.getElementById('petugas').value = '';

      alert('Agenda berhasil ditambahkan');
    }

    renderTable();
  </script>

</body>
</html>
