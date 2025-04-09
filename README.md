<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Employee Management System</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }

    body {
      background: #f0f2f5;
      color: #333;
      line-height: 1.6;
    }

    .container {
      max-width: 1200px;
      margin: auto;
      padding: 20px;
    }

    header {
      background: linear-gradient(135deg, #2c3e50, #3498db);
      color: white;
      padding: 40px 20px;
      margin-bottom: 30px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    }

    h1 {
      text-align: center;
      font-size: 2.5em;
      margin-bottom: 20px;
      text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
    }

    .welcome-text {
      text-align: center;
      max-width: 800px;
      margin: 0 auto 40px;
      font-size: 1.2em;
      color: #fff;
    }

    .controls, .search-container {
      display: flex;
      gap: 20px;
      flex-wrap: wrap;
      margin-bottom: 30px;
    }

    input, select, button {
      padding: 12px;
      border: none;
      border-radius: 5px;
      font-size: 1em;
    }

    input, select {
      flex: 1;
      background: white;
      border: 1px solid #ddd;
    }

    button {
      background: #3498db;
      color: white;
      cursor: pointer;
      transition: all 0.3s;
      min-width: 120px;
    }

    button:hover {
      background: #2980b9;
      transform: translateY(-2px);
      box-shadow: 0 4px 8px rgba(0,0,0,0.1);
    }

    .employee-list {
      background: white;
      border-radius: 10px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
      overflow-x: auto;
      margin-bottom: 40px;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      min-width: 600px;
    }

    th, td {
      padding: 15px;
      text-align: left;
      border-bottom: 1px solid #eee;
    }

    th {
      background: #2c3e50;
      color: white;
      position: sticky;
      top: 0;
    }

    tr:hover {
      background: #f8f9fa;
    }

    .action-btn {
      padding: 8px 12px;
      margin: 0 5px;
      border-radius: 4px;
      transition: all 0.3s;
    }

    .edit-btn {
      background: #f39c12;
      color: white;
    }

    .edit-btn:hover {
      background: #d35400;
    }

    .delete-btn {
      background: #e74c3c;
      color: white;
    }

    .delete-btn:hover {
      background: #c0392b;
    }

    .modal {
      display: none;
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      background: rgba(0,0,0,0.5);
      z-index: 1000;
    }

    .modal-content {
      background: white;
      width: 90%;
      max-width: 500px;
      margin: 60px auto;
      padding: 20px;
      border-radius: 10px;
      position: relative;
    }

    .close {
      position: absolute;
      right: 20px;
      top: 10px;
      font-size: 24px;
      cursor: pointer;
    }

    .stats-container {
      display: flex;
      gap: 20px;
      margin-bottom: 40px;
      flex-wrap: wrap;
    }

    .stat-card {
      background: white;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
      flex: 1;
      min-width: 200px;
      text-align: center;
    }

    .stat-value {
      font-size: 2em;
      color: #3498db;
      font-weight: bold;
    }

    .stat-label {
      color: #666;
      margin-top: 10px;
    }

    .about-section {
      background: white;
      padding: 40px;
      border-radius: 10px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
      margin-bottom: 40px;
    }

    .about-section h2 {
      color: #2c3e50;
      margin-bottom: 20px;
    }

    .about-section p, ul {
      color: #666;
    }

    @media (max-width: 768px) {
      .controls, .search-container {
        flex-direction: column;
      }

      input, select, button {
        width: 100%;
      }

      table {
        min-width: unset;
      }

      h1 {
        font-size: 2em;
      }

      .welcome-text {
        font-size: 1em;
        padding: 0 10px;
      }
    }
  </style>
</head>
<body>
  <header>
    <div class="container">
      <h1>Employee Management System</h1>
      <div class="welcome-text">
        Manage your team with ease. Add, update, search, and monitor employee data anytime, anywhere!
      </div>
    </div>
  </header>

  <div class="container">
    <div class="stats-container">
      <div class="stat-card">
        <div class="stat-value" id="totalEmployees">0</div>
        <div class="stat-label">Total Employees</div>
      </div>
      <div class="stat-card">
        <div class="stat-value" id="avgSalary">$0</div>
        <div class="stat-label">Average Salary</div>
      </div>
      <div class="stat-card">
        <div class="stat-value" id="positions">0</div>
        <div class="stat-label">Unique Positions</div>
      </div>
    </div>

    <div class="controls">
      <input type="text" id="name" placeholder="Employee Name">
      <input type="text" id="position" placeholder="Position">
      <input type="number" id="salary" placeholder="Salary">
      <button onclick="addEmployee()">Add Employee</button>
    </div>

    <div class="search-container">
      <input type="text" id="search" placeholder="Search employees...">
    </div>

    <div class="employee-list">
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>Name</th>
            <th>Position</th>
            <th>Salary</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody id="employeeTable"></tbody>
      </table>
    </div>

    <div class="about-section">
      <h2>About This System</h2>
      <p>This system helps organizations manage employees easily with built-in search, stats, and management features. It works offline and saves data in your browser using localStorage.</p>
      <ul>
        <li>Easy add/edit/delete features</li>
        <li>Mobile-friendly design</li>
        <li>Live statistics</li>
        <li>Persistent storage</li>
      </ul>
    </div>

    <p style="text-align:center;">&copy; 2025 Employee Management System by Yash Devdhe</p>
  </div>

  <div id="editModal" class="modal">
    <div class="modal-content">
      <span class="close" onclick="closeModal()">&times;</span>
      <h2>Edit Employee</h2>
      <input type="hidden" id="editId">
      <input type="text" id="editName" placeholder="Employee Name">
      <input type="text" id="editPosition" placeholder="Position">
      <input type="number" id="editSalary" placeholder="Salary">
      <button onclick="updateEmployee()">Update</button>
    </div>
  </div>

  <script>
    let employees = JSON.parse(localStorage.getItem('employees')) || [];

    function updateStats() {
      document.getElementById('totalEmployees').textContent = employees.length;
      let total = employees.reduce((sum, emp) => sum + Number(emp.salary), 0);
      let avg = employees.length ? Math.round(total / employees.length) : 0;
      document.getElementById('avgSalary').textContent = "$" + avg;
      let positions = new Set(employees.map(emp => emp.position));
      document.getElementById('positions').textContent = positions.size;
    }

    function saveEmployees() {
      localStorage.setItem('employees', JSON.stringify(employees));
    }

    function renderEmployees(data = employees) {
      const table = document.getElementById('employeeTable');
      table.innerHTML = '';
      data.forEach(emp => {
        const row = document.createElement('tr');
        row.innerHTML = `
          <td>${emp.id}</td>
          <td>${emp.name}</td>
          <td>${emp.position}</td>
          <td>$${emp.salary}</td>
          <td>
            <button class="action-btn edit-btn" onclick="openEditModal(${emp.id})">Edit</button>
            <button class="action-btn delete-btn" onclick="deleteEmployee(${emp.id})">Delete</button>
          </td>`;
        table.appendChild(row);
      });
    }

    function addEmployee() {
      const name = document.getElementById('name').value;
      const position = document.getElementById('position').value;
      const salary = document.getElementById('salary').value;
      if (name && position && salary) {
        const employee = { id: Date.now(), name, position, salary };
        employees.push(employee);
        saveEmployees();
        renderEmployees();
        updateStats();
        document.getElementById('name').value = '';
        document.getElementById('position').value = '';
        document.getElementById('salary').value = '';
      }
    }

    function deleteEmployee(id) {
      if (confirm("Are you sure?")) {
        employees = employees.filter(emp => emp.id !== id);
        saveEmployees();
        renderEmployees();
        updateStats();
      }
    }

    function openEditModal(id) {
      const emp = employees.find(e => e.id === id);
      if (emp) {
        document.getElementById('editId').value = emp.id;
        document.getElementById('editName').value = emp.name;
        document.getElementById('editPosition').value = emp.position;
        document.getElementById('editSalary').value = emp.salary;
        document.getElementById('editModal').style.display = 'block';
      }
    }

    function closeModal() {
      document.getElementById('editModal').style.display = 'none';
    }

    function updateEmployee() {
      const id = parseInt(document.getElementById('editId').value);
      const name = document.getElementById('editName').value;
      const position = document.getElementById('editPosition').value;
      const salary = document.getElementById('editSalary').value;
      const index = employees.findIndex(emp => emp.id === id);
      if (index !== -1) {
        employees[index] = { id, name, position, salary };
        saveEmployees();
        renderEmployees();
        updateStats();
        closeModal();
      }
    }

    document.getElementById('search').addEventListener('input', e => {
      const term = e.target.value.toLowerCase();
      const filtered = employees.filter(emp =>
        emp.name.toLowerCase().includes(term) ||
        emp.position.toLowerCase().includes(term)
      );
      renderEmployees(filtered);
    });

    window.onclick = function(e) {
      if (e.target === document.getElementById('editModal')) {
        closeModal();
      }
    };

    renderEmployees();
    updateStats();
  </script>
</body>
</html>
