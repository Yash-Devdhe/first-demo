<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Employee Management System</title>
  <style>
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: #f4f7f9;
      margin: 0;
      padding: 0;
    }

    header {
      background-color: #2c3e50;
      color: white;
      padding: 20px;
      text-align: center;
    }

    main {
      max-width: 900px;
      margin: 30px auto;
      padding: 20px;
      background: white;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    }

    h2 {
      color: #34495e;
    }

    form {
      margin-bottom: 30px;
    }

    label {
      display: block;
      margin: 10px 0 5px;
      font-weight: 600;
    }

    input[type="text"],
    input[type="submit"] {
      width: 100%;
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 5px;
      margin-bottom: 15px;
      font-size: 14px;
    }

    input[type="submit"] {
      background-color: #2980b9;
      color: white;
      border: none;
      cursor: pointer;
      transition: background 0.3s;
    }

    input[type="submit"]:hover {
      background-color: #1c6ea4;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 10px;
    }

    th, td {
      padding: 12px 15px;
      text-align: left;
      border-bottom: 1px solid #ddd;
    }

    th {
      background-color: #3498db;
      color: white;
    }

    tr:hover {
      background-color: #f1f1f1;
    }

    footer {
      text-align: center;
      padding: 15px;
      margin-top: 30px;
      background-color: #2c3e50;
      color: white;
    }
  </style>
</head>
<body>

  <header>
    <h1>Employee Management System</h1>
  </header>

  <main>
    <section>
      <h2>Add New Employee</h2>
      <form>
        <label for="empName">Full Name</label>
        <input type="text" id="empName" name="empName">

        <label for="empId">Employee ID</label>
        <input type="text" id="empId" name="empId">

        <label for="department">Department</label>
        <input type="text" id="department" name="department">

        <label for="role">Role</label>
        <input type="text" id="role" name="role">

        <input type="submit" value="Add Employee">
      </form>
    </section>

    <section>
      <h2>Employee Records</h2>
      <table>
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
          <tr>
            <td>Sneha Patil</td>
            <td>EMP102</td>
            <td>HR</td>
            <td>Manager</td>
          </tr>
          <tr>
            <td>Rajesh Kulkarni</td>
            <td>EMP103</td>
            <td>Development</td>
            <td>Team Lead</td>
          </tr>
        </tbody>
      </table>
    </section>
  </main>

  <footer>
    &copy; 2025 Yash Devdhe | Government Polytechnic
  </footer>

</body>
</html>
