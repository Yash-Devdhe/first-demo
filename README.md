
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

    body {
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(to bottom, #e3f2fd, #f8f9fa);
      color: #333;
      line-height: 1.6;
    }

    header {
      background-color: #0d47a1;
      color: white;
      padding: 30px 20px;
      text-align: center;
    }

    nav {
      background-color: #1976d2;
      display: flex;
      justify-content: center;
      padding: 10px;
    }

    nav a {
      color: white;
      margin: 0 15px;
      text-decoration: none;
      font-weight: bold;
    }

    nav a:hover {
      text-decoration: underline;
    }

    main {
      max-width: 1000px;
      margin: 20px auto;
      padding: 20px;
      background: white;
      border-radius: 12px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }

    section {
      margin-bottom: 60px;
    }

    h2 {
      color: #0d47a1;
      margin-bottom: 20px;
    }

    form label {
      display: block;
      margin: 10px 0 5px;
      font-weight: bold;
    }

    input[type="text"] {
      width: 100%;
      padding: 10px;
      border: 2px solid #90caf9;
      border-radius: 6px;
      margin-bottom: 15px;
      font-size: 15px;
    }

    input[type="submit"] {
      background-color: #2196f3;
      color: white;
      border: none;
      padding: 12px 20px;
      border-radius: 6px;
      cursor: pointer;
      font-size: 16px;
    }

    input[type="submit"]:hover {
      background-color: #1565c0;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 20px;
    }

    th, td {
      padding: 12px 15px;
      border-bottom: 1px solid #ccc;
    }

    th {
      background-color: #64b5f6;
      color: white;
    }

    tr:hover {
      background-color: #f1f1f1;
    }

    .gallery {
      display: flex;
      gap: 20px;
      flex-wrap: wrap;
      margin-top: 30px;
    }

    .gallery img {
      width: 100%;
      max-width: 300px;
      border-radius: 12px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.1);
      transition: transform 0.3s;
    }

    .gallery img:hover {
      transform: scale(1.05);
    }

    footer {
      text-align: center;
      padding: 30px;
      background-color: #0d47a1;
      color: white;
      margin-top: 50px;
    }

    html {
      scroll-behavior: smooth;
    }
  </style>
</head>
<body>

  <header>
    <h1>Employee Management System</h1>
  </header>

  <nav>
    <a href="#add">Add Employee</a>
    <a href="#list">Employee Records</a>
    <a href="#gallery">Gallery</a>
    <a href="#about">About</a>
  </nav>

  <main>
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

        <input type="submit" value="Add Employee">
      </form>
    </section>

    <section id="list">
      <h2>Employee Records</h2>
      <table id="employeeTable">
        <thead>
          <tr>
            <th>Full Name</th>
            <th>Employee ID</th>
            <th>Department</th>
            <th>Role</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>Aarav Mehta</td>
            <td>EMP101</td>
            <td>Finance</td>
            <td>Accountant</td>
          </tr>
        </tbody>
      </table>
    </section>

    <section id="gallery">
      <h2>Our Team Moments</h2>
      <div class="gallery">
        <img src="https://source.unsplash.com/300x200/?office,team" alt="Team 1">
        <img src="https://source.unsplash.com/301x200/?workplace,meeting" alt="Team 2">
        <img src="https://source.unsplash.com/302x200/?corporate,people" alt="Team 3">
      </div>
    </section>

    <section id="about">
      <h2>About This System</h2>
      <p>
        This is a simple Employee Management System created by <strong>Yash Devdhe</strong>, a passionate student at Government Polytechnic, Chhatrapati Sambhajinagar.
        It is designed to help manage employees in a smooth and elegant way using only HTML, CSS, and JavaScript.
      </p>
    </section>
  </main>

  <footer>
    &copy; 2025 Yash Devdhe | All Rights Reserved
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

      const newRow = table.insertRow();

      newRow.innerHTML = `
        <td>${name}</td>
        <td>${id}</td>
        <td>${dept}</td>
        <td>${role}</td>
      `;

      form.reset();
    });
  </script>

</body>
</html>
