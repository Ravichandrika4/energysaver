# energysaver
Smart Energy Manager – An AI-inspired classroom energy optimization system.  Detects occupancy, automatically turns 🌀 fans and 💡 lights ON/OFF, and tracks energy savings. Provides real-time monitoring, live empty-time counter, and usage reports. Helps reduce energy waste and promotes sustainable practices . 

code
1.index.html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Smart Energy Manager</title>
<link rel="stylesheet" href="style.css">
</head>
<body>

<div class="landing">
    <h1>⚡ Smart Energy Manager</h1>
    <p>AI-based Classroom Energy Optimization</p>
    <button onclick="window.location.href='dashboard.html'">Enter Dashboard</button>
</div>

</body>
</html>
2.dashboard.html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Dashboard</title>
<link rel="stylesheet" href="style.css">
</head>
<body>

<h2>📊 Dashboard</h2>

<div class="grid">
    <div class="box" onclick="window.location.href='classroom.html'">🏫 Classroom Control</div>
    <div class="box" onclick="window.location.href='report.html'">📈 Energy Reports</div>
    <div class="box" onclick="alert('IoT Sensors Connected (Demo)')">📡 Sensors</div>
</div>

<div style="text-align:center; margin-top:30px;">
    <button onclick="window.location.href='index.html'">⬅ Logout</button>
</div>

</body>
</html>
3.classroom.html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Classroom Control</title>
<link rel="stylesheet" href="style.css">
</head>
<body>

<h2>🏫 Classroom: CSE-101</h2>

<!-- Status with Live Empty Time -->
<div class="status">
    Occupancy: <span id="occ">Occupied</span><br>
    Empty Time: <span id="emptyTime">0</span> sec
</div>

<!-- Devices -->
<div class="devices">
    <div id="fan">🌀 Fan ON</div>
    <div id="light">💡 Light ON</div>
</div>

<!-- Control Buttons -->
<div style="text-align:center; margin-top:20px;">
    <button class="red" onclick="setEmpty()">Set Empty</button>
    <button class="green" onclick="setOccupied()">Set Occupied</button>
    <button onclick="window.location.href='dashboard.html'">⬅ Back</button>
</div>

<!-- Warning Message -->
<div id="warning" style="text-align:center; color:red; font-weight:bold; margin-top:20px;"></div>

<script>
// ======= Variables =======
let emptyTime = 0;
let timer;

// ======= Set Empty Function =======
function setEmpty(){
    document.getElementById("occ").innerText = "Empty";
    document.getElementById("warning").innerText = "";
    clearInterval(timer);
    emptyTime = 0;
    document.getElementById("emptyTime").innerText = emptyTime; // reset display

    timer = setInterval(()=>{
        emptyTime++;
        document.getElementById("emptyTime").innerText = emptyTime; // update live

        if(emptyTime >= 10){
            // Turn OFF devices
            document.getElementById("fan").innerText = "Fan OFF";
            document.getElementById("light").innerText = "Light OFF";

            // Show warning
            document.getElementById("warning").innerText = "⚠️ Fans and Lights turned OFF to save energy!";

            // Save demo data
            localStorage.setItem("savedUnits","5 Units Saved (Demo)");

            clearInterval(timer);
        }
    },1000);
}

// ======= Set Occupied Function =======
function setOccupied(){
    clearInterval(timer);
    emptyTime = 0;

    document.getElementById("occ").innerText = "Occupied";
    document.getElementById("fan").innerText = "🌀 Fan ON";
    document.getElementById("light").innerText = "💡 Light ON";
    document.getElementById("warning").innerText = "";
    document.getElementById("emptyTime").innerText = emptyTime;

    // Keep previous saved units if any
    localStorage.setItem("savedUnits", localStorage.getItem("savedUnits") || "0 Units Saved (Demo)");
}
</script>

</body>
</html>

4.report.html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Energy Report</title>
<link rel="stylesheet" href="style.css">
</head>
<body>

<h2>📈 Energy Report</h2>

<p id="reportData">No data yet</p>

<div style="text-align:center; margin-top:30px;">
    <button onclick="window.location.href='dashboard.html'">⬅ Back</button>
</div>

<script>
const data = localStorage.getItem("savedUnits") || "No data yet";
document.getElementById("reportData").innerText = data;
</script>

</body>
</html>
5.style.css
/* ========== Global Styles ========== */
body{
    font-family: Arial, sans-serif;
    background:#f5f5f5;
    color:#222;
    margin:0;
    padding:0;
}

h1,h2{
    text-align:center;
}

button{
    padding:10px 20px;
    margin:10px;
    border:none;
    border-radius:8px;
    cursor:pointer;
    font-size:16px;
}

button:hover{
    opacity:0.9;
}

/* ========== Landing Page ========== */
.landing{
    display:flex;
    flex-direction:column;
    justify-content:center;
    align-items:center;
    height:100vh;
    background:#38bdf8;
    color:white;
}

/* ========== Dashboard Page ========== */
.grid{
    display:flex;
    justify-content:center;
    gap:20px;
    margin-top:50px;
}

.box{
    background:#fcd34d;
    padding:40px;
    text-align:center;
    border-radius:12px;
    cursor:pointer;
    width:180px;
    font-size:18px;
}

.box:hover{
    background:#fbbf24;
}

/* ========== Classroom Page ========== */
.devices{
    display:flex;
    justify-content:center;
    gap:50px;
    margin-top:30px;
    font-size:28px;
}

.status{
    text-align:center;
    margin-top:20px;
    font-size:20px;
}

button.green{
    background:#22c55e;
    color:black;
}

button.red{
    background:#ef4444;
    color:white;
}

/* ========== Report Page ========== */
#reportData{
    text-align:center;
    font-size:20px;
    margin-top:50px;
}

<img width="1886" height="773" alt="Screenshot 2026-01-22 232057" src="https://github.com/user-attachments/assets/b5afeba1-af89-4cdc-95f2-b93dd3be168d" />
<img width="1900" height="812" alt="Screenshot 2026-01-22 232128" src="https://github.com/user-attachments/assets/0ba351f3-a15f-4e3e-8372-298f105db89e" />




