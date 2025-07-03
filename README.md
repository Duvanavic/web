# web
Sistema de Gestión de Créditos
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistema de Gestión de Créditos - Global Pacific SAS</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jszip/3.10.1/jszip.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/FileSaver.js/2.0.5/FileSaver.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
    <style>
        /* Estilos optimizados y mejorados */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #1a2a6c, #b21f1f, #1a2a6c);
            color: #333;
            line-height: 1.6;
            padding: 20px;
            min-height: 100vh;
            background-size: 400% 400%;
            animation: gradientBG 15s ease infinite;
        }
        
        @keyframes gradientBG {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
        }
        
        header {
            text-align: center;
            margin-bottom: 30px;
            padding: 30px;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
            animation: fadeInDown 1s ease;
            position: relative;
        }
        
        @keyframes fadeInDown {
            from {
                opacity: 0;
                transform: translateY(-20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        h1 {
            color: #1a2a6c;
            margin-bottom: 10px;
            font-size: 2.5rem;
        }
        
        .subtitle {
            color: #b21f1f;
            font-weight: 500;
            font-size: 1.2rem;
        }
        
        .form-container {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 10px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.25);
            overflow: hidden;
            margin-bottom: 30px;
            animation: fadeInUp 1s ease;
        }
        
        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        .form-header {
            background: #1a2a6c;
            color: white;
            padding: 15px 25px;
            font-size: 1.4rem;
            display: flex;
            align-items: center;
        }
        
        .form-header i {
            margin-right: 10px;
            font-size: 1.6rem;
        }
        
        .form-body {
            padding: 25px;
        }
        
        .form-section {
            margin-bottom: 30px;
            padding-bottom: 20px;
            border-bottom: 1px solid #eaeaea;
        }
        
        .section-title {
            background: #e9ecef;
            padding: 10px 15px;
            border-left: 4px solid #b21f1f;
            margin-bottom: 20px;
            font-weight: 600;
            color: #1a2a6c;
            display: flex;
            align-items: center;
            border-radius: 4px;
        }
        
        .section-title i {
            margin-right: 10px;
            color: #b21f1f;
        }
        
        .form-row {
            display: flex;
            flex-wrap: wrap;
            margin: 0 -10px 15px;
        }
        
        .form-group {
            flex: 1 0 300px;
            padding: 0 10px;
            margin-bottom: 15px;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #495057;
        }
        
        input, select, textarea {
            width: 100%;
            padding: 12px 15px;
            border: 1px solid #ced4da;
            border-radius: 6px;
            font-size: 1rem;
            transition: all 0.3s;
        }
        
        input:focus, select:focus, textarea:focus {
            outline: none;
            border-color: #1a2a6c;
            box-shadow: 0 0 0 3px rgba(26, 42, 108, 0.1);
        }
        
        .documents-section {
            background: #f8f9fa;
            border-radius: 8px;
            padding: 20px;
            margin-top: 20px;
            border: 1px solid #eaeaea;
        }
        
        .document-table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
        }
        
        .document-table th {
            background: #1a2a6c;
            color: white;
            padding: 12px 15px;
            text-align: left;
        }
        
        .document-table td {
            padding: 12px 15px;
            border-bottom: 1px solid #eaeaea;
        }
        
        .document-table tr:nth-child(even) {
            background: #f1f3f5;
        }
        
        .document-status {
            display: inline-block;
            padding: 5px 10px;
            border-radius: 20px;
            font-size: 0.85rem;
            font-weight: 500;
        }
        
        .status-pending {
            background: #ffe3e3;
            color: #c92a2a;
        }
        
        .status-complete {
            background: #d3f9d8;
            color: #2b8a3e;
        }
        
        .status-review {
            background: #fff3cd;
            color: #856404;
        }
        
        .btn {
            padding: 12px 25px;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-size: 1rem;
            font-weight: 600;
            transition: all 0.3s;
            display: inline-flex;
            align-items: center;
            justify-content: center;
        }
        
        .btn i {
            margin-right: 8px;
        }
        
        .btn-primary {
            background: #1a2a6c;
            color: white;
        }
        
        .btn-primary:hover {
            background: #0d1a4a;
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        
        .btn-secondary {
            background: #495057;
            color: white;
        }
        
        .btn-secondary:hover {
            background: #343a40;
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        
        .btn-success {
            background: #2b8a3e;
            color: white;
        }
        
        .btn-success:hover {
            background: #237532;
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        
        .btn-danger {
            background: #c92a2a;
            color: white;
        }
        
        .btn-danger:hover {
            background: #a61e1e;
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        
        .btn-warning {
            background: #e67700;
            color: white;
        }
        
        .btn-warning:hover {
            background: #d35400;
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        
        .btn-info {
            background: #0dcaf0;
            color: white;
        }
        
        .btn-info:hover {
            background: #0aa2c0;
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        
        .action-buttons {
            display: flex;
            gap: 15px;
            margin-top: 30px;
            justify-content: center;
            flex-wrap: wrap;
        }
        
        .file-upload {
            position: relative;
            display: inline-block;
            cursor: pointer;
        }
        
        .file-upload input[type="file"] {
            position: absolute;
            left: 0;
            top: 0;
            opacity: 0;
            width: 100%;
            height: 100%;
            cursor: pointer;
        }
        
        footer {
            text-align: center;
            padding: 20px;
            color: white;
            font-size: 0.9rem;
            background: rgba(0, 0, 0, 0.2);
            border-radius: 10px;
            margin-top: 20px;
        }
        
        .person-type {
            display: flex;
            gap: 20px;
            margin-bottom: 20px;
        }
        
        .person-card {
            flex: 1;
            background: white;
            border-radius: 8px;
            padding: 20px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
            border: 2px solid transparent;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .person-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 16px rgba(0,0,0,0.15);
        }
        
        .person-card.selected {
            border-color: #1a2a6c;
            background: #f0f7ff;
        }
        
        .person-card h3 {
            color: #1a2a6c;
            margin-bottom: 15px;
            text-align: center;
        }
        
        .document-list {
            padding-left: 20px;
        }
        
        .document-list li {
            margin-bottom: 8px;
            position: relative;
            padding-left: 25px;
        }
        
        .document-list li:before {
            content: "•";
            color: #1a2a6c;
            font-size: 1.5rem;
            position: absolute;
            left: 0;
            top: -5px;
        }
        
        @media (max-width: 768px) {
            .person-type {
                flex-direction: column;
            }
            
            .action-buttons {
                flex-direction: column;
            }
            
            .form-header {
                font-size: 1.2rem;
            }
            
            h1 {
                font-size: 2rem;
            }
        }
        
        .progress-container {
            width: 100%;
            background: #e9ecef;
            border-radius: 20px;
            height: 10px;
            margin: 15px 0;
            overflow: hidden;
        }
        
        .progress-bar {
            height: 100%;
            background: #1a2a6c;
            border-radius: 20px;
            width: 0;
            transition: width 0.5s ease;
        }
        
        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            padding: 15px 20px;
            border-radius: 6px;
            color: white;
            font-weight: 500;
            box-shadow: 0 4px 12px rgba(0,0,0,0.15);
            z-index: 1000;
            transform: translateX(200%);
            transition: transform 0.4s ease;
            max-width: 90%;
        }
        
        .notification.show {
            transform: translateX(0);
        }
        
        .notification.success {
            background: #2b8a3e;
        }
        
        .notification.error {
            background: #c92a2a;
        }
        
        .notification.warning {
            background: #e67700;
        }
        
        /* Estilos para el panel de administración */
        .admin-panel {
            display: none;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 10px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.25);
            padding: 25px;
            margin-top: 30px;
            animation: fadeInUp 1s ease;
        }
        
        .admin-header {
            background: #1a2a6c;
            color: white;
            padding: 15px 25px;
            font-size: 1.4rem;
            display: flex;
            align-items: center;
            justify-content: space-between;
            border-radius: 10px 10px 0 0;
        }
        
        .admin-header h2 {
            display: flex;
            align-items: center;
        }
        
        .admin-header h2 i {
            margin-right: 10px;
        }
        
        .admin-actions {
            margin: 20px 0;
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
        }
        
        .submissions-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }
        
        .submissions-table th, .submissions-table td {
            padding: 12px 15px;
            border: 1px solid #ddd;
            text-align: left;
        }
        
        .submissions-table th {
            background: #1a2a6c;
            color: white;
        }
        
        .submissions-table tr:nth-child(even) {
            background: #f1f3f5;
        }
        
        .back-button {
            background: #495057;
            color: white;
            padding: 10px 15px;
            border-radius: 6px;
            text-decoration: none;
            display: inline-flex;
            align-items: center;
            font-weight: 500;
        }
        
        .back-button i {
            margin-right: 8px;
        }
        
        .tab-container {
            margin-top: 20px;
        }
        
        .tabs {
            display: flex;
            border-bottom: 2px solid #1a2a6c;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }
        
        .tab {
            padding: 12px 20px;
            cursor: pointer;
            background: #e9ecef;
            border-radius: 5px 5px 0 0;
            margin-right: 5px;
            min-width: 120px;
            text-align: center;
        }
        
        .tab.active {
            background: #1a2a6c;
            color: white;
            font-weight: 600;
        }
        
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
        }
        
        .stats-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }
        
        .stat-card {
            background: white;
            border-radius: 8px;
            padding: 20px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
            text-align: center;
        }
        
        .stat-card h3 {
            color: #1a2a6c;
            margin-bottom: 10px;
        }
        
        .stat-card .stat-value {
            font-size: 2.5rem;
            font-weight: 700;
            color: #b21f1f;
        }
        
        .stat-card .stat-label {
            color: #495057;
            font-size: 0.9rem;
        }
        
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.7);
            z-index: 10000;
            align-items: center;
            justify-content: center;
        }
        
        .modal-content {
            background: white;
            padding: 30px;
            border-radius: 10px;
            max-width: 500px;
            width: 90%;
            max-height: 90vh;
            overflow-y: auto;
            position: relative;
        }
        
        .close-modal {
            position: absolute;
            top: 15px;
            right: 15px;
            font-size: 1.5rem;
            cursor: pointer;
            color: #495057;
        }
        
        .login-container {
            max-width: 400px;
            margin: 100px auto;
            padding: 30px;
            background: white;
            border-radius: 10px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.25);
            text-align: center;
        }
        
        .login-container h2 {
            color: #1a2a6c;
            margin-bottom: 20px;
        }
        
        .login-container input {
            width: 100%;
            padding: 12px;
            margin-bottom: 15px;
            border: 1px solid #ced4da;
            border-radius: 6px;
        }
        
        .login-container button {
            width: 100%;
            padding: 12px;
            background: #1a2a6c;
            color: white;
            border: none;
            border-radius: 6px;
            font-weight: 600;
            cursor: pointer;
        }
        
        .credentials-form {
            background: #f8f9fa;
            border-radius: 8px;
            padding: 20px;
            margin-top: 20px;
            border: 1px solid #eaeaea;
        }
        
        .credentials-form h3 {
            color: #1a2a6c;
            margin-bottom: 15px;
            text-align: center;
        }
        
        .download-all-btn {
            margin: 15px 0;
            text-align: center;
        }
        
        .download-link {
            color: #1a2a6c;
            text-decoration: none;
            display: inline-flex;
            align-items: center;
            gap: 5px;
            padding: 5px 10px;
            border-radius: 4px;
            transition: all 0.3s;
        }
        
        .download-link:hover {
            background: #e9ecef;
        }
        
        .file-info {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        /* Nuevos estilos para generación de enlaces */
        .link-form {
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
            margin-bottom: 20px;
        }
        
        .link-form h3 {
            color: #1a2a6c;
            margin-bottom: 15px;
            text-align: center;
        }
        
        .generated-link {
            background: #f1f3f5;
            padding: 15px;
            border-radius: 8px;
            margin-top: 15px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        
        .generated-link a {
            color: #1a2a6c;
            font-weight: 600;
            font-size: 1rem;
            text-decoration: none;
            word-break: break-all;
            text-align: center;
            margin-bottom: 15px;
        }
        
        .qr-container {
            margin: 15px 0;
            display: flex;
            justify-content: center;
        }
        
        .link-actions {
            display: flex;
            gap: 10px;
            justify-content: center;
            margin-top: 10px;
        }
        
        .client-list {
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
            margin-top: 20px;
        }
        
        .client-list h3 {
            color: #1a2a6c;
            margin-bottom: 15px;
            text-align: center;
        }
        
        .client-item {
            padding: 12px;
            border-bottom: 1px solid #eaeaea;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .client-item:last-child {
            border-bottom: none;
        }
        
        .client-info {
            flex: 1;
        }
        
        .client-info h4 {
            color: #1a2a6c;
            margin-bottom: 5px;
        }
        
        .client-actions {
            display: flex;
            gap: 10px;
        }
        
        .link-badge {
            background: #e9ecef;
            padding: 5px 10px;
            border-radius: 20px;
            font-size: 0.85rem;
            display: inline-flex;
            align-items: center;
            gap: 5px;
        }
        
        .link-badge i {
            color: #1a2a6c;
        }
        
        .file-preview {
            max-width: 100px;
            max-height: 100px;
            margin-top: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            display: none;
        }
        
        .status-badge {
            padding: 3px 8px;
            border-radius: 10px;
            font-size: 0.8rem;
            font-weight: 500;
        }
        
        .status-complete-badge {
            background-color: #d4edda;
            color: #155724;
        }
        
        .status-pending-badge {
            background-color: #fff3cd;
            color: #856404;
        }
        
        .document-actions {
            display: flex;
            gap: 5px;
        }
        
        .action-btn {
            padding: 5px 10px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 0.85rem;
        }
        
        .view-btn {
            background: #1a2a6c;
            color: white;
        }
        
        .remove-btn {
            background: #c92a2a;
            color: white;
        }
        
        .admin-logo {
            position: absolute;
            top: 15px;
            right: 15px;
            background: #1a2a6c;
            color: white;
            padding: 5px 10px;
            border-radius: 4px;
            font-size: 0.9rem;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1><i class="fas fa-file-contract"></i> Sistema de Gestión de Créditos</h1>
            <p class="subtitle">Global Pacific SAS - V.1 2023</p>
            <button id="adminButton" class="btn btn-secondary" style="margin-top: 20px;">
                <i class="fas fa-lock"></i> Acceso Administración
            </button>
            
            <div id="adminLogo" class="admin-logo" style="display: none;">
                <i class="fas fa-user-shield"></i> Modo Administrador
            </div>
        </header>
        
        <!-- Formulario principal -->
        <div id="formContainer" class="form-container">
            <div class="form-header">
                <i class="fas fa-user-edit"></i>
                <span>1. IDENTIFICACIÓN DEL CLIENTE</span>
            </div>
            
            <div class="form-body">
                <div class="form-section">
                    <div class="form-row">
                        <div class="form-group">
                            <label for="fullName"><i class="fas fa-user"></i> NOMBRE COMPLETO Y/O RAZON SOCIAL:</label>
                            <input type="text" id="fullName" placeholder="Ingrese nombre completo o razón social" required>
                        </div>
                        
                        <div class="form-group">
                            <label for="idType"><i class="fas fa-id-card"></i> IDENTIFICACIÓN:</label>
                            <div style="display: flex; gap: 10px;">
                                <select id="idType" style="flex: 1;" required>
                                    <option value="">Tipo</option>
                                    <option value="C.C">C.C</option>
                                    <option value="NIT">NIT</option>
                                </select>
                                <input type="text" id="idNumber" placeholder="Número" style="flex: 2;" required>
                            </div>
                        </div>
                    </div>
                    
                    <div class="form-row">
                        <div class="form-group">
                            <label for="address"><i class="fas fa-map-marker-alt"></i> DIRECCIÓN:</label>
                            <input type="text" id="address" placeholder="Ingrese dirección completa" required>
                        </div>
                        
                        <div class="form-group">
                            <label for="city"><i class="fas fa-city"></i> CIUDAD:</label>
                            <input type="text" id="city" placeholder="Ciudad" required>
                        </div>
                        
                        <div class="form-group">
                            <label for="department"><i class="fas fa-globe-americas"></i> DEPARTAMENTO:</label>
                            <input type="text" id="department" placeholder="Departamento" required>
                        </div>
                    </div>
                    
                    <div class="form-row">
                        <div class="form-group">
                            <label for="phone"><i class="fas fa-phone"></i> TELÉFONO (PRINCIPAL):</label>
                            <input type="tel" id="phone" placeholder="Teléfono principal" required>
                        </div>
                        
                        <div class="form-group">
                            <label for="email"><i class="fas fa-envelope"></i> EMAIL:</label>
                            <input type="email" id="email" placeholder="Correo electrónico" required>
                        </div>
                        
                        <div class="form-group">
                            <label for="mobile"><i class="fas fa-mobile-alt"></i> CELULAR:</label>
                            <input type="tel" id="mobile" placeholder="Número de celular" required>
                        </div>
                    </div>
                    
                    <div class="form-row">
                        <div class="form-group">
                            <label for="legalNature"><i class="fas fa-balance-scale"></i> NATURALEZA JURÍDICA:</label>
                            <select id="legalNature" required>
                                <option value="">Seleccione una opción</option>
                                <option value="juridica">Persona Jurídica</option>
                                <option value="natural">Persona Natural</option>
                            </select>
                        </div>
                    </div>
                </div>
                
                <div class="section-title">
                    <i class="fas fa-user-tie"></i>
                    <span>TIPO DE PERSONA</span>
                </div>
                
                <div class="person-type">
                    <div class="person-card selected" id="juridicaCard" onclick="selectPersonType('juridica')">
                        <h3><i class="fas fa-building"></i> Persona Jurídica</h3>
                        <p>Seleccione esta opción si representa una empresa u organización.</p>
                        <ul class="document-list">
                            <li>Solicitud de Actualización de Crédito</li>
                            <li>Estados financieros</li>
                            <li>Declaración de renta</li>
                            <li>Fotocopia CC representante</li>
                            <li>RUT y Cámara de Comercio</li>
                            <li>Referencias comerciales</li>
                        </ul>
                    </div>
                    
                    <div class="person-card" id="naturalCard" onclick="selectPersonType('natural')">
                        <h3><i class="fas fa-user"></i> Persona Natural</h3>
                        <p>Seleccione esta opción si es una persona individual.</p>
                        <ul class="document-list">
                            <li>Solicitud de Actualización de Crédito</li>
                            <li>Pagaré firmado</li>
                            <li>Declaración de renta</li>
                            <li>RUT y Cámara de Comercio</li>
                            <li>Fotocopia CC y extractos</li>
                            <li>Referencias comerciales</li>
                        </ul>
                    </div>
                </div>
                
                <div class="section-title">
                    <i class="fas fa-file-contract"></i>
                    <span>9. DOCUMENTOS REQUERIDOS</span>
                </div>
                
                <div class="progress-container">
                    <div class="progress-bar" id="progressBar"></div>
                </div>
                <div style="text-align: center; margin-bottom: 15px; font-weight: 500;">
                    <span id="progressText">0% completado</span>
                </div>
                
                <div class="documents-section">
                    <table class="document-table">
                        <thead>
                            <tr>
                                <th>DOCUMENTO REQUERIDO</th>
                                <th>ARCHIVO</th>
                                <th>ESTADO</th>
                                <th>ACCIÓN</th>
                            </tr>
                        </thead>
                        <tbody id="documentsBody">
                            <!-- Documentos se cargarán dinámicamente -->
                        </tbody>
                    </table>
                </div>
                
                <div class="action-buttons">
                    <button class="btn btn-primary" onclick="saveForm()">
                        <i class="fas fa-save"></i> Guardar Todo
                    </button>
                    <button class="btn btn-success" onclick="validateDocuments()">
                        <i class="fas fa-check-circle"></i> Validar Documentos
                    </button>
                    <button class="btn btn-danger" onclick="clearForm()">
                        <i class="fas fa-trash-alt"></i> Limpiar Formulario
                    </button>
                </div>
            </div>
        </div>
        
        <!-- Panel de administración -->
        <div id="adminPanel" class="admin-panel">
            <div class="admin-header">
                <h2><i class="fas fa-tachometer-alt"></i> Panel de Administración</h2>
                <a href="#" class="back-button" id="backButton"><i class="fas fa-arrow-left"></i> Volver al formulario</a>
            </div>
            
            <div class="admin-actions">
                <button class="btn btn-primary" onclick="loadSubmissions()">
                    <i class="fas fa-sync-alt"></i> Actualizar
                </button>
                <button class="btn btn-success" onclick="exportToExcel()">
                    <i class="fas fa-file-excel"></i> Exportar a Excel
                </button>
                <button class="btn btn-info" onclick="openCredentialsModal()">
                    <i class="fas fa-user-cog"></i> Cambiar Credenciales
                </button>
                <button class="btn btn-warning" onclick="logout()">
                    <i class="fas fa-sign-out-alt"></i> Cerrar Sesión
                </button>
            </div>
            
            <div class="tab-container">
                <div class="tabs">
                    <div class="tab active" onclick="openTab('dashboard')">Dashboard</div>
                    <div class="tab" onclick="openTab('solicitudes')">Solicitudes</div>
                    <div class="tab" onclick="openTab('reportes')">Reportes</div>
                    <div class="tab" onclick="openTab('invitaciones')">Enlaces</div>
                </div>
                
                <div id="dashboard" class="tab-content active">
                    <div class="stats-container">
                        <div class="stat-card">
                            <h3>Solicitudes Totales</h3>
                            <div class="stat-value" id="totalRequests">0</div>
                            <div class="stat-label">Registradas en el sistema</div>
                        </div>
                        <div class="stat-card">
                            <h3>Completas</h3>
                            <div class="stat-value" id="completeRequests">0</div>
                            <div class="stat-label">Documentación completa</div>
                        </div>
                        <div class="stat-card">
                            <h3>Pendientes</h3>
                            <div class="stat-value" id="pendingRequests">0</div>
                            <div class="stat-label">Documentación incompleta</div>
                        </div>
                        <div class="stat-card">
                            <h3>Personas Naturales</h3>
                            <div class="stat-value" id="naturalRequests">0</div>
                            <div class="stat-label">Solicitudes de personas naturales</div>
                        </div>
                    </div>
                    
                    <h3 style="margin: 20px 0 15px; color: #1a2a6c;">Últimas Solicitudes</h3>
                    <table class="submissions-table">
                        <thead>
                            <tr>
                                <th>Fecha</th>
                                <th>Nombre</th>
                                <th>Identificación</th>
                                <th>Tipo</th>
                                <th>Documentos</th>
                                <th>Estado</th>
                            </tr>
                        </thead>
                        <tbody id="recentSubmissions">
                            <!-- Últimas solicitudes se cargarán aquí -->
                        </tbody>
                    </table>
                </div>
                
                <div id="solicitudes" class="tab-content">
                    <div style="margin: 20px 0; display: flex; gap: 15px; flex-wrap: wrap;">
                        <input type="text" id="searchInput" placeholder="Buscar por nombre o identificación" style="flex: 1; min-width: 250px; padding: 10px;">
                        <button class="btn btn-primary" onclick="searchSubmissions()">
                            <i class="fas fa-search"></i> Buscar
                        </button>
                    </div>
                    
                    <table class="submissions-table">
                        <thead>
                            <tr>
                                <th>Fecha</th>
                                <th>Nombre</th>
                                <th>Identificación</th>
                                <th>Tipo</th>
                                <th>Documentos</th>
                                <th>Estado</th>
                                <th>Acciones</th>
                            </tr>
                        </thead>
                        <tbody id="submissionsTableBody">
                            <!-- Las solicitudes se cargarán aquí -->
                        </tbody>
                    </table>
                </div>
                
                <div id="reportes" class="tab-content">
                    <h3 style="margin: 20px 0 15px; color: #1a2a6c;">Reportes y Estadísticas</h3>
                    
                    <div class="form-row">
                        <div class="form-group">
                            <label for="startDate">Fecha Inicio:</label>
                            <input type="date" id="startDate">
                        </div>
                        <div class="form-group">
                            <label for="endDate">Fecha Fin:</label>
                            <input type="date" id="endDate">
                        </div>
                        <div class="form-group">
                            <label for="reportType">Tipo de Reporte:</label>
                            <select id="reportType">
                                <option value="all">Todos los registros</option>
                                <option value="complete">Documentación completa</option>
                                <option value="incomplete">Documentación incompleta</option>
                                <option value="natural">Personas naturales</option>
                                <option value="juridica">Personas jurídicas</option>
                            </select>
                        </div>
                    </div>
                    
                    <div style="text-align: center; margin: 20px 0;">
                        <button class="btn btn-success" onclick="generateReport()">
                            <i class="fas fa-chart-bar"></i> Generar Reporte
                        </button>
                        <button class="btn btn-primary" onclick="exportReport()">
                            <i class="fas fa-download"></i> Exportar Reporte
                        </button>
                    </div>
                    
                    <div id="reportResults" style="margin-top: 20px;">
                        <!-- Resultados del reporte se mostrarán aquí -->
                    </div>
                </div>
                
                <!-- Nueva pestaña para generación de enlaces -->
                <div id="invitaciones" class="tab-content">
                    <div class="link-form">
                        <h3><i class="fas fa-user-plus"></i> Generar Enlace Personalizado</h3>
                        <p>Cree un enlace personalizado para compartir con sus clientes. Al abrirlo, el formulario se pre-llenará con los datos del cliente.</p>
                        
                        <div class="form-row">
                            <div class="form-group">
                                <label for="clientName"><i class="fas fa-user"></i> Nombre del Cliente:</label>
                                <input type="text" id="clientName" placeholder="Ingrese nombre completo del cliente" required>
                            </div>
                            
                            <div class="form-group">
                                <label for="clientId"><i class="fas fa-id-card"></i> Identificación:</label>
                                <input type="text" id="clientId" placeholder="Número de identificación" required>
                            </div>
                        </div>
                        
                        <div class="form-row">
                            <div class="form-group">
                                <label for="clientEmail"><i class="fas fa-envelope"></i> Email (opcional):</label>
                                <input type="email" id="clientEmail" placeholder="Correo electrónico del cliente">
                            </div>
                            
                            <div class="form-group">
                                <label for="clientType"><i class="fas fa-users"></i> Tipo de Persona:</label>
                                <select id="clientType">
                                    <option value="juridica">Persona Jurídica</option>
                                    <option value="natural">Persona Natural</option>
                                </select>
                            </div>
                        </div>
                        
                        <button class="btn btn-success" onclick="generateClientLink()" style="width: 100%;">
                            <i class="fas fa-link"></i> Generar Enlace Personalizado
                        </button>
                        
                        <div id="generatedLink" class="generated-link" style="display: none;">
                            <h4><i class="fas fa-check-circle" style="color: #2b8a3e;"></i> Enlace Generado</h4>
                            <a id="clientSpecificLink" href="#" target="_blank"></a>
                            
                            <div class="qr-container" id="qrCodeContainer"></div>
                            
                            <div class="link-actions">
                                <button class="btn btn-info" onclick="copySpecificLink()">
                                    <i class="fas fa-copy"></i> Copiar Enlace
                                </button>
                                <button class="btn btn-primary" onclick="emailClientLink()">
                                    <i class="fas fa-envelope"></i> Enviar por Email
                                </button>
                            </div>
                        </div>
                    </div>
                    
                    <div class="client-list">
                        <h3><i class="fas fa-users"></i> Clientes con Enlaces Generados</h3>
                        <div id="clientLinksList">
                            <!-- Lista de clientes con enlaces generados -->
                        </div>
                    </div>
                    
                    <div class="link-form" style="margin-top: 30px;">
                        <h3><i class="fas fa-share-alt"></i> Instrucciones para Compartir</h3>
                        <ol style="margin-left: 20px; padding: 15px 0;">
                            <li style="margin-bottom: 10px;"><strong>Genera el enlace:</strong> Completa los datos del cliente y haz clic en "Generar Enlace Personalizado".</li>
                            <li style="margin-bottom: 10px;"><strong>Copia el enlace:</strong> Haz clic en "Copiar Enlace" o utiliza el código QR para compartirlo fácilmente.</li>
                            <li style="margin-bottom: 10px;"><strong>Comparte con el cliente:</strong> Envía el enlace por email, WhatsApp, SMS o cualquier otro medio.</li>
                            <li style="margin-bottom: 10px;"><strong>El cliente completa el formulario:</strong> Al abrir el enlace, los datos estarán pre-llenados y sólo deberá subir los documentos requeridos.</li>
                            <li><strong>Recibe la solicitud:</strong> Las solicitudes completadas aparecerán en el panel de administración.</li>
                        </ol>
                    </div>
                </div>
            </div>
            
            <!-- Sección para cambiar credenciales -->
            <div class="credentials-form">
                <h3><i class="fas fa-key"></i> Gestión de Credenciales</h3>
                <div class="form-row">
                    <div class="form-group">
                        <label>Usuario actual: <span id="currentUser">admin</span></label>
                    </div>
                </div>
                <div class="form-row">
                    <div class="form-group">
                        <button class="btn btn-info" onclick="openCredentialsModal()">
                            <i class="fas fa-edit"></i> Cambiar Usuario y Contraseña
                        </button>
                    </div>
                </div>
            </div>
        </div>
        
        <footer>
            <p>Global Pacific SAS &copy; 2023 | Cra 42 nro 50a-40, Itagui, Colombia</p>
            <p>Tel: (604) 123 4567 | Email: contabilidad@globalpacificsas.com</p>
        </footer>
    </div>
    
    <!-- Modal para detalles de solicitud -->
    <div class="modal" id="detailsModal">
        <div class="modal-content">
            <span class="close-modal" onclick="closeModal()">&times;</span>
            <div id="modalContent"></div>
        </div>
    </div>
    
    <!-- Modal para cambiar credenciales -->
    <div class="modal" id="credentialsModal">
        <div class="modal-content">
            <span class="close-modal" onclick="closeCredentialsModal()">&times;</span>
            <h3 style="color: #1a2a6c; margin-bottom: 20px; text-align: center;">
                <i class="fas fa-user-cog"></i> Cambiar Credenciales
            </h3>
            
            <div class="form-group">
                <label for="currentUsername">Usuario Actual:</label>
                <input type="text" id="currentUsername" placeholder="Usuario actual" required>
            </div>
            
            <div class="form-group">
                <label for="currentPassword">Contraseña Actual:</label>
                <input type="password" id="currentPassword" placeholder="Contraseña actual" required>
            </div>
            
            <div class="form-group">
                <label for="newUsername">Nuevo Usuario:</label>
                <input type="text" id="newUsername" placeholder="Nuevo usuario" required>
            </div>
            
            <div class="form-group">
                <label for="newPassword">Nueva Contraseña:</label>
                <input type="password" id="newPassword" placeholder="Nueva contraseña" required>
            </div>
            
            <div class="form-group">
                <label for="confirmPassword">Confirmar Contraseña:</label>
                <input type="password" id="confirmPassword" placeholder="Confirmar contraseña" required>
            </div>
            
            <div class="action-buttons">
                <button class="btn btn-success" onclick="changeCredentials()">
                    <i class="fas fa-save"></i> Guardar Cambios
                </button>
                <button class="btn btn-danger" onclick="closeCredentialsModal()">
                    <i class="fas fa-times"></i> Cancelar
                </button>
            </div>
        </div>
    </div>
    
    <!-- Panel de login -->
    <div id="loginPanel" class="login-container" style="display: none;">
        <h2><i class="fas fa-lock"></i> Acceso Administrativo</h2>
        <input type="text" id="username" placeholder="Usuario" required>
        <input type="password" id="password" placeholder="Contraseña" required>
        <button class="btn btn-primary" onclick="login()">
            <i class="fas fa-sign-in-alt"></i> Iniciar Sesión
        </button>
    </div>
    
    <div class="notification" id="notification">
        Mensaje de notificación
    </div>

    <script>
        // Datos para documentos requeridos
        const documentosRequeridos = {
            juridica: [
                "Solicitud-Actualización de crédito (Diligenciada y firmada)",
                "Estados financieros dos años más recientes",
                "Última declaración de renta año más reciente",
                "Fotocopia CC representante legal",
                "RUT",
                "Cámara de comercio no mayor a 3 meses",
                "2 referencias comerciales (crédito vigente)"
            ],
            natural: [
                "Solicitud-Actualización de crédito (Diligenciada y firmada)",
                "Pagaré firmado",
                "Última declaración de renta más reciente",
                "RUT",
                "Cámara de comercio no mayor a 3 meses",
                "Fotocopia CC y extractos del último trimestre",
                "2 referencias comerciales (crédito vigente)"
            ]
        };
        
        // Tipo de persona seleccionado
        let tipoPersona = "juridica";
        let documentosSubidos = {};
        let isAdmin = false;
        
        // Credenciales de administrador
        let adminCredentials = {
            username: "admin",
            password: "admin123"
        };
        
        // Cargar credenciales guardadas si existen
        const savedCredentials = localStorage.getItem('adminCredentials');
        if (savedCredentials) {
            adminCredentials = JSON.parse(savedCredentials);
        }
        
        // Inicializar el formulario
        document.addEventListener('DOMContentLoaded', function() {
            cargarDocumentos();
            document.getElementById('legalNature').addEventListener('change', function() {
                if (this.value === 'natural') {
                    selectPersonType('natural');
                } else if (this.value === 'juridica') {
                    selectPersonType('juridica');
                }
            });
            
            // Eventos para administración
            document.getElementById('adminButton').addEventListener('click', function() {
                if (isAdmin) {
                    showAdminPanel();
                } else {
                    showLogin();
                }
            });
            
            document.getElementById('backButton').addEventListener('click', function(e) {
                e.preventDefault();
                hideAdminPanel();
            });
            
            // Inicializar fechas para reportes
            const today = new Date();
            document.getElementById('startDate').value = new Date(today.getFullYear(), today.getMonth(), 1).toISOString().split('T')[0];
            document.getElementById('endDate').value = today.toISOString().split('T')[0];
            
            // Mostrar usuario actual
            document.getElementById('currentUser').textContent = adminCredentials.username;
            
            // Cargar datos de cliente desde URL si existen
            loadClientDataFromUrl();
            
            // Cargar lista de clientes con enlaces
            updateClientLinksList();
        });
        
        // Cargar datos del cliente desde parámetros URL
        function loadClientDataFromUrl() {
            const urlParams = new URLSearchParams(window.location.search);
            const clientName = urlParams.get('name');
            const clientId = urlParams.get('id');
            const clientType = urlParams.get('type');
            const clientEmail = urlParams.get('email');
            
            if (clientName && clientId) {
                document.getElementById('fullName').value = decodeURIComponent(clientName);
                document.getElementById('idNumber').value = decodeURIComponent(clientId);
                
                if (clientEmail) {
                    document.getElementById('email').value = decodeURIComponent(clientEmail);
                }
                
                if (clientType) {
                    selectPersonType(clientType);
                    document.getElementById('legalNature').value = clientType;
                }
                
                showNotification(`Bienvenido ${decodeURIComponent(clientName)}! Sus datos se han cargado automáticamente.`, 'success');
            }
        }
        
        // Mostrar panel de login
        function showLogin() {
            document.getElementById('formContainer').style.display = 'none';
            document.getElementById('adminPanel').style.display = 'none';
            document.getElementById('loginPanel').style.display = 'block';
            document.getElementById('username').value = '';
            document.getElementById('password').value = '';
        }
        
        // Iniciar sesión
        function login() {
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            
            if (username === adminCredentials.username && password === adminCredentials.password) {
                isAdmin = true;
                document.getElementById('adminLogo').style.display = 'block';
                showAdminPanel();
                document.getElementById('loginPanel').style.display = 'none';
                showNotification('Sesión iniciada correctamente', 'success');
            } else {
                showNotification('Credenciales incorrectas', 'error');
            }
        }
        
        // Cerrar sesión
        function logout() {
            isAdmin = false;
            document.getElementById('adminLogo').style.display = 'none';
            showLogin();
            showNotification('Sesión cerrada correctamente', 'success');
        }
        
        // Mostrar panel de administración
        function showAdminPanel() {
            if (!isAdmin) {
                showLogin();
                return;
            }
            document.getElementById('formContainer').style.display = 'none';
            document.getElementById('adminPanel').style.display = 'block';
            document.getElementById('loginPanel').style.display = 'none';
            loadSubmissions();
            updateDashboardStats();
        }
        
        // Ocultar panel de administración
        function hideAdminPanel() {
            document.getElementById('formContainer').style.display = 'block';
            document.getElementById('adminPanel').style.display = 'none';
        }
        
        // Abrir modal para cambiar credenciales
        function openCredentialsModal() {
            document.getElementById('currentUsername').value = adminCredentials.username;
            document.getElementById('credentialsModal').style.display = 'flex';
        }
        
        // Cerrar modal de credenciales
        function closeCredentialsModal() {
            document.getElementById('credentialsModal').style.display = 'none';
            document.getElementById('currentUsername').value = '';
            document.getElementById('currentPassword').value = '';
            document.getElementById('newUsername').value = '';
            document.getElementById('newPassword').value = '';
            document.getElementById('confirmPassword').value = '';
        }
        
        // Función para seleccionar tipo de persona
        function selectPersonType(tipo) {
            tipoPersona = tipo;
            document.getElementById('juridicaCard').classList.toggle('selected', tipo === 'juridica');
            document.getElementById('naturalCard').classList.toggle('selected', tipo === 'natural');
            document.getElementById('legalNature').value = tipo;
            cargarDocumentos();
        }
        
        // Función para cargar documentos
        function cargarDocumentos() {
            const documentos = documentosRequeridos[tipoPersona];
            const tbody = document.getElementById('documentsBody');
            tbody.innerHTML = '';
            
            documentos.forEach((documento, index) => {
                const tr = document.createElement('tr');
                
                // Celda de documento
                const tdDocumento = document.createElement('td');
                tdDocumento.textContent = documento;
                tr.appendChild(tdDocumento);
                
                // Celda de archivo
                const tdArchivo = document.createElement('td');
                const fileContainer = document.createElement('div');
                fileContainer.className = 'file-upload';
                
                // Verificar si ya está subido
                if (documentosSubidos[documento]) {
                    fileContainer.innerHTML = `
                        <div class="file-info">
                            <i class="fas fa-file-pdf" style="color: #e74c3c; font-size: 1.5rem;"></i>
                            <div>
                                <div style="font-weight: 500;">${documentosSubidos[documento].name}</div>
                                <div style="font-size: 0.85rem; color: #495057;">${formatBytes(documentosSubidos[documento].size)}</div>
                            </div>
                        </div>
                    `;
                } else {
                    fileContainer.innerHTML = `
                        <button class="btn btn-secondary">
                            <i class="fas fa-upload"></i> Seleccionar Archivo
                        </button>
                        <input type="file" id="doc-${index}" data-doc="${documento}" onchange="documentUploaded(this, '${documento}')">
                    `;
                }
                
                tdArchivo.appendChild(fileContainer);
                tr.appendChild(tdArchivo);
                
                // Celda de estado
                const tdEstado = document.createElement('td');
                if (documentosSubidos[documento]) {
                    tdEstado.innerHTML = '<span class="document-status status-complete">ADJUNTADO</span>';
                } else {
                    tdEstado.innerHTML = '<span class="document-status status-pending">PENDIENTE</span>';
                }
                tr.appendChild(tdEstado);
                
                // Celda de acción
                const tdAccion = document.createElement('td');
                if (documentosSubidos[documento]) {
                    tdAccion.innerHTML = `
                        <div class="document-actions">
                            <button class="action-btn view-btn" onclick="viewDocument('${documento}')">
                                <i class="fas fa-eye"></i>
                            </button>
                            <button class="action-btn remove-btn" onclick="removeDocument('${documento}')">
                                <i class="fas fa-trash"></i>
                            </button>
                        </div>
                    `;
                } else {
                    tdAccion.innerHTML = '-';
                }
                tr.appendChild(tdAccion);
                
                tbody.appendChild(tr);
            });
            
            actualizarProgreso();
        }
        
        // Función para manejar la subida de documentos
        function documentUploaded(input, documento) {
            if (input.files.length > 0) {
                const file = input.files[0];
                documentosSubidos[documento] = {
                    name: file.name,
                    size: file.size,
                    type: file.type,
                    file: file
                };
                cargarDocumentos();
                showNotification(`"${file.name}" se ha adjuntado correctamente`, 'success');
            }
        }
        
        // Función para eliminar documento
        function removeDocument(documento) {
            delete documentosSubidos[documento];
            cargarDocumentos();
            showNotification(`Documento "${documento}" eliminado`, 'error');
        }
        
        // Función para ver documento
        function viewDocument(documento) {
            const file = documentosSubidos[documento].file;
            const fileURL = URL.createObjectURL(file);
            
            // Abrir en nueva pestaña para visualización
            window.open(fileURL, '_blank');
        }
        
        // Función para actualizar progreso
        function actualizarProgreso() {
            const documentos = documentosRequeridos[tipoPersona];
            const total = documentos.length;
            const completados = documentos.filter(doc => documentosSubidos[doc]).length;
            const porcentaje = Math.round((completados / total) * 100);
            
            document.getElementById('progressBar').style.width = `${porcentaje}%`;
            document.getElementById('progressText').textContent = `${porcentaje}% completado (${completados}/${total} documentos)`;
        }
        
        // Función para validar documentos
        function validateDocuments() {
            const documentos = documentosRequeridos[tipoPersona];
            const total = documentos.length;
            const completados = documentos.filter(doc => documentosSubidos[doc]).length;
            
            if (completados === total) {
                showNotification('¡Todos los documentos requeridos han sido adjuntados correctamente!', 'success');
            } else {
                showNotification(`Aún faltan ${total - completados} documentos por adjuntar. Por favor, complete todos los documentos requeridos.`, 'error');
            }
        }
        
        // Función para guardar el formulario
        function saveForm() {
            // Validar campos básicos
            const nombre = document.getElementById('fullName').value;
            const id = document.getElementById('idNumber').value;
            const idType = document.getElementById('idType').value;
            
            if (!nombre || !id || !idType) {
                showNotification('Por favor complete los campos de identificación antes de guardar', 'error');
                return;
            }
            
            // Validar documentos
            const documentos = documentosRequeridos[tipoPersona];
            const total = documentos.length;
            const completados = documentos.filter(doc => documentosSubidos[doc]).length;
            
            if (completados < total) {
                showNotification(`Aún faltan ${total - completados} documentos por adjuntar. No se puede guardar.`, 'error');
                return;
            }
            
            // Recopilar datos del formulario
            const formData = {
                fullName: nombre,
                idType: idType,
                idNumber: id,
                address: document.getElementById('address').value,
                city: document.getElementById('city').value,
                department: document.getElementById('department').value,
                phone: document.getElementById('phone').value,
                email: document.getElementById('email').value,
                mobile: document.getElementById('mobile').value,
                legalNature: tipoPersona,
                documents: {},
                timestamp: new Date().toISOString(),
                status: completados === total ? 'Completa' : 'Incompleta'
            };
            
            // Convertir archivos a base64 para almacenamiento
            Object.entries(documentosSubidos).forEach(([docName, docInfo]) => {
                formData.documents[docName] = {
                    name: docInfo.name,
                    size: docInfo.size,
                    type: docInfo.type
                };
            });
            
            // Guardar en localStorage
            const submissions = JSON.parse(localStorage.getItem('submissions')) || [];
            submissions.push(formData);
            localStorage.setItem('submissions', JSON.stringify(submissions));
            
            showNotification('Formulario guardado exitosamente. Los documentos han sido enviados para revisión.', 'success');
            clearForm(true);
        }
        
        // Función para limpiar el formulario
        function clearForm(force = false) {
            if (force || confirm('¿Está seguro de que desea limpiar todo el formulario? Se perderán todos los datos ingresados.')) {
                document.getElementById('fullName').value = '';
                document.getElementById('idType').value = '';
                document.getElementById('idNumber').value = '';
                document.getElementById('address').value = '';
                document.getElementById('city').value = '';
                document.getElementById('department').value = '';
                document.getElementById('phone').value = '';
                document.getElementById('email').value = '';
                document.getElementById('mobile').value = '';
                document.getElementById('legalNature').value = '';
                documentosSubidos = {};
                cargarDocumentos();
                tipoPersona = "juridica";
                document.getElementById('juridicaCard').classList.add('selected');
                document.getElementById('naturalCard').classList.remove('selected');
                
                if (!force) {
                    showNotification('Formulario limpiado exitosamente', 'success');
                }
            }
        }
        
        // Función para abrir pestañas
        function openTab(tabName) {
            document.querySelectorAll('.tab-content').forEach(tab => tab.classList.remove('active'));
            document.querySelectorAll('.tab').forEach(tab => tab.classList.remove('active'));
            document.getElementById(tabName).classList.add('active');
            document.querySelectorAll('.tab').forEach(tab => {
                if (tab.textContent === 'Dashboard' && tabName === 'dashboard') tab.classList.add('active');
                else if (tab.textContent === 'Solicitudes' && tabName === 'solicitudes') tab.classList.add('active');
                else if (tab.textContent === 'Reportes' && tabName === 'reportes') tab.classList.add('active');
                else if (tab.textContent === 'Enlaces' && tabName === 'invitaciones') tab.classList.add('active');
            });
        }
        
        // Cargar solicitudes en el panel de administración
        function loadSubmissions() {
            const submissions = JSON.parse(localStorage.getItem('submissions')) || [];
            const tableBody = document.getElementById('submissionsTableBody');
            tableBody.innerHTML = '';
            
            if (submissions.length === 0) {
                tableBody.innerHTML = '<tr><td colspan="7" style="text-align: center;">No hay solicitudes registradas</td></tr>';
                return;
            }
            
            submissions.forEach((sub, index) => {
                const tr = document.createElement('tr');
                tr.innerHTML = `
                    <td>${formatDate(sub.timestamp)}</td>
                    <td>${sub.fullName}</td>
                    <td>${sub.idType}: ${sub.idNumber}</td>
                    <td>${sub.legalNature === 'juridica' ? 'Jurídica' : 'Natural'}</td>
                    <td>${Object.keys(sub.documents).length}</td>
                    <td><span class="document-status ${sub.status === 'Completa' ? 'status-complete' : 'status-pending'}">${sub.status}</span></td>
                    <td>
                        <button class="btn btn-primary" onclick="viewSubmission(${index})">
                            <i class="fas fa-eye"></i> Ver
                        </button>
                        <button class="btn btn-danger" onclick="deleteSubmission(${index})">
                            <i class="fas fa-trash"></i> Eliminar
                        </button>
                    </td>
                `;
                tableBody.appendChild(tr);
            });
            
            updateDashboardStats();
        }
        
        // Función para formatear fecha
        function formatDate(dateString) {
            const date = new Date(dateString);
            return date.toLocaleDateString() + ' ' + date.toLocaleTimeString();
        }
        
        // Función para formatear tamaño de archivos
        function formatBytes(bytes, decimals = 2) {
            if (bytes === 0) return '0 Bytes';
            const k = 1024;
            const dm = decimals < 0 ? 0 : decimals;
            const sizes = ['Bytes', 'KB', 'MB', 'GB'];
            const i = Math.floor(Math.log(bytes) / Math.log(k));
            return parseFloat((bytes / Math.pow(k, i)).toFixed(dm)) + ' ' + sizes[i];
        }
        
        // Función para actualizar estadísticas
        function updateDashboardStats() {
            const submissions = JSON.parse(localStorage.getItem('submissions')) || [];
            document.getElementById('totalRequests').textContent = submissions.length;
            document.getElementById('completeRequests').textContent = submissions.filter(s => s.status === 'Completa').length;
            document.getElementById('pendingRequests').textContent = submissions.filter(s => s.status !== 'Completa').length;
            document.getElementById('naturalRequests').textContent = submissions.filter(s => s.legalNature === 'natural').length;
            
            const recentBody = document.getElementById('recentSubmissions');
            recentBody.innerHTML = '';
            const recentSubmissions = submissions.slice(-5).reverse();
            recentSubmissions.forEach(sub => {
                const tr = document.createElement('tr');
                tr.innerHTML = `
                    <td>${formatDate(sub.timestamp)}</td>
                    <td>${sub.fullName}</td>
                    <td>${sub.idType}: ${sub.idNumber}</td>
                    <td>${sub.legalNature === 'juridica' ? 'Jurídica' : 'Natural'}</td>
                    <td>${Object.keys(sub.documents).length}</td>
                    <td><span class="document-status ${sub.status === 'Completa' ? 'status-complete' : 'status-pending'}">${sub.status}</span></td>
                `;
                recentBody.appendChild(tr);
            });
        }
        
        // Función para ver detalles de solicitud
        function viewSubmission(index) {
            const submissions = JSON.parse(localStorage.getItem('submissions')) || [];
            const submission = submissions[index];
            let content = `
                <h3 style="color: #1a2a6c; margin-bottom: 20px; border-bottom: 2px solid #eaeaea; padding-bottom: 10px;">
                    Detalles de la Solicitud
                </h3>
                <div class="form-row">
                    <div class="form-group">
                        <label>Nombre:</label>
                        <p>${submission.fullName}</p>
                    </div>
                    <div class="form-group">
                        <label>Identificación:</label>
                        <p>${submission.idType}: ${submission.idNumber}</p>
                    </div>
                </div>
                <div class="form-row">
                    <div class="form-group">
                        <label>Tipo:</label>
                        <p>${submission.legalNature === 'juridica' ? 'Persona Jurídica' : 'Persona Natural'}</p>
                    </div>
                    <div class="form-group">
                        <label>Fecha de solicitud:</label>
                        <p>${formatDate(submission.timestamp)}</p>
                    </div>
                </div>
                <div class="form-row">
                    <div class="form-group">
                        <label>Dirección:</label>
                        <p>${submission.address}</p>
                    </div>
                    <div class="form-group">
                        <label>Ciudad:</label>
                        <p>${submission.city}</p>
                    </div>
                    <div class="form-group">
                        <label>Departamento:</label>
                        <p>${submission.department}</p>
                    </div>
                </div>
                <div class="form-row">
                    <div class="form-group">
                        <label>Teléfono:</label>
                        <p>${submission.phone}</p>
                    </div>
                    <div class="form-group">
                        <label>Email:</label>
                        <p>${submission.email}</p>
                    </div>
                    <div class="form-group">
                        <label>Celular:</label>
                        <p>${submission.mobile}</p>
                    </div>
                </div>
                <div class="form-row">
                    <div class="form-group">
                        <label>Estado:</label>
                        <p><span class="document-status ${submission.status === 'Completa' ? 'status-complete' : 'status-pending'}">${submission.status}</span></p>
                    </div>
                </div>
                <h4 style="margin-top: 20px; color: #1a2a6c; border-bottom: 1px solid #eaeaea; padding-bottom: 10px;">
                    Documentos Adjuntos
                </h4>
                <ul style="margin-left: 20px; margin-bottom: 20px;">
            `;
            
            Object.entries(submission.documents).forEach(([docName, docInfo]) => {
                content += `<li><strong>${docName}:</strong> ${docInfo.name} (${formatBytes(docInfo.size)})</li>`;
            });
            
            content += `</ul>`;
            
            // Botón para descargar todos los documentos
            content += `
                <div class="download-all-btn">
                    <button class="btn btn-success" onclick="downloadAllDocuments(${index})">
                        <i class="fas fa-download"></i> Descargar todos los documentos
                    </button>
                </div>
            `;
            
            document.getElementById('modalContent').innerHTML = content;
            document.getElementById('detailsModal').style.display = 'flex';
        }
        
        // Función para cerrar modal
        function closeModal() {
            document.getElementById('detailsModal').style.display = 'none';
        }
        
        // Función para eliminar solicitud
        function deleteSubmission(index) {
            if (confirm('¿Está seguro de eliminar esta solicitud?')) {
                const submissions = JSON.parse(localStorage.getItem('submissions')) || [];
                submissions.splice(index, 1);
                localStorage.setItem('submissions', JSON.stringify(submissions));
                loadSubmissions();
                updateDashboardStats();
                showNotification('Solicitud eliminada', 'success');
            }
        }
        
        // Función para buscar solicitudes
        function searchSubmissions() {
            const searchTerm = document.getElementById('searchInput').value.toLowerCase();
            const submissions = JSON.parse(localStorage.getItem('submissions')) || [];
            const tableBody = document.getElementById('submissionsTableBody');
            tableBody.innerHTML = '';
            
            if (submissions.length === 0) {
                tableBody.innerHTML = '<tr><td colspan="7" style="text-align: center;">No hay solicitudes registradas</td></tr>';
                return;
            }
            
            const filtered = submissions.filter(sub => 
                sub.fullName.toLowerCase().includes(searchTerm) || 
                sub.idNumber.toLowerCase().includes(searchTerm)
            );
            
            if (filtered.length === 0) {
                tableBody.innerHTML = '<tr><td colspan="7" style="text-align: center;">No se encontraron resultados</td></tr>';
                return;
            }
            
            filtered.forEach((sub, index) => {
                const tr = document.createElement('tr');
                tr.innerHTML = `
                    <td>${formatDate(sub.timestamp)}</td>
                    <td>${sub.fullName}</td>
                    <td>${sub.idType}: ${sub.idNumber}</td>
                    <td>${sub.legalNature === 'juridica' ? 'Jurídica' : 'Natural'}</td>
                    <td>${Object.keys(sub.documents).length}</td>
                    <td><span class="document-status ${sub.status === 'Completa' ? 'status-complete' : 'status-pending'}">${sub.status}</span></td>
                    <td>
                        <button class="btn btn-primary" onclick="viewSubmission(${submissions.indexOf(sub)})">
                            <i class="fas fa-eye"></i> Ver
                        </button>
                        <button class="btn btn-danger" onclick="deleteSubmission(${submissions.indexOf(sub)})">
                            <i class="fas fa-trash"></i> Eliminar
                        </button>
                    </td>
                `;
                tableBody.appendChild(tr);
            });
        }
        
        // Función para generar reportes
        function generateReport() {
            const startDate = document.getElementById('startDate').value;
            const endDate = document.getElementById('endDate').value;
            const reportType = document.getElementById('reportType').value;
            const submissions = JSON.parse(localStorage.getItem('submissions')) || [];
            let filtered = [...submissions];
            
            if (startDate && endDate) {
                filtered = filtered.filter(sub => {
                    const subDate = new Date(sub.timestamp).toISOString().split('T')[0];
                    return subDate >= startDate && subDate <= endDate;
                });
            }
            
            if (reportType === 'complete') filtered = filtered.filter(sub => sub.status === 'Completa');
            else if (reportType === 'incomplete') filtered = filtered.filter(sub => sub.status !== 'Completa');
            else if (reportType === 'natural') filtered = filtered.filter(sub => sub.legalNature === 'natural');
            else if (reportType === 'juridica') filtered = filtered.filter(sub => sub.legalNature === 'juridica');
            
            const resultsContainer = document.getElementById('reportResults');
            resultsContainer.innerHTML = '';
            
            if (filtered.length === 0) {
                resultsContainer.innerHTML = '<p style="text-align: center; padding: 20px;">No se encontraron resultados para los criterios seleccionados</p>';
                return;
            }
            
            let content = `
                <h4 style="color: #1a2a6c; margin-bottom: 15px;">Resultados del Reporte: ${filtered.length} solicitudes encontradas</h4>
                <div style="overflow-x: auto;">
                    <table class="submissions-table" style="font-size: 0.9rem;">
                        <thead>
                            <tr>
                                <th>Fecha</th>
                                <th>Nombre</th>
                                <th>Identificación</th>
                                <th>Tipo</th>
                                <th>Documentos</th>
                                <th>Estado</th>
                            </tr>
                        </thead>
                        <tbody>
            `;
            
            filtered.forEach(sub => {
                content += `
                    <tr>
                        <td>${formatDate(sub.timestamp)}</td>
                        <td>${sub.fullName}</td>
                        <td>${sub.idType}: ${sub.idNumber}</td>
                        <td>${sub.legalNature === 'juridica' ? 'Jurídica' : 'Natural'}</td>
                        <td>${Object.keys(sub.documents).length}</td>
                        <td><span class="document-status ${sub.status === 'Completa' ? 'status-complete' : 'status-pending'}">${sub.status}</span></td>
                    </tr>
                `;
            });
            
            content += `
                        </tbody>
                    </table>
                </div>
            `;
            
            resultsContainer.innerHTML = content;
        }
        
        // Función para descargar todos los documentos de una solicitud
        function downloadAllDocuments(index) {
            const submissions = JSON.parse(localStorage.getItem('submissions')) || [];
            const submission = submissions[index];
            const docs = submission.documents;
            
            if (!docs || Object.keys(docs).length === 0) {
                showNotification('No hay documentos para descargar', 'error');
                return;
            }
            
            // Crear un archivo ZIP con todos los documentos
            const zip = new JSZip();
            
            // Crear una carpeta para los documentos
            const folder = zip.folder(`documentos_${submission.fullName.replace(/[^a-z0-9]/gi, '_')}`);
            
            // Agregar cada documento al ZIP (en un sistema real, aquí se agregarían los archivos reales)
            Object.entries(docs).forEach(([docName, docInfo]) => {
                // Simulamos contenido del documento
                folder.file(docInfo.name, `Contenido del documento: ${docName}\nCliente: ${submission.fullName}\nFecha: ${new Date().toLocaleString()}`);
            });
            
            // Generar el archivo ZIP y descargarlo
            zip.generateAsync({type:"blob"}).then(function(content) {
                saveAs(content, `documentos_${submission.fullName.replace(/[^a-z0-9]/gi, '_')}.zip`);
                showNotification('Descarga iniciada', 'success');
            });
        }
        
        // Función para exportar todas las solicitudes a Excel
        function exportToExcel() {
            const submissions = JSON.parse(localStorage.getItem('submissions')) || [];
            if (submissions.length === 0) {
                showNotification('No hay datos para exportar', 'error');
                return;
            }
            
            // Preparar datos para la hoja de cálculo
            const data = submissions.map(sub => ({
                'Fecha': formatDate(sub.timestamp),
                'Nombre': sub.fullName,
                'Identificación': `${sub.idType}: ${sub.idNumber}`,
                'Tipo': sub.legalNature === 'juridica' ? 'Jurídica' : 'Natural',
                'Documentos': Object.keys(sub.documents).length,
                'Estado': sub.status,
                'Dirección': sub.address,
                'Ciudad': sub.city,
                'Departamento': sub.department,
                'Teléfono': sub.phone,
                'Email': sub.email,
                'Celular': sub.mobile
            }));
            
            // Crear libro de Excel
            const worksheet = XLSX.utils.json_to_sheet(data);
            const workbook = XLSX.utils.book_new();
            XLSX.utils.book_append_sheet(workbook, worksheet, "Solicitudes");
            
            // Generar archivo y descargar
            XLSX.writeFile(workbook, 'solicitudes_creditos.xlsx');
            showNotification('Exportación a Excel completada', 'success');
        }
        
        // Función para exportar el reporte actual a Excel
        function exportReport() {
            const startDate = document.getElementById('startDate').value;
            const endDate = document.getElementById('endDate').value;
            const reportType = document.getElementById('reportType').value;
            const submissions = JSON.parse(localStorage.getItem('submissions')) || [];
            let filtered = [...submissions];
            
            if (startDate && endDate) {
                filtered = filtered.filter(sub => {
                    const subDate = new Date(sub.timestamp).toISOString().split('T')[0];
                    return subDate >= startDate && subDate <= endDate;
                });
            }
            
            if (reportType === 'complete') filtered = filtered.filter(sub => sub.status === 'Completa');
            else if (reportType === 'incomplete') filtered = filtered.filter(sub => sub.status !== 'Completa');
            else if (reportType === 'natural') filtered = filtered.filter(sub => sub.legalNature === 'natural');
            else if (reportType === 'juridica') filtered = filtered.filter(sub => sub.legalNature === 'juridica');
            
            if (filtered.length === 0) {
                showNotification('No hay datos para exportar', 'error');
                return;
            }
            
            // Preparar datos para la hoja de cálculo
            const data = filtered.map(sub => ({
                'Fecha': formatDate(sub.timestamp),
                'Nombre': sub.fullName,
                'Identificación': `${sub.idType}: ${sub.idNumber}`,
                'Tipo': sub.legalNature === 'juridica' ? 'Jurídica' : 'Natural',
                'Documentos': Object.keys(sub.documents).length,
                'Estado': sub.status,
                'Dirección': sub.address,
                'Ciudad': sub.city,
                'Departamento': sub.department,
                'Teléfono': sub.phone,
                'Email': sub.email,
                'Celular': sub.mobile
            }));
            
            // Crear libro de Excel
            const worksheet = XLSX.utils.json_to_sheet(data);
            const workbook = XLSX.utils.book_new();
            XLSX.utils.book_append_sheet(workbook, worksheet, "Reporte");
            
            // Generar archivo y descargar
            XLSX.writeFile(workbook, `reporte_${new Date().toISOString().split('T')[0]}.xlsx`);
            showNotification('Reporte exportado a Excel', 'success');
        }
        
        // Función para mostrar notificaciones
        function showNotification(message, type) {
            const notification = document.getElementById('notification');
            notification.textContent = message;
            notification.className = `notification ${type} show`;
            
            setTimeout(() => {
                notification.classList.remove('show');
            }, 3000);
        }
        
        /* Funcionalidad para generar enlaces de cliente */
        
        // Generar enlace personalizado para cliente
        function generateClientLink() {
            const clientName = document.getElementById('clientName').value;
            const clientId = document.getElementById('clientId').value;
            const clientEmail = document.getElementById('clientEmail').value;
            const clientType = document.getElementById('clientType').value;
            
            if (!clientName || !clientId) {
                showNotification('Por favor complete el nombre y la identificación del cliente', 'error');
                return;
            }
            
            // Generar un ID único para este cliente
            const currentUrl = window.location.href.split('?')[0];
            const clientLink = `${currentUrl}?name=${encodeURIComponent(clientName)}&id=${encodeURIComponent(clientId)}&type=${clientType}&email=${encodeURIComponent(clientEmail || '')}`;
            
            // Mostrar el enlace generado
            document.getElementById('clientSpecificLink').textContent = clientLink;
            document.getElementById('clientSpecificLink').href = clientLink;
            document.getElementById('generatedLink').style.display = 'block';
            
            // Generar código QR
            const qrContainer = document.getElementById('qrCodeContainer');
            qrContainer.innerHTML = '';
            new QRCode(qrContainer, {
                text: clientLink,
                width: 150,
                height: 150
            });
            
            // Guardar enlace en localStorage
            saveClientLink(clientName, clientId, clientEmail, clientType, clientLink);
            
            showNotification(`Enlace generado para ${clientName}`, 'success');
        }
        
        // Guardar enlace generado en localStorage
        function saveClientLink(name, id, email, type, link) {
            const clientLinks = JSON.parse(localStorage.getItem('clientLinks')) || [];
            
            // Verificar si ya existe
            const existingIndex = clientLinks.findIndex(client => client.id === id);
            
            if (existingIndex !== -1) {
                // Actualizar existente
                clientLinks[existingIndex] = { name, id, email, type, link, date: new Date().toISOString() };
            } else {
                // Agregar nuevo
                clientLinks.push({
                    name,
                    id,
                    email,
                    type,
                    link,
                    date: new Date().toISOString()
                });
            }
            
            localStorage.setItem('clientLinks', JSON.stringify(clientLinks));
            
            // Actualizar lista de clientes
            updateClientLinksList();
        }
        
        // Actualizar lista de clientes con enlaces generados
        function updateClientLinksList() {
            const clientLinks = JSON.parse(localStorage.getItem('clientLinks')) || [];
            const clientList = document.getElementById('clientLinksList');
            
            if (clientLinks.length === 0) {
                clientList.innerHTML = '<div class="client-item"><p>No hay clientes registrados</p></div>';
                return;
            }
            
            clientList.innerHTML = '';
            
            clientLinks.forEach(client => {
                const clientItem = document.createElement('div');
                clientItem.className = 'client-item';
                clientItem.innerHTML = `
                    <div class="client-info">
                        <h4>${client.name}</h4>
                        <p><i class="fas fa-id-card"></i> ${client.id}</p>
                        ${client.email ? `<p><i class="fas fa-envelope"></i> ${client.email}</p>` : ''}
                        <p><i class="fas fa-users"></i> ${client.type === 'juridica' ? 'Persona Jurídica' : 'Persona Natural'}</p>
                    </div>
                    <div class="client-actions">
                        <button class="btn btn-primary" onclick="copyClientLink('${client.link}')">
                            <i class="fas fa-copy"></i>
                        </button>
                        <button class="btn btn-info" onclick="openClientLink('${client.link}')">
                            <i class="fas fa-eye"></i>
                        </button>
                    </div>
                `;
                clientList.appendChild(clientItem);
            });
        }
        
        // Copiar enlace específico
        function copySpecificLink() {
            const link = document.getElementById('clientSpecificLink').href;
            copyToClipboard(link);
            showNotification('Enlace copiado al portapapeles', 'success');
        }
        
        // Copiar cualquier enlace
        function copyClientLink(link) {
            copyToClipboard(link);
            showNotification('Enlace copiado al portapapeles', 'success');
        }
        
        // Función para copiar al portapapeles
        function copyToClipboard(text) {
            const textarea = document.createElement('textarea');
            textarea.value = text;
            document.body.appendChild(textarea);
            textarea.select();
            document.execCommand('copy');
            document.body.removeChild(textarea);
        }
        
        // Abrir enlace del cliente
        function openClientLink(link) {
            window.open(link, '_blank');
        }
        
        // Enviar enlace por email (simulado)
        function emailClientLink() {
            const clientName = document.getElementById('clientName').value;
            const clientEmail = document.getElementById('clientEmail').value;
            const link = document.getElementById('clientSpecificLink').href;
            
            if (!clientEmail) {
                showNotification('Por favor ingrese un email para enviar el enlace', 'error');
                return;
            }
            
            // Simulación de envío de email
            const emailBody = `Hola ${clientName},\n\nPuedes completar tu solicitud de crédito en el siguiente enlace:\n\n${link}\n\nSaludos,\nGlobal Pacific SAS`;
            
            // En un sistema real, aquí se enviaría el email
            // Simulamos la acción con una notificación
            showNotification(`Enlace enviado por email a ${clientEmail}`, 'success');
        }
        
        // Cambiar credenciales de administrador
        function changeCredentials() {
            const currentUsername = document.getElementById('currentUsername').value;
            const currentPassword = document.getElementById('currentPassword').value;
            const newUsername = document.getElementById('newUsername').value;
            const newPassword = document.getElementById('newPassword').value;
            const confirmPassword = document.getElementById('confirmPassword').value;
            
            // Validar credenciales actuales
            if (currentUsername !== adminCredentials.username || currentPassword !== adminCredentials.password) {
                showNotification('Credenciales actuales incorrectas', 'error');
                return;
            }
            
            // Validar nueva contraseña
            if (newPassword !== confirmPassword) {
                showNotification('Las nuevas contraseñas no coinciden', 'error');
                return;
            }
            
            // Actualizar credenciales
            adminCredentials.username = newUsername;
            adminCredentials.password = newPassword;
            
            // Guardar en localStorage
            localStorage.setItem('adminCredentials', JSON.stringify(adminCredentials));
            
            // Actualizar UI
            document.getElementById('currentUser').textContent = newUsername;
            
            showNotification('Credenciales actualizadas correctamente', 'success');
            closeCredentialsModal();
        }
    </script>
</body>
</html>
