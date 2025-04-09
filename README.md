<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
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
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        header {
            background: #2c3e50;
            color: white;
            padding: 20px 0;
            margin-bottom: 30px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }

        h1 {
            text-align: center;
            font-size: 2.5em;
            margin-bottom: 20px;
        }

        .controls {
            display: flex;
            gap: 20px;
            margin-bottom: 30px;
            flex-wrap: wrap;
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
            transition: background 0.3s;
        }

        button:hover {
            background: #2980b9;
        }

        .employee-list {
            background: white;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            overflow: hidden;
        }

        table {
            width: 100%;
            border-collapse: collapse;
        }

        th, td {
            padding: 15px;
            text-align: left;
            border-bottom: 1px solid #eee;
        }

        th {
            background: #2c3e50;
            color: white;
        }

        tr:hover {
            background: #f8f9fa;
        }

        .action-btn {
            padding: 8px 12px;
            margin: 0 5px;
            border-radius: 4px;
        }

        .edit-btn {
            background: #f39c12;
        }

        .edit-btn:hover {
            background: #d35400;
        }

        .delete-btn {
            background: #e74c3c;
        }

        .delete-btn:hover {
            background: #c0392b;
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
        }

        .modal-content {
            background: white;
            width: 90%;
            max-width: 500px;
            margin: 50px auto;
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

        .search-container {
            position: relative;
            flex: 2;
        }

        .search-container input {
            width: 100%;
            padding-left: 40px;
        }

        .search-icon {
            position: absolute;
            left: 12px;
            top: 50%;
            transform: translateY(-50%);
            color: #666;
        }
    </style>
</head>
<body>
    <header>
        <div class="container">
            <h1>Employee Management System</h1>
        </div>
    </header>

    <div class="container">
        <div class="controls">
            <input type="text" id="name" placeholder="Employee Name">
            <input type="text" id="position" placeholder="Position">
            <input type="number" id="salary" placeholder="Salary">
            <button onclick="addEmployee()">Add Employee</button>
        </div>

        <div class="search-container">
            <span class="search-icon">🔍</span>
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
        let currentEditId = null;

        function addEmployee() {
            const name = document.getElementById('name').value;
            const position = document.getElementById('position').value;
            const salary = document.getElementById('salary').value;

            if (name && position && salary) {
                const employee = {
                    id: Date.now(),
                    name,
                    position,
                    salary
                };

                employees.push(employee);
                saveEmployees();
                renderEmployees();
                clearInputs();
            }
        }

        function renderEmployees(filteredEmployees = employees) {
            const table = document.getElementById('employeeTable');
            table.innerHTML = '';

            filteredEmployees.forEach(employee => {
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${employee.id}</td>
                    <td>${employee.name}</td>
                    <td>${employee.position}</td>
                    <td>$${employee.salary}</td>
                    <td>
                        <button class="action-btn edit-btn" onclick="openEditModal(${employee.id})">Edit</button>
                        <button class="action-btn delete-btn" onclick="deleteEmployee(${employee.id})">Delete</button>
                    </td>
                `;
                table.appendChild(row);
            });
        }

        function clearInputs() {
            document.getElementById('name').value = '';
            document.getElementById('position').value = '';
            document.getElementById('salary').value = '';
        }

        function saveEmployees() {
            localStorage.setItem('employees', JSON.stringify(employees));
        }

        function deleteEmployee(id) {
            if (confirm('Are you sure you want to delete this employee?')) {
                employees = employees.filter(emp => emp.id !== id);
                saveEmployees();
                renderEmployees();
            }
        }

        function openEditModal(id) {
            const employee = employees.find(emp => emp.id === id);
            if (employee) {
                document.getElementById('editId').value = employee.id;
                document.getElementById('editName').value = employee.name;
                document.getElementById('editPosition').value = employee.position;
                document.getElementById('editSalary').value = employee.salary;
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

            if (name && position && salary) {
                const index = employees.findIndex(emp => emp.id === id);
                if (index !== -1) {
                    employees[index] = { id, name, position, salary };
                    saveEmployees();
                    renderEmployees();
                    closeModal();
                }
            }
        }

        document.getElementById('search').addEventListener('input', (e) => {
            const searchTerm = e.target.value.toLowerCase();
            const filteredEmployees = employees.filter(emp => 
                emp.name.toLowerCase().includes(searchTerm) ||
                emp.position.toLowerCase().includes(searchTerm)
            );
            renderEmployees(filteredEmployees);
        });

        window.onclick = function(event) {
            const modal = document.getElementById('editModal');
            if (event.target === modal) {
                closeModal();
            }
        }

        renderEmployees();
    </script>
</body>
</html>
