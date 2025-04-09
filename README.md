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
            line-height: 1.6;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        header {
            background: linear-gradient(135deg, #2c3e50, #3498db);
            color: white;
            padding: 40px 0;
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
            overflow: hidden;
            margin-bottom: 40px;
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
        }

        .edit-btn:hover {
            background: #d35400;
            transform: translateY(-2px);
        }

        .delete-btn {
            background: #e74c3c;
        }

        .delete-btn:hover {
            background: #c0392b;
            transform: translateY(-2px);
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            z-index: 1000;
        }

        .modal-content {
            background: white;
            width: 90%;
            max-width: 500px;
            margin: 50px auto;
            padding: 20px;
            border-radius: 10px;
            position: relative;
            animation: modalFadeIn 0.3s;
        }

        @keyframes modalFadeIn {
            from {opacity: 0; transform: translateY(-20px);}
            to {opacity: 1; transform: translateY(0);}
        }

        .close {
            position: absolute;
            right: 20px;
            top: 10px;
            font-size: 24px;
            cursor: pointer;
            transition: transform 0.3s;
        }

        .close:hover {
            transform: rotate(90deg);
        }

        .search-container {
            position: relative;
            flex: 2;
            margin-bottom: 30px;
        }

        .search-container input {
            width: 100%;
            padding-left: 40px;
            transition: all 0.3s;
        }

        .search-container input:focus {
            box-shadow: 0 0 10px rgba(52, 152, 219, 0.3);
        }

        .search-icon {
            position: absolute;
            left: 12px;
            top: 50%;
            transform: translateY(-50%);
            color: #666;
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
            transition: transform 0.3s;
        }

        .stat-card:hover {
            transform: translateY(-5px);
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

        .about-section p {
            margin-bottom: 20px;
            color: #666;
        }

        @media (max-width: 768px) {
            .controls {
                flex-direction: column;
            }

            input, select, button {
                width: 100%;
            }

            .stat-card {
                min-width: 100%;
            }

            table {
                display: block;
                overflow-x: auto;
            }

            .modal-content {
                width: 95%;
                margin: 20px auto;
            }

            h1 {
                font-size: 2em;
            }

            .welcome-text {
                font-size: 1em;
                padding: 0 20px;
            }
        }
    </style>
</head>
<body>
    <header>
        <div class="container">
            <h1>Employee Management System</h1>
            <div class="welcome-text">
                Welcome to our comprehensive Employee Management System. This platform helps you efficiently manage your workforce, track employee information, and maintain accurate records. Our system provides a user-friendly interface for adding, editing, and managing employee details with ease.
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

        <div class="about-section">
            <h2>About Our Employee Management System</h2>
            <p>Our Employee Management System is designed to streamline your HR processes and improve workforce management efficiency. With this system, you can easily maintain accurate employee records, track important information, and make data-driven decisions.</p>
            <p>The system features a modern, responsive design that works seamlessly on both desktop and mobile devices. Whether you're in the office or on the go, you can access and manage your employee database with ease.</p>
            <p>Key features include:</p>
            <ul style="margin-left: 20px; margin-bottom: 20px;">
                <li>Easy employee data entry and management</li>
                <li>Real-time search functionality</li>
                <li>Comprehensive employee statistics</li>
                <li>Secure data storage</li>
                <li>Responsive design for all devices</li>
            </ul>
            <p>Our system is built with the latest web technologies to ensure reliability, security, and performance. The intuitive interface makes it easy for users of all technical levels to manage their employee database effectively.</p>
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

        function updateStats() {
            document.getElementById('totalEmployees').textContent = employees.length;
            
            const avgSalary = employees.length > 0 
                ? Math.round(employees.reduce((sum, emp) => sum + Number(emp.salary), 0) / employees.length)
                : 0;
            document.getElementById('avgSalary').textContent = '$' + avgSalary;
            
            const uniquePositions = new Set(employees.map(emp => emp.position)).size;
            document.getElementById('positions').textContent = uniquePositions;
        }

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
                updateStats();
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
                updateStats();
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
                    updateStats();
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
        updateStats();
    </script>

        <p><center>&copy;Employee Management System devepoled by Yash Devdhe</center></p>

</body>
</html>
