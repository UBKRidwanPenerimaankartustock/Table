<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistem Manajemen Farmasi</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        :root {
            --primary: #3498db;
            --secondary: #2c3e50;
            --success: #27ae60;
            --danger: #e74c3c;
            --warning: #f39c12;
            --info: #2980b9;
            --light: #f8f9fa;
            --dark: #343a40;
            --sidebar-width: 280px;
        }

        body {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 0;
        }

        .app-container {
            display: flex;
            min-height: 100vh;
        }

        /* Sidebar Navigation */
        .sidebar {
            width: var(--sidebar-width);
            background: var(--secondary);
            color: white;
            padding: 20px 0;
            transition: all 0.3s ease;
            position: fixed;
            height: 100vh;
            overflow-y: auto;
        }

        .sidebar-header {
            padding: 20px;
            text-align: center;
            border-bottom: 1px solid rgba(255,255,255,0.1);
        }

        .sidebar-header h2 {
            font-size: 1.5em;
            margin-bottom: 5px;
        }

        .sidebar-header p {
            font-size: 0.9em;
            opacity: 0.8;
        }

        .sidebar-menu {
            list-style: none;
            padding: 20px 0;
        }

        .sidebar-menu li {
            margin-bottom: 5px;
        }

        .sidebar-menu a {
            display: flex;
            align-items: center;
            padding: 15px 20px;
            color: white;
            text-decoration: none;
            transition: all 0.3s ease;
            border-left: 4px solid transparent;
        }

        .sidebar-menu a:hover {
            background: rgba(255,255,255,0.1);
            border-left-color: var(--primary);
        }

        .sidebar-menu a.active {
            background: rgba(255,255,255,0.15);
            border-left-color: var(--primary);
        }

        .sidebar-menu i {
            margin-right: 15px;
            width: 20px;
            text-align: center;
            font-size: 1.1em;
        }

        /* Main Content */
        .main-content {
            flex: 1;
            margin-left: var(--sidebar-width);
            background: var(--light);
            min-height: 100vh;
        }

        .top-bar {
            background: white;
            padding: 15px 30px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .search-box {
            display: flex;
            align-items: center;
            background: var(--light);
            border-radius: 25px;
            padding: 8px 20px;
            width: 350px;
        }

        .search-box input {
            border: none;
            background: transparent;
            padding: 8px;
            width: 100%;
            outline: none;
            font-size: 0.95em;
        }

        .user-menu {
            display: flex;
            align-items: center;
            gap: 20px;
        }

        .user-avatar {
            width: 45px;
            height: 45px;
            border-radius: 50%;
            background: var(--primary);
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            font-size: 1.1em;
        }

        /* Page Content */
        .page-content {
            padding: 30px;
            display: none;
        }

        .page-content.active {
            display: block;
        }

        .page-header {
            margin-bottom: 30px;
        }

        .page-header h1 {
            color: var(--secondary);
            font-size: 2.2em;
            margin-bottom: 10px;
        }

        .page-header p {
            color: #6c757d;
            font-size: 1.1em;
        }

        /* Dashboard Cards */
        .dashboard-cards {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 25px;
            margin-bottom: 40px;
        }

        .card {
            background: white;
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.08);
            text-align: center;
            transition: transform 0.3s ease;
        }

        .card:hover {
            transform: translateY(-5px);
        }

        .card i {
            font-size: 2.5em;
            color: var(--primary);
            margin-bottom: 20px;
        }

        .card h3 {
            font-size: 1.3em;
            margin-bottom: 15px;
            color: var(--secondary);
        }

        .card p {
            font-size: 2.2em;
            font-weight: bold;
            color: var(--dark);
        }

        /* Table Styles */
        .table-container {
            background: white;
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.08);
            margin-bottom: 30px;
            overflow-x: auto;
        }

        .table-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            flex-wrap: wrap;
            gap: 15px;
        }

        .table-header h2 {
            color: var(--secondary);
            font-size: 1.5em;
        }

        .table-actions {
            display: flex;
            gap: 12px;
            flex-wrap: wrap;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            background: white;
            border-radius: 10px;
            overflow: hidden;
        }

        th, td {
            padding: 18px 15px;
            text-align: left;
            border-bottom: 1px solid #e9ecef;
        }

        th {
            background: linear-gradient(135deg, var(--primary) 0%, var(--info) 100%);
            color: white;
            font-weight: 600;
            text-transform: uppercase;
            font-size: 0.9em;
            letter-spacing: 0.5px;
            position: sticky;
            top: 0;
        }

        tr:hover {
            background-color: #f8f9fa;
        }

        .checkbox-cell {
            text-align: center;
            width: 60px;
        }

        input[type="checkbox"] {
            width: 20px;
            height: 20px;
            cursor: pointer;
        }

        input[type="text"], input[type="number"], input[type="date"], select {
            width: 100%;
            padding: 12px;
            border: 2px solid #e9ecef;
            border-radius: 8px;
            font-size: 0.95em;
            transition: all 0.3s ease;
        }

        input:focus, select:focus {
            outline: none;
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.1);
        }

        /* Button Styles */
        button {
            padding: 12px 25px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            gap: 8px;
            font-size: 0.95em;
        }

        .btn-primary {
            background: linear-gradient(135deg, var(--success) 0%, #2ecc71 100%);
            color: white;
        }

        .btn-secondary {
            background: linear-gradient(135deg, #95a5a6 0%, #7f8c8d 100%);
            color: white;
        }

        .btn-danger {
            background: linear-gradient(135deg, var(--danger) 0%, #c0392b 100%);
            color: white;
        }

        .btn-info {
            background: linear-gradient(135deg, var(--info) 0%, #3498db 100%);
            color: white;
        }

        .btn-warning {
            background: linear-gradient(135deg, var(--warning) 0%, #e67e22 100%);
            color: white;
        }

        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }

        /* Status Badges */
        .status-badge {
            padding: 8px 15px;
            border-radius: 20px;
            font-size: 0.85em;
            font-weight: 600;
            text-transform: uppercase;
            display: inline-block;
            text-align: center;
        }

        .status-baik {
            background: #d4edda;
            color: #155724;
        }

        .status-rusak {
            background: #f8d7da;
            color: #721c24;
        }

        .status-kadaluarsa {
            background: #fff3cd;
            color: #856404;
        }

        /* Modal Styles */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            z-index: 1000;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }

        .modal-content {
            background: white;
            padding: 30px;
            border-radius: 15px;
            width: 90%;
            max-width: 600px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.2);
            max-height: 90vh;
            overflow-y: auto;
        }

        .modal-header {
            margin-bottom: 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .modal-header h2 {
            color: var(--secondary);
            font-size: 1.5em;
        }

        .modal-body {
            margin-bottom: 25px;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            color: var(--secondary);
            font-weight: 600;
        }

        .modal-footer {
            display: flex;
            gap: 12px;
            justify-content: flex-end;
        }

        /* Signature Section */
        .signature-section {
            padding: 25px;
            background: white;
            border-radius: 15px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.08);
            margin-top: 30px;
        }

        .signature-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 30px;
        }

        .signature-item {
            text-align: center;
        }

        .signature-item h4 {
            color: var(--secondary);
            margin-bottom: 15px;
            font-size: 1.1em;
        }

        .signature-line {
            height: 2px;
            background: var(--primary);
            margin: 20px 0;
        }

        .signature-placeholder {
            height: 80px;
            border: 2px dashed #bdc3c7;
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: #7f8c8d;
            font-style: italic;
            margin-bottom: 15px;
        }

        /* Responsive Design */
        @media (max-width: 1024px) {
            .sidebar {
                width: 250px;
                transform: translateX(-100%);
                z-index: 1000;
            }
            
            .sidebar.active {
                transform: translateX(0);
            }
            
            .main-content {
                margin-left: 0;
            }
            
            .menu-toggle {
                display: block;
            }
        }

        @media (max-width: 768px) {
            .top-bar {
                padding: 15px 20px;
            }
            
            .search-box {
                width: 250px;
            }
            
            .dashboard-cards {
                grid-template-columns: 1fr;
            }
            
            .table-header {
                flex-direction: column;
                align-items: flex-start;
            }
            
            .table-actions {
                width: 100%;
                justify-content: center;
            }
            
            th, td {
                padding: 12px 8px;
                font-size: 0.9em;
            }
            
            .modal-content {
                padding: 20px;
            }
        }

        @media (max-width: 480px) {
            .search-box {
                width: 200px;
            }
            
            .user-menu {
                gap: 12px;
            }
            
            .page-content {
                padding: 20px;
            }
            
            .table-container {
                padding: 15px;
            }
        }

        /* Animation */
        @keyframes slideIn {
            from {
                transform: translateX(-100%);
            }
            to {
                transform: translateX(0);
            }
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(-20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .fade-in {
            animation: fadeIn 0.5s ease;
        }

        /* Menu Toggle for Mobile */
        .menu-toggle {
            display: none;
            background: var(--primary);
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 1.2em;
        }

        @media (max-width: 1024px) {
            .menu-toggle {
                display: block;
            }
        }
    </style>
</head>
<body>
    <div class="app-container">
        <!-- Sidebar Navigation -->
        <div class="sidebar">
            <div class="sidebar-header">
                <h2><i class="fas fa-pills"></i> PharmaSys</h2>
                <p>Management System</p>
            </div>
            <ul class="sidebar-menu">
                <li><a href="#dashboard" class="active" onclick="showPage('dashboard')"><i class="fas fa-home"></i> Dashboard</a></li>
                <li><a href="#penerimaan" onclick="showPage('penerimaan')"><i class="fas fa-truck-loading"></i> Penerimaan Obat</a></li>
                <li><a href="#penyimpanan" onclick="showPage('penyimpanan')"><i class="fas fa-warehouse"></i> Penyimpanan Obat</a></li>
                <li><a href="#inventory" onclick="showPage('inventory')"><i class="fas fa-boxes"></i> Inventory</a></li>
                <li><a href="#reports" onclick="showPage('reports')"><i class="fas fa-chart-bar"></i> Laporan</a></li>
                <li><a href="#settings" onclick="showPage('settings')"><i class="fas fa-cog"></i> Pengaturan</a></li>
            </ul>
        </div>

        <!-- Main Content -->
        <div class="main-content">
            <div class="top-bar">
                <button class="menu-toggle" onclick="toggleSidebar()">
                    <i class="fas fa-bars"></i>
                </button>
                <div class="search-box">
                    <i class="fas fa-search"></i>
                    <input type="text" placeholder="Cari obat atau perbekalan..." id="searchInput">
                </div>
                <div class="user-menu">
                    <i class="fas fa-bell
