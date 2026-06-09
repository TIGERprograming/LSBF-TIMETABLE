<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8"/>
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>LSBF Timetable — May 2026</title>
  <link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet"/>
  <style>
    :root {
      --bg: #ffffff;
      --surface: #f8f9fb;
      --surface2: #f0f2f5;
      --border: #e2e5ea;
      --border2: #cdd1d8;
      --text: #1a1d23;
      --muted: #7a8094;
      --accent:  #2563eb;
      --accent-bg: #eff6ff;
      /* programme colours */
      --c-dcs:   #2563eb; --c-dcs-bg:   #eff6ff;
      --c-dpsy:  #7c3aed; --c-dpsy-bg:  #f5f3ff;
      --c-dhrm:  #0891b2; --c-dhrm-bg:  #ecfeff;
      --c-dia:   #d97706; --c-dia-bg:   #fffbeb;
      --c-dhm:   #059669; --c-dhm-bg:   #ecfdf5;
      --c-ddm:   #db2777; --c-ddm-bg:   #fdf2f8;
      --c-die:   #ea580c; --c-die-bg:   #fff7ed;
      --c-dlsc:  #0d9488; --c-dlsc-bg:  #f0fdfa;
      --c-fia:   #4f46e5; --c-fia-bg:   #eef2ff;
      --c-fiacca:#7c3aed; --c-fiacca-bg:#f5f3ff;
      --c-dosh:  #be123c; --c-dosh-bg:  #fff1f2;
      --c-dhcm:  #0369a1; --c-dhcm-bg:  #f0f9ff;
      --c-cib:   #15803d; --c-cib-bg:   #f0fdf4;
      --c-chs:   #ca8a04; --c-chs-bg:   #fefce8;
      --c-cie:   #9333ea; --c-cie-bg:   #faf5ff;
      --c-uos:   #64748b; --c-uos-bg:   #f8fafc;
      --c-fis:   #b45309; --c-fis-bg:   #fffbeb;
      --c-dba:   #0f766e; --c-dba-bg:   #f0fdfa;
      --c-odl:   #6b7280; --c-odl-bg:   #f9fafb;
    }
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body { background: var(--bg); color: var(--text); font-family: 'DM Sans', sans-serif; min-height: 100vh; }

    /* ── LOGIN ── */
    #login-screen { display:flex; flex-direction:column; align-items:center; justify-content:center; min-height:100vh; background: var(--surface); }
    .login-box { background:#fff; border:1px solid var(--border); border-radius:16px; padding:2.5rem; width:360px; box-shadow:0 4px 24px rgba(0,0,0,.06); display:flex; flex-direction:column; gap:1rem; }
    .login-logo { font-family:'Space Mono',monospace; font-size:1.1rem; font-weight:700; color:var(--accent); letter-spacing:.04em; }
    .login-box h2 { font-size:1.15rem; font-weight:600; color:var(--text); }
    .login-box p { font-size:.85rem; color:var(--muted); }
    .role-btns { display:flex; gap:.5rem; }
    .role-btn { flex:1; padding:.6rem; border-radius:8px; border:1px solid var(--border); background:#fff; color:var(--muted); font-size:.85rem; cursor:pointer; transition:all .15s; font-family:'DM Sans',sans-serif; }
    .role-btn.active { border-color:var(--accent); color:var(--accent); background:var(--accent-bg); font-weight:600; }
    #pin-wrap { display:none; flex-direction:column; gap:.4rem; }
    .pin-input { background:#fff; border:1px solid var(--border); border-radius:8px; color:var(--text); font-size:.9rem; padding:.55rem .75rem; outline:none; width:100%; font-family:'Space Mono',monospace; }
    .pin-input:focus { border-color:var(--accent); box-shadow:0 0 0 3px rgba(37,99,235,.1); }
    .login-btn { background:var(--accent); color:#fff; border:none; border-radius:8px; padding:.65rem; font-weight:600; font-size:.9rem; cursor:pointer; transition:opacity .15s; font-family:'DM Sans',sans-serif; }
    .login-btn:hover { opacity:.9; }
    .err-msg { font-size:.78rem; color:#dc2626; min-height:16px; }

    /* ── HEADER ── */
    header { height:60px; display:flex; align-items:center; justify-content:space-between; padding:0 1.5rem; border-bottom:1px solid var(--border); position:sticky; top:0; background:#fff; z-index:200; box-shadow:0 1px 4px rgba(0,0,0,.04); }
    .logo { font-family:'Space Mono',monospace; font-size:.95rem; font-weight:700; color:var(--accent); letter-spacing:.04em; }
    .header-right { display:flex; align-items:center; gap:.75rem; flex-wrap:wrap; }
    .clock-wrap { text-align:right; }
    .clock { font-family:'Space Mono',monospace; font-size:1rem; color:var(--text); font-weight:700; letter-spacing:.06em; }
    .date-str { font-size:.68rem; color:var(--muted); font-family:'Space Mono',monospace; }
    .sem-badge { font-size:.7rem; font-family:'Space Mono',monospace; color:var(--muted); border:1px solid var(--border); padding:.25rem .6rem; border-radius:2rem; }
    .admin-badge { font-size:.7rem; background:var(--accent-bg); border:1px solid #bfdbfe; color:var(--accent); padding:.25rem .65rem; border-radius:2rem; font-family:'Space Mono',monospace; font-weight:700; }
    .logout-btn { font-size:.75rem; color:var(--muted); background:#fff; border:1px solid var(--border); border-radius:8px; padding:.28rem .65rem; cursor:pointer; font-family:'DM Sans',sans-serif; transition:all .15s; }
    .logout-btn:hover { border-color:var(--border2); color:var(--text); }

    /* ── FILTER BAR ── */
    .filter-bar { background:#fff; border-bottom:1px solid var(--border); padding:.75rem 1.5rem; position:sticky; top:60px; z-index:150; }
    .filter-inner { max-width:1400px; margin:0 auto; display:flex; flex-wrap:wrap; gap:.5rem; align-items:center; }
    .filter-label { font-size:.72rem; font-weight:600; color:var(--muted); text-transform:uppercase; letter-spacing:.08em; margin-right:.25rem; white-space:nowrap; }
    .filter-chip { display:inline-flex; align-items:center; gap:.3rem; font-size:.75rem; font-weight:500; padding:.3rem .7rem; border-radius:2rem; border:1.5px solid var(--border); background:#fff; cursor:pointer; transition:all .15s; color:var(--muted); white-space:nowrap; }
    .filter-chip:hover { border-color:var(--border2); color:var(--text); }
    .filter-chip.active { color:#fff; border-color:transparent; }
    .filter-chip .dot { width:7px; height:7px; border-radius:50%; flex-shrink:0; }
    .filter-divider { width:1px; height:20px; background:var(--border); margin:0 .25rem; }
    .filter-clear { font-size:.75rem; color:var(--accent); background:none; border:none; cursor:pointer; font-family:'DM Sans',sans-serif; padding:.3rem .5rem; border-radius:6px; }
    .filter-clear:hover { background:var(--accent-bg); }

    /* ── HERO ── */
    .hero { padding:1.5rem 1.5rem 1rem; max-width:1400px; margin:0 auto; }
    .hero h1 { font-size:clamp(1.4rem,3vw,2rem); font-weight:700; color:var(--text); margin-bottom:.2rem; }
    .hero h1 span { color:var(--accent); }
    .hero p { color:var(--muted); font-size:.85rem; }

    /* ── ADMIN PANEL ── */
    .admin-panel { max-width:1400px; margin:0 auto 1rem; padding:0 1.5rem; }
    .admin-inner { background:var(--accent-bg); border:1px solid #bfdbfe; border-radius:12px; padding:1rem 1.25rem; }
    .admin-inner h3 { font-size:.78rem; color:var(--accent); font-family:'Space Mono',monospace; letter-spacing:.08em; text-transform:uppercase; margin-bottom:.85rem; }
    .admin-grid { display:grid; grid-template-columns:repeat(auto-fill,minmax(220px,1fr)); gap:.6rem; }
    .admin-row { display:flex; flex-direction:column; gap:.25rem; }
    .admin-label { font-size:.67rem; color:var(--muted); }
    .admin-code { font-size:.73rem; font-weight:600; color:var(--text); }
    .admin-select { background:#fff; border:1px solid var(--border); border-radius:8px; color:var(--text); font-size:.78rem; padding:.38rem .6rem; outline:none; width:100%; font-family:'DM Sans',sans-serif; }
    .admin-select:focus { border-color:var(--accent); }
    .admin-actions { display:flex; gap:.5rem; margin-top:.85rem; align-items:center; flex-wrap:wrap; }
    .admin-save { background:var(--accent); color:#fff; border:none; border-radius:8px; padding:.45rem .95rem; font-size:.8rem; font-weight:600; cursor:pointer; font-family:'DM Sans',sans-serif; }
    .admin-clear { background:#fff; border:1px solid #dc2626; color:#dc2626; border-radius:8px; padding:.45rem .95rem; font-size:.8rem; cursor:pointer; font-family:'DM Sans',sans-serif; }
    .admin-msg { font-size:.73rem; color:#16a34a; min-height:14px; }

    /* ── TABLE ── */
    .table-wrap { max-width:1400px; margin:0 auto; padding:0 1.5rem 4rem; overflow-x:auto; }
    table { width:100%; border-collapse:collapse; min-width:900px; }
    thead th { font-family:'Space Mono',monospace; font-size:.65rem; letter-spacing:.08em; text-transform:uppercase; color:var(--muted); padding:.6rem .75rem; border-bottom:2px solid var(--border); text-align:left; background:#fff; }
    thead th:first-child { width:100px; }
    thead th.today-col { color:var(--accent); border-bottom-color:var(--accent); }
    .time-col { font-family:'Space Mono',monospace; font-size:.68rem; color:var(--muted); padding:.75rem; vertical-align:top; white-space:nowrap; border-bottom:1px solid var(--border); background:var(--surface); font-weight:700; }
    td { padding:.4rem .35rem; vertical-align:top; border-bottom:1px solid var(--border); }
    td.today-col { background:rgba(37,99,235,.03); }
    .cell { border-radius:8px; padding:.6rem .75rem; min-height:76px; display:flex; flex-direction:column; justify-content:space-between; gap:.2rem; transition:transform .12s,box-shadow .12s; cursor:default; border:1px solid transparent; }
    .cell:hover { transform:translateY(-2px); box-shadow:0 4px 16px rgba(0,0,0,.1); }
    .cell-code { font-size:.62rem; font-family:'Space Mono',monospace; font-weight:700; opacity:.7; text-transform:uppercase; margin-bottom:1px; }
    .cell-subject { font-size:.75rem; font-weight:600; line-height:1.25; }
    .cell-meta { display:flex; align-items:center; gap:.35rem; flex-wrap:wrap; margin-top:2px; }
    .cell-teacher { font-size:.67rem; opacity:.75; }
    .cell-prog { font-size:.62rem; font-family:'Space Mono',monospace; opacity:.6; font-weight:700; }
    .avail-dot { width:6px; height:6px; border-radius:50%; margin-left:auto; flex-shrink:0; }
    .cell-cancelled { opacity:.6; text-decoration-line:line-through; }
    .cancelled-badge { font-size:.62rem; background:#fee2e2; color:#dc2626; border-radius:4px; padding:1px 5px; font-weight:600; }
    .c-free { background:transparent; border:1px dashed var(--border); }
    .c-free .cell-subject { color:var(--muted); font-weight:400; font-size:.72rem; }

    /* programme cell colours */
    .p-dcs    { background:var(--c-dcs-bg);    border-color:#bfdbfe; color:var(--c-dcs); }
    .p-dpsy   { background:var(--c-dpsy-bg);   border-color:#ddd6fe; color:var(--c-dpsy); }
    .p-dhrm   { background:var(--c-dhrm-bg);   border-color:#a5f3fc; color:var(--c-dhrm); }
    .p-dia    { background:var(--c-dia-bg);     border-color:#fde68a; color:var(--c-dia); }
    .p-dhm    { background:var(--c-dhm-bg);     border-color:#a7f3d0; color:var(--c-dhm); }
    .p-ddm    { background:var(--c-ddm-bg);     border-color:#fbcfe8; color:var(--c-ddm); }
    .p-die    { background:var(--c-die-bg);     border-color:#fed7aa; color:var(--c-die); }
    .p-dlsc   { background:var(--c-dlsc-bg);    border-color:#99f6e4; color:var(--c-dlsc); }
    .p-fia    { background:var(--c-fia-bg);     border-color:#c7d2fe; color:var(--c-fia); }
    .p-fiacca { background:var(--c-fiacca-bg);  border-color:#ddd6fe; color:var(--c-fiacca); }
    .p-dosh   { background:var(--c-dosh-bg);    border-color:#fecdd3; color:var(--c-dosh); }
    .p-dhcm   { background:var(--c-dhcm-bg);    border-color:#bae6fd; color:var(--c-dhcm); }
    .p-cib    { background:var(--c-cib-bg);     border-color:#bbf7d0; color:var(--c-cib); }
    .p-chs    { background:var(--c-chs-bg);     border-color:#fef08a; color:var(--c-chs); }
    .p-cie    { background:var(--c-cie-bg);     border-color:#e9d5ff; color:var(--c-cie); }
    .p-uos    { background:var(--c-uos-bg);     border-color:#e2e8f0; color:var(--c-uos); }
    .p-fis    { background:var(--c-fis-bg);     border-color:#fde68a; color:var(--c-fis); }
    .p-dba    { background:var(--c-dba-bg);     border-color:#99f6e4; color:var(--c-dba); }
    .p-odl    { background:var(--c-odl-bg);     border-color:#e5e7eb; color:var(--c-odl); }

    .break-row td { padding:0; border-bottom:1px solid var(--border); }
    .break-label { font-family:'Space Mono',monospace; font-size:.62rem; text-transform:uppercase; letter-spacing:.12em; color:var(--muted); padding:.35rem 1rem; background:var(--surface2); display:flex; align-items:center; gap:.5rem; }
    .break-label::after { content:''; flex:1; height:1px; background:var(--border); }

    .hidden-row { display:none; }
    @keyframes fadeUp { from{opacity:0;transform:translateY(8px)} to{opacity:1;transform:translateY(0)} }
    tbody tr { animation:fadeUp .25s ease both; }
  </style>
</head>
<body>

<!-- ════════ LOGIN ════════ -->
<div id="login-screen">
  <div class="login-box">
    <div class="login-logo">LSBF</div>
    <h2>Campus Timetable</h2>
    <p>May 2026 Semester — Sign in to continue</p>
    <div class="role-btns">
      <button class="role-btn active" id="btn-user" onclick="setRole('user')">👤 Student / Staff</button>
      <button class="role-btn" id="btn-admin" onclick="setRole('admin')">🔐 Admin</button>
    </div>
    <div id="pin-wrap">
      <input class="pin-input" type="password" id="pin-input" placeholder="Enter admin PIN" maxlength="10" onkeydown="if(event.key==='Enter')doLogin()"/>
    </div>
    <button class="login-btn" onclick="doLogin()">Enter →</button>
    <div class="err-msg" id="err-msg"></div>
  </div>
</div>

<!-- ════════ MAIN ════════ -->
<div id="main-screen" style="display:none">

  <header>
    <div class="logo">LSBF <span style="color:var(--muted);font-weight:400">·</span> Timetable</div>
    <div class="header-right">
      <div class="clock-wrap">
        <div class="clock" id="live-clock">00:00:00</div>
        <div class="date-str" id="live-date"></div>
      </div>
      <div class="sem-badge">MAY 2026 · V11</div>
      <div class="admin-badge" id="role-badge" style="display:none">⚙ ADMIN</div>
      <button class="logout-btn" onclick="doLogout()">Sign out</button>
    </div>
  </header>

  <!-- FILTER BAR -->
  <div class="filter-bar">
    <div class="filter-inner" id="filter-inner">
      <span class="filter-label">Programme</span>
    </div>
  </div>

  <div class="hero">
    <h1>Master Campus <span>Class Timetable</span></h1>
    <p>May 2026 Semester &nbsp;·&nbsp; All Programmes</p>
  </div>

  <!-- Admin Panel -->
  <div class="admin-panel" id="admin-panel" style="display:none">
    <div class="admin-inner">
      <h3>⚙ Admin — Class Availability</h3>
      <div class="admin-grid" id="admin-grid"></div>
      <div class="admin-actions">
        <button class="admin-save" onclick="saveAvailability()">Save changes</button>
        <button class="admin-clear" onclick="clearAll()">Reset all</button>
        <div class="admin-msg" id="admin-msg"></div>
      </div>
    </div>
  </div>

  <div class="table-wrap">
    <table id="tt-table">
      <thead>
        <tr>
          <th>Time</th>
          <th id="th-mon">Monday</th>
          <th id="th-tue">Tuesday</th>
          <th id="th-wed">Wednesday</th>
          <th id="th-thu">Thursday</th>
          <th id="th-fri">Friday</th>
          <th id="th-sat">Saturday</th>
          <th id="th-sun">Sunday</th>
        </tr>
      </thead>
      <tbody id="tt-body"></tbody>
    </table>
  </div>
</div>

<script>
const ADMIN_PIN = '1234';

const PROGS = {
  DCS:    { label:'DCS',    color:'#2563eb', cls:'p-dcs'    },
  DPSY:   { label:'DPSY',   color:'#7c3aed', cls:'p-dpsy'   },
  DHRM:   { label:'DHRM',   color:'#0891b2', cls:'p-dhrm'   },
  DIA:    { label:'DIA',    color:'#d97706', cls:'p-dia'    },
  DHM:    { label:'DHM',    color:'#059669', cls:'p-dhm'    },
  DDM:    { label:'DDM',    color:'#db2777', cls:'p-ddm'    },
  DIE:    { label:'DIE',    color:'#ea580c', cls:'p-die'    },
  DLSC:   { label:'DLSC',   color:'#0d9488', cls:'p-dlsc'   },
  FIA:    { label:'FIA',    color:'#4f46e5', cls:'p-fia'    },
  FIACCA: { label:'FIACCA', color:'#7c3aed', cls:'p-fiacca' },
  DOSH:   { label:'DOSH',   color:'#be123c', cls:'p-dosh'   },
  DHCM:   { label:'DHCM',   color:'#0369a1', cls:'p-dhcm'   },
  CIB:    { label:'CIB',    color:'#15803d', cls:'p-cib'    },
  CHS:    { label:'CHS',    color:'#ca8a04', cls:'p-chs'    },
  CIE:    { label:'CIE',    color:'#9333ea', cls:'p-cie'    },
  UOS:    { label:'UOS/UOG',color:'#64748b', cls:'p-uos'    },
  FIS:    { label:'FIS',    color:'#b45309', cls:'p-fis'    },
  DBA:    { label:'DBA',    color:'#0f766e', cls:'p-dba'    },
  ODL:    { label:'ODL',    color:'#6b7280', cls:'p-odl'    },
};

const DAYS = ['Monday','Tuesday','Wednesday','Thursday','Friday','Saturday','Sunday'];
const DKEYS = ['mon','tue','wed','thu','fri','sat','sun'];

// Each entry: { prog, code, subject, room, teacher }
// room field used for block/room info
const SCHEDULE = {
  s1: { // 08:30 - 10:30
    mon: [
      { prog:'DIA',    code:'DAC 1501',  subject:'Financial Accounting 3',             teacher:'Ms Khairul Bariah',   room:'02-01' },
      { prog:'DIE',    code:'ECO 0101',  subject:'Microeconomics',                     teacher:'Mr Firdaus Akmal',    room:'02-02' },
      { prog:'DDM',    code:'DSCM 1242', subject:'Business Microeconomics',            teacher:'Mr Firdaus Akmal',    room:'02-02' },
      { prog:'DIA',    code:'ECO 0101',  subject:'Microeconomics',                     teacher:'Mr Firdaus Akmal',    room:'02-02' },
      { prog:'DBA',    code:'ECO 0101',  subject:'Microeconomics',                     teacher:'Mr Firdaus Akmal',    room:'02-02' },
      { prog:'DLSC',   code:'DSCM 1242', subject:'Business Microeconomics',            teacher:'Mr Firdaus Akmal',    room:'02-02' },
      { prog:'CIE',    code:'ESP 2003',  subject:'English Writing Skill 2',            teacher:'Dr Seyedeh Somayeh',  room:'02-03' },
      { prog:'DPSY',   code:'PSY 2143',  subject:'Psychological Testing',              teacher:'Ms Zakirah',          room:'02-03A'},
      { prog:'UOS',    code:'IMDPSY122', subject:'Everyday Psychology',                teacher:'Ms Tengku Nur Nusrah',room:'02-05' },
      { prog:'DCS',    code:'DCS 1123',  subject:'Database Fundamentals',              teacher:'Mr Vijay Kumar',      room:'02-06' },
    ],
    tue: [
      { prog:'FIA',    code:'ENG 0101',  subject:'English (I)',                        teacher:'Ms Darling Darlene',  room:'02-01' },
      { prog:'DPSY',   code:'PSY 2135',  subject:'Organisational Psychology',          teacher:'Ms Tengku Nur Nusrah',room:'02-02' },
      { prog:'DIE',    code:'MGT 0100',  subject:'Fundamentals of Management',         teacher:'Mr Mohamad Nazmi',    room:'02-03' },
      { prog:'DDM',    code:'MGT1213',   subject:'Management Principles',              teacher:'Mr Mohamad Nazmi',    room:'02-03' },
      { prog:'DBA',    code:'MGT 0100',  subject:'Fundamentals of Management',         teacher:'Mr Mohamad Nazmi',    room:'02-03' },
      { prog:'DHCM',   code:'MGT1213',   subject:'Management Principles',              teacher:'Mr Mohamad Nazmi',    room:'02-03' },
      { prog:'DLSC',   code:'DSCM 1141', subject:'Fundamentals of Management',         teacher:'Mr Mohamad Nazmi',    room:'02-03' },
      { prog:'DOSH',   code:'OSH1112',   subject:'Chemistry',                          teacher:'Dr Noor Aimi',        room:'02-03A'},
      { prog:'CHS',    code:'OSH1112',   subject:'Chemistry',                          teacher:'Dr Noor Aimi',        room:'02-03A'},
      { prog:'FIS',    code:'MTH 0104',  subject:'Mathematics I',                      teacher:'Ms Wan Nurul Huda',   room:'02-05' },
      { prog:'UOS',    code:'MPU3373',   subject:'Integrity & Anti-Corruption',        teacher:'Ms Zuria Suzieanna',  room:'03-01' },
      { prog:'DHM',    code:'IHM1123',   subject:'Introduction to Hospitality Industry',teacher:'Ms Nik Umairah',    room:'03-02' },
      { prog:'DCS',    code:'DCS 2133',  subject:'Platform-based Development',         teacher:'Mr Vijay Kumar',      room:'Lab A' },
    ],
    wed: [
      { prog:'DPSY',   code:'PSY 2241',  subject:'Adolescent Psychology',              teacher:'Ms E',                room:'02-01' },
      { prog:'FIACCA', code:'FA2',       subject:'Maintaining Financial Records',      teacher:'Mr Alex Chang',       room:'02-02' },
      { prog:'DIE',    code:'ENG 0101',  subject:'English for Academic Purposes',      teacher:'Dr Seyedeh Somayeh',  room:'02-03' },
      { prog:'DBA',    code:'ENG 0101',  subject:'English for Academic Purposes',      teacher:'Dr Seyedeh Somayeh',  room:'02-03' },
      { prog:'DHM',    code:'HMI 1213',  subject:'Housekeeping Management',            teacher:'Ms Nur Nazirah',      room:'02-03A'},
      { prog:'DHRM',   code:'DHRM 1116', subject:'Performance Management',             teacher:'Mdm Noorliza',        room:'02-05' },
      { prog:'DDM',    code:'MKT 0102',  subject:'Social Media Marketing',             teacher:'Ms Nabilla Mohd Johan',room:'02-06'},
      { prog:'CIE',    code:'ASC 1000',  subject:'Active Listening Skills',            teacher:'Ms Darling Darlene',  room:'Lab A' },
      { prog:'CIB',    code:'BAS 1134',  subject:'Basic Statistics',                   teacher:'Ms Wan Nurul Huda',   room:'03-02' },
    ],
    thu: [
      { prog:'CIE',    code:'ASC 1001',  subject:'Reading & Vocabulary Skills 1',      teacher:'Dr Seyedeh Somayeh',  room:'02-01' },
      { prog:'DIA',    code:'ACT 0102',  subject:'Costing',                            teacher:'Ms Norzilah Mahmod',  room:'02-02' },
      { prog:'DHCM',   code:'DHM1114',   subject:'Anatomy and Physiology',             teacher:'Dr Nurliana',         room:'02-03' },
      { prog:'DLSC',   code:'DSCM 2141', subject:'International Logistics',            teacher:'Prof Vijay',          room:'02-03A'},
      { prog:'UOS',    code:'IMDPSY112', subject:'Foundations of Social & Dev. Psychology',teacher:'Ms Tengku Nur Nusrah',room:'02-05'},
    ],
    fri: [
      { prog:'DPSY',   code:'PSY 2242',  subject:'Counselling Psychology',             teacher:'Mr Anwari Ariffin',   room:'02-01' },
      { prog:'FIACCA', code:'MA2',       subject:'Managing Costs and Finance',         teacher:'Ms Norzilah Mahmod',  room:'02-02' },
      { prog:'CIB',    code:'ACC 1234',  subject:'Introduction to Accounting',         teacher:'Ms Siti Mahirah',     room:'02-03' },
      { prog:'DIA',    code:'DAC 1000',  subject:'Financial Accounting 1',             teacher:'Ms Siti Mahirah',     room:'02-03' },
      { prog:'UOS',    code:'MPU3183',   subject:'Penghayatan Etika & Peradaban',      teacher:'Ms Zuria Suzieanna',  room:'03-01' },
      { prog:'FIS',    code:'FIA 1002',  subject:'Basic ICT',                          teacher:'Mr Veluswamy',        room:'03-02' },
    ],
    sat: [
      { prog:'ODL',    code:'DAC 100',   subject:'Financial Accounting 1',             teacher:'Ms Siti Mahirah',     room:'02-01' },
      { prog:'ODL',    code:'MTH 0101',  subject:'Business Statistics',                teacher:'Ms Wan Nurul Huda',   room:'02-02' },
    ],
    sun: [
      { prog:'ODL',    code:'GED 108',   subject:'General Psychology',                 teacher:'Ms Tengku Nur Nusrah',room:'02-01' },
      { prog:'ODL',    code:'BBBA 2074', subject:'E-Commerce',                         teacher:'Ms Nabilla Mohd Johan',room:'02-02'},
      { prog:'DPSY',   code:'PSY 1135',  subject:'Social Psychology (PT)',             teacher:'Mr Anwari Ariffin',   room:'02-03' },
    ],
  },
  s2: { // 10:45 - 12:45
    mon: [
      { prog:'DHRM',   code:'DHRM 1115', subject:'Human Resource Development',         teacher:'Mdm Noorliza',        room:'02-01' },
      { prog:'FIACCA', code:'FA1',       subject:'Recording Financial Transactions',   teacher:'Ms Norzilah Mahmod',  room:'02-02' },
      { prog:'DPSY',   code:'PSY 2134',  subject:'Cross-cultural Psychology',          teacher:'Mr Anwari Arifin',    room:'02-03' },
      { prog:'DHM',    code:'COR 1133',  subject:'Personality Development',            teacher:'Mr Mohamad Nazmi',    room:'02-03A'},
      { prog:'CIE',    code:'ESP 2000',  subject:'Public Speaking',                    teacher:'Ms Darling Darlene',  room:'02-05' },
      { prog:'DDM',    code:'BAN 0100',  subject:'Fundamentals of Business',           teacher:'Mr Firdaus Akmal',    room:'02-06' },
      { prog:'DPSY',   code:'PSY 1133',  subject:'Research Methodology',               teacher:'Ms Tengku Nur Nusrah',room:'03-01' },
      { prog:'DCS',    code:'DCS 1113',  subject:'Programming Fundamentals',           teacher:'Mr Vijay Kumar',      room:'Lab A' },
    ],
    tue: [
      { prog:'FIACCA', code:'FIP',       subject:'Introduction to Professionalism',    teacher:'Ms Shakila Rao',      room:'02-01' },
      { prog:'DHCM',   code:'OSH 1313',  subject:'Introduction to OHS',               teacher:'Ms Jazatul Ikma',     room:'02-02' },
      { prog:'DOSH',   code:'OSH 1313',  subject:'Introduction to OHS',               teacher:'Ms Jazatul Ikma',     room:'02-02' },
      { prog:'DIE',    code:'MTH 0101',  subject:'Statistics',                         teacher:'Ms Wan Nurul Huda',   room:'02-03' },
      { prog:'DDM',    code:'DSCM 1144', subject:'Business Statistics',                teacher:'Ms Wan Nurul Huda',   room:'02-03' },
      { prog:'DBA',    code:'MTH 0101',  subject:'Statistics',                         teacher:'Ms Wan Nurul Huda',   room:'02-03' },
      { prog:'DLSC',   code:'DSCM 1144', subject:'Business Statistics',                teacher:'Ms Wan Nurul Huda',   room:'02-03' },
      { prog:'CHS',    code:'MTH 0101',  subject:'Statistics',                         teacher:'Ms Wan Nurul Huda',   room:'02-03' },
      { prog:'DPSY',   code:'PSY 1331',  subject:'Statistics',                         teacher:'Ms Wan Nurul Huda',   room:'02-03' },
      { prog:'FIA',    code:'FIA 3001',  subject:'Writing & Research Skills',          teacher:'Dr Nurliana',         room:'02-03A'},
      { prog:'DHM',    code:'SFH2133',   subject:'Safety & Hygiene',                   teacher:'Ms Nik Umairah',      room:'02-05' },
      { prog:'DCS',    code:'DCS 1253',  subject:'Algorithms and Complexity',          teacher:'Mr Vijay Kumar',      room:'Lab A' },
    ],
    wed: [
      { prog:'FIA',    code:'FIN 0101',  subject:'Introduction to Finance',            teacher:'Mr Alex Chang',       room:'02-01' },
      { prog:'DCS',    code:'DCS 1243',  subject:'Statistics and Probability',         teacher:'Ms Wan Nurul Huda',   room:'02-02' },
      { prog:'DHRM',   code:'MKT 0100',  subject:'Fundamentals of Marketing',          teacher:'Ms Nabilla Mohd Johan',room:'02-03'},
      { prog:'DIE',    code:'MKT 0100',  subject:'Fundamentals of Marketing',          teacher:'Ms Nabilla Mohd Johan',room:'02-03'},
      { prog:'DDM',    code:'MKT 0100',  subject:'Fundamentals of Marketing',          teacher:'Ms Nabilla Mohd Johan',room:'02-03'},
      { prog:'DBA',    code:'MKT 0100',  subject:'Fundamentals of Marketing',          teacher:'Ms Nabilla Mohd Johan',room:'02-03'},
      { prog:'DIA',    code:'DSCM 1241', subject:'Introduction to Marketing',          teacher:'Ms Nabilla Mohd Johan',room:'02-03'},
      { prog:'DLSC',   code:'DSCM 1241', subject:'Introduction to Marketing',          teacher:'Ms Nabilla Mohd Johan',room:'02-03'},
      { prog:'FIACCA', code:'FAU',       subject:'Foundations in Audit',               teacher:'Ms Khairul Bariah',   room:'02-03A'},
      { prog:'CIE',    code:'ESP 2004',  subject:'Creative Writing',                   teacher:'Ms Darling Darlene',  room:'02-05' },
      { prog:'DPSY',   code:'PSY 1332',  subject:'Abnormal Psychology',                teacher:'Ms E',                room:'02-06' },
      { prog:'UOS',    code:'AI1101',    subject:'Computer Fundamentals',              teacher:'Mr Veluswamy',        room:'03-01' },
      { prog:'DHM',    code:'CUS 1113',  subject:'Fundamental of Cuisine',             teacher:'Mr Mohamad Nazmi',    room:'03-02' },
    ],
    thu: [
      { prog:'DHCM',   code:'COM1233',   subject:'Communication Skills',               teacher:'Ms Darling Darlene',  room:'02-01' },
      { prog:'DPSY',   code:'PSY 2132',  subject:'Applied Psychology',                 teacher:'Ms Shakila Rao',      room:'02-02' },
      { prog:'DLSC',   code:'DSCM 2142', subject:'Physical Distribution & Warehouse Mgmt', teacher:'Prof Vijay',     room:'02-03' },
      { prog:'DIA',    code:'AUD 0100',  subject:'Auditing Application',               teacher:'Ms Khairul Bariah',   room:'02-03A'},
      { prog:'DDM',    code:'CS 0100',   subject:'Fundamentals of IT',                 teacher:'Ms Syuhada Azwa',     room:'02-05' },
      { prog:'DCS',    code:'DCS2143',   subject:'Human-Computer Interaction',         teacher:'Mr Veluswamy',        room:'Lab A' },
    ],
    fri: [
      { prog:'CIB',    code:'AEG 1123',  subject:'Academic English',                   teacher:'Ms Darling Darlene',  room:'02-01' },
      { prog:'CHS',    code:'AEG 1123',  subject:'Academic English',                   teacher:'Ms Darling Darlene',  room:'02-01' },
      { prog:'DOSH',   code:'OSH1115',   subject:'Microbiology',                       teacher:'Dr Nurliana',         room:'02-02' },
      { prog:'FIA',    code:'DAC 102',   subject:'Management Accounting',              teacher:'Ms Norzilah Mahmod',  room:'02-03' },
      { prog:'DBA',    code:'CS 0101',   subject:'Fundamentals of Multimedia Technology',teacher:'Ms Syuhada Azwa',   room:'02-03A'},
    ],
    sat: [],
    sun: [
      { prog:'ODL',    code:'MGT 0102',  subject:'Introduction to Entrepreneurship',   teacher:'Ms Nabilla Mohd Johan',room:'02-01'},
      { prog:'ODL',    code:'CS 0100',   subject:'Fundamentals of IT',                 teacher:'Mr B',                room:'02-02' },
      { prog:'DPSY',   code:'PSY 1134',  subject:'Sensation & Perception (PT)',        teacher:'Mr Anwari Ariffin',   room:'02-03' },
    ],
  },
  break: {},
  s3: { // 01:45 - 03:45
    mon: [
      { prog:'DPSY',   code:'PSY 1134',  subject:'Sensation and Perception',           teacher:'Ms Zakirah',          room:'02-01' },
      { prog:'CIE',    code:'ESP 3000',  subject:'Writing and Reporting',              teacher:'Dr Seyedeh Somayeh',  room:'02-03' },
      { prog:'DIA',    code:'TAX 0100',  subject:'Taxation System',                    teacher:'Ms Khairul Bariah',   room:'02-03A'},
      { prog:'DHM',    code:'HOH 1233',  subject:'Supervision in Hospitality Industry',teacher:'Mr Mohamad Nazmi',    room:'02-05' },
      { prog:'DHRM',   code:'DHRM 1118',subject:'Occupational Safety & Health Mgmt',  teacher:'Ms Jazatul Ikma',     room:'02-06' },
      { prog:'DDM',    code:'MGT 0103',  subject:'Human Resource Management',          teacher:'Ms Nabilla Mohd Johan',room:'03-01'},
      { prog:'DLSC',   code:'DSCM 1142',subject:'Intro to Human Resource Management', teacher:'Ms Nabilla Mohd Johan',room:'03-01'},
      { prog:'UOS',    code:'IMDPSY111',subject:'Foundation of Biological & Cognitive Psych',teacher:'Ms Tengku Nur Nusrah',room:'03-02'},
      { prog:'DCS',    code:'DCS 1133',  subject:'Computer Architecture',              teacher:'Mr Vijay Kumar',      room:'Lab A' },
    ],
    tue: [
      { prog:'DLSC',   code:'DSCM 1143',subject:'Accounting and Business Decisions',  teacher:'Ms Norzilah Mahmod',  room:'02-01' },
      { prog:'DIA',    code:'ACT 0101',  subject:'Accounting and Business Decisions',  teacher:'Ms Norzilah Mahmod',  room:'02-01' },
      { prog:'DOSH',   code:'OSH1111',   subject:'General Language Training',          teacher:'Dr Seyedeh Somayeh',  room:'02-02' },
      { prog:'DIE',    code:'CTA 1000',  subject:'Creative Thinking',                  teacher:'Dr Nurliana',         room:'02-03' },
      { prog:'DBA',    code:'CTA 1000',  subject:'Creative Thinking',                  teacher:'Dr Nurliana',         room:'02-03' },
      { prog:'CIE',    code:'CTA 1000',  subject:'Creative Thinking',                  teacher:'Dr Nurliana',         room:'02-03' },
      { prog:'DHM',    code:'LMH 1223',  subject:'Hotel Operations Management',        teacher:'Ms Nik Umairah',      room:'02-03A'},
      { prog:'DDM',    code:'MGT 0102',  subject:'Intro to Digital Entrepreneurship',  teacher:'Mdm Noorliza',        room:'02-05' },
      { prog:'FIS',    code:'CC 0100',   subject:'Co-curriculum',                      teacher:'Ms Nabilla Mohd Johan',room:'02-06'},
      { prog:'FIA',    code:'CC 0100',   subject:'Co-curriculum',                      teacher:'Ms Nabilla Mohd Johan',room:'02-06'},
      { prog:'UOS',    code:'MPU3193',   subject:'Philosophy & Current Issues',        teacher:'Ms Zuria Suzieanna',  room:'03-01' },
      { prog:'DPSY',   code:'PSY 1135',  subject:'Social Psychology',                  teacher:'Ms Shakila Rao',      room:'03-02' },
      { prog:'DCS',    code:'DCS 2123',  subject:'Systems Fundamentals',               teacher:'Mr Vijay Kumar',      room:'Lab A' },
    ],
    wed: [],
    thu: [
      { prog:'DPSY',   code:'PSY 2131',  subject:'Physiological Psychology',           teacher:'Dr Nurliana',         room:'02-01' },
      { prog:'DLSC',   code:'DSCM 2143',subject:'Operations Management',              teacher:'Ms Nabilla Mohd Johan',room:'02-02'},
      { prog:'CIE',    code:'ESP 1000',  subject:'Basic English Grammar',              teacher:'Ms Darling Darlene',  room:'02-03' },
      { prog:'DHCM',   code:'DHM1124',   subject:'Introduction to Health Care Management',teacher:'Dr Seyedeh Somayeh',room:'02-03A'},
      { prog:'DIA',    code:'FRA 0100',  subject:'Introduction to Financial Reporting & Audit',teacher:'Ms Norzilah Mahmod',room:'02-05'},
      { prog:'DHRM',   code:'DHRM 1114',subject:'Managing Human Resource',            teacher:'Prof Vijay',          room:'02-06' },
      { prog:'DCS',    code:'DCS 1323',  subject:'Network & Data Communication',       teacher:'Mr Vijay Kumar',      room:'Lab A' },
    ],
    fri: [
      { prog:'FIA',    code:'ENG 0102',  subject:'English II',                         teacher:'Ms Darling Darlene',  room:'02-01' },
      { prog:'DBA',    code:'GED 108',   subject:'General Psychology',                 teacher:'Ms Tengku Nur Nusrah',room:'02-02' },
      { prog:'CIB',    code:'MGT 1114',  subject:'Basic Management',                   teacher:'Mr Mohamad Nazmi',    room:'02-03' },
      { prog:'CHS',    code:'MGT 1114',  subject:'Basic Management',                   teacher:'Mr Mohamad Nazmi',    room:'02-03' },
      { prog:'FIS',    code:'FIA 1001',  subject:'Thinking Skills',                    teacher:'Dr Nurliana',         room:'02-03A'},
      { prog:'FIACCA', code:'FMA',       subject:'Management Accounting',              teacher:'Ms Norzilah Mahmod',  room:'02-05' },
      { prog:'DPSY',   code:'PSY 1132',  subject:'History of Psychology',              teacher:'Ms Zakirah',          room:'02-06' },
      { prog:'UOS',    code:'MPU3143',   subject:'Bahasa Malaysia Komunikasi 2',       teacher:'Ms Zuria Suzieanna',  room:'03-01' },
      { prog:'DOSH',   code:'OSH1114',   subject:'Applied Digital Skills',             teacher:'Mr Veluswamy',        room:'Lab A' },
    ],
    sat: [
      { prog:'ODL',    code:'BBEC 107',  subject:'Organisation Behaviour',             teacher:'Mr Mohamad Nazmi',    room:'02-01' },
      { prog:'ODL',    code:'ENG 0100',  subject:'English Language',                   teacher:'Dr Seyedeh Somayeh',  room:'02-02' },
    ],
    sun: [],
  },
  s4: { // 04:00 - 06:00 (all free per PDF)
    mon:[], tue:[], wed:[], thu:[], fri:[], sat:[], sun:[]
  },
};

const SLOT_META = [
  { id:'s1', label:'08:30 – 10:30' },
  { id:'s2', label:'10:45 – 12:45' },
  { id:'break', label:'' },
  { id:'s3', label:'01:45 – 03:45' },
  { id:'s4', label:'04:00 – 06:00' },
];

let availability = {};
let currentRole = 'user';
let clockTimer = null;
let activeFilters = new Set();
let allProgsInData = new Set();

// ── gather which progs actually appear ──
function gatherProgs() {
  SLOT_META.filter(s=>s.id!=='break').forEach(s=>{
    DKEYS.forEach(d=>{
      (SCHEDULE[s.id][d]||[]).forEach(e=>allProgsInData.add(e.prog));
    });
  });
}

// ── AUTH ──
function setRole(r){
  currentRole=r;
  document.getElementById('btn-user').classList.toggle('active',r==='user');
  document.getElementById('btn-admin').classList.toggle('active',r==='admin');
  document.getElementById('pin-wrap').style.display=r==='admin'?'flex':'none';
  document.getElementById('err-msg').textContent='';
}
function doLogin(){
  if(currentRole==='admin'){
    const pin=document.getElementById('pin-input').value.trim();
    if(pin!==ADMIN_PIN){document.getElementById('err-msg').textContent='✕ Incorrect PIN.';return;}
  }
  document.getElementById('login-screen').style.display='none';
  document.getElementById('main-screen').style.display='block';
  if(currentRole==='admin'){
    document.getElementById('admin-panel').style.display='block';
    document.getElementById('role-badge').style.display='inline';
    buildAdminGrid();
  }
  gatherProgs();
  buildFilterBar();
  buildTable();
  startClock();
  highlightToday();
}
function doLogout(){
  clearInterval(clockTimer);
  document.getElementById('main-screen').style.display='none';
  document.getElementById('login-screen').style.display='flex';
  document.getElementById('admin-panel').style.display='none';
  document.getElementById('role-badge').style.display='none';
  document.getElementById('pin-input').value='';
  document.getElementById('err-msg').textContent='';
  activeFilters.clear();
  currentRole='user';
  setRole('user');
}

// ── CLOCK ──
function startClock(){
  const DN=['Sunday','Monday','Tuesday','Wednesday','Thursday','Friday','Saturday'];
  const MN=['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];
  function tick(){
    const n=new Date();
    document.getElementById('live-clock').textContent=
      String(n.getHours()).padStart(2,'0')+':'+String(n.getMinutes()).padStart(2,'0')+':'+String(n.getSeconds()).padStart(2,'0');
    document.getElementById('live-date').textContent=
      DN[n.getDay()]+', '+n.getDate()+' '+MN[n.getMonth()]+' '+n.getFullYear();
  }
  tick(); clockTimer=setInterval(tick,1000);
}

// ── TODAY HIGHLIGHT ──
function highlightToday(){
  const d=new Date().getDay(); // 0=Sun
  const map={1:'th-mon',2:'th-tue',3:'th-wed',4:'th-thu',5:'th-fri',6:'th-sat',0:'th-sun'};
  const id=map[d];
  if(id){
    const el=document.getElementById(id);
    if(el) el.classList.add('today-col');
  }
}

// ── FILTER BAR ──
function buildFilterBar(){
  const wrap=document.getElementById('filter-inner');
  wrap.innerHTML='<span class="filter-label">Programme</span>';
  const sorted=[...allProgsInData].sort();
  sorted.forEach(prog=>{
    const p=PROGS[prog]||{label:prog,color:'#888',cls:'p-odl'};
    const chip=document.createElement('button');
    chip.className='filter-chip';
    chip.dataset.prog=prog;
    chip.innerHTML=`<span class="dot" style="background:${p.color}"></span>${p.label}`;
    chip.onclick=()=>toggleFilter(prog,chip,p.color);
    wrap.appendChild(chip);
  });
  const div=document.createElement('div'); div.className='filter-divider'; wrap.appendChild(div);
  const clr=document.createElement('button'); clr.className='filter-clear'; clr.textContent='Clear all';
  clr.onclick=clearFilters; wrap.appendChild(clr);
}

function toggleFilter(prog,chip,color){
  if(activeFilters.has(prog)){
    activeFilters.delete(prog);
    chip.classList.remove('active');
    chip.style.background='';
    chip.style.color='';
  } else {
    activeFilters.add(prog);
    chip.classList.add('active');
    chip.style.background=color;
    chip.style.color='#fff';
  }
  rebuildTable();
}

function clearFilters(){
  activeFilters.clear();
  document.querySelectorAll('.filter-chip').forEach(c=>{
    c.classList.remove('active');
    c.style.background='';
    c.style.color='';
  });
  rebuildTable();
}

// ── BUILD TABLE ──
function buildTable(){ document.getElementById('tt-body').innerHTML=''; renderRows(); }
function rebuildTable(){ renderRows(); }

function renderRows(){
  const tbody=document.getElementById('tt-body');
  tbody.innerHTML='';
  const todayIdx=new Date().getDay(); // 0=Sun,1=Mon…6=Sat → DKEYS index: mon=0…sun=6
  const dayMap={1:0,2:1,3:2,4:3,5:4,6:5,0:6};
  const tdi=dayMap[todayIdx];

  SLOT_META.forEach(slot=>{
    if(slot.id==='break'){
      const tr=document.createElement('tr'); tr.className='break-row';
      tr.innerHTML='<td colspan="8"><div class="break-label"> Lunch Break · 12:45 – 01:45</div></td>';
      tbody.appendChild(tr); return;
    }

    const entries=DKEYS.map(d=>(SCHEDULE[slot.id][d]||[]));
    // filter check: if filters active, hide row if no matching entries exist in any day
    if(activeFilters.size>0){
      const anyMatch=entries.some(dayEntries=>dayEntries.some(e=>activeFilters.has(e.prog)));
      if(!anyMatch) return;
    }

    const tr=document.createElement('tr');
    let html='<td class="time-col">'+slot.label.replace(' – ','<br>')+'</td>';
    DKEYS.forEach((day,di)=>{
      const isToday=di===tdi;
      const dayEntries=(SCHEDULE[slot.id][day]||[]);
      const filtered=activeFilters.size>0?dayEntries.filter(e=>activeFilters.has(e.prog)):dayEntries;
      html+='<td'+(isToday?' class="today-col"':'')+'>';
      if(filtered.length===0){
        html+='<div class="cell c-free"><div class="cell-subject">—</div></div>';
      } else {
        filtered.forEach(e=>{
          const p=PROGS[e.prog]||PROGS.ODL;
          const k=slot.id+'_'+day+'_'+e.code;
          const avail=availability[k]||'available';
          const cancelled=avail==='cancelled';
          html+='<div class="cell '+p.cls+(cancelled?' cell-cancelled':'')+'" style="margin-bottom:'+(filtered.length>1?'4px':'0')+'px">';
          html+='<div class="cell-code">'+e.prog+' · '+e.code+'</div>';
          html+='<div class="cell-subject">'+(cancelled?'<span class="cancelled-badge">Cancelled</span> ':'')+e.subject+'</div>';
          html+='<div class="cell-meta"><span class="cell-teacher">'+e.teacher+'</span>';
          if(e.room) html+='<span class="cell-prog" style="margin-left:auto">'+e.room+'</span>';
          if(!cancelled) html+='<span class="avail-dot" style="background:#16a34a"></span>';
          html+='</div></div>';
        });
      }
      html+='</td>';
    });
    tr.innerHTML=html;
    tbody.appendChild(tr);
  });
}

// ── ADMIN ──
function buildAdminGrid(){
  const grid=document.getElementById('admin-grid'); grid.innerHTML='';
  SLOT_META.filter(s=>s.id!=='break').forEach(slot=>{
    DKEYS.forEach((day,di)=>{
      (SCHEDULE[slot.id][day]||[]).forEach(e=>{
        const k=slot.id+'_'+day+'_'+e.code;
        const cur=availability[k]||'available';
        const div=document.createElement('div'); div.className='admin-row';
        div.innerHTML='<div class="admin-label">'+DAYS[di]+' · '+slot.label+'</div>'+
          '<div class="admin-code">'+e.prog+' · '+e.code+'</div>'+
          '<select class="admin-select" id="sel_'+k+'">'+
          '<option value="available"'+(cur==='available'?' selected':'')+'>✅ Available</option>'+
          '<option value="cancelled"'+(cur==='cancelled'?' selected':'')+'>❌ Cancelled</option>'+
          '</select>';
        grid.appendChild(div);
      });
    });
  });
}
function saveAvailability(){
  SLOT_META.filter(s=>s.id!=='break').forEach(slot=>{
    DKEYS.forEach(day=>{
      (SCHEDULE[slot.id][day]||[]).forEach(e=>{
        const k=slot.id+'_'+day+'_'+e.code;
        const sel=document.getElementById('sel_'+k);
        if(sel) availability[k]=sel.value;
      });
    });
  });
  rebuildTable();
  const msg=document.getElementById('admin-msg');
  msg.textContent='✓ Changes saved';
  setTimeout(()=>{msg.textContent='';},2500);
}
function clearAll(){
  availability={};
  buildAdminGrid();
  rebuildTable();
  document.getElementById('admin-msg').textContent='✓ Reset to defaults';
  setTimeout(()=>{document.getElementById('admin-msg').textContent='';},2500);
}
</script>
</body>
</html>
