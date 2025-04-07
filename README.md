<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Employee Management System</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Segoe UI', sans-serif;
    }
    body {
      background: linear-gradient(to bottom, #fffbea, #f7f7f7);
      color: #333;
    }
    header {
      background: #fbc531;
      padding: 30px 20px;
      text-align: center;
    }
    header h1 {
      color: #2f3640;
      font-size: 2.5rem;
    }
    header p {
      color: #444;
      font-size: 1.2rem;
      margin-top: 10px;
    }
    nav {
      background: #636e72;
      text-align: center;
      padding: 15px 0;
    }
    nav a {
      color: white;
      margin: 0 15px;
      text-decoration: none;
      font-weight: bold;
    }
    .image-section {
      display: flex;
      justify-content: center;
      gap: 30px;
      padding: 30px 20px;
      flex-wrap: wrap;
    }
    .image-section img {
      width: 250px;
      border-radius: 12px;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    }
    .form-section, .table-section {
      max-width: 1000px;
      margin: 30px auto;
      background: white;
      padding: 30px;
      border-radius: 15px;
      box-shadow: 0 4px 15px rgba(0, 0, 0, 0.05);
    }
    .form-section h2, .table-section h2 {
      margin-bottom: 20px;
      color: #2d3436;
    }
    .form-section label {
      display: block;
      margin-bottom: 8px;
      color: #2d3436;
    }
    .form-section input {
      width: 100%;
      padding: 10px;
      border: 2px solid #fbc531;
      border-radius: 8px;
      margin-bottom: 15px;
    }
    .form-section button {
      background: #00cec9;
      color: white;
      padding: 12px 20px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      transition: background 0.3s;
    }
    .form-section button:hover {
      background: #0984e3;
    }
    table {
      width: 100%;
      border-collapse: collapse;
    }
    table th, table td {
      border: 1px solid #ccc;
      padding: 12px;
      text-align: center;
    }
    table th {
      background: #ffeaa7;
    }
    footer {
      text-align: center;
      padding: 20px;
      background: #2d3436;
      color: white;
      margin-top: 40px;
    }
  </style>
</head>
<body>
  <header>
    <h1>Employee Management System</h1>
    <p>Effortless employee records – designed with color and clarity!</p>
  </header>

  <nav>
    <a href="#add">Add Employee</a>
    <a href="#records">Employee Records</a>
    <a href="#about">About</a>
  </nav>

  <section class="image-section">
    <img src="download (1).jpg" alt="Employee Management System 1">
    <img src="download (2).jpg" alt="Team Collaboration">
    <img src="download.jpg" alt="EMS Purple Graphic">
  </section>

  <section class="form-section" id="add">
    <h2>Add New Employee</h2>
    <label for="name">Full Name</label>
    <input type="text" id="name" placeholder="Enter full name">

    <label for="position">Position</label>
    <input type="text" id="position" placeholder="Enter position">

    <label for="salary">Salary</label>
    <input type="number" id="salary" placeholder="Enter salary">

    <button onclick="addEmployee()">Add Employee</button>
  </section>

  <section class="table-section" id="records">
    <h2>Employee Records</h2>
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Position</th>
          <th>Salary (₹)</th>
        </tr>
      </thead>
      <tbody id="employeeTable"></tbody>
    </table>
  </section>

  <footer id="about">
    <p>© 2025 Employee Management System. Designed by Yash Devdhe.</p>
  </footer>

  <script>
    function addEmployee() {
      const name = document.getElementById("name").value;
      const position = document.getElementById("position").value;
      const salary = document.getElementById("salary").value;

      if (name && position && salary) {
        const table = document.getElementById("employeeTable");
        const row = table.insertRow();
        row.insertCell(0).innerText = name;
        row.insertCell(1).innerText = position;
        row.insertCell(2).innerText = `₹${salary}`;

        document.getElementById("name").value = "";
        document.getElementById("position").value = "";
        document.getElementById("salary").value = "";
      } else {
        alert("Please fill all the fields!");
      }
    }
  </script>
</body>
</html>
