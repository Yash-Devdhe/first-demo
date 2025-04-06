
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Employee Management System</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    html, body {
      height: 100%;
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(45deg, #e0f7fa, #f3e5f5);
      scroll-behavior: smooth;
    }

    header {
      background: linear-gradient(to right, #6a11cb, #2575fc);
      color: white;
      padding: 40px 20px;
      text-align: center;
    }

    nav {
      background-color: #1e88e5;
      display: flex;
      justify-content: center;
      padding: 12px 0;
    }

    nav a {
      color: white;
      text-decoration: none;
      margin: 0 20px;
      font-weight: bold;
      font-size: 16px;
    }

    nav a:hover {
      text-decoration: underline;
    }

    main {
      max-width: 1200px;
      margin: 30px auto;
      padding: 30px;
      background-color: white;
      border-radius: 16px;
      box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
    }

    section {
      margin-bottom: 80px;
    }

    h2 {
      color: #2c3e50;
      margin-bottom: 25px;
    }

    form label {
      display: block;
      margin-top: 15px;
      font-weight: bold;
      color: #333;
    }

    input[type="text"] {
      width: 100%;
      padding: 12px;
      border: 2px solid #a5d6a7;
      border-radius: 8px;
      margin-top: 5px;
      font-size: 15px;
    }

    input[type="submit"] {
      background-color: #43a047;
      color: white;
      padding: 14px 20px;
      border: none;
      border-radius: 8px;
      margin-top: 20px;
      font-size: 16px;
      cursor: pointer;
    }

    input[type="submit"]:hover {
      background-color: #2e7d32;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 30px;
    }

    th, td {
      border-bottom: 1px solid #ddd;
      padding: 15px;
      text-align: left;
    }

    th {
      background-color: #00acc1;
      color: white;
    }

    tr:hover {
      background-color: #f1f8e9;
    }

    .images {
      display: flex;
      justify-content: space-around;
      margin: 40px 0;
      flex-wrap: wrap;
    }

    .images img {
      max-width: 100%;
      width: 350px;
      height: auto;
      margin: 10px;
      border-radius: 12px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.2);
      transition: transform 0.3s;
    }

    .images img:hover {
      transform: scale(1.05);
    }

    footer {
      background-color: #2c3e50;
      color: white;
      padding: 25px;
      text-align: center;
      margin-top: 50px;
    }
  </style>
</head>
<body>

  <header>
    <h1>Employee Management System</h1>
    <p>Manage your team efficiently and with style</p>
  </header>

  <nav>
    <a href="#add">Add Employee</a>
    <a href="#records">Employee Records</a>
    <a href="#about">About</a>
  </nav>

  <main>
    <div class="images">
      <img src="https://source.unsplash.com/400x250/?office,work" alt="Office">
      <img src="https://source.unsplash.com/401x250/?employees,team" alt="Team">
      <img src="https://source.unsplash.com/402x250/?business,people" alt="People Working">
    </div>

    <section id="add">
      <h2>Add New Employee</h2>
      <form id="employeeForm">
        <label for="empName">Full Name</label>
        <input type="text" id="empName" required>

        <label for="empId">Employee ID</label>
        <input type="text" id="empId" required>

        <label for="department">Department</label>
        <input type="text" id="department" required>

        <label for="role">Role</label>
        <input type="text" id="role" required>

        <label for="salary">Salary (₹)</label>
        <input type="text" id="salary" required>

        <input type="submit" value="Add Employee">
      </form>
    </section>

    <section id="records">
      <h2>Employee Records</h2>
      <table id="employeeTable">
        <thead>
          <tr>
            <th>Full Name</th>
            <th>Employee ID</th>
            <th>Department</th>
            <th>Role</th>
            <th>Salary (₹)</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>Aarav Mehta</td>
            <td>EMP101</td>
            <td>Finance</td>
            <td>Accountant</td>
            <td>₹45,000</td>
          </tr>
        </tbody>
      </table>
    </section>

    <section id="about">
      <h2>About This Project</h2>
      <p>
        This system is developed by <strong>Yash Devdhe</strong>, a Diploma Computer Engineering student at Government Polytechnic, Chhatrapati Sambhajinagar.
        The goal is to provide an elegant and simple system to manage employee data like names, roles, departments, IDs, and salaries — all in a browser without a backend.
      </p>
    </section>
  </main>

  <footer>
    &copy; 2025 Yash Devdhe | Designed with 💻 and 🎨 | Government Polytechnic
  </footer>

  <script>
    const form = document.getElementById("employeeForm");
    const table = document.getElementById("employeeTable").getElementsByTagName("tbody")[0];

    form.addEventListener("submit", function(e) {
      e.preventDefault();

      const name = document.getElementById("empName").value;
      const id = document.getElementById("empId").value;
      const dept = document.getElementById("department").value;
      const role = document.getElementById("role").value;
      const salary = document.getElementById("salary").value;

      const newRow = table.insertRow();
      newRow.innerHTML = `
        <td>${name}</td>
        <td>${id}</td>
        <td>${dept}</td>
        <td>${role}</td>
        <td>₹${salary}</td>
      `;

      form.reset();
    });
  </script>

</body>
</html>
