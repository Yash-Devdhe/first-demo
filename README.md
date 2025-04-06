
<html>
<head>
  <title>Employee Management System</title>
</head>
<body>

  <h1>Employee Management System</h1>

  <section>
    <h2>Add New Employee</h2>
    <form>
      <label for="empName">Name:</label><br>
      <input type="text" id="empName" name="empName"><br><br>

      <label for="empId">Employee ID:</label><br>
      <input type="text" id="empId" name="empId"><br><br>

      <label for="department">Department:</label><br>
      <input type="text" id="department" name="department"><br><br>

      <label for="role">Role:</label><br>
      <input type="text" id="role" name="role"><br><br>

      <input type="submit" value="Add Employee">
    </form>
  </section>

  <section>
    <h2>Employee List</h2>
    <table border="1" cellpadding="10">
      <thead>
        <tr>
          <th>Name</th>
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
      </tbody>
    </table>
  </section>

</body>
</html>
