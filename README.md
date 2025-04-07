<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Employee Management System</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary-color: #4e73df;
            --secondary-color: #f8f9fc;
            --accent-color: #2e59d9;
            --text-color: #5a5c69;
        }
        
        body {
            background: linear-gradient(135deg, #f8f9fc 0%, #d1e0f0 100%);
            min-height: 100vh;
            color: var(--text-color);
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        .container {
            padding-top: 2rem;
            padding-bottom: 2rem;
        }
        
        /* Decorative border for the main container */
        .decorative-border {
            position: relative;
            padding: 2rem;
            background: white;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            border: 1px solid rgba(0, 0, 0, 0.1);
            overflow: hidden;
        }
        
        .decorative-border::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 8px;
            background: linear-gradient(90deg, var(--primary-color), var(--accent-color));
            background: linear-gradient(90deg, #4e73df, #224abe);
        }
        
        .card {
            border-radius: 12px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            border: none;
            overflow: hidden;
            margin-bottom: 1.5rem;
            position: relative;
            border: 1px solid rgba(0, 0, 0, 0.05);
        }
        
        .card::after {
            content: "";
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: linear-gradient(90deg, var(--primary-color), var(--accent-color));
        }
        
        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
        }
        
        .employee-table {
            background: white;
            border-radius: 10px;
            overflow: hidden;
            border: 1px solid rgba(0, 0, 0, 0.05);
        }
        
        .table-hover tbody tr:hover {
            background-color: rgba(78, 115, 223, 0.05);
        }
        
        .action-btns .btn {
            margin: 0 2px;
            padding: 5px 8px;
            font-size: 0.8rem;
        }
        
        h1 {
            color: var(--primary-color);
            font-weight: 700;
            margin-bottom: 1.5rem;
            position: relative;
            display: inline-block;
        }
        
        h1::after {
            content: "";
            position: absolute;
            bottom: -10px;
            left: 0;
            width: 50px;
            height: 3px;
            background: var(--primary-color);
            border-radius: 3px;
        }
        
        .stat-card {
            color: white;
            border-radius: 10px;
            overflow: hidden;
            position: relative;
            z-index: 1;
        }
        
        .stat-card::before {
            content: "";
            position: absolute;
            top: -50%;
            right: -20%;
            width: 100%;
            height: 200%;
            background: rgba(255, 255, 255, 0.1);
            transform: rotate(30deg);
            z-index: -1;
        }
        
        .stat-card i {
            font-size: 2rem;
            opacity: 0.3;
            position: absolute;
            right: 20px;
            top: 20px;
        }
        
        /* Mobile specific styles */
        @media (max-width: 768px) {
            .container {
                padding: 1rem;
            }
            
            .decorative-border {
                padding: 1rem;
                border-radius: 10px;
            }
            
            h1 {
                font-size: 1.8rem;
            }
            
            .card-body {
                padding: 1rem;
            }
            
            .row.g-3 > [class^="col-"] {
                margin-bottom: 0.5rem;
            }
            
            .action-btns .btn {
                margin: 2px 0;
                display: block;
                width: 100%;
            }
            
            .table td, .table th {
                padding: 0.5rem;
            }
            
            #searchInput {
                width: 100% !important;
                margin-top: 1rem;
            }
        }
        
        /* Desktop specific styles */
        @media (min-width: 769px) {
            .container {
                max-width: 1200px;
            }
            
            .stat-card {
                height: 100%;
            }
        }
        
        /* Form input styling */
        .form-control {
            border-radius: 8px;
            border: 1px solid rgba(0, 0, 0, 0.1);
            padding: 0.5rem 1rem;
            transition: all 0.3s;
        }
        
        .form-control:focus {
            border-color: var(--primary-color);
            box-shadow: 0 0 0 0.25rem rgba(78, 115, 223, 0.25);
        }
        
        /* Button styling */
        .btn-primary {
            background-color: var(--primary-color);
            border-color: var(--primary-color);
            border-radius: 8px;
            padding: 0.5rem 1.5rem;
            font-weight: 500;
        }
        
        .btn-primary:hover {
            background-color: var(--accent-color);
            border-color: var(--accent-color);
        }
        
        /* Table styling */
        .table {
            margin-bottom: 0;
        }
        
        .table thead th {
            background-color: var(--primary-color);
            color: white;
            border-bottom: none;
            padding: 1rem;
        }
        
        .table tbody td {
            padding: 0.75rem 1rem;
            vertical-align: middle;
        }
        
        /* Animation for new entries */
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .employee-table tr {
            animation: fadeIn 0.3s ease forwards;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="decorative-border">
            <h1 class="text-center mb-4"><i class="fas fa-users me-2"></i>Employee Management System</h1>
            
            <!-- Add Employee Form -->
            <div class="card mb-4">
                <div class="card-body">
                    <h5 class="card-title"><i class="fas fa-user-plus me-2"></i>Add New Employee</h5>
                    <form id="employeeForm" onsubmit="addEmployee(event)">
                        <div class="row g-3">
                            <div class="col-md-4">
                                <input type="text" class="form-control" placeholder="Full Name" id="name" required>
                            </div>
                            <div class="col-md-4">
                                <input type="email" class="form-control" placeholder="Email" id="email" required>
                            </div>
                            <div class="col-md-4">
                                <input type="text" class="form-control" placeholder="Position" id="position" required>
                            </div>
                            <div class="col-md-4">
                                <input type="number" class="form-control" placeholder="Salary" id="salary" required min="0">
                            </div>
                            <div class="col-md-4">
                                <input type="date" class="form-control" id="hireDate" required>
                            </div>
                            <div class="col-md-4">
                                <button type="submit" class="btn btn-primary w-100">
                                    <i class="fas fa-plus me-2"></i>Add Employee
                                </button>
                            </div>
                        </div>
                    </form>
                </div>
            </div>

            <!-- Statistics Cards -->
            <div class="row mb-4">
                <div class="col-md-4 mb-3">
                    <div class="stat-card bg-primary">
                        <div class="card-body">
                            <i class="fas fa-users"></i>
                            <h5>Total Employees</h5>
                            <h2 id="totalEmployees">0</h2>
                        </div>
                    </div>
                </div>
                <div class="col-md-4 mb-3">
                    <div class="stat-card bg-success">
                        <div class="card-body">
                            <i class="fas fa-dollar-sign"></i>
                            <h5>Average Salary</h5>
                            <h2 id="avgSalary">$0</h2>
                        </div>
                    </div>
                </div>
                <div class="col-md-4 mb-3">
                    <div class="stat-card bg-info">
                        <div class="card-body">
                            <i class="fas fa-calendar-alt"></i>
                            <h5>Newest Hire</h5>
                            <h2 id="newestHire">-</h2>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Search and Table -->
            <div class="card">
                <div class="card-body">
                    <div class="d-flex justify-content-between align-items-center mb-3 flex-column flex-md-row">
                        <h5 class="card-title mb-3 mb-md-0"><i class="fas fa-list me-2"></i>Employee Directory</h5>
                        <input type="text" class="form-control" style="width: 300px;" placeholder="Search employees..." id="searchInput" onkeyup="searchEmployees()">
                    </div>
                    <div class="table-responsive">
                        <table class="table table-hover">
                            <thead>
                                <tr>
                                    <th>Name</th>
                                    <th>Email</th>
                                    <th>Position</th>
                                    <th>Salary</th>
                                    <th>Hire Date</th>
                                    <th>Actions</th>
                                </tr>
                            </thead>
                            <tbody id="employeeTable">
                                <!-- Employee data will be inserted here -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        let employees = JSON.parse(localStorage.getItem('employees')) || [];

        // Initialize with sample data if empty
        if (employees.length === 0) {
            employees = [
                {
                    id: 1,
                    name: "John Doe",
                    email: "john@example.com",
                    position: "Manager",
                    salary: 75000,
                    hireDate: "2022-01-15"
                },
                {
                    id: 2,
                    name: "Jane Smith",
                    email: "jane@example.com",
                    position: "Developer",
                    salary: 65000,
                    hireDate: "2022-03-20"
                },
                {
                    id: 3,
                    name: "Mike Johnson",
                    email: "mike@example.com",
                    position: "Designer",
                    salary: 60000,
                    hireDate: "2022-05-10"
                }
            ];
            saveToLocalStorage();
        }

        function saveToLocalStorage() {
            localStorage.setItem('employees', JSON.stringify(employees));
        }

        function addEmployee(e) {
            e.preventDefault();
            const employee = {
                id: Date.now(),
                name: document.getElementById('name').value,
                email: document.getElementById('email').value,
                position: document.getElementById('position').value,
                salary: parseFloat(document.getElementById('salary').value),
                hireDate: document.getElementById('hireDate').value
            };

            employees.push(employee);
            saveToLocalStorage();
            updateUI();
            document.getElementById('employeeForm').reset();
            
            // Show success notification
            alert('Employee added successfully!');
        }

        function updateUI() {
            updateEmployeeTable();
            updateStatistics();
        }

        function updateEmployeeTable() {
            const tbody = document.getElementById('employeeTable');
            tbody.innerHTML = '';

            // Sort by newest first
            const sortedEmployees = [...employees].sort((a, b) => new Date(b.hireDate) - new Date(a.hireDate));

            sortedEmployees.forEach(employee => {
                const tr = document.createElement('tr');
                tr.innerHTML = `
                    <td>${employee.name}</td>
                    <td>${employee.email}</td>
                    <td>${employee.position}</td>
                    <td>$${employee.salary.toLocaleString()}</td>
                    <td>${new Date(employee.hireDate).toLocaleDateString()}</td>
                    <td class="action-btns">
                        <button class="btn btn-sm btn-warning" onclick="editEmployee(${employee.id})">
                            <i class="fas fa-edit me-1"></i>Edit
                        </button>
                        <button class="btn btn-sm btn-danger" onclick="deleteEmployee(${employee.id})">
                            <i class="fas fa-trash me-1"></i>Delete
                        </button>
                    </td>
                `;
                tbody.appendChild(tr);
            });
        }

        function updateStatistics() {
            document.getElementById('totalEmployees').textContent = employees.length;
            
            const totalSalary = employees.reduce((sum, emp) => sum + emp.salary, 0);
            const avgSalary = employees.length > 0 ? totalSalary / employees.length : 0;
            document.getElementById('avgSalary').textContent = `$${avgSalary.toLocaleString(undefined, {maximumFractionDigits: 2})}`;

            const newest = [...employees].sort((a, b) => new Date(b.hireDate) - new Date(a.hireDate))[0];
            document.getElementById('newestHire').textContent = newest ? newest.name : '-';
        }

        function searchEmployees() {
            const searchTerm = document.getElementById('searchInput').value.toLowerCase();
            const filtered = employees.filter(emp => 
                emp.name.toLowerCase().includes(searchTerm) ||
                emp.email.toLowerCase().includes(searchTerm) ||
                emp.position.toLowerCase().includes(searchTerm)
            );
            
            const tbody = document.getElementById('employeeTable');
            tbody.innerHTML = '';
            
            filtered.forEach(emp => {
                const tr = document.createElement('tr');
                tr.innerHTML = `
                    <td>${emp.name}</td>
                    <td>${emp.email}</td>
                    <td>${emp.position}</td>
                    <td>$${emp.salary.toLocaleString()}</td>
                    <td>${new Date(emp.hireDate).toLocaleDateString()}</td>
                    <td class="action-btns">
                        <button class="btn btn-sm btn-warning" onclick="editEmployee(${emp.id})">
                            <i class="fas fa-edit me-1"></i>Edit
                        </button>
                        <button class="btn btn-sm btn-danger" onclick="deleteEmployee(${emp.id})">
                            <i class="fas fa-trash me-1"></i>Delete
                        </button>
                    </td>
                `;
                tbody.appendChild(tr);
            });
        }

        function deleteEmployee(id) {
            if (confirm('Are you sure you want to delete this employee?')) {
                employees = employees.filter(emp => emp.id !== id);
                saveToLocalStorage();
                updateUI();
                alert('Employee deleted successfully!');
            }
        }

        function editEmployee(id) {
            const employee = employees.find(emp => emp.id === id);
            if (employee) {
                document.getElementById('name').value = employee.name;
                document.getElementById('email').value = employee.email;
                document.getElementById('position').value = employee.position;
                document.getElementById('salary').value = employee.salary;
                document.getElementById('hireDate').value = employee.hireDate;
                
                deleteEmployee(id);
                
                // Scroll to form
                document.getElementById('employeeForm').scrollIntoView({ behavior: 'smooth' });
            }
        }

        // Initialize the UI when page loads
        document.addEventListener('DOMContentLoaded', function() {
            updateUI();
            
            // Set today's date as default for hire date
            const today = new Date();
            const formattedDate = today.toISOString().substr(0, 10);
            document.getElementById('hireDate').value = formattedDate;
        });
    </script>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
