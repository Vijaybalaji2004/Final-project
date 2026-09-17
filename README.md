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

        :root {
            --purple: #7c3aed;
            --blue: #4f46e5;
            --cyan: #06b6d4;
            --pink: #ec4899;
            --green: #10b981;
            --red: #ef4444;
            --dark: #111827;
            --text: #1f2937;
            --muted: #64748b;
        }

        html {
            scroll-behavior: smooth;
        }

        body {
            font-family: Arial, sans-serif;
            color: var(--text);
            min-height: 100vh;

            background:
                radial-gradient(
                    circle at 10% 10%,
                    rgba(124, 58, 237, 0.18),
                    transparent 28%
                ),
                radial-gradient(
                    circle at 90% 20%,
                    rgba(6, 182, 212, 0.16),
                    transparent 25%
                ),
                radial-gradient(
                    circle at 70% 90%,
                    rgba(236, 72, 153, 0.13),
                    transparent 25%
                ),
                #f7f8fc;
        }

        /* ================= HEADER ================= */

        header {
            position: sticky;
            top: 0;
            z-index: 50;

            padding: 16px 8%;

            color: white;

            display: flex;
            justify-content: space-between;
            align-items: center;

            background: rgba(17, 24, 39, 0.90);
            backdrop-filter: blur(15px);

            border-bottom: 1px solid rgba(255,255,255,0.12);

            box-shadow:
                0 8px 30px rgba(15,23,42,0.18);
        }

        .logo {
            font-size: 25px;
            font-weight: 800;
        }

        .logo::before {
            content: "✦";
            color: #22d3ee;
            margin-right: 8px;
        }

        nav {
            display: flex;
            gap: 28px;
        }

        nav a {
            color: #e5e7eb;
            text-decoration: none;
            font-weight: 600;
            transition: 0.3s;
        }

        nav a:hover {
            color: #67e8f9;
        }

        /* ================= HERO ================= */

        .hero {
            position: relative;
            overflow: hidden;

            padding: 90px 8% 85px;

            color: white;

            background:
                linear-gradient(
                    120deg,
                    #4f46e5,
                    #7c3aed 50%,
                    #06b6d4
                );
        }

        .hero::before {
            content: "";

            position: absolute;

            width: 300px;
            height: 300px;

            right: 8%;
            top: -100px;

            border-radius: 50%;

            background: rgba(255,255,255,0.13);
        }

        .hero::after {
            content: "";

            position: absolute;

            width: 220px;
            height: 220px;

            left: 42%;
            bottom: -150px;

            border-radius: 50%;

            background: rgba(236,72,153,0.2);
        }

        .hero h1 {
            max-width: 850px;

            font-size: 55px;

            line-height: 1.1;

            margin-bottom: 18px;

            font-weight: 900;
        }

        .hero p {
            max-width: 720px;

            font-size: 18px;

            line-height: 1.7;

            margin-bottom: 28px;

            color: #eef2ff;
        }

        button {
            border: none;

            padding: 13px 21px;

            border-radius: 12px;

            color: white;

            cursor: pointer;

            font-size: 15px;

            font-weight: bold;

            background:
                linear-gradient(
                    135deg,
                    #4f46e5,
                    #7c3aed
                );

            box-shadow:
                0 8px 18px rgba(79,70,229,0.25);

            transition: 0.3s;
        }

        button:hover {
            transform: translateY(-3px);

            box-shadow:
                0 12px 25px rgba(79,70,229,0.35);
        }

        .hero button {
            background: white;
            color: #4f46e5;
        }

        /* ================= DASHBOARD ================= */

        .dashboard {
            width: 84%;
            max-width: 1400px;

            margin: 42px auto;
        }

        /* ================= STATS ================= */

        .stats {
            display: grid;

            grid-template-columns:
                repeat(3, 1fr);

            gap: 22px;

            margin-bottom: 30px;
        }

        .stat-card {
            position: relative;
            overflow: hidden;

            background: rgba(255,255,255,0.95);

            padding: 26px;

            min-height: 140px;

            border-radius: 20px;

            border: 1px solid #e5e7eb;

            box-shadow:
                0 12px 35px rgba(30,41,59,0.08);

            transition: 0.3s;
        }

        .stat-card:hover {
            transform: translateY(-6px);

            box-shadow:
                0 18px 42px rgba(30,41,59,0.14);
        }

        .stat-card::after {
            content: "";

            position: absolute;

            width: 90px;
            height: 90px;

            right: -25px;
            bottom: -30px;

            border-radius: 50%;

            background: rgba(124,58,237,0.10);
        }

        .stat-card:nth-child(2)::after {
            background: rgba(6,182,212,0.12);
        }

        .stat-card:nth-child(3)::after {
            background: rgba(16,185,129,0.12);
        }

        .stat-card h3 {
            color: var(--muted);

            margin-bottom: 12px;

            font-size: 14px;

            text-transform: uppercase;

            letter-spacing: 1px;
        }

        .stat-card h2 {
            font-size: 38px;

            color: var(--purple);
        }

        .stat-card:nth-child(2) h2 {
            color: var(--cyan);
        }

        .stat-card:nth-child(3) h2 {
            color: var(--green);
        }

        /* ================= CONTROLS ================= */

        .controls {
            display: flex;

            gap: 14px;

            margin-bottom: 30px;

            padding: 18px;

            border-radius: 18px;

            background: rgba(255,255,255,0.80);

            border: 1px solid #e5e7eb;

            box-shadow:
                0 10px 28px rgba(30,41,59,0.06);
        }

        .controls input,
        .controls select {
            flex: 1;

            padding: 14px 16px;

            border: 1px solid #dbe3ef;

            border-radius: 12px;

            font-size: 15px;

            outline: none;

            background: white;

            transition: 0.3s;
        }

        .controls input:focus,
        .controls select:focus {
            border-color: #8b5cf6;

            box-shadow:
                0 0 0 4px rgba(139,92,246,0.12);
        }

        .controls button {
            background:
                linear-gradient(
                    135deg,
                    #ec4899,
                    #8b5cf6
                );

            white-space: nowrap;
        }

        /* ================= LOADING ================= */

        #loading {
            text-align: center;

            margin: 35px;

            font-size: 18px;

            color: #64748b;

            font-weight: bold;
        }

        /* ================= EMPLOYEE CARDS ================= */

        .employee-container {
            display: grid;

            grid-template-columns:
                repeat(3, 1fr);

            gap: 25px;
        }

        .employee-card {
            position: relative;
            overflow: hidden;

            background: rgba(255,255,255,0.96);

            padding: 25px;

            border-radius: 22px;

            border: 1px solid #e5e7eb;

            box-shadow:
                0 12px 35px rgba(30,41,59,0.08);

            transition: 0.3s;
        }

        .employee-card::before {
            content: "";

            position: absolute;

            left: 0;
            top: 0;

            width: 100%;
            height: 5px;

            background:
                linear-gradient(
                    90deg,
                    #7c3aed,
                    #06b6d4,
                    #ec4899
                );
        }

        .employee-card:hover {
            transform: translateY(-8px);

            box-shadow:
                0 20px 45px rgba(30,41,59,0.15);
        }

        .employee-card img {
            width: 96px;
            height: 96px;

            border-radius: 50%;

            object-fit: cover;

            display: block;

            margin: 5px auto 15px;

            border: 5px solid #ede9fe;

            box-shadow:
                0 8px 20px rgba(124,58,237,0.18);
        }

        .employee-card h2 {
            text-align: center;

            margin: 10px 0;

            font-size: 21px;
        }

        .employee-card p {
            color: #64748b;

            margin: 10px 0;

            font-size: 14px;

            line-height: 1.5;

            word-break: break-word;
        }

        .employee-card p strong {
            color: #334155;
        }

        /* ================= BADGE ================= */

        .badge {
            display: block;

            width: max-content;

            margin: 8px auto 18px;

            padding: 6px 14px;

            border-radius: 30px;

            font-size: 12px;

            font-weight: bold;

            text-transform: uppercase;
        }

        .employee-card .badge {
            background: #ede9fe;

            color: #6d28d9;
        }

        .employee-card:nth-child(3n+2) .badge {
            background: #cffafe;

            color: #0e7490;
        }

        .employee-card:nth-child(3n) .badge {
            background: #fce7f3;

            color: #be185d;
        }

        /* ================= DELETE ================= */

        .delete-btn {
            width: 100%;

            margin-top: 15px;

            background:
                linear-gradient(
                    135deg,
                    #ef4444,
                    #dc2626
                );
        }

        /* ================= MODAL ================= */

        .modal {
            display: none;

            position: fixed;

            inset: 0;

            background: rgba(15,23,42,0.70);

            backdrop-filter: blur(8px);

            justify-content: center;

            align-items: center;

            z-index: 100;

            padding: 20px;
        }

        .modal-content {
            width: 430px;

            max-width: 100%;

            background: white;

            padding: 32px;

            border-radius: 24px;

            position: relative;

            box-shadow:
                0 30px 80px rgba(0,0,0,0.25);

            animation: pop 0.25s ease;
        }

        @keyframes pop {
            from {
                transform: scale(0.92);
                opacity: 0;
            }

            to {
                transform: scale(1);
                opacity: 1;
            }
        }

        .modal-content h2 {
            margin-bottom: 22px;

            color: #4f46e5;

            font-size: 26px;
        }

        .close {
            position: absolute;

            right: 20px;
            top: 12px;

            font-size: 30px;

            cursor: pointer;

            color: #64748b;
        }

        .close:hover {
            color: #ef4444;
        }

        #employeeForm {
            display: flex;

            flex-direction: column;

            gap: 14px;
        }

        #employeeForm input,
        #employeeForm select {
            padding: 14px;

            border: 1px solid #dbe3ef;

            border-radius: 12px;

            outline: none;

            font-size: 15px;
        }

        #employeeForm input:focus,
        #employeeForm select:focus {
            border-color: #8b5cf6;

            box-shadow:
                0 0 0 4px rgba(139,92,246,0.10);
        }

        #employeeForm button {
            margin-top: 5px;

            background:
                linear-gradient(
                    135deg,
                    #7c3aed,
                    #ec4899
                );
        }

        /* ================= FOOTER ================= */

        footer {
            margin-top: 70px;

            padding: 42px 20px;

            text-align: center;

            background:
                linear-gradient(
                    135deg,
                    #111827,
                    #312e81
                );

            color: white;
        }

        footer h3 {
            font-size: 22px;
        }

        footer p {
            margin-top: 9px;

            color: #cbd5e1;
        }

        /* ================= RESPONSIVE ================= */

        @media(max-width: 1000px) {

            .employee-container {
                grid-template-columns:
                    repeat(2, 1fr);
            }
        }

        @media(max-width: 900px) {

            .stats {
                grid-template-columns: 1fr;
            }

            .controls {
                flex-wrap: wrap;
            }
        }

        @media(max-width: 600px) {

            header {
                flex-direction: column;

                gap: 15px;

                padding: 16px 5%;
            }

            nav {
                gap: 18px;

                font-size: 14px;
            }

            .hero {
                padding: 65px 6%;
            }

            .hero h1 {
                font-size: 34px;
            }

            .hero p {
                font-size: 16px;
            }

            .dashboard {
                width: 90%;
            }

            .controls {
                flex-direction: column;
            }

            .employee-container {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>

<body>

    <!-- ================= HEADER ================= -->

    <header>

        <div class="logo">
            Vijay Balaji
        </div>

        <nav>
            <a href="#">Dashboard</a>
            <a href="#employees">Employees</a>
            <a href="#about">About</a>
        </nav>

    </header>


    <!-- ================= HERO ================= -->

    <section class="hero">

        <h1>
            Employee Management Dashboard
        </h1>

        <p>
            Manage employees easily with search,
            filtering, adding and deleting features.
        </p>

        <button onclick="loadEmployees()">
            🚀 Load Employees
        </button>

    </section>


    <!-- ================= DASHBOARD ================= -->

    <section class="dashboard">

        <!-- STATISTICS -->

        <div class="stats">

            <div class="stat-card">

                <h3>
                    Total Employees
                </h3>

                <h2 id="totalEmployees">
                    0
                </h2>

            </div>


            <div class="stat-card">

                <h3>
                    Displayed Employees
                </h3>

                <h2 id="displayedEmployees">
                    0
                </h2>

            </div>


            <div class="stat-card">

                <h3>
                    Added Employees
                </h3>

                <h2 id="addedEmployees">
                    0
                </h2>

            </div>

        </div>


        <!-- SEARCH + FILTER -->

        <div class="controls">

            <input
                type="text"
                id="searchInput"
                placeholder="🔍 Search employee..."
                onkeyup="searchEmployees()"
            >


            <select
                id="genderFilter"
                onchange="filterEmployees()"
            >

                <option value="all">
                    All Gender
                </option>

                <option value="male">
                    Male
                </option>

                <option value="female">
                    Female
                </option>

            </select>


            <button onclick="openForm()">
                ➕ Add Employee
            </button>

        </div>


        <!-- LOADING -->

        <div id="loading">
            Loading employees...
        </div>


        <!-- EMPLOYEE CARDS -->

        <div
            id="employees"
            class="employee-container"
        ></div>

    </section>


    <!-- ================= MODAL ================= -->

    <div
        id="employeeModal"
        class="modal"
    >

        <div class="modal-content">

            <span
                class="close"
                onclick="closeForm()"
            >
                &times;
            </span>


            <h2>
                Add New Employee
            </h2>


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

                    <option value="male">
                        Male
                    </option>

                    <option value="female">
                        Female
                    </option>

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


    <!-- ================= FOOTER ================= -->

    <footer id="about">

        <h3>
            Vijay Balaji
        </h3>

        <p>
            JavaScript Employee Management Project
        </p>

        <p>
            HTML • CSS • JavaScript • Fetch API
        </p>

    </footer>


    <!-- ================= JAVASCRIPT ================= -->

    <script>

        const API_URL =
            "https://dummyjson.com/users";

        let employees = [];

        let addedEmployees = [];


        /* ================= FETCH API ================= */

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

                    throw new Error(
                        "API Error"
                    );

                }


                const data =
                    await response.json();


                employees =
                    data.users;


                document.getElementById(
                    "totalEmployees"
                ).innerText =
                    employees.length;


                displayEmployees(
                    employees
                );

            }

            catch(error) {

                loading.innerText =
                    "❌ Unable to load employees.";

                console.log(error);

            }

        }


        /* ================= DISPLAY ================= */

        function displayEmployees(data) {

            const container =
                document.getElementById(
                    "employees"
                );


            const loading =
                document.getElementById(
                    "loading"
                );


            container.innerHTML = "";

            loading.style.display = "none";


            document.getElementById(
                "displayedEmployees"
            ).innerText =
                data.length;


            if(data.length === 0) {

                container.innerHTML = `
                    <h2>
                        No employees found
                    </h2>
                `;

                return;
            }


            data.forEach(function(employee) {

                const card =
                    document.createElement(
                        "div"
                    );


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
                        <strong>
                            📧 Email:
                        </strong>

                        ${employee.email}
                    </p>


                    <p>
                        <strong>
                            📞 Phone:
                        </strong>

                        ${employee.phone}
                    </p>


                    <p>
                        <strong>
                            🏢 Company:
                        </strong>

                        ${employee.company.name}
                    </p>


                    <p>
                        <strong>
                            💼 Department:
                        </strong>

                        ${employee.company.department}
                    </p>


                    <button
                        class="delete-btn"
                        onclick="deleteEmployee(${employee.id})"
                    >
                        🗑 Delete Employee
                    </button>

                `;


                container.appendChild(card);

            });

        }


        /* ================= SEARCH ================= */

        function searchEmployees() {

            const value =
                document
                .getElementById(
                    "searchInput"
                )
                .value
                .toLowerCase();


            const result =
                employees.filter(
                    function(employee) {

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

                    }
                );


            displayEmployees(result);

        }


        /* ================= FILTER ================= */

        function filterEmployees() {

            const gender =
                document.getElementById(
                    "genderFilter"
                ).value;


            if(gender === "all") {

                displayEmployees(
                    employees
                );

                return;
            }


            const result =
                employees.filter(
                    function(employee) {

                        return (
                            employee.gender ===
                            gender
                        );

                    }
                );


            displayEmployees(result);

        }


        /* ================= DELETE ================= */

        function deleteEmployee(id) {

            const confirmDelete =
                confirm(
                    "Are you sure you want to delete this employee?"
                );


            if(!confirmDelete) {

                return;

            }


            employees =
                employees.filter(
                    function(employee) {

                        return employee.id !== id;

                    }
                );


            document.getElementById(
                "totalEmployees"
            ).innerText =
                employees.length;


            displayEmployees(
                employees
            );

        }


        /* ================= OPEN FORM ================= */

        function openForm() {

            document.getElementById(
                "employeeModal"
            ).style.display =
                "flex";

        }


        /* ================= CLOSE FORM ================= */

        function closeForm() {

            document.getElementById(
                "employeeModal"
            ).style.display =
                "none";

        }


        /* ================= ADD EMPLOYEE ================= */

        document
        .getElementById(
            "employeeForm"
        )
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

                    firstName:
                        firstName,

                    lastName:
                        lastName,

                    email:
                        email,

                    gender:
                        gender,

                    phone:
                        "Not Available",

                    image:
                        "https://randomuser.me/api/portraits/lego/1.jpg",

                    company: {

                        name:
                            company,

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


        /* ================= INITIAL LOAD ================= */

        loadEmployees();

    </script>

</body>
</html>
