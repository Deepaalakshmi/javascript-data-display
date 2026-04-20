# javascript-data-display
machine data card using js and html



<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Machine Dashboard</title>
  <style>
    body {
      margin: 0;
      font-family: "Segoe UI", Arial, sans-serif;
      background: linear-gradient(to right, #eef2f3, #dfe9f3);
    }

    h2 {
      text-align: center;
      padding: 20px;
      margin: 0;
    }

    .container {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
      gap: 20px;
      padding: 20px;
    }

    .card {
      background: white;
      border-radius: 12px;
      padding: 20px;
      box-shadow: 0 6px 15px rgba(0,0,0,0.1);
      transition: transform 0.2s, box-shadow 0.2s;
      position: relative;
      overflow: hidden;
    }

    .card:hover {
      transform: translateY(-5px);
      box-shadow: 0 10px 25px rgba(0,0,0,0.15);
    }

    .status {
      font-weight: bold;
      padding: 5px 10px;
      border-radius: 20px;
      display: inline-block;
      font-size: 14px;
    }

    .running {
      background: #e6f9ec;
      color: #1b8a3c;
    }

    .stopped {
      background: #fdecea;
      color: #c0392b;
    }

    .warning {
      background: #fff4e5;
      color: #e67e22;
    }

    .temp {
      font-size: 28px;
      margin-top: 10px;
    }

    .bar {
      height: 8px;
      border-radius: 5px;
      background: #ddd;
      margin-top: 10px;
      overflow: hidden;
    }

    .fill {
      height: 100%;
      border-radius: 5px;
    }

    .low { background: #2ecc71; }
    .medium { background: #f1c40f; }
    .high { background: #e74c3c; }
  </style>
</head>
<body>

<h2>⚙️ Machine Monitoring Dashboard</h2>
<div class="container" id="machineContainer"></div>

<script>
  const machines = [
    { name: "PLC_CUT_SECTOR1", status: "Running", temperature: 65 },
    { name: "PLC_CUT_SECTOR2", status: "Stopped", temperature: 30 },
    { name: "PLC_CUT_SECTOR3", status: "Warning", temperature: 85 }
  ];

  const container = document.getElementById("machineContainer");

  machines.forEach(machine => {
    const card = document.createElement("div");
    card.className = "card";

    let statusClass = machine.status.toLowerCase();

    // Temperature color logic
    let tempClass = "low";
    if (machine.temperature > 70) tempClass = "high";
    else if (machine.temperature > 50) tempClass = "medium";

    card.innerHTML = `
      <h3>${machine.name}</h3>
      <span class="status ${statusClass}">${machine.status}</span>
      <div class="temp">${machine.temperature}°C</div>

      <div class="bar">
        <div class="fill ${tempClass}" style="width:${machine.temperature}%"></div>
      </div>
    `;

    container.appendChild(card);
  });
</script>

</body>
</html>
