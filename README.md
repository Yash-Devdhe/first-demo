<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Employee Management System</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            padding: 0;
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            color: #333;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        
        header {
            background: linear-gradient(to right, #4b6cb7, #182848);
            color: white;
            padding: 30px 0;
            text-align: center;
            border-radius: 0 0 10px 10px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            margin-bottom: 30px;
        }
        
        h1 {
            margin: 0;
            font-size: 2.5em;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
        }
        
        .form-section {
            background-color: white;
            padding: 25px;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            margin-bottom: 30px;
        }
        
        .form-group {
            margin-bottom: 15px;
        }
        
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: 600;
            color: #4b6cb7;
        }
        
        input, select {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-size: 16px;
        }
        
        button {
            background: linear-gradient(to right, #4b6cb7, #182848);
            color: white;
            border: none;
            padding: 12px 20px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
            font-weight: 600;
            transition: all 0.3s ease;
        }
        
        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }
        
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
            background-color: white;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            border-radius: 8px;
            overflow: hidden;
        }
        
        th, td {
            padding: 15px;
            text-align: left;
            border-bottom: 1px solid #ddd;
        }
        
        th {
            background: linear-gradient(to right, #4b6cb7, #182848);
            color: white;
            font-weight: 600;
        }
        
        tr:hover {
            background-color: #f5f5f5;
        }
        
        .actions {
            display: flex;
            gap: 10px;
        }
        
        .edit-btn {
            background: #4CAF50;
            padding: 5px 10px;
            font-size: 14px;
        }
        
        .delete-btn {
            background: #f44336;
            padding: 5px 10px;
            font-size: 14px;
        }
        
        footer {
            text-align: center;
            margin-top: 40px;
            padding: 20px;
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
        <section class="form-section">
            <h2>Add New Employee</h2>
            <form id="employeeForm">
                <div class="form-group">
                    <label for="name">Employee Name</label>
                    <input type="text" id="name" required>
                </div>
                
                <div class="form-group">
                    <label for="position">Position</label>
                    <input type="text" id="position" required>
                </div>
                
                <div class="form-group">
                    <label for="salary">Salary</label>
                    <input type="number" id="salary" required>
                </div>
                
                <div class="form-group">
                    <label for="department">Department</label>
                    <select id="department" required>
                        <option value="">Select Department</option>
                        <option value="IT">IT</option>
                        <option value="HR">HR</option>
                        <option value="Finance">Finance</option>
                        <option value="Marketing">Marketing</option>
                        <option value="Operations">Operations</option>
                    </select>
                </div>
                
                <button type="submit">Add Employee</button>
            </form>
        </section>
        
        <section class="form-section">
            <h2>Employee Records</h2>
            <table id="employeeTable">
                <thead>
                    <tr>
                        <th>ID</th>
                        <th>Name</th>
                        <th>Position</th>
                        <th>Salary</th>
                        <th>Department</th>
                        <th>Actions</th>
                    </tr>
                </thead>
                <tbody>
                    <!-- Sample data - will be populated by JavaScript -->
                    <tr>
                        <td>1</td>
                        <td>John Doe</td>
                        <td>Software Developer</td>
                        <td>$85,000</td>
                        <td>IT</td>
                        <td class="actions">
                            <button class="edit-btn">Edit</button>
                            <button class="delete-btn">Delete</button>
                        </td>
                    </tr>
                    <tr>
                        <td>2</td>
                        <td>Jane Smith</td>
                        <td>HR Manager</td>
                        <td>$75,000</td>
                        <td>HR</td>
                        <td class="actions">
                            <button class="edit-btn">Edit</button>
                            <button class="delete-btn">Delete</button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </section>
    </div>
    
    <footer>
        <p>&copy; 2025 Employee Management System.Designed by Yash Devdhe. All rights reserved.</p>
    </footer>
    
    <script>
        document.getElementById('employeeForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            // Get form values
            const name = document.getElementById('name').value;
            const position = document.getElementById('position').value;
            const salary = document.getElementById('salary').value;
            const department = document.getElementById('department').value;
            
            // Create new table row
            const table = document.getElementById('employeeTable').getElementsByTagName('tbody')[0];
            const newRow = table.insertRow();
            
            // Get the next ID (simple implementation)
            const nextId = table.rows.length + 1;
            
            // Insert cells
            const cell1 = newRow.insertCell(0);
            const cell2 = newRow.insertCell(1);
            const cell3 = newRow.insertCell(2);
            const cell4 = newRow.insertCell(3);
            const cell5 = newRow.insertCell(4);
            const cell6 = newRow.insertCell(5);
            
            // Add data to cells
            cell1.innerHTML = nextId;
            cell2.innerHTML = name;
            cell3.innerHTML = position;
            cell4.innerHTML = '$' + Number(salary).toLocaleString();
            cell5.innerHTML = department;
            cell6.innerHTML = `
                <div class="actions">
                    <button class="edit-btn">Edit</button>
                    <button class="delete-btn">Delete</button>
                </div>
            `;
            
            // Reset form
            document.getElementById('employeeForm').reset();
            
            // Add event listeners to new buttons
            addRowEventListeners(newRow);
        });
        
        // Function to add event listeners to row buttons
        function addRowEventListeners(row) {
            row.querySelector('.edit-btn').addEventListener('click', function() {
                const cells = row.cells;
                const name = cells[1].textContent;
                const position = cells[2].textContent;
                const salary = cells[3].textContent.replace('$', '').replace(/,/g, '');
                const department = cells[4].textContent;
                
                // Fill the form with this data
                document.getElementById('name').value = name;
                document.getElementById('position').value = position;
                document.getElementById('salary').value = salary;
                document.getElementById('department').value = department;
                
                // Remove the row
                row.remove();
            });
            
            row.querySelector('.delete-btn').addEventListener('click', function() {
                if (confirm('Are you sure you want to delete this employee?')) {
                    row.remove();
                }
            });
        }
        
        // Add event listeners to existing rows
        document.querySelectorAll('#employeeTable tbody tr').forEach(row => {
            addRowEventListeners(row);
        });
    </script>
</body>
</html>
