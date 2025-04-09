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
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }

    body {
      background: #f0f2f5;
      color: #333;
    }

    .container {
      width: 95%;
      max-width: 1200px;
      margin: auto;
      padding: 10px;
    }

    header {
      background: linear-gradient(135deg, #2c3e50, #3498db);
      color: white;
      padding: 30px 10px;
      text-align: center;
    }

    h1 {
      font-size: 2rem;
      margin-bottom: 10px;
    }

    .welcome-text {
      font-size: 1rem;
      max-width: 800px;
      margin: auto;
    }

    .stats-container {
      display: flex;
      flex-wrap: wrap;
      gap: 15px;
      margin: 20px 0;
    }

    .stat-card {
      flex: 1;
      min-width: 150px;
      background: white;
      padding: 15px;
      border-radius: 10px;
      text-align: center;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    }

    .stat-value {
      font-size: 1.5em;
      color: #3498db;
    }

    .controls, .search-container {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      margin: 15px 0;
    }

    .controls input, .controls select, .controls button,
    .search-container input {
      flex: 1;
      padding: 10px;
      font-size: 1em;
      border-radius: 5px;
      border: 1px solid #ccc;
    }

    button {
      background: #3498db;
      color: white;
      border: none;
      cursor: pointer;
      transition: background 0.3s;
    }

    button:hover {
      background: #2980b9;
    }

    .search-container {
      position: relative;
    }

    .search-container input {
      padding-left: 35px;
    }

    .search-icon {
      position: absolute;
      left: 10px;
      top: 50%;
      transform: translateY(-50%);
      color: #666;
    }

    .employee-list {
      overflow-x: auto;
      background: white;
      border-radius: 10px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
    }

    table {
      width: 100%;
      border-collapse: collapse;
    }

    th, td {
      padding: 12px;
      border-bottom: 1px solid #ddd;
    }

    th {
      background: #2c3e50;
      color: white;
    }

    .action-btn {
      padding: 5px 10px;
      border-radius: 5px;
      margin-right: 5px;
      font-size: 0.9em;
    }

    .edit-btn {
      background: #f39c12;
      color: white;
    }

    .delete-btn {
      background: #e74c3c;
      color: white;
    }

    .about-section {
      background: white;
      padding: 20px;
      margin: 20px 0;
      border-radius: 10px;
    }

    .modal {
      display: none;
      position: fixed;
      inset: 0;
      background: rgba(0,0,0,0.5);
      z-index: 999;
      justify-content: center;
      align-items: center;
    }

    .modal-content {
      background: white;
      padding: 20px;
      border-radius: 10px;
      width: 90%;
      max-width: 400px;
    }

    .close {
      float: right;
      font-size: 24px;
      cursor: pointer;
    }

    @media screen and (max-width: 600px) {
      h1 {
        font-size: 1.5rem;
      }

      .stat-card {
        flex: 100%;
      }

      .controls, .search-container {
        flex-direction: column;
      }

      .controls input, .controls button, .search-container input {
        width: 100%;
      }
    }
  </style>
</head>
<body>
  <header>
    <h1>Employee Management System</h1>
    <div class="welcome-text">
      Manage your employees efficiently with a responsive, modern interface.
    </div>
  </header>

  <div class="container">
    <div class="stats-container">
      <div class="stat-card">
        <div class="stat-value" id="totalEmployees">0</div>
        <div>Total Employees</div>
      </div>
      <div class="stat-card">
        <div class="stat-value" id="avgSalary">$0</div>
        <div>Average Salary</div>
      </div>
      <div class="stat-card">
        <div class="stat-value" id="positions">0</div>
        <div>Unique Positions</div>
      </div>
    </div>

    <div class="controls">
      <input type="text" id="name" placeholder="Name">
      <input type="text" id="position" placeholder="Position">
      <input type="number" id="salary" placeholder="Salary">
      <button onclick="addEmployee()">Add</button>
    </div>

    <div class="search-container">
      <span class="search-icon">🔍</span>
      <input type="text" id="search" placeholder="Search employees...">
    </div>

    <div class="employee-list">
      <table>
        <thead>
          <tr>
            <th>ID</th><th>Name</th><th>Position</th><th>Salary</th><th>Actions</th>
          </tr>
        </thead>
        <tbody id="employeeTable"></tbody>
      </table>
    </div>

    <div class="about-section">
      <h2>About</h2>
      <p>This system helps you manage employees with real-time data tracking, salary analysis, and mobile-friendly design.</p>
    </div>
  </div>

  <div id="editModal" class="modal">
    <div class="modal-content">
      <span class="close" onclick="closeModal()">&times;</span>
      <h2>Edit Employee</h2>
      <input type="hidden" id="editId">
      <input type="text" id="editName" placeholder="Name">
      <input type="text" id="editPosition" placeholder="Position">
      <input type="number" id="editSalary" placeholder="Salary">
      <button onclick="updateEmployee()">Update</button>
    </div>
  </div>

  <script>
    let employees = JSON.parse(localStorage.getItem('employees')) || [];
    const table = document.getElementById('employeeTable');

    function updateStats() {
      document.getElementById('totalEmployees').textContent = employees.length;
      const avg = employees.length ? Math.round(employees.reduce((a, b) => a + Number(b.salary), 0) / employees.length) : 0;
      document.getElementById('avgSalary').textContent = '$' + avg;
      document.getElementById('positions').textContent = new Set(employees.map(e => e.position)).size;
    }

    function renderEmployees(list = employees) {
      table.innerHTML = '';
      list.forEach(emp => {
        const row = document.createElement('tr');
        row.innerHTML = `
          <td>${emp.id}</td>
          <td>${emp.name}</td>
          <td>${emp.position}</td>
          <td>$${emp.salary}</td>
          <td>
            <button class="action-btn edit-btn" onclick="editEmployee(${emp.id})">Edit</button>
            <button class="action-btn delete-btn" onclick="deleteEmployee(${emp.id})">Delete</button>
          </td>`;
        table.appendChild(row);
      });
    }

    function addEmployee() {
      const name = document.getElementById('name').value.trim();
      const position = document.getElementById('position').value.trim();
      const salary = document.getElementById('salary').value.trim();
      if (name && position && salary) {
        const emp = { id: Date.now(), name, position, salary };
        employees.push(emp);
        saveAndRender();
        document.getElementById('name').value = '';
        document.getElementById('position').value = '';
        document.getElementById('salary').value = '';
      }
    }

    function deleteEmployee(id) {
      if (confirm('Delete this employee?')) {
        employees = employees.filter(emp => emp.id !== id);
        saveAndRender();
      }
    }

    function editEmployee(id) {
      const emp = employees.find(e => e.id === id);
      if (emp) {
        document.getElementById('editId').value = emp.id;
        document.getElementById('editName').value = emp.name;
        document.getElementById('editPosition').value = emp.position;
        document.getElementById('editSalary').value = emp.salary;
        document.getElementById('editModal').style.display = 'flex';
      }
    }

    function closeModal() {
      document.getElementById('editModal').style.display = 'none';
    }

    function updateEmployee() {
      const id = +document.getElementById('editId').value;
      const name = document.getElementById('editName').value;
      const position = document.getElementById('editPosition').value;
      const salary = document.getElementById('editSalary').value;
      const index = employees.findIndex(emp => emp.id === id);
      if (index !== -1) {
        employees[index] = { id, name, position, salary };
        saveAndRender();
        closeModal();
      }
    }

    function saveAndRender() {
      localStorage.setItem('employees', JSON.stringify(employees));
      renderEmployees();
      updateStats();
    }

    document.getElementById('search').addEventListener('input', (e) => {
      const q = e.target.value.toLowerCase();
      const filtered = employees.filter(emp =>
        emp.name.toLowerCase().includes(q) || emp.position.toLowerCase().includes(q)
      );
      renderEmployees(filtered);
    });

    window.addEventListener('click', (e) => {
      const modal = document.getElementById('editModal');
      if (e.target === modal) closeModal();
    });

    renderEmployees();
    updateStats();
  </script>

  <footer style="text-align:center; padding:10px; background:#fff; margin-top:20px;">
    &copy; 2025 Employee Management System by Yash Devdhe
  </footer>
</body>
</html>
