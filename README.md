<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vijay Balaji - Employee Dashboard</title>

    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: Arial, sans-serif;
            background: #f4f7fb;
            color: #222;
        }

        header {
            padding: 18px 8%;
            background: #111827;
            color: white;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            font-size: 25px;
            font-weight: bold;
        }

        nav {
            display: flex;
            gap: 25px;
        }

        nav a {
            color: white;
            text-decoration: none;
        }

        nav a:hover {
            color: #38bdf8;
        }

        .hero {
            padding: 70px 8%;
            background: linear-gradient(135deg, #1e3a8a, #2563eb, #06b6d4);
            color: white;
        }

        .hero h1 {
            font-size: 45px;
            margin-bottom: 15px;
        }

        .hero p {
            font-size: 18px;
            line-height: 1.6;
            margin-bottom: 25px;
        }

        button {
            border: none;
            padding: 12px 22px;
            border-radius: 8px;
            background: #2563eb;
            color: white;
            cursor: pointer;
            font-size: 15px;
            font-weight: bold;
        }

        button:hover {
            opacity: 0.85;
        }

        .hero button {
            background: white;
            color: #1d4ed8;
        }

        .dashboard {
            width: 84%;
            margin: 40px auto;
        }

        .stats {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 20px;
            margin-bottom: 30px;
        }

        .stat-card {
            background: white;
            padding: 25px;
            border-radius: 15px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.08);
        }

        .stat-card h3 {
            color: #64748b;
            margin-bottom: 10px;
        }

        .stat-card h2 {
            font-size: 35px;
            color: #2563eb;
        }

        .controls {
            display: flex;
            gap: 15px;
            margin-bottom: 30px;
        }

        .controls input,
        .controls select {
            flex: 1;
            padding: 13px;
            border: 1px solid #d1d5db;
            border-radius: 8px;
            font-size: 15px;
            outline: none;
        }

        .controls input:focus,
        .controls select:focus {
            border-color: #2563eb;
        }

        #loading {
            text-align: center;
            margin: 30px;
            font-size: 18px;
        }

        .employee-container {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 25px;
        }

        .employee-card {
            background: white;
            padding: 25px;
            border-radius: 15px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.08);
            transition: 0.3s;
        }

        .employee-card:hover {
            transform: translateY(-5px);
        }

        .employee-card img {
            width: 90px;
            height: 90px;
            border-radius: 50%;
            object-fit: cover;
            display: block;
            margin: auto;
        }

        .employee-card h2 {
            text-align: center;
            margin: 15px 0 10px;
        }

        .employee-card p {
            color: #64748b;
            margin: 8px 0;
            font-size: 14px;
        }

        .badge {
            display: block;
            width: fit-content;
            margin: 10px auto;
            padding: 5px 12px;
            border-radius: 20px;
            background: #dbeafe;
            color: #1d4ed8;
            font-size: 13px;
        }

        .delete-btn {
            width: 100%;
            margin-top: 15px;
            background: #dc2626;
        }

        .modal {
            display: none;
            position: fixed;
            inset: 0;
            background: rgba(0,0,0,0.6);
            justify-content: center;
            align-items: center;
            z-index: 100;
        }

        .modal-content {
            width: 400px;
            background: white;
            padding: 30px;
            border-radius: 15px;
            position: relative;
        }

        .modal-content h2 {
            margin-bottom: 20px;
        }

        .close {
            position: absolute;
            right: 20px;
            top: 12px;
            font-size: 30px;
            cursor: pointer;
        }

        #employeeForm {
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        #employeeForm input,
        #employeeForm select {
            padding: 13px;
            border: 1px solid #d1d5db;
            border-radius: 8px;
            outline: none;
        }

        footer {
            margin-top: 60px;
            padding: 35px;
            text-align: center;
            background: #111827;
            color: white;
        }

        footer p {
            margin-top: 8px;
            color: #cbd5e1;
        }

        @media (max-width: 900px) {
            .employee-container {
                grid-template-columns: repeat(2, 1fr);
            }

            .stats {
                grid-template-columns: 1fr;
            }
        }

        @media (max-width: 600px) {
            header {
                flex-direction: column;
                gap: 15px;
            }

            .hero h1 {
                font-size: 32px;
            }

            .dashboard {
                width: 92%;
            }

            .controls {
                flex-direction: column;
            }

            .employee-container {
                grid-template-columns: 1fr;
            }

            .modal-content {
                width: 90%;
            }
        }
    </style>
</head>

<body>

    <header>
        <div class="logo">Vijay Balaji</div>

        <nav>
            <a href="#">Dashboard</a>
            <a href="#employees">Employees</a>
            <a href="#about">About</a>
        </nav>
    </header>


    <section class="hero">

        <h1>Employee Management Dashboard</h1>

        <p>
            Manage employees easily with search, filtering,
            adding and deleting features.
        </p>

        <button onclick="loadEmployees()">
            Load Employees
        </button>

    </section>


    <section class="dashboard">

        <div class="stats">

            <div class="stat-card">
                <h3>Total Employees</h3>
                <h2 id="totalEmployees">0</h2>
            </div>

            <div class="stat-card">
                <h3>Displayed Employees</h3>
                <h2 id="displayedEmployees">0</h2>
            </div>

            <div class="stat-card">
                <h3>Added Employees</h3>
                <h2 id="addedEmployees">0</h2>
            </div>

        </div>


        <div class="controls">

            <input
                type="text"
                id="searchInput"
                placeholder="Search employee..."
                onkeyup="searchEmployees()"
            >

            <select
                id="genderFilter"
                onchange="filterEmployees()"
            >
                <option value="all">All Gender</option>
                <option value="male">Male</option>
                <option value="female">Female</option>
            </select>

            <button onclick="openForm()">
                + Add Employee
            </button>

        </div>


        <div id="loading">
            Loading employees...
        </div>


        <div id="employees" class="employee-container"></div>

    </section>


    <div id="employeeModal" class="modal">

        <div class="modal-content">

            <span class="close" onclick="closeForm()">
                &times;
            </span>

            <h2>Add Employee</h2>

            <form id="employeeForm">

                <input
                    type="text"
                    id="firstName"
                    placeholder="First Name"
                    required
                >

                <input
                    type="text"
                    id="lastName"
                    placeholder="Last Name"
                    required
                >

                <input
                    type="email"
                    id="email"
                    placeholder="Email"
                    required
                >

                <select id="gender">
                    <option value="male">Male</option>
                    <option value="female">Female</option>
                </select>

                <input
                    type="text"
                    id="company"
                    placeholder="Company"
                    required
                >

                <button type="submit">
                    Add Employee
                </button>

            </form>

        </div>

    </div>


    <footer id="about">

        <h3>Vijay Balaji</h3>

        <p>
            JavaScript Employee Management Project
        </p>

        <p>
            HTML • CSS • JavaScript • Fetch API
        </p>

    </footer>


    <script>

        const API_URL = "https://dummyjson.com/users";

        let employees = [];

        let addedEmployees = [];


        // FETCH API DATA

        async function loadEmployees() {

            const loading =
                document.getElementById("loading");

            loading.style.display = "block";

            loading.innerText =
                "Loading employees...";


            try {

                const response =
                    await fetch(API_URL);


                if (!response.ok) {

                    throw new Error("API Error");

                }


                const data =
                    await response.json();


                employees =
                    data.users;


                document.getElementById(
                    "totalEmployees"
                ).innerText =
                    employees.length;


                displayEmployees(employees);


            }

            catch(error) {

                loading.innerText =
                    "Unable to load employees.";

                console.log(error);

            }

        }


        // DISPLAY EMPLOYEES

        function displayEmployees(data) {

            const container =
                document.getElementById("employees");


            const loading =
                document.getElementById("loading");


            container.innerHTML = "";

            loading.style.display = "none";


            document.getElementById(
                "displayedEmployees"
            ).innerText =
                data.length;


            if(data.length === 0) {

                container.innerHTML =
                    "<h2>No employees found</h2>";

                return;

            }


            data.forEach(function(employee) {

                const card =
                    document.createElement("div");


                card.className =
                    "employee-card";


                card.innerHTML = `

                    <img
                        src="${employee.image}"
                        alt="${employee.firstName}"
                    >

                    <h2>
                        ${employee.firstName}
                        ${employee.lastName}
                    </h2>

                    <span class="badge">
                        ${employee.gender}
                    </span>

                    <p>
                        <strong>Email:</strong>
                        ${employee.email}
                    </p>

                    <p>
                        <strong>Phone:</strong>
                        ${employee.phone}
                    </p>

                    <p>
                        <strong>Company:</strong>
                        ${employee.company.name}
                    </p>

                    <p>
                        <strong>Department:</strong>
                        ${employee.company.department}
                    </p>

                    <button
                        class="delete-btn"
                        onclick="deleteEmployee(${employee.id})"
                    >
                        Delete
                    </button>

                `;


                container.appendChild(card);

            });

        }


        // SEARCH

        function searchEmployees() {

            const value =
                document
                .getElementById("searchInput")
                .value
                .toLowerCase();


            const result =
                employees.filter(function(employee) {

                    const fullName =
                        employee.firstName +
                        " " +
                        employee.lastName;


                    return (
                        fullName
                        .toLowerCase()
                        .includes(value)
                        ||
                        employee.email
                        .toLowerCase()
                        .includes(value)
                    );

                });


            displayEmployees(result);

        }


        // FILTER

        function filterEmployees() {

            const gender =
                document.getElementById(
                    "genderFilter"
                ).value;


            if(gender === "all") {

                displayEmployees(employees);

                return;

            }


            const result =
                employees.filter(function(employee) {

                    return employee.gender === gender;

                });


            displayEmployees(result);

        }


        // DELETE

        function deleteEmployee(id) {

            const confirmDelete =
                confirm(
                    "Are you sure you want to delete this employee?"
                );


            if(!confirmDelete) {

                return;

            }


            employees =
                employees.filter(function(employee) {

                    return employee.id !== id;

                });


            document.getElementById(
                "totalEmployees"
            ).innerText =
                employees.length;


            displayEmployees(employees);

        }


        // OPEN FORM

        function openForm() {

            document.getElementById(
                "employeeModal"
            ).style.display =
                "flex";

        }


        // CLOSE FORM

        function closeForm() {

            document.getElementById(
                "employeeModal"
            ).style.display =
                "none";

        }


        // ADD EMPLOYEE

        document
        .getElementById("employeeForm")
        .addEventListener(
            "submit",
            function(event) {

                event.preventDefault();


                const firstName =
                    document.getElementById(
                        "firstName"
                    ).value;


                const lastName =
                    document.getElementById(
                        "lastName"
                    ).value;


                const email =
                    document.getElementById(
                        "email"
                    ).value;


                const gender =
                    document.getElementById(
                        "gender"
                    ).value;


                const company =
                    document.getElementById(
                        "company"
                    ).value;


                const newEmployee = {

                    id: Date.now(),

                    firstName: firstName,

                    lastName: lastName,

                    email: email,

                    gender: gender,

                    phone: "Not Available",

                    image:
                        "https://randomuser.me/api/portraits/lego/1.jpg",

                    company: {

                        name: company,

                        department:
                            "New Employee"

                    }

                };


                employees.unshift(
                    newEmployee
                );


                addedEmployees.push(
                    newEmployee
                );


                document.getElementById(
                    "totalEmployees"
                ).innerText =
                    employees.length;


                document.getElementById(
                    "addedEmployees"
                ).innerText =
                    addedEmployees.length;


                displayEmployees(
                    employees
                );


                document.getElementById(
                    "employeeForm"
                ).reset();


                closeForm();

            }
        );


        // LOAD DATA WHEN PAGE OPENS

        loadEmployees();

    </script>

</body>
</html>
