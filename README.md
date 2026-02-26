<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>DSHS School System - Complete Version</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
<style>
  /*------ COLOR SCHEME ------*/
  :root {
    --main-red: #8B0000;
    --main-blue: #003366;
    --main-gray: #6c757d;
    --sub-yellow: #ffc107;
    --sub-orange: #fd7e14;
    --light-gray: #f8f9fa;
    --dark-gray: #495057;
    --success: #28a745;
    --danger: #dc3545;
    --warning: #ffc107;
    --info: #17a2b8;
    --bg-light: #f8f9fa;
    --bg-white: #ffffff;
    --text-dark: #212529;
    --text-muted: #6c757d;
    --border-color: #dee2e6;
    --shadow: 0 4px 15px rgba(0,0,0,0.1);
    --transition: all 0.3s ease;
  }

  [data-theme="dark"] {
    --bg-light: #1a1a2e;
    --bg-white: #16213e;
    --text-dark: #e4e4e4;
    --text-muted: #a0a0a0;
    --border-color: #2d3748;
    --shadow: 0 4px 15px rgba(0,0,0,0.3);
    --main-gray: #a0a0a0;
  }

  * { box-sizing: border-box; }

  body { 
    margin: 0; 
    min-height: 100vh; 
    background: linear-gradient(135deg, #1a1a2e 0%, #16213e 50%, #0f3460 100%);
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    color: var(--text-dark);
    transition: var(--transition);
  }

  [data-theme="dark"] body {
    background: linear-gradient(135deg, #0f0f1a 0%, #1a1a2e 50%, #16213e 100%);
  }

  .text-center { text-align: center; }
  .text-left { text-align: left; }
  .text-right { text-align: right; }
  .mt-1 { margin-top: 8px; }
  .mt-2 { margin-top: 16px; }
  .mt-3 { margin-top: 24px; }
  .mb-1 { margin-bottom: 8px; }
  .mb-2 { margin-bottom: 16px; }
  .mb-3 { margin-bottom: 24px; }
  .p-1 { padding: 8px; }
  .p-2 { padding: 16px; }
  .p-3 { padding: 24px; }
  .d-flex { display: flex; }
  .d-none { display: none; }
  .d-block { display: block; }
  .flex-wrap { flex-wrap: wrap; }
  .justify-between { justify-content: space-between; }
  .justify-center { justify-content: center; }
  .align-center { align-items: center; }
  .gap-1 { gap: 8px; }
  .gap-2 { gap: 16px; }
  .gap-3 { gap: 24px; }
  .w-100 { width: 100%; }
  .h-100 { height: 100%; }
  .rounded { border-radius: 8px; }
  .rounded-lg { border-radius: 12px; }
  .shadow { box-shadow: var(--shadow); }
  .border { border: 1px solid var(--border-color); }
  .bg-white { background: var(--bg-white); }
  .bg-light { background: var(--bg-light); }
  .text-muted { color: var(--text-muted); }
  .text-success { color: var(--success); }
  .text-danger { color: var(--danger); }
  .text-warning { color: var(--warning); }
  .text-info { color: var(--info); }
  .font-bold { font-weight: bold; }
  .font-sm { font-size: 12px; }
  .font-md { font-size: 14px; }
  .font-lg { font-size: 18px; }
  .font-xl { font-size: 24px; }
  .overflow-auto { overflow: auto; }
  .cursor-pointer { cursor: pointer; }

  .btn {
    padding: 10px 20px;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    font-size: 14px;
    font-weight: 600;
    transition: var(--transition);
    display: inline-flex;
    align-items: center;
    gap: 8px;
  }

  .btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(0,0,0,0.2);
  }

  .btn:active { transform: translateY(0); }

  .btn-primary {
    background: linear-gradient(135deg, var(--main-red) 0%, var(--main-blue) 100%);
    color: white;
  }

  .btn-success { background: var(--success); color: white; }
  .btn-danger { background: var(--danger); color: white; }
  .btn-warning { background: var(--warning); color: #000; }
  .btn-info { background: var(--info); color: white; }
  .btn-outline {
    background: transparent;
    border: 2px solid var(--main-blue);
    color: var(--main-blue);
  }

  .btn-sm { padding: 6px 12px; font-size: 12px; }
  .btn-lg { padding: 14px 28px; font-size: 16px; }
  .btn-block { width: 100%; justify-content: center; }
  .btn-icon { width: 40px; height: 40px; padding: 0; justify-content: center; }

  input, button, textarea, select { 
    width: 100%; 
    padding: 12px; 
    margin-top: 8px; 
    box-sizing: border-box; 
    font-size: 14px;
    border: 2px solid var(--border-color);
    border-radius: 6px;
    transition: var(--transition);
    background: var(--bg-white);
    color: var(--text-dark);
  }

  input:focus, textarea:focus, select:focus {
    border-color: var(--main-blue);
    outline: none;
    box-shadow: 0 0 0 3px rgba(0,51,102,0.1);
  }

  label {
    font-weight: 600;
    color: var(--text-dark);
    margin-bottom: 4px;
    display: block;
  }

  .form-group { margin-bottom: 16px; }

  .input-group { display: flex; gap: 8px; }

  .input-icon { position: relative; }

  .input-icon i {
    position: absolute;
    left: 12px;
    top: 50%;
    transform: translateY(-50%);
    color: var(--text-muted);
  }

  .input-icon input { padding-left: 36px; }

  .card {
    background: var(--bg-white);
    border-radius: 12px;
    box-shadow: var(--shadow);
    padding: 20px;
    margin-bottom: 20px;
    transition: var(--transition);
  }

  .card:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 25px rgba(0,0,0,0.15);
  }

  .card-header {
    font-size: 18px;
    font-weight: bold;
    color: var(--main-blue);
    padding-bottom: 12px;
    border-bottom: 2px solid var(--sub-yellow);
    margin-bottom: 16px;
    display: flex;
    align-items: center;
    gap: 10px;
  }

  table { 
    border-collapse: collapse; 
    width: 100%; 
    margin-top: 16px; 
    overflow-x: auto;
  }

  table, th, td { 
    border: 1px solid var(--border-color); 
    text-align: center; 
    padding: 12px; 
  }

  th { 
    background: linear-gradient(135deg, var(--main-red) 0%, var(--main-blue) 100%); 
    color: white; 
    font-weight: bold;
  }

  tr:nth-child(even) { background-color: var(--bg-light); }
  tr:hover { background-color: #e9ecef; }

  .loading-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0,0,0,0.7);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 9999;
    backdrop-filter: blur(5px);
  }

  .spinner {
    width: 50px;
    height: 50px;
    border: 5px solid rgba(255,255,255,0.3);
    border-top: 5px solid var(--sub-yellow);
    border-radius: 50%;
    animation: spin 1s linear infinite;
  }

  @keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
  }

  .toast-container {
    position: fixed;
    top: 80px;
    right: 20px;
    z-index: 10000;
    display: flex;
    flex-direction: column;
    gap: 10px;
  }

  .toast {
    padding: 16px 24px;
    border-radius: 8px;
    color: white;
    font-weight: 600;
    box-shadow: 0 4px 15px rgba(0,0,0,0.3);
    animation: slideIn 0.3s ease;
    display: flex;
    align-items: center;
    gap: 12px;
    min-width: 280px;
  }

  .toast-success { background: var(--success); }
  .toast-danger { background: var(--danger); }
  .toast-warning { background: var(--warning); color: #000; }
  .toast-info { background: var(--info); }

  @keyframes slideIn {
    from { transform: translateX(400px); opacity: 0; }
    to { transform: translateX(0); opacity: 1; }
  }

  .modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0,0,0,0.6);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 10001;
    backdrop-filter: blur(5px);
  }

  .modal {
    background: var(--bg-white);
    border-radius: 15px;
    padding: 25px;
    max-width: 500px;
    width: 90%;
    max-height: 90vh;
    overflow-y: auto;
    box-shadow: 0 15px 50px rgba(0,0,0,0.4);
    animation: modalIn 0.3s ease;
  }

  @keyframes modalIn {
    from { transform: scale(0.8); opacity: 0; }
    to { transform: scale(1); opacity: 1; }
  }

  .modal-header {
    font-size: 20px;
    font-weight: bold;
    color: var(--main-blue);
    margin-bottom: 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .modal-close {
    background: none;
    border: none;
    font-size: 24px;
    cursor: pointer;
    color: var(--text-muted);
    width: auto;
    padding: 0;
  }

  .modal-close:hover {
    color: var(--danger);
    transform: none;
    box-shadow: none;
  }

  .modal-footer {
    margin-top: 20px;
    display: flex;
    gap: 10px;
    justify-content: flex-end;
  }

  .toggle-btn { 
    background: linear-gradient(135deg, var(--main-red) 0%, var(--main-blue) 100%); 
    color: white; 
    font-size: 18px; 
    border: none; 
    position: fixed; 
    top: 12px; 
    left: 12px; 
    z-index: 1000; 
    padding: 12px 16px; 
    border-radius: 8px;
    cursor: pointer;
    display: flex;
    align-items: center;
    gap: 8px;
    box-shadow: 0 4px 15px rgba(0,0,0,0.3);
    transition: var(--transition);
  }

  .toggle-btn:hover { 
    background: linear-gradient(135deg, #660000 0%, #002244 100%);
    transform: scale(1.05);
  }

  .toggle-btn .icon { font-size: 22px; }
  .toggle-btn .text { display: none; white-space: nowrap; }
  .toggle-btn:hover .text { display: block; }

  .theme-toggle {
    position: fixed;
    top: 12px;
    right: 12px;
    z-index: 1000;
    background: var(--sub-yellow);
    border: none;
    border-radius: 8px;
    width: 45px;
    height: 45px;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 20px;
    box-shadow: 0 4px 15px rgba(0,0,0,0.3);
    transition: var(--transition);
  }

  .theme-toggle:hover { transform: scale(1.1); }

  .login-wrapper {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 20px;
  }

  .login-logo {
    width: 120px;
    height: 120px;
    background: linear-gradient(135deg, var(--main-red) 0%, var(--main-blue) 100%);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 20px;
    box-shadow: 0 8px 30px rgba(0,0,0,0.3);
    font-size: 50px;
    color: white;
  }

  .login { 
    display: flex; 
    justify-content: center; 
    align-items: center; 
    padding: 20px;
    width: 100%;
  }

  .login-box { 
    background: var(--bg-white); 
    padding: 40px; 
    width: 100%; 
    max-width: 420px; 
    border-radius: 15px; 
    box-shadow: 0 15px 40px rgba(0,0,0,0.3); 
    text-align: center; 
    border-top: 5px solid var(--main-red);
  }

  .login-box h2 {
    color: var(--main-blue);
    margin-bottom: 25px;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
  }

  .signup-link { 
    color: var(--main-blue); 
    font-weight: bold; 
    cursor: pointer; 
  }

  .signup-link:hover { text-decoration: underline; }

  .pass-wrapper { position: relative; }
  .pass-wrapper span { 
    position: absolute; 
    right: 15px; 
    top: 18px; 
    cursor: pointer; 
    font-size: 18px;
  }

  .dashboard { display: none; min-height: 100vh; }

  .header { 
    background: linear-gradient(135deg, var(--main-red) 0%, var(--main-blue) 100%); 
    color: white; 
    padding: 18px; 
    text-align: center; 
    font-size: 18px; 
    position: relative; 
    z-index: 1;
    padding-left: 70px;
    box-shadow: 0 4px 15px rgba(0,0,0,0.2);
  }

  .container { 
    display: flex; 
    min-height: calc(100vh - 60px); 
    position: relative; 
  }

  .menu-overlay {
    display: none;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0,0,0,0.6);
    z-index: 998;
    backdrop-filter: blur(3px);
  }

  .menu-overlay.show { display: block; }

  .menu {
    width: 300px;
    background: linear-gradient(180deg, var(--main-red) 0%, #5a0000 50%, var(--main-blue) 100%);
    padding: 15px;
    display: flex;
    flex-direction: column;
    position: fixed;
    top: 0;
    left: 0;
    height: 100%;
    z-index: 999;
    transition: transform 0.4s cubic-bezier(0.68, -0.55, 0.265, 1.55);
    transform: translateX(-100%);
    overflow-y: auto;
    padding-top: 80px;
    box-shadow: 5px 0 25px rgba(0,0,0,0.4);
  }
  
  .menu.show { transform: translateX(0); }
  
  .menu-header {
    color: white;
    text-align: center;
    padding: 15px;
    border-bottom: 2px solid rgba(255,255,255,0.3);
    margin-bottom: 20px;
    background: rgba(255,255,255,0.1);
    border-radius: 10px;
  }
  
  .menu-header h3 {
    margin: 0;
    font-size: 22px;
    color: var(--sub-yellow);
  }
  
  .menu-header p { margin: 5px 0 0 0; font-size: 13px; opacity: 0.9; }
  
  .menu button {
    background: rgba(255,255,255,0.15);
    color: white;
    margin-top: 10px;
    font-size: 15px;
    border: 1px solid rgba(255,255,255,0.25);
    border-radius: 8px;
    padding: 14px 15px;
    transition: all 0.3s;
    text-align: left;
    display: flex;
    align-items: center;
    gap: 12px;
  }
  
  .menu button:hover { 
    background: rgba(255,255,255,0.3); 
    transform: translateX(8px);
    padding-left: 20px;
  }
  
  .menu button:active {
    background: rgba(255,255,255,0.4);
    transform: scale(0.98);
  }
  
  .menu button .tab-icon { font-size: 20px; width: 30px; text-align: center; }
  
  .logout { 
    margin-top: auto; 
    background: var(--sub-orange) !important; 
    color: white !important; 
    text-align: center;
    justify-content: center;
  }
  .logout:hover { background: #e6730f !important; }
  
  .content { 
    flex: 1; 
    padding: 25px; 
    display: flex; 
    flex-direction: column; 
    align-items: center; 
    overflow-y: auto; 
    background: rgba(248,249,250,0.9);
  }
  
  [data-theme="dark"] .content { background: rgba(26, 26, 46, 0.95); }
  
  .section { 
    background: var(--bg-white); 
    padding: 25px; 
    border-radius: 12px; 
    width: 100%; 
    max-width: 900px; 
    margin-top: 20px; 
    box-shadow: 0 4px 20px rgba(0,0,0,0.1);
    border-left: 5px solid var(--main-blue);
  }
  
  .section h3 {
    color: var(--main-blue);
    border-bottom: 2px solid var(--sub-yellow);
    padding-bottom: 10px;
    margin-top: 0;
  }
  
  .section h4 {
    color: var(--main-blue);
    margin-top: 20px;
    margin-bottom: 12px;
  }
  
  .schedule-box { 
    display: flex; 
    flex-wrap: wrap; 
    gap: 15px; 
    margin-top: 20px; 
  }
  
  .schedule-box div { 
    flex: 1 1 180px; 
    background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%); 
    border: 2px solid #dee2e6; 
    padding: 18px; 
    border-radius: 10px; 
    text-align: center; 
    transition: all 0.3s;
  }
  
  .schedule-box div:hover {
    border-color: var(--main-blue);
    transform: translateY(-3px);
    box-shadow: 0 6px 15px rgba(0,0,0,0.15);
  }
  
  .schedule-box div strong {
    color: var(--main-blue);
    display: block;
    margin-bottom: 8px;
  }
  
  .chatbox { 
    border: 2px solid #dee2e6; 
    padding: 15px; 
    height: 320px; 
    width: 100%; 
    overflow-y: auto; 
    margin-top: 12px; 
    border-radius: 8px; 
    background: #fafafa;
  }
  
  .chat-message { 
    margin-bottom: 12px; 
    padding: 12px; 
    border-radius: 8px;
    animation: fadeIn 0.3s ease;
  }
  
  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(10px); }
    to { opacity: 1; transform: translateY(0); }
  }
  
  .chat-user { 
    background: linear-gradient(135deg, #e3f2fd 0%, #bbdefb 100%); 
    text-align: left; 
    margin-left: 20%;
  }
  .chat-ai { 
    background: linear-gradient(135deg, #f3e5f5 0%, #e1bee7 100%); 
    text-align: left; 
    margin-right: 20%;
  }
  
  .id-card { 
    background: linear-gradient(135deg, var(--main-red) 0%, var(--main-blue) 100%); 
    border: 4px solid var(--sub-yellow); 
    border-radius: 18px; 
    padding: 22px; 
    width: 100%; 
    max-width: 360px; 
    margin: 18px; 
    display: inline-block; 
    vertical-align: top; 
    color: white;
    position: relative;
    box-shadow: 0 10px 30px rgba(0,0,0,0.3);
  }
  
  .id-card-header { 
    background: rgba(255,255,255,0.12); 
    padding: 18px; 
    text-align: center; 
    border-radius: 12px 12px 0 0; 
    margin: -22px -22px 18px -22px; 
    border-bottom: 3px solid var(--sub-yellow);
  }
  
  .id-card-header h3 { 
    margin: 0; 
    font-size: 17px; 
    color: var(--sub-yellow); 
    letter-spacing: 1px;
  }
  
  .id-card-header p { 
    margin: 6px 0 0 0; 
    font-size: 11px; 
    color: #ddd; 
  }
  
  .id-card-photo { 
    width: 110px; 
    height: 110px; 
    background: #eee; 
    border-radius: 50%; 
    margin: 12px auto; 
    display: flex; 
    align-items: center; 
    justify-content: center; 
    overflow: hidden; 
    border: 5px solid var(--sub-yellow);
    box-shadow: 0 4px 15px rgba(0,0,0,0.3);
  }
  
  .id-card-photo img { 
    width: 100%; 
    height: 100%; 
    object-fit: cover; 
  }
  
  .id-card-info { 
    text-align: left; 
    font-size: 14px; 
    background: rgba(0,0,0,0.25); 
    padding: 18px; 
    border-radius: 12px;
  }
  
  .id-card-info p { 
    margin: 10px 0; 
    display: flex;
    justify-content: space-between;
  }
  
  .id-card-info strong { color: var(--sub-yellow); }
  
  .id-card-footer {
    text-align: center;
    margin-top: 18px;
    padding-top: 12px;
    border-top: 1px solid rgba(255,255,255,0.3);
    font-size: 10px;
    color: #ccc;
  }
  
  .id-card-checkbox {
    position: absolute;
    top: 12px;
    right: 12px;
    width: 28px;
    height: 28px;
    cursor: pointer;
    accent-color: var(--sub-yellow);
  }
  
  .attendance-calendar { 
    display: grid; 
    grid-template-columns: repeat(7, 1fr); 
    gap: 6px; 
    margin-top: 18px; 
    overflow-x: auto;
  }
  
  .attendance-day { 
    padding: 14px 10px; 
    text-align: center; 
    border: 2px solid #dee2e6; 
    border-radius: 8px; 
    min-width: 45px;
    cursor: pointer;
    transition: all 0.2s;
    font-weight: bold;
  }
  
  .attendance-day:hover { transform: scale(1.1); border-color: var(--main-blue); }
  
  .attendance-day.present { 
    background: linear-gradient(135deg, #d4edda 0%, #c3e6cb 100%); 
    border-color: #28a745;
  }
  
  .attendance-day.absent { 
    background: linear-gradient(135deg, #f8d7da 0%, #f5c6cb 100%); 
    border-color: #dc3545;
  }
  
  .attendance-day.header { 
    background: linear-gradient(135deg, var(--main-red) 0%, var(--main-blue) 100%); 
    color: white; 
    font-weight: bold; 
    padding: 12px;
    cursor: default;
  }
  
  .attendance-day.header:hover { transform: none; }
  
  .subject-item { 
    display: flex; 
    align-items: center; 
    padding: 12px; 
    border: 2px solid #dee2e6; 
    margin: 10px 0; 
    border-radius: 8px; 
    flex-wrap: wrap;
    gap: 12px;
    background: #fafafa;
  }
  
  .subject-item:hover {
    border-color: var(--main-blue);
    background: white;
  }
  
  .subject-item input[type="text"] { flex: 1; min-width: 140px; margin: 0; }
  
  .planner-container { 
    max-height: 500px; 
    overflow-y: auto; 
    padding: 18px; 
    border: 2px solid #dee2e6; 
    border-radius: 10px; 
    background: #f8f9fa; 
  }
  
  .planner-section { margin-bottom: 25px; }
  
  .planner-section h4 { 
    background: linear-gradient(135deg, var(--main-red) 0%, var(--main-blue) 100%); 
    color: white; 
    padding: 12px; 
    margin: 0 0 12px 0; 
    border-radius: 8px 8px 0 0; 
    display: flex;
    align-items: center;
    gap: 10px;
  }
  
  .planner-item { 
    display: flex; 
    align-items: center; 
    padding: 12px; 
    border: 2px solid #dee2e6; 
    margin: 8px 0; 
    border-radius: 8px; 
    background: white; 
    flex-wrap: wrap;
    gap: 12px;
    transition: all 0.2s;
  }
  
  .planner-item:hover { border-color: var(--main-blue); }
  
  .planner-item input[type="checkbox"] { 
    width: auto; 
    margin: 0; 
    width: 22px;
    height: 22px;
    cursor: pointer;
    accent-color: var(--main-blue);
  }
  
  .planner-item.completed { 
    text-decoration: line-through; 
    opacity: 0.6; 
    background: #f0f0f0;
  }
  
  .planner-item .goal-text { flex: 1; min-width: 180px; }
  
  .planner-item .goal-time { 
    font-size: 13px; 
    color: var(--main-gray);
    background: #e9ecef;
    padding: 4px 10px;
    border-radius: 15px;
  }
  
  .planner-item .alarm-btn { 
    width: auto; 
    padding: 8px 14px; 
    font-size: 13px; 
    background: linear-gradient(135deg, var(--main-red) 0%, var(--main-blue) 100%); 
    color: white; 
    border-radius: 20px;
  }
  
  .attendance-legend { margin-top: 15px; }
  .attendance-legend h4 { margin-bottom: 10px; }
  .attendance-legend p { margin: 5px 0; }
  
  .performance-box {
    background: linear-gradient(135deg, var(--main-red) 0%, var(--main-blue) 100%); 
    color: white;
    padding: 25px;
    border-radius: 12px;
    margin: 20px 0;
    text-align: center;
    box-shadow: 0 6px 20px rgba(0,0,0,0.2);
  }
  
  .performance-box h3 { color: var(--sub-yellow); margin-top: 0; }
  
  .performance-stats { 
    display: flex; 
    justify-content: space-around; 
    margin-top: 20px; 
    flex-wrap: wrap;
    gap: 15px;
  }
  
  .stat-item { 
    text-align: center; 
    background: rgba(255,255,255,0.15);
    padding: 15px 25px;
    border-radius: 10px;
    min-width: 100px;
  }
  
  .stat-number { font-size: 32px; font-weight: bold; color: var(--sub-yellow); }
  .stat-label { font-size: 13px; opacity: 0.9; margin-top: 5px; }
  
  .mood-selector {
    display: flex;
    justify-content: center;
    gap: 18px;
    margin: 25px 0;
    flex-wrap: wrap;
  }
  
  .mood-btn {
    width: 70px;
    height: 70px;
    border-radius: 50%;
    border: 4px solid transparent;
    font-size: 35px;
    cursor: pointer;
    transition: all 0.3s;
    background: white;
    box-shadow: 0 4px 15px rgba(0,0,0,0.1);
  }
  
  .mood-btn:hover { 
    transform: scale(1.15); 
    border-color: var(--main-blue);
    box-shadow: 0 8px 25px rgba(0,0,0,0.2);
  }
  
  .mood-btn.selected {
    transform: scale(1.2);
    border-color: var(--sub-orange);
    box-shadow: 0 0 25px rgba(253, 126, 20, 0.5);
  }
  
  .parent-account-card {
    background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
    border: 3px solid var(--main-blue);
    border-radius: 12px;
    padding: 20px;
    margin: 15px 0;
  }
  
  .parent-account-card h4 {
    color: var(--main-blue);
    margin-top: 0;
    display: flex;
    align-items: center;
    gap: 10px;
  }
  
  .parent-account-card .credentials {
    background: white;
    padding: 15px;
    border-radius: 8px;
    margin-top: 12px;
    border: 2px dashed var(--main-blue);
  }
  
  .parent-account-card .credentials p {
    margin: 8px 0;
    font-family: 'Courier New', monospace;
    font-weight: bold;
    color: var(--main-blue);
  }
  
  .print-controls {
    background: linear-gradient(135deg, #fff3cd 0%, #ffeeba 100%);
    padding: 18px;
    border-radius: 10px;
    margin-bottom: 20px;
    border: 3px solid var(--sub-yellow);
  }
  
  .print-controls h4 {
    color: var(--main-gray);
    margin-top: 0;
    display: flex;
    align-items: center;
    gap: 10px;
  }
  
  .school-map-container {
    background: #f8f9fa;
    border-radius: 12px;
    padding: 20px;
    margin-top: 15px;
    text-align: center;
  }
  
  .school-map-container img {
    max-width: 100%;
    border-radius: 10px;
    box-shadow: 0 4px 15px rgba(0,0,0,0.2);
  }
  
  .qr-scanner-container {
    background: #000;
    border-radius: 10px;
    overflow: hidden;
    margin: 15px 0;
    max-width: 400px;
  }
  
  #qr-scanner video {
    width: 100%;
    display: block;
  }
  
  .scanner-result {
    padding: 12px;
    border-radius: 8px;
    margin-top: 12px;
    text-align: center;
    font-weight: bold;
  }
  
  .scanner-result.success {
    background: #d4edda;
    color: #155724;
    border: 2px solid #c3e6cb;
  }
  
  .scanner-result.error {
    background: #f8d7da;
    color: #721c24;
    border: 2px solid #f5c6cb;
  }
  
  .sem-selector {
    display: flex;
    gap: 12px;
    margin: 15px 0;
    flex-wrap: wrap;
    justify-content: center;
  }
  
  .sem-btn {
    padding: 12px 24px;
    border: 3px solid var(--main-blue);
    background: white;
    color: var(--main-blue);
    border-radius: 25px;
    font-weight: bold;
    cursor: pointer;
    transition: all 0.3s;
    min-width: 140px;
  }
  
  .sem-btn:hover {
    background: var(--main-blue);
    color: white;
    transform: translateY(-2px);
  }
  
  .sem-btn.active {
    background: linear-gradient(135deg, var(--main-red) 0%, var(--main-blue) 100%);
    color: white;
    border-color: var(--sub-yellow);
  }
  
  .quarter-selector {
    display: flex;
    gap: 10px;
    margin: 15px 0;
    flex-wrap: wrap;
    justify-content: center;
  }
  
  .quarter-btn {
    padding: 10px 20px;
    border: 2px solid var(--main-gray);
    background: white;
    color: var(--main-gray);
    border-radius: 20px;
    font-weight: bold;
    cursor: pointer;
    transition: all 0.3s;
  }
  
  .quarter-btn:hover {
    border-color: var(--main-blue);
    color: var(--main-blue);
  }
  
  .quarter-btn.active {
    background: var(--main-blue);
    color: white;
    border-color: var(--main-blue);
  }
  
  .school-welcome {
    background: linear-gradient(135deg, var(--main-red) 0%, var(--main-blue) 100%);
    color: white;
    padding: 30px;
    border-radius: 15px;
    text-align: center;
    margin-bottom: 25px;
    box-shadow: 0 8px 25px rgba(0,0,0,0.2);
  }
  
  .school-welcome h2 { margin: 0 0 10px 0; color: var(--sub-yellow); }
  .school-welcome p { margin: 0; opacity: 0.95; }
  
  .profile-card {
    background: linear-gradient(135deg, var(--main-red) 0%, var(--main-blue) 100%);
    border-radius: 15px;
    padding: 25px;
    text-align: center;
    color: white;
    margin-bottom: 20px;
    box-shadow: 0 8px 25px rgba(0,0,0,0.2);
  }
  
  .profile-card .profile-photo {
    width: 120px;
    height: 120px;
    border-radius: 50%;
    border: 5px solid var(--sub-yellow);
    margin: 0 auto 15px;
    overflow: hidden;
    box-shadow: 0 4px 15px rgba(0,0,0,0.3);
  }
  
  .profile-card .profile-photo img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
  
  .profile-card h3 { color: var(--sub-yellow); margin: 0 0 5px 0; }
  .profile-card p { margin: 5px 0; opacity: 0.9; }
  
  .profile-details {
    background: var(--bg-white);
    border-radius: 10px;
    padding: 20px;
    text-align: left;
  }
  
  .profile-details .detail-row {
    display: flex;
    justify-content: space-between;
    padding: 10px 0;
    border-bottom: 1px solid #eee;
  }
  
  .profile-details .detail-row:last-child { border-bottom: none; }
  .profile-details .detail-label { font-weight: bold; color: var(--main-blue); }
  .profile-details .detail-value { color: var(--text-muted); }
  
  .mood-chat-container { max-width: 600px; margin: 0 auto; }
  .mood-chat-container .chatbox { height: 400px; }
  
  .mood-chat-container .input-area {
    display: flex;
    gap: 10px;
    margin-top: 15px;
  }
  
  .mood-chat-container .input-area input { flex: 1; margin: 0; }
  .mood-chat-container .input-area button { width: auto; white-space: nowrap; }
  
  /*------ ASSIGNMENTS ------*/
  .assignment-card {
    background: var(--bg-white);
    border-radius: 10px;
    padding: 20px;
    margin-bottom: 15px;
    border-left: 5px solid var(--main-blue);
    box-shadow: 0 2px 10px rgba(0,0,0,0.1);
  }
  
  .assignment-card.urgent {
    border-left-color: var(--danger);
    background: linear-gradient(90deg, #fff5f5 0%, var(--bg-white) 100%);
  }
  
  .assignment-card.completed {
    border-left-color: var(--success);
    opacity: 0.8;
  }
  
  .assignment-header {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    margin-bottom: 12px;
  }
  
  .assignment-title {
    font-size: 16px;
    font-weight: bold;
    color: var(--text-dark);
  }
  
  .assignment-subject {
    background: var(--main-blue);
    color: white;
    padding: 4px 12px;
    border-radius: 15px;
    font-size: 12px;
    margin-top: 5px;
    display: inline-block;
  }
  
  .assignment-due {
    font-size: 13px;
    color: var(--text-muted);
    display: flex;
    align-items: center;
    gap: 5px;
  }
  
  .assignment-due.overdue {
    color: var(--danger);
    font-weight: bold;
  }
  
  .assignment-due.soon {
    color: var(--warning);
    font-weight: bold;
  }
  
  .assignment-desc {
    margin: 12px 0;
    color: var(--text-dark);
    line-height: 1.6;
  }
  
  .assignment-files {
    margin-top: 12px;
  }
  
  .assignment-file {
    display: flex;
    align-items: center;
    gap: 8px;
    padding: 8px;
    background: var(--bg-light);
    border-radius: 6px;
    margin-top: 8px;
    cursor: pointer;
    transition: var(--transition);
  }
  
  .assignment-file:hover {
    background: #e9ecef;
  }
  
  .assignment-actions {
    display: flex;
    gap: 10px;
    margin-top: 15px;
    flex-wrap: wrap;
  }
  
  .assignment-points {
    background: var(--sub-yellow);
    color: #000;
    padding: 4px 12px;
    border-radius: 15px;
    font-size: 12px;
    font-weight: bold;
  }
  
  /*------ QUIZ/EXAM ------*/
  .quiz-container {
    max-width: 800px;
    margin: 0 auto;
  }
  
  .quiz-header {
    background: linear-gradient(135deg, var(--main-red) 0%, var(--main-blue) 100%);
    color: white;
    padding: 20px;
    border-radius: 12px;
    margin-bottom: 20px;
  }
  
  .quiz-question {
    background: var(--bg-white);
    padding: 20px;
    border-radius: 10px;
    margin-bottom: 15px;
    box-shadow: 0 2px 10px rgba(0,0,0,0.1);
  }
  
  .quiz-question-number {
    background: var(--main-blue);
    color: white;
    width: 30px;
    height: 30px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: bold;
    margin-bottom: 10px;
  }
  
  .quiz-options {
    margin-top: 15px;
  }
  
  .quiz-option {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 12px;
    border: 2px solid var(--border-color);
    border-radius: 8px;
    margin-top: 8px;
    cursor: pointer;
    transition: var(--transition);
  }
  
  .quiz-option:hover {
    border-color: var(--main-blue);
    background: #f0f7ff;
  }
  
  .quiz-option.selected {
    border-color: var(--main-blue);
    background: #e3f2fd;
  }
  
  .quiz-option.correct {
    border-color: var(--success);
    background: #d4edda;
  }
  
  .quiz-option.wrong {
    border-color: var(--danger);
    background: #f8d7da;
  }
  
  .quiz-timer {
    background: var(--sub-orange);
    color: white;
    padding: 10px 20px;
    border-radius: 25px;
    font-weight: bold;
    display: inline-flex;
    align-items: center;
    gap: 8px;
  }
  
  /*------ LEARNING MATERIALS ------*/
  .material-card {
    background: var(--bg-white);
    border-radius: 10px;
    padding: 20px;
    margin-bottom: 15px;
    display: flex;
    gap: 15px;
    align-items: flex-start;
    box-shadow: 0 2px 10px rgba(0,0,0,0.1);
  }
  
  .material-icon {
    width: 60px;
    height: 60px;
    background: linear-gradient(135deg, var(--main-red) 0%, var(--main-blue) 100%);
    border-radius: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
    font-size: 24px;
    flex-shrink: 0;
  }
  
  .material-info { flex: 1; }
  .material-title { font-weight: bold; font-size: 16px; color: var(--text-dark); margin-bottom: 5px; }
  .material-meta { font-size: 12px; color: var(--text-muted); }
  .material-desc { margin: 10px 0; color: var(--text-dark); }
  
  /*------ SCHOOL CALENDAR ------*/
  .calendar-container {
    background: var(--bg-white);
    border-radius: 12px;
    padding: 20px;
    box-shadow: 0 2px 15px rgba(0,0,0,0.1);
  }
  
  .calendar-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
  }
  
  .calendar-nav {
    display: flex;
    align-items: center;
    gap: 15px;
  }
  
  .calendar-nav button {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  .calendar-month {
    font-size: 20px;
    font-weight: bold;
    color: var(--main-blue);
  }
  
  .calendar-grid {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    gap: 5px;
  }
  
  .calendar-day-header {
    text-align: center;
    font-weight: bold;
    padding: 10px;
    color: var(--main-blue);
    background: var(--bg-light);
    border-radius: 5px;
  }
  
  .calendar-day {
    padding: 10px;
    text-align: center;
    border-radius: 8px;
    cursor: pointer;
    transition: var(--transition);
    min-height: 80px;
    position: relative;
  }
  
  .calendar-day:hover {
    background: var(--bg-light);
  }
  
  .calendar-day.other-month {
    opacity: 0.4;
  }
  
  .calendar-day.today {
    background: linear-gradient(135deg, var(--main-red) 0%, var(--main-blue) 100%);
    color: white;
  }
  
  .calendar-day.has-event {
    background: var(--sub-yellow);
    color: #000;
    font-weight: bold;
  }
  
  .calendar-day-number {
    font-weight: bold;
    margin-bottom: 5px;
  }
  
  .calendar-event-dot {
    width: 8px;
    height: 8px;
    background: var(--main-blue);
    border-radius: 50%;
    margin: 2px auto;
  }
  
  .calendar-event-list {
    position: absolute;
    top: 100%;
    left: 0;
    background: var(--bg-white);
    border-radius: 8px;
    box-shadow: 0 5px 20px rgba(0,0,0,0.2);
    padding: 10px;
    z-index: 100;
    min-width: 200px;
    display: none;
  }
  
  .calendar-day:hover .calendar-event-list {
    display: block;
  }
  
  /*------ REPORT CARD ------*/
  .report-card {
    background: var(--bg-white);
    border-radius: 15px;
    padding: 30px;
    box-shadow: 0 5px 20px rgba(0,0,0,0.15);
    max-width: 800px;
    margin: 0 auto;
  }
  
  .report-header {
    text-align: center;
    border-bottom: 3px solid var(--main-blue);
    padding-bottom: 20px;
    margin-bottom: 20px;
  }
  
  .report-school-name {
    font-size: 24px;
    font-weight: bold;
    color: var(--main-blue);
  }
  
  .report-student-info {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 15px;
    margin-bottom: 20px;
    background: var(--bg-light);
    padding: 15px;
    border-radius: 8px;
  }
  
  .report-subject-grades {
    margin-bottom: 20px;
  }
  
  .report-footer {
    text-align: center;
    margin-top: 30px;
    padding-top: 20px;
    border-top: 2px solid var(--border-color);
  }
  
  .grade-a { color: var(--success); }
  .grade-b { color: #17a2b8; }
  .grade-c { color: var(--warning); }
  .grade-d { color: var(--sub-orange); }
  .grade-f { color: var(--danger); }
  
  /*------ GRADE ANALYTICS ------*/
  .analytics-card {
    background: var(--bg-white);
    border-radius: 12px;
    padding: 20px;
    text-align: center;
    box-shadow: 0 2px 15px rgba(0,0,0,0.1);
  }
  
  .analytics-number {
    font-size: 36px;
    font-weight: bold;
    color: var(--main-blue);
  }
  
  .analytics-label {
    font-size: 14px;
    color: var(--text-muted);
    margin-top: 5px;
  }
  
  .grade-chart {
    display: flex;
    align-items: flex-end;
    justify-content: center;
    gap: 10px;
    height: 200px;
    padding: 20px;
  }
  
  .grade-bar {
    width: 40px;
    background: linear-gradient(135deg, var(--main-red) 0%, var(--main-blue) 100%);
    border-radius: 5px 5px 0 0;
    transition: var(--transition);
    position: relative;
  }
  
  .grade-bar:hover {
    transform: scaleY(1.05);
  }
  
  .grade-bar-label {
    position: absolute;
    bottom: -25px;
    left: 50%;
    transform: translateX(-50%);
    font-size: 12px;
    font-weight: bold;
  }
  
  .grade-bar-value {
    position: absolute;
    top: -25px;
    left: 50%;
    transform: translateX(-50%);
    font-size: 12px;
    font-weight: bold;
    color: var(--main-blue);
  }
  
    /*------ NOTIFICATIONS ------*/
  .notification-item {
    display: flex;
    gap: 15px;
    padding: 15px;
    background: var(--bg-white);
    border-radius: 10px;
    margin-bottom: 10px;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    transition: var(--transition);
  }
  
  .notification-item:hover {
    transform: translateX(5px);
    box-shadow: 0 4px 15px rgba(0,0,0,0.15);
  }
  
  .notification-item.unread {
    border-left: 4px solid var(--main-blue);
    background: linear-gradient(90deg, #f0f7ff 0%, var(--bg-white) 100%);
  }
  
  .notification-icon {
    width: 50px;
    height: 50px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 20px;
    flex-shrink: 0;
  }
  
  .notification-icon.info { background: #e3f2fd; color: var(--main-blue); }
  .notification-icon.success { background: #d4edda; color: var(--success); }
  .notification-icon.warning { background: #fff3cd; color: var(--warning); }
  .notification-icon.danger { background: #f8d7da; color: var(--danger); }
  
  .notification-content { flex: 1; }
  .notification-title { font-weight: bold; color: var(--text-dark); margin-bottom: 5px; }
  .notification-message { font-size: 14px; color: var(--text-muted); margin-bottom: 5px; }
  .notification-time { font-size: 12px; color: var(--text-muted); }
  
  /*------ FILE UPLOAD ------*/
  .file-upload-area {
    border: 3px dashed var(--border-color);
    border-radius: 12px;
    padding: 30px;
    text-align: center;
    cursor: pointer;
    transition: var(--transition);
  }
  
  .file-upload-area:hover {
    border-color: var(--main-blue);
    background: #f0f7ff;
  }
  
  .file-upload-area.dragover {
    border-color: var(--main-blue);
    background: #e3f2fd;
  }
  
  .file-upload-icon {
    font-size: 48px;
    color: var(--main-blue);
    margin-bottom: 10px;
  }
  
  .file-upload-text { color: var(--text-muted); }
  .file-upload-text strong { color: var(--main-blue); }
  
  .file-list {
    margin-top: 15px;
  }
  
  .file-item {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 10px;
    background: var(--bg-light);
    border-radius: 8px;
    margin-top: 8px;
  }
  
  .file-item-icon { font-size: 24px; color: var(--main-blue); }
  .file-item-info { flex: 1; }
  .file-item-name { font-weight: bold; color: var(--text-dark); }
  .file-item-size { font-size: 12px; color: var(--text-muted); }
  
  /*------ SEARCH ------*/
  .search-box {
    position: relative;
    margin-bottom: 20px;
  }
  
  .search-box input {
    padding-left: 45px;
    background: var(--bg-white);
  }
  
  .search-box i {
    position: absolute;
    left: 15px;
    top: 50%;
    transform: translateY(-50%);
    color: var(--text-muted);
  }
  
  .search-results {
    position: absolute;
    top: 100%;
    left: 0;
    width: 100%;
    background: var(--bg-white);
    border-radius: 8px;
    box-shadow: 0 5px 20px rgba(0,0,0,0.15);
    z-index: 1000;
    max-height: 300px;
    overflow-y: auto;
    display: none;
  }
  
  .search-results.show { display: block; }
  
  .search-result-item {
    padding: 12px 15px;
    cursor: pointer;
    transition: var(--transition);
    border-bottom: 1px solid var(--border-color);
  }
  
  .search-result-item:hover {
    background: var(--bg-light);
  }
  
  /*------ DATA EXPORT ------*/
  .export-options {
    display: flex;
    gap: 15px;
    flex-wrap: wrap;
    justify-content: center;
  }
  
  .export-btn {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 10px;
    padding: 20px 30px;
    background: var(--bg-white);
    border: 2px solid var(--border-color);
    border-radius: 12px;
    cursor: pointer;
    transition: var(--transition);
    min-width: 120px;
  }
  
  .export-btn:hover {
    border-color: var(--main-blue);
    transform: translateY(-3px);
    box-shadow: 0 5px 15px rgba(0,0,0,0.1);
  }
  
  .export-btn i { font-size: 32px; color: var(--main-blue); }
  .export-btn span { font-weight: 600; color: var(--text-dark); }
  
  /*------ LIBRARY ------*/
  .library-book {
    display: flex;
    gap: 20px;
    background: var(--bg-white);
    padding: 20px;
    border-radius: 12px;
    margin-bottom: 15px;
    box-shadow: 0 2px 10px rgba(0,0,0,0.1);
  }
  
  .book-cover {
    width: 100px;
    height: 150px;
    background: linear-gradient(135deg, var(--main-red) 0%, var(--main-blue) 100%);
    border-radius: 8px;
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
    font-size: 32px;
    flex-shrink: 0;
  }
  
  .book-info { flex: 1; }
  .book-title { font-size: 18px; font-weight: bold; color: var(--text-dark); margin-bottom: 5px; }
  .book-author { font-size: 14px; color: var(--text-muted); margin-bottom: 10px; }
  .book-meta { font-size: 13px; color: var(--text-muted); display: flex; gap: 15px; flex-wrap: wrap; }
  .book-status {
    display: inline-block;
    padding: 4px 12px;
    border-radius: 15px;
    font-size: 12px;
    font-weight: bold;
    margin-top: 10px;
  }
  
  .book-status.available { background: #d4edda; color: #155724; }
  .book-status.borrowed { background: #f8d7da; color: #721c24; }
  .book-status.reserved { background: #fff3cd; color: #856404; }
  
  /*------ FEES/PAYMENTS ------*/
  .fee-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px;
    background: var(--bg-white);
    border-radius: 10px;
    margin-bottom: 10px;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  }
  
  .fee-info { display: flex; align-items: center; gap: 15px; }
  .fee-icon {
    width: 45px;
    height: 45px;
    background: linear-gradient(135deg, var(--main-red) 0%, var(--main-blue) 100%);
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
    font-size: 18px;
  }
  
  .fee-details h4 { margin: 0 0 3px 0; color: var(--text-dark); }
  .fee-details p { margin: 0; font-size: 13px; color: var(--text-muted); }
  .fee-amount { font-size: 20px; font-weight: bold; color: var(--main-blue); }
  .fee-amount.paid { color: var(--success); }
  .fee-amount.unpaid { color: var(--danger); }
  
  .payment-summary {
    background: linear-gradient(135deg, var(--main-red) 0%, var(--main-blue) 100%);
    color: white;
    padding: 25px;
    border-radius: 12px;
    margin-bottom: 20px;
  }
  
  .payment-summary h3 { margin: 0 0 15px 0; color: var(--sub-yellow); }
  .payment-row { display: flex; justify-content: space-between; margin: 10px 0; }
  .payment-total { border-top: 2px solid rgba(255,255,255,0.3); padding-top: 15px; margin-top: 15px; font-size: 18px; font-weight: bold; }
  
  /*------ SYLLABUS ------*/
  .syllabus-section {
    margin-bottom: 25px;
  }
  
  .syllabus-section h4 {
    background: linear-gradient(135deg, var(--main-red) 0%, var(--main-blue) 100%);
    color: white;
    padding: 15px;
    border-radius: 8px 8px 0 0;
    margin: 0;
  }
  
  .syllabus-topics {
    border: 2px solid var(--border-color);
    border-top: none;
    border-radius: 0 0 8px 8px;
  }
  
  .syllabus-topic {
    display: flex;
    align-items: center;
    padding: 12px 15px;
    border-bottom: 1px solid var(--border-color);
    transition: var(--transition);
  }
  
  .syllabus-topic:last-child { border-bottom: none; }
  .syllabus-topic:hover { background: var(--bg-light); }
  .syllabus-topic-icon { margin-right: 12px; color: var(--main-blue); }
  .syllabus-topic-title { flex: 1; color: var(--text-dark); }
  .syllabus-topic-weeks { font-size: 12px; color: var(--text-muted); background: var(--bg-light); padding: 4px 10px; border-radius: 15px; }
  
  /*------ DATA BACKUP ------*/
  .backup-option {
    display: flex;
    align-items: center;
    gap: 20px;
    padding: 20px;
    background: var(--bg-white);
    border-radius: 12px;
    margin-bottom: 15px;
    box-shadow: 0 2px 10px rgba(0,0,0,0.1);
  }
  
  .backup-icon {
    width: 60px;
    height: 60px;
    background: linear-gradient(135deg, var(--main-red) 0%, var(--main-blue) 100%);
    border-radius: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
    font-size: 24px;
  }
  
  .backup-info { flex: 1; }
  .backup-info h4 { margin: 0 0 5px 0; color: var(--text-dark); }
  .backup-info p { margin: 0; font-size: 13px; color: var(--text-muted); }
  
  /*------ MEDIA QUERIES ------*/
  @media (max-width: 768px) {
    .menu { width: 85%; max-width: 340px; }
    .section { padding: 18px; margin-top: 12px; }
    .schedule-box div { flex: 1 1 100%; }
    table { display: block; overflow-x: auto; white-space: nowrap; }
    .id-card { max-width: 100%; margin: 12px 0; }
    .mood-selector { gap: 12px; }
    .mood-btn { width: 60px; height: 60px; font-size: 28px; }
    .header { padding-left: 55px; font-size: 15px; }
    .toggle-btn { padding: 8px 12px; font-size: 14px; }
    .login-box { padding: 25px; }
    .stat-number { font-size: 26px; }
    .mood-chat-container .chatbox { height: 300px; }
    .mood-chat-container .input-area { flex-direction: column; }
    .mood-chat-container .input-area button { width: 100%; }
    
    .calendar-day { min-height: 60px; padding: 5px; }
    .calendar-day-number { font-size: 12px; }
    .calendar-event-dot { width: 6px; height: 6px; }
    
    .assignment-header { flex-direction: column; gap: 10px; }
    .assignment-actions { flex-direction: column; }
    .assignment-actions button { width: 100%; justify-content: center; }
    
    .report-student-info { grid-template-columns: 1fr; }
    
    .library-book { flex-direction: column; align-items: center; text-align: center; }
    .book-info { text-align: center; }
    .book-meta { justify-content: center; }
    .fee-item { flex-direction: column; gap: 15px; text-align: center; }
    .fee-info { flex-direction: column; }
  }
  
  @media print {
    .menu, .toggle-btn, .theme-toggle, .header, .print-controls, .menu-overlay, .toast-container {
      display: none !important;
    }
    
    .id-card { 
      break-inside: avoid; 
      page-break-inside: avoid; 
      border: 3px solid #000; 
      display: inline-block;
      margin: 10px;
    }
    
    .content { padding: 0; }
    .section { box-shadow: none; padding: 10px; border: none; }
    
    body { background: white; }
    
    .report-card {
      box-shadow: none;
      border: 1px solid #000;
    }
  }
  
  /*------ ACCESSIBILITY ------*/
  *:focus {
    outline: 2px solid var(--main-blue);
    outline-offset: 2px;
  }
  
  .skip-link {
    position: absolute;
    top: -40px;
    left: 0;
    background: var(--main-blue);
    color: white;
    padding: 8px 16px;
    z-index: 10000;
    transition: top 0.3s;
  }
  
  .skip-link:focus { top: 0; }
  
  /*------ PRINT STYLES FOR REPORT CARD ------*/
  @media print {
    .no-print { display: none !important; }
    
    .print-only { display: block !important; }
    
    .report-card {
      page-break-inside: avoid;
      break-inside: avoid;
    }
    
    .report-subject-grades table {
      page-break-inside: avoid;
    }
  }
  
  /*------ SCROLLBAR STYLES ------*/
  ::-webkit-scrollbar {
    width: 10px;
    height: 10px;
  }
  
  ::-webkit-scrollbar-track {
    background: var(--bg-light);
    border-radius: 5px;
  }
  
  ::-webkit-scrollbar-thumb {
    background: linear-gradient(135deg, var(--main-red) 0%, var(--main-blue) 100%);
    border-radius: 5px;
  }
  
  ::-webkit-scrollbar-thumb:hover {
    background: linear-gradient(135deg, #660000 0%, #002244 100%);
  }
  
  /*------ SELECTION STYLES ------*/
  ::selection {
    background: var(--main-blue);
    color: white;
  }
  
  /*------ ANIMATIONS ------*/
  .animate-bounce {
    animation: bounce 2s infinite;
  }
  
  @keyframes bounce {
    0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
    40% { transform: translateY(-10px); }
    60% { transform: translateY(-5px); }
  }
  
  .animate-pulse {
    animation: pulse 2s infinite;
  }
  
  @keyframes pulse {
    0% { transform: scale(1); }
    50% { transform: scale(1.05); }
    100% { transform: scale(1); }
  }
  
  .animate-fade-in {
    animation: fadeIn 0.5s ease;
  }
  
  @keyframes fadeIn {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}

.animate-slide-up {
  animation: slideUp 0.5s ease;
}

@keyframes slideUp {
  from { opacity: 0; transform: translateY(50px); }
  to { opacity: 1; transform: translateY(0); }
}

.animate-zoom-in {
  animation: zoomIn 0.3s ease;
}

@keyframes zoomIn {
  from { opacity: 0; transform: scale(0.8); }
  to { opacity: 1; transform: scale(1); }
}

/*------ ICONS ------*/
.fa-check-circle { color: var(--success); }
.fa-times-circle { color: var(--danger); }
.fa-exclamation-circle { color: var(--warning); }
.fa-info-circle { color: var(--info); }
</style>

<script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
<script src="https://unpkg.com/html5-qrcode/html5-qrcode.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/3.9.1/chart.min.js"></script>
</head>
<body>

<a href="#main-content" class="skip-link">Skip to main content</a>

<div class="toast-container" id="toastContainer"></div>

<div class="login-wrapper" id="loginWrapper">
  <div class="login-logo">🎓</div>
  <h1 style="color: white; margin-bottom: 10px;">DSHS School System</h1>
  <p style="color: rgba(255,255,255,0.8); margin-bottom: 30px;">Dumingag Senior High School</p>
</div>

<div class="login" id="login">
  <div class="login-box">
    <h2><i class="fas fa-sign-in-alt"></i> Login</h2>
    <div class="input-icon">
      <i class="fas fa-user"></i>
      <input type="text" id="loginUsername" placeholder="Username">
    </div>
    <div class="pass-wrapper">
      <div class="input-icon">
        <i class="fas fa-lock"></i>
        <input type="password" id="loginPassword" placeholder="Password">
      </div>
      <span onclick="togglePassword()"><i class="fas fa-eye"></i></span>
    </div>
    <button onclick="login()" class="btn btn-primary btn-block btn-lg mt-2">
      <i class="fas fa-sign-in-alt"></i> Login
    </button>
    <p id="msg" class="text-center text-danger mt-2"></p>
    <p class="text-center mt-2">Don't have an account? <span class="signup-link" onclick="showSignup()">Sign up!</span></p>
  </div>
</div>

<div class="login" id="signup" style="display:none;">
  <div class="login-box">
    <h2><i class="fas fa-user-plus"></i> Student Sign Up</h2>
    <input type="text" id="signupName" placeholder="Full Name">
    <input type="text" id="signupID" placeholder="Student ID">
    <input type="text" id="signupSection" placeholder="Section">
    <input type="text" id="signupTrack" placeholder="Track">
    <input type="text" id="signupStrand" placeholder="Strand">
    <input type="text" id="signupGradeLevel" placeholder="Grade Level">
    <input type="text" id="signupUsername" placeholder="Username">
    <input type="password" id="signupPass" placeholder="Password">
    <button onclick="submitSignup()" class="btn btn-primary btn-block btn-lg mt-2">
      <i class="fas fa-user-plus"></i> Create Account
    </button>
    <button onclick="clearSignup()" class="btn btn-outline btn-block mt-1">
      <i class="fas fa-redo"></i> Clear
    </button>
    <p class="text-center mt-2">Already have an account? <span class="signup-link" onclick="showLogin()">Login</span></p>
  </div>
</div>

<div class="dashboard" id="dashboard">
  <button class="toggle-btn" id="toggleBtn" onclick="toggleMenu()">
    <span class="icon"><i class="fas fa-bars"></i></span>
    <span class="text">Menu</span>
  </button>
  
  <button class="theme-toggle" onclick="toggleTheme()" title="Toggle Dark Mode">
    <i class="fas fa-moon" id="themeIcon"></i>
  </button>
  
  <div class="menu-overlay" id="menuOverlay" onclick="toggleMenu()"></div>
  <div class="header" id="roleTitle"></div>
  <div class="container">
    <div class="menu" id="menu"></div>
    <div class="content" id="content">
      <div class="school-welcome">
        <h2>🏫 Dumingag Senior High School</h2>
        <p>Welcome to the DSHS School System</p>
      </div>
      <div class="section">
        <h3>👋 Welcome</h3>
        <p>Select an option from the menu to get started.</p>
      </div>
    </div>
  </div>
</div>

<!-- MODAL TEMPLATE -->
<div id="modalContainer"></div>

<script>
// ==================== ENHANCED SECURITY ====================
const SECRET_KEY = "DSHS2024SECUREKEY";

// Enhanced hash function (multiple rounds)
function secureHash(str) {
  let hash = 0;
  for (let i = 0; i < 1000; i++) {
    hash = ((hash << 5) - hash) + str.charCodeAt(i % str.length);
    hash = hash & hash;
  }
  return hash.toString(16) + str.length.toString(16);
}

// Session management
let sessionToken = null;
function generateSessionToken() {
  return 'DSHS_' + Date.now() + '_' + Math.random().toString(36).substr(2);
}

function setSession(token) {
  sessionToken = token;
  localStorage.setItem('dshs_session', token);
}

function getSession() {
  return localStorage.getItem('dshs_session');
}

function clearSession() {
  sessionToken = null;
  localStorage.removeItem('dshs_session');
}

// ==================== DATA STORAGE ====================
let role = "", currentUser = "";

let students = JSON.parse(localStorage.getItem('dshs_students')) || [
  {name: "Jibdel", id: "ST001", section: "12-A", track: "Academic", strand: "STEM", gradeLevel: "12", username: "jibdel", password: secureHash("1234"), approved: true, pic: ""},
  {name: "Viennes", id: "ST002", section: "12-B", track: "Academic", strand: "ABM", gradeLevel: "12", username: "viennes", password: secureHash("5678"), approved: true, pic: ""},
  {name: "Jurl", id: "ST003", section: "12-C", track: "Academic", strand: "STEM", gradeLevel: "12", username: "jurl", password: secureHash("abcd"), approved: true, pic: ""}
];

let teachers = JSON.parse(localStorage.getItem('dshs_teachers')) || [
  {name: "Mr. Smith", id: "TE001", position: "Teacher III", sectionHandled: "12-A", username: "teacher1", password: secureHash("teach123")}
];

let parents = JSON.parse(localStorage.getItem('dshs_parents')) || [
  {name: "Parent of Jibdel", child: "Jibdel", username: "parentSt001", password: secureHash("par123")}
];

let subjects = JSON.parse(localStorage.getItem('dshs_subjects')) || ["3I's", "Genchem 2", "P6 2", "Perdev", "CPAR", "Entrepreneurship"];

let scheduleTimes = JSON.parse(localStorage.getItem('dshs_scheduleTimes')) || {
  "3I's": "8:00-9:00", "Genchem 2": "9:00-10:00", "P6 2": "10:00-11:00",
  "Perdev": "11:45-12:30", "CPAR": "12:30-1:00", "Entrepreneurship": "1:00-2:00"
};

let gradesData = JSON.parse(localStorage.getItem('dshs_gradesData')) || {};
if (Object.keys(gradesData).length === 0) {
  students.forEach(s => {
    gradesData[s.name] = {};
    subjects.forEach(sub => gradesData[s.name][sub] = { q1: 0, q2: 0, q3: 0, q4: 0 });
  });
}

let attendanceData = JSON.parse(localStorage.getItem('dshs_attendanceData')) || {};
students.forEach(s => { if (!attendanceData[s.name]) attendanceData[s.name] = {}; });

let bulletinBoard = JSON.parse(localStorage.getItem('dshs_bulletinBoard')) || ["Welcome to DSHS School System!"];

let plannerData = JSON.parse(localStorage.getItem('dshs_plannerData')) || {};

// NEW: Assignments Data
let assignments = JSON.parse(localStorage.getItem('dshs_assignments')) || [];

// NEW: Learning Materials
let learningMaterials = JSON.parse(localStorage.getItem('dshs_materials')) || [];

// NEW: School Calendar Events
let calendarEvents = JSON.parse(localStorage.getItem('dshs_calendarEvents')) || [];

// NEW: Library Books
let libraryBooks = JSON.parse(localStorage.getItem('dshs_libraryBooks')) || [
  {id: 1, title: "STEM Mathematics", author: "John Smith", category: "Mathematics", status: "available", copies: 5},
  {id: 2, title: "General Chemistry", author: "Maria Garcia", category: "Science", status: "available", copies: 3},
  {id: 3, title: "English Literature", author: "David Brown", category: "English", status: "borrowed", copies: 2},
  {id: 4, title: "Philippine History", author: "Juan dela Cruz", category: "History", status: "available", copies: 4},
  {id: 5, title: "Accountancy", author: "Ana Reyes", category: "ABM", status: "available", copies: 3}
];

// NEW: Fees/Payments
let feesData = JSON.parse(localStorage.getItem('dshs_feesData')) || {};
students.forEach(s => {
  if (!feesData[s.name]) {
    feesData[s.name] = [
      {id: 1, name: "Tuition Fee", amount: 5000, paid: 0, dueDate: "2024-03-31"},
      {id: 2, name: "Miscellaneous", amount: 2000, paid: 0, dueDate: "2024-03-31"},
      {id: 3, name: "Laboratory Fee", amount: 1000, paid: 0, dueDate: "2024-04-30"}
    ];
  }
});

// NEW: Syllabus
let syllabusData = JSON.parse(localStorage.getItem('dshs_syllabus')) || {
  "3I's": [
    {topic: "Introduction to Research", weeks: "1-2"},
    {topic: "Research Methods", weeks: "3-4"},
    {topic: "Data Collection", weeks: "5-6"},
    {topic: "Data Analysis", weeks: "7-8"},
    {topic: "Research Writing", weeks: "9-10"}
  ],
  "Genchem 2": [
    {topic: "Chemical Thermodynamics", weeks: "1-3"},
    {topic: "Chemical Kinetics", weeks: "4-6"},
    {topic: "Chemical Equilibrium", weeks: "7-9"},
    {topic: "Acids and Bases", weeks: "10-12"}
  ]
};

// NEW: Notifications
let notifications = JSON.parse(localStorage.getItem('dshs_notifications')) || [];

let adminAccount = {name: "Administrator", username: "admin", password: secureHash("admin123")};

// ==================== SAVE DATA ====================
function saveData() {
  try {
    localStorage.setItem('dshs_students', JSON.stringify(students));
    localStorage.setItem('dshs_teachers', JSON.stringify(teachers));
    localStorage.setItem('dshs_parents', JSON.stringify(parents));
    localStorage.setItem('dshs_subjects', JSON.stringify(subjects));
    localStorage.setItem('dshs_scheduleTimes', JSON.stringify(scheduleTimes));
    localStorage.setItem('dshs_gradesData', JSON.stringify(gradesData));
    localStorage.setItem('dshs_attendanceData', JSON.stringify(attendanceData));
    localStorage.setItem('dshs_bulletinBoard', JSON.stringify(bulletinBoard));
    localStorage.setItem('dshs_plannerData', JSON.stringify(plannerData));
    localStorage.setItem('dshs_assignments', JSON.stringify(assignments));
    localStorage.setItem('dshs_materials', JSON.stringify(learningMaterials));
    localStorage.setItem('dshs_calendarEvents', JSON.stringify(calendarEvents));
    localStorage.setItem('dshs_libraryBooks', JSON.stringify(libraryBooks));
    localStorage.setItem('dshs_feesData', JSON.stringify(feesData));
    localStorage.setItem('dshs_syllabus', JSON.stringify(syllabusData));
    localStorage.setItem('dshs_notifications', JSON.stringify(notifications));
  } catch (e) {
    showToast("Storage error occurred!", "danger");
  }
}

// ==================== TOAST NOTIFICATIONS ====================
function showToast(message, type = "info") {
  const container = document.getElementById('toastContainer');
  const toast = document.createElement('div');
  toast.className = `toast toast-${type}`;
  
  const icons = {
    success: 'fa-check-circle',
    danger: 'fa-times-circle',
    warning: 'fa-exclamation-circle',
    info: 'fa-info-circle'
  };
  
  toast.innerHTML = `<i class="fas ${icons[type]}"></i> ${message}`;
  container.appendChild(toast);
  
  setTimeout(() => toast.remove(), 4000);
}

// ==================== MODAL SYSTEM ====================
function showModal(title, content, buttons = []) {
  const modalHTML = `
    <div class="modal-overlay" onclick="closeModal(event)">
      <div class="modal" onclick="event.stopPropagation()">
        <div class="modal-header">
          <span>${title}</span>
          <button class="modal-close" onclick="closeAllModals()">&times;</button>
        </div>
        <div class="modal-body">${content}</div>
        ${buttons.length > 0 ? `<div class="modal-footer">${buttons.map(b => `<button class="btn ${b.class}" onclick="${b.onclick}">${b.text}</button>`).join('')}</div>` : ''}
      </div>
    </div>
  `;
  
  document.getElementById('modalContainer').innerHTML = modalHTML;
}

function closeModal(event) {
  if (event.target.classList.contains('modal-overlay')) {
    closeAllModals();
  }
}

function closeAllModals() {
  document.getElementById('modalContainer').innerHTML = '';
}

// ==================== LOADING SPINNER ====================
function showLoading() {
  const overlay = document.createElement('div');
  overlay.className = 'loading-overlay';
  overlay.id = 'loadingOverlay';
  overlay.innerHTML = '<div class="spinner"></div>';
  document.body.appendChild(overlay);
}

function hideLoading() {
  const overlay = document.getElementById('loadingOverlay');
  if (overlay) overlay.remove();
}

// ==================== THEME TOGGLE ====================
function toggleTheme() {
  const body = document.body;
  const icon = document.getElementById('themeIcon');
  
  if (body.getAttribute('data-theme') === 'dark') {
    body.setAttribute('data-theme', 'light');
    icon.className = 'fas fa-moon';
    localStorage.setItem('dshs_theme', 'light');
  } else {
    body.setAttribute('data-theme', 'dark');
    icon.className = 'fas fa-sun';
    localStorage.setItem('dshs_theme', 'dark');
  }
}

// Load saved theme
(function loadTheme() {
  const saved = localStorage.getItem('dshs_theme');
  if (saved === 'dark') {
    document.body.setAttribute('data-theme', 'dark');
    document.getElementById('themeIcon').className = 'fas fa-sun';
  }
})();

// ==================== MENU TOGGLE ====================
function toggleMenu() {
  const menu = document.getElementById('menu');
  const overlay = document.getElementById('menuOverlay');
  menu.classList.toggle('show');
  overlay.classList.toggle('show');
}

// ==================== PASSWORD TOGGLE ====================
function togglePassword() {
  const p = document.getElementById('loginPassword');
  p.type = (p.type === 'password') ? 'text' : 'password';
}

//========= LOGIN ======

function login() {
  showLoading();
  
  setTimeout(() => {
    const username = document.getElementById('loginUsername').value.trim();
    const pass = secureHash(document.getElementById('loginPassword').value);
    let found = false;

    if (username === adminAccount.username && pass === adminAccount.password) {
      role = 'admin';
      currentUser = adminAccount.name;
      found = true;
      setSession(generateSessionToken());
    }
    
    teachers.forEach(t => {
      if (username === t.username && pass === t.password) {
        role = 'teacher';
        currentUser = t.name;
        found = true;
        setSession(generateSessionToken());
      }
    });
    
    students.forEach(s => {
      if (username === s.username && pass === s.password) {
        if (s.approved) {
          role = 'student';
          currentUser = s.name;
          found = true;
          setSession(generateSessionToken());
        } else {
          document.getElementById('msg').innerText = 'Account not approved yet';
          hideLoading();
          return;
        }
      }
    });
    
    parents.forEach(p => {
      if (username === p.username && pass === p.password) {
        role = 'parent';
        currentUser = p.child;
        found = true;
        setSession(generateSessionToken());
      }
    });

    if (!found) {
      document.getElementById('msg').innerText = 'Invalid login or not approved yet';
      hideLoading();
      return;
    }
    
    hideLoading();
    document.getElementById('login').style.display = 'none';
    document.getElementById('signup').style.display = 'none';
    document.getElementById('loginWrapper').style.display = 'none';
    document.getElementById('dashboard').style.display = 'block';
    loadDashboard();
    showToast('Welcome back, ' + currentUser + '!', 'success');
  }, 500);
}

//========= DASHBOARD ======

function loadDashboard() {
  document.getElementById('roleTitle').innerText = role.toUpperCase() + ' DASHBOARD';
  const menu = document.getElementById('menu');
  menu.innerHTML = '';
  
  let items = [
    {name: 'Attendance', icon: '📅'},
    {name: 'Subject Schedule', icon: '📚'},
    {name: 'My Info', icon: '👤'},
    {name: 'Bulletin Board', icon: '📢'},
    {name: 'School Map', icon: '🗺️'},
    {name: 'Notifications', icon: '🔔'}
  ];
  
  if (role === 'teacher') {
    items = [
      {name: 'Dashboard Home', icon: '🏠'},
      {name: 'Attendance', icon: '📅'},
      {name: 'Subject Schedule', icon: '📚'},
      {name: 'My Info', icon: '👤'},
      {name: 'Bulletin Board', icon: '📢'},
      {name: 'Grades', icon: '📊'},
      {name: 'Assignments', icon: '📝'},
      {name: 'Learning Materials', icon: '📚'},
      {name: 'Quiz/Exam', icon: '✍️'},
      {name: 'Syllabus', icon: '📋'},
      {name: 'Parent Chat', icon: '💬'},
      {name: 'My Planner', icon: '📆'},
      {name: 'School Calendar', icon: '📅'},
      {name: 'Notifications', icon: '🔔'},
      {name: 'Emergency Numbers', icon: '🚨'},
      {name: 'School Map', icon: '🗺️'}
    ];
  } else if (role === 'student') {
    items = [
      {name: 'Dashboard Home', icon: '🏠'},
      {name: 'Attendance', icon: '📅'},
      {name: 'Subject Schedule', icon: '📚'},
      {name: 'My Info', icon: '👤'},
      {name: 'Bulletin Board', icon: '📢'},
      {name: 'Grades', icon: '📊'},
      {name: 'Grade Analytics', icon: '📈'},
      {name: 'Report Card', icon: '🎓'},
      {name: 'Assignments', icon: '📝'},
      {name: 'Learning Materials', icon: '📚'},
      {name: 'Quiz/Exam', icon: '✍️'},
      {name: 'Syllabus', icon: '📋'},
      {name: 'QR Code', icon: '🔳'},
      {name: 'My Mood', icon: '😊'},
      {name: 'My Planner', icon: '📆'},
      {name: 'School Calendar', icon: '📅'},
      {name: 'Library', icon: '📖'},
      {name: 'Fees', icon: '💰'},
      {name: 'Notifications', icon: '🔔'},
      {name: 'Emergency Numbers', icon: '🚨'},
      {name: 'School Map', icon: '🗺️'}
    ];
  } else if (role === 'parent') {
    items = [
      {name: 'Dashboard Home', icon: '🏠'},
      {name: 'Child Attendance', icon: '📅'},
      {name: 'Child Grades', icon: '📊'},
      {name: 'Child Schedule', icon: '📚'},
      {name: 'Child Assignments', icon: '📝'},
      {name: 'My Info', icon: '👤'},
      {name: 'Bulletin Board', icon: '📢'},
      {name: 'Teacher Chat', icon: '💬'},
      {name: 'School Calendar', icon: '📅'},
      {name: 'Fees', icon: '💰'},
      {name: 'Notifications', icon: '🔔'},
      {name: 'Emergency Numbers', icon: '🚨'},
      {name: 'School Map', icon: '🗺️'}
    ];
  } else if (role === 'admin') {
    items = [
      {name: 'Dashboard Home', icon: '🏠'},
      {name: 'Student Approval', icon: '✅'},
      {name: 'Create Teacher', icon: '👨‍🏫'},
      {name: 'All Students', icon: '👨‍🎓'},
      {name: 'Parent Accounts', icon: '👪'},
      {name: 'Manage Users', icon: '⚙️'},
      {name: 'Bulletin Board', icon: '📢'},
      {name: 'School Calendar', icon: '📅'},
      {name: 'Library Management', icon: '📖'},
      {name: 'Data Backup', icon: '💾'},
      {name: 'Data Export', icon: '📤'},
      {name: 'Notifications', icon: '🔔'},
      {name: 'Emergency Numbers', icon: '🚨'},
      {name: 'School Map', icon: '🗺️'}
    ];
  }

  menu.innerHTML = '<div class="menu-header"><h3>🎓 DSHS Menu</h3><p>👤 ' + currentUser + '</p></div>';
  
  items.forEach(item => {
    const btn = document.createElement('button');
    btn.innerHTML = '<span class="tab-icon">' + item.icon + '</span> ' + item.name;
    btn.onclick = function() {
      toggleMenu();
      loadSection(item.name);
    };
    menu.appendChild(btn);
  });

  const logoutBtn = document.createElement('button');
  logoutBtn.innerHTML = '<span class="tab-icon">⬅</span> Logout';
  logoutBtn.className = 'logout';
  logoutBtn.onclick = function() {
    toggleMenu();
    logout();
  };
  menu.appendChild(logoutBtn);
}

//========= LOGOUT ======

function logout() {
  clearSession();
  role = '';
  currentUser = '';
  document.getElementById('dashboard').style.display = 'none';
  document.getElementById('login').style.display = 'flex';
  document.getElementById('loginWrapper').style.display = 'flex';
  document.getElementById('menu').classList.remove('show');
  document.getElementById('menuOverlay').classList.remove('show');
  document.getElementById('loginUsername').value = '';
  document.getElementById('loginPassword').value = '';
  showToast('Logged out successfully!', 'info');
}

//========= SIGNUP FUNCTIONS ======

function showSignup() {
  document.getElementById('login').style.display = 'none';
  document.getElementById('signup').style.display = 'flex';
}

function showLogin() {
  document.getElementById('signup').style.display = 'none';
  document.getElementById('login').style.display = 'flex';
}

function clearSignup() {
  ['signupName', 'signupID', 'signupSection', 'signupTrack', 'signupStrand', 'signupGradeLevel', 'signupUsername', 'signupPass'].forEach(id => {
    document.getElementById(id).value = '';
  });
}

function submitSignup() {
  const name = document.getElementById('signupName').value.trim();
  const id = document.getElementById('signupID').value.trim();
  const section = document.getElementById('signupSection').value.trim();
  const track = document.getElementById('signupTrack').value.trim();
  const strand = document.getElementById('signupStrand').value.trim();
  const gradeLevel = document.getElementById('signupGradeLevel').value.trim();
  const username = document.getElementById('signupUsername').value.trim();
  const password = document.getElementById('signupPass').value.trim();
  
  if (!name || !id || !section || !track || !strand || !gradeLevel || !username || !password) {
    showToast('All fields are required!', 'danger');
    return;
  }
  
  if (password.length < 6) {
    showToast('Password must be at least 6 characters!', 'danger');
    return;
  }
  
  if (students.find(s => s.username === username) || students.find(s => s.id === id)) {
    showToast('Username or ID already exists!', 'danger');
    return;
  }
  
  const parentUsername = 'parent' + id;
  const parentPassword = Math.random().toString(36).slice(-6);
  
  students.push({
    name, id, section, track, strand, gradeLevel,
    username, password: secureHash(password), approved: false, pic: ''
  });
  
  gradesData[name] = {};
  subjects.forEach(sub => gradesData[name][sub] = { q1: 0, q2: 0, q3: 0, q4: 0 });
  attendanceData[name] = {};
  
  parents.push({
    name: 'Parent of ' + name,
    child: name,
    username: parentUsername,
    password: secureHash(parentPassword)
  });
  
  let parentAccounts = JSON.parse(localStorage.getItem('dshs_parentAccounts')) || [];
  parentAccounts.push({ studentName: name, studentId: id, section, parentUsername, parentPassword });
  localStorage.setItem('dshs_parentAccounts', JSON.stringify(parentAccounts));
  
  saveData();
  showToast('Signup successful! Wait for admin approval.', 'success');
  setTimeout(() => {
    clearSignup();
    showLogin();
  }, 2000);
}

//========= LOAD SECTION ======

function loadSection(tab) {
  const content = document.getElementById('content');
  content.innerHTML = '';
  const section = document.createElement('div');
  section.className = 'section';
  
  // Dashboard Home
  if (tab === 'Dashboard Home') {
    section.innerHTML = `
      <h3>🏠 Dashboard Home</h3>
      <div class="d-flex gap-2 flex-wrap">
        <div class="card" style="flex:1;min-width:200px;">
          <h4>👤 Profile</h4>
          <p>Welcome, ${currentUser}!</p>
          <p class="text-muted">Role: ${role.charAt(0).toUpperCase() + role.slice(1)}</p>
        </div>
        <div class="card" style="flex:1;min-width:200px;">
          <h4>📅 Today's Date</h4>
          <p>${new Date().toLocaleDateString('en-US', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' })}</p>
        </div>
        <div class="card" style="flex:1;min-width:200px;">
          <h4>🔔 Notifications</h4>
          <p>${notifications.length} unread notifications</p>
        </div>
      </div>
    `;
    
    if (role === 'student') {
      const student = students.find(s => s.name === currentUser);
      if (student) {
        section.innerHTML += `
          <div class="card mt-2">
            <h4>📚 Quick Stats</h4>
            <div class="d-flex gap-2 flex-wrap">
              <div class="analytics-card" style="flex:1;">
                <div class="analytics-number">${subjects.length}</div>
                <div class="analytics-label">Subjects</div>
              </div>
              <div class="analytics-card" style="flex:1;">
                <div class="analytics-number">${Object.keys(attendanceData[currentUser] || {}).length}</div>
                <div class="analytics-label">Attendance Days</div>
              </div>
              <div class="analytics-card" style="flex:1;">
                <div class="analytics-number">${assignments.filter(a => a.student === currentUser && !a.submitted).length}</div>
                <div class="analytics-label">Pending Tasks</div>
              </div>
            </div>
          </div>
        `;
      }
    }
  }
  
  // Attendance
  if (tab === 'Attendance' || tab === 'Child Attendance') {
    section.innerHTML = '<h3>📅 Attendance</h3>';
    
    let studentName = currentUser;
    if (role === 'teacher') {
      const selectStudent = document.createElement('select');
      selectStudent.id = 'attendanceStudentSelect';
      const teacher = teachers.find(t => t.name === currentUser);
      students.filter(s => s.section === teacher.sectionHandled).forEach(s => {
        const opt = document.createElement('option');
        opt.value = s.name;
        opt.innerText = s.name;
        selectStudent.appendChild(opt);
      });
      section.appendChild(selectStudent);
      studentName = selectStudent.value;
      
      selectStudent.onchange = function() {
        studentName = this.value;
        renderAttendanceCalendar(section, studentName);
      };
    } else if (role === 'parent') {
      const selectStudent = document.createElement('select');
      selectStudent.id = 'attendanceStudentSelect';
      const parent = parents.find(p => p.child === currentUser);
      if (parent) {
        const child = students.find(s => s.name === parent.child);
        if (child) {
          const opt = document.createElement('option');
          opt.value = child.name;
          opt.innerText = child.name;
          selectStudent.appendChild(opt);
          studentName = child.name;
        }
      }
      section.appendChild(selectStudent);
    }
    
    const dateInput = document.createElement('input');
    dateInput.type = 'month';
    dateInput.value = new Date().toISOString().split('T')[0].substring(0, 7);
    section.appendChild(dateInput);
    
    const qrDiv = document.createElement('div');
    qrDiv.id = 'scanner-container';
    section.appendChild(qrDiv);
    
    const resultDiv = document.createElement('div');
    resultDiv.id = 'scanner-result';
    section.appendChild(resultDiv);
    
    content.appendChild(section);
    
    renderAttendanceCalendar(section, studentName);
    
    if (role === 'teacher') {
      const scannerDiv = document.createElement('div');
      scannerDiv.id = 'qr-scanner';
      scannerDiv.className = 'qr-scanner-container';
      scannerDiv.style.marginTop = '20px';
      section.appendChild(scannerDiv);
      
      const scannerResult = document.createElement('div');
      scannerResult.id = 'scanner-result';
      scannerResult.className = 'scanner-result';
      scannerResult.style.display = 'none';
      section.appendChild(scannerResult);
      
      setTimeout(() => {
        try {
          const html5QrCode = new Html5Qrcode('qr-scanner');
          html5QrCode.start(
            { facingMode: 'environment' },
            { fps: 10, qrbox: 250 },
            decodedText => {
              const parts = decodedText.split('-');
              const scannedStudent = parts[0];
              const today = new Date().toISOString().split('T')[0];
              
              if (attendanceData[scannedStudent]) {
                attendanceData[scannedStudent][today] = 'P';
                saveData();
                const resultDiv = document.getElementById('scanner-result');
                resultDiv.style.display = 'block';
                resultDiv.className = 'scanner-result success';
                resultDiv.innerHTML = '✅ Marked ' + scannedStudent + ' present on ' + today;
                renderAttendanceCalendar(section, studentName);
              }
              html5QrCode.stop();
            },
            errorMessage => {}
          ).catch(err => {
            console.log('Scanner error:', err);
            const scannerResult = document.getElementById('scanner-result');
            if (scannerResult) {
              scannerResult.style.display = 'block';
              scannerResult.className = 'scanner-result error';
              scannerResult.innerHTML = '❌ Camera access denied or not available';
            }
          });
        } catch (e) {
          console.log('Scanner initialization error:', e);
          const scannerResult = document.getElementById('scanner-result');
          if (scannerResult) {
            scannerResult.style.display = 'block';
            scannerResult.className = 'scanner-result error';
            scannerResult.innerHTML = '❌ QR Scanner not supported on this device';
          }
        }
      }, 500);
    }
  }
  
  // Grades
  if (tab === 'Grades' || tab === 'Child Grades') {
    section.innerHTML = '<h3>📊 Grades</h3>';
    
    const semSelector = document.createElement('div');
    semSelector.className = 'sem-selector';
    semSelector.innerHTML = `
      <button class="sem-btn active" onclick="selectSemester(1, this)">1st Semester</button>
      <button class="sem-btn" onclick="selectSemester(2, this)">2nd Semester</button>
    `;
    section.appendChild(semSelector);
    
    const quarterSelector = document.createElement('div');
    quarterSelector.className = 'quarter-selector';
    quarterSelector.id = 'quarterSelector';
    quarterSelector.innerHTML = `
      <button class="quarter-btn active" onclick="selectQuarter(1, this)">1st Quarter</button>
      <button class="quarter-btn" onclick="selectQuarter(2, this)">2nd Quarter</button>
      <button class="quarter-btn" onclick="selectQuarter(3, this)">3rd Quarter</button>
      <button class="quarter-btn" onclick="selectQuarter(4, this)">4th Quarter</button>
    `;
    section.appendChild(quarterSelector);
    
    let studentName = currentUser;
    if (role === 'teacher') {
      const selectStudent = document.createElement('select');
      selectStudent.id = 'gradesStudentSelect';
      const teacher = teachers.find(t => t.name === currentUser);
      students.filter(s => s.section === teacher.sectionHandled).forEach(s => {
        const opt = document.createElement('option');
        opt.value = s.name;
        opt.innerText = s.name;
        selectStudent.appendChild(opt);
      });
      section.appendChild(selectStudent);
      studentName = selectStudent.value;
      
              selectStudent.onchange = function() {
          studentName = this.value;
          renderGradesTable(section, studentName);
        };
      } else if (role === 'parent') {
        const parent = parents.find(p => p.child === currentUser);
        if (parent) {
          const child = students.find(s => s.name === parent.child);
          if (child) studentName = child.name;
        }
      }
      
      content.appendChild(section);
      renderGradesTable(section, studentName);
    }
    
    // Grade Analytics
    if (tab === 'Grade Analytics' && role === 'student') {
      section.innerHTML = '<h3>📈 Grade Analytics</h3>';
      
      const student = students.find(s => s.name === currentUser);
      if (student && gradesData[currentUser]) {
        const subjectsList = Object.keys(gradesData[currentUser]);
        const grades = subjectsList.map(sub => {
          const data = gradesData[currentUser][sub];
          return { subject: sub, grade: (data.q1 + data.q2 + data.q3 + data.q4) / 4 };
        });
        
        const avgGrade = grades.reduce((sum, g) => sum + g.grade, 0) / grades.length;
        
        section.innerHTML += `
          <div class="d-flex gap-2 flex-wrap mb-2">
            <div class="analytics-card" style="flex:1;">
              <div class="analytics-number">${avgGrade.toFixed(2)}</div>
              <div class="analytics-label">Average Grade</div>
            </div>
            <div class="analytics-card" style="flex:1;">
              <div class="analytics-number">${grades.filter(g => g.grade >= 75).length}</div>
              <div class="analytics-label">Passing Subjects</div>
            </div>
            <div class="analytics-card" style="flex:1;">
              <div class="analytics-number">${grades.filter(g => g.grade < 75).length}</div>
              <div class="analytics-label">Needs Improvement</div>
            </div>
          </div>
          
          <div class="card">
            <h4>📊 Grade Distribution</h4>
            <div class="grade-chart" id="gradeChart"></div>
          </div>
        `;
        
        setTimeout(() => {
          const chartContainer = document.getElementById('gradeChart');
          if (chartContainer && grades.length > 0) {
            const maxGrade = Math.max(...grades.map(g => g.grade));
            grades.forEach(g => {
              const bar = document.createElement('div');
              bar.className = 'grade-bar';
              const height = (g.grade / 100) * 150;
              bar.style.height = height + 'px';
              bar.innerHTML = `
                <span class="grade-bar-value">${g.grade.toFixed(0)}</span>
                <span class="grade-bar-label">${g.subject.substring(0, 8)}</span>
              `;
              chartContainer.appendChild(bar);
            });
          }
        }, 100);
      }
    }
    
    // Report Card
    if (tab === 'Report Card' && role === 'student') {
      section.innerHTML = '<h3>🎓 Report Card</h3>';
      
      const student = students.find(s => s.name === currentUser);
      if (student && gradesData[currentUser]) {
        section.innerHTML = `
          <div class="report-card" id="reportCard">
            <div class="report-header">
              <div class="report-school-name">🎓 DUMINGAG SENIOR HIGH SCHOOL</div>
              <p>Dumingag, Zamboanga del Sur</p>
              <h2>REPORT CARD</h2>
            </div>
            
            <div class="report-student-info">
              <div><strong>Name:</strong> ${student.name}</div>
              <div><strong>ID No:</strong> ${student.id}</div>
              <div><strong>Section:</strong> ${student.section}</div>
              <div><strong>Grade Level:</strong> ${student.gradeLevel}</div>
              <div><strong>Track:</strong> ${student.track}</div>
              <div><strong>Strand:</strong> ${student.strand}</div>
            </div>
            
            <div class="report-subject-grades">
              <table>
                <thead>
                  <tr>
                    <th>Subject</th>
                    <th>Q1</th>
                    <th>Q2</th>
                    <th>Q3</th>
                    <th>Q4</th>
                    <th>Average</th>
                  </tr>
                </thead>
                <tbody>
        `;
        
        let totalQ1 = 0, totalQ2 = 0, totalQ3 = 0, totalQ4 = 0;
        const subjectsList = Object.keys(gradesData[currentUser]);
        
        subjectsList.forEach(sub => {
          const data = gradesData[currentUser][sub];
          const avg = (data.q1 + data.q2 + data.q3 + data.q4) / 4;
          totalQ1 += data.q1;
          totalQ2 += data.q2;
          totalQ3 += data.q3;
          totalQ4 += data.q4;
          
          let gradeClass = 'grade-a';
          if (avg < 60) gradeClass = 'grade-f';
          else if (avg < 70) gradeClass = 'grade-d';
          else if (avg < 80) gradeClass = 'grade-c';
          else if (avg < 90) gradeClass = 'grade-b';
          
          section.innerHTML += `
            <tr>
              <td>${sub}</td>
              <td>${data.q1}</td>
              <td>${data.q2}</td>
              <td>${data.q3}</td>
              <td>${data.q4}</td>
              <td class="${gradeClass}"><strong>${avg.toFixed(2)}</strong></td>
            </tr>
          `;
        });
        
        const overallAvg = (totalQ1 + totalQ2 + totalQ3 + totalQ4) / (subjectsList.length * 4);
        
        section.innerHTML += `
                  <tr style="background: #f0f0f0;">
                    <td><strong>Overall Average</strong></td>
                    <td><strong>${(totalQ1 / subjectsList.length).toFixed(2)}</strong></td>
                    <td><strong>${(totalQ2 / subjectsList.length).toFixed(2)}</strong></td>
                    <td><strong>${(totalQ3 / subjectsList.length).toFixed(2)}</strong></td>
                    <td><strong>${(totalQ4 / subjectsList.length).toFixed(2)}</strong></td>
                    <td><strong>${overallAvg.toFixed(2)}</strong></td>
                  </tr>
                </tbody>
              </table>
            </div>
            
            <div class="report-footer">
              <p>Generated on: ${new Date().toLocaleDateString()}</p>
              <p>DSHS School System</p>
            </div>
          </div>
          
          <button class="btn btn-primary mt-2" onclick="window.print()">
            <i class="fas fa-print"></i> Print Report Card
          </button>
        `;
      }
    }
    
    // Subject Schedule
    if (tab === 'Subject Schedule' || tab === 'Child Schedule') {
      section.innerHTML = '<h3>📚 Subject Schedule</h3>';
      
      let studentName = currentUser;
      if (role === 'parent') {
        const parent = parents.find(p => p.child === currentUser);
        if (parent) {
          const child = students.find(s => s.name === parent.child);
          if (child) studentName = child.name;
        }
      }
      
      const scheduleBox = document.createElement('div');
      scheduleBox.className = 'schedule-box';
      
      subjects.forEach(sub => {
        const div = document.createElement('div');
        const time = scheduleTimes[sub] || 'TBA';
        div.innerHTML = '<strong>' + sub + '</strong><br>' + time;
        scheduleBox.appendChild(div);
      });
      section.appendChild(scheduleBox);
      
      if (role === 'teacher' || role === 'admin') {
        section.innerHTML += '<h4>Manage Subjects</h4>';
        subjects.forEach((sub, index) => {
          const item = document.createElement('div');
          item.className = 'subject-item';
          item.innerHTML = '<input type="text" value="' + sub + '" onchange="updateSubject(' + index + ', this.value)">' +
            '<input type="text" value="' + (scheduleTimes[sub] || '') + '" placeholder="Time" onchange="updateScheduleTime(\'' + sub + '\', this.value)">' +
            '<button onclick="deleteSubject(' + index + ')" style="width:auto;background:#dc3545;color:white;">🗑️ Delete</button>';
          section.appendChild(item);
        });
        
        const addDiv = document.createElement('div');
        addDiv.className = 'subject-item';
        addDiv.innerHTML = '<input type="text" id="newSubjectName" placeholder="New Subject">' +
          '<input type="text" id="newSubjectTime" placeholder="Time">' +
          '<button onclick="addSubject()" style="width:auto;background:#28a745;color:white;">➕ Add</button>';
        section.appendChild(addDiv);
      }
    }
    
    // QR Code
    if (tab === 'QR Code' && role === 'student') {
      section.innerHTML = '<h3>🔳 Your QR Code</h3>';
      
      const student = students.find(s => s.name === currentUser);
      const studentId = student ? student.id : 'ST000';
      const studentSection = student ? student.section : 'Unknown';
      
      const qrDiv = document.createElement('div');
      qrDiv.id = 'qr-code';
      qrDiv.style.textAlign = 'center';
      qrDiv.style.padding = '20px';
      section.appendChild(qrDiv);
      
      const qrCodeData = currentUser + '-' + studentId + '-' + studentSection;
      new QRCode(qrDiv, {
        text: qrCodeData,
        width: 200,
        height: 200,
        colorDark: '#003366',
        colorLight: '#ffffff',
        correctLevel: QRCode.CorrectLevel.H
      });
      
      section.innerHTML += '<p style="text-align:center;margin-top:15px;">📱 Scan this QR code for attendance</p>';
      
      const perfBox = document.createElement('div');
      perfBox.className = 'performance-box';
      const totalDays = Object.keys(attendanceData[currentUser] || {}).length;
      const presentDays = Object.values(attendanceData[currentUser] || {}).filter(s => s === 'P').length;
      const absentDays = totalDays - presentDays;
      const percentage = totalDays > 0 ? Math.round((presentDays / totalDays) * 100) : 0;
      
      perfBox.innerHTML = '<h3>📈 Your Attendance Performance</h3>' +
        '<div class="performance-stats">' +
        '<div class="stat-item"><div class="stat-number">' + presentDays + '</div><div class="stat-label">✅ Present</div></div>' +
        '<div class="stat-item"><div class="stat-number">' + absentDays + '</div><div class="stat-label">❌ Absent</div></div>' +
        '<div class="stat-item"><div class="stat-number">' + percentage + '%</div><div class="stat-label">📊 Rate</div></div>' +
        '</div>';
      section.appendChild(perfBox);
    }
    
    // Chat
    if (tab === 'Parent Chat' || tab === 'Teacher Chat') {
      section.innerHTML = '<h3>💬 ' + tab + '</h3>';
      
      if (tab === 'Parent Chat' && role === 'teacher') {
        section.innerHTML += '<label>Select Parent:</label>';
        const parentSelect = document.createElement('select');
        parentSelect.id = 'chatParentSelect';
        
        const teacher = teachers.find(t => t.name === currentUser);
        if (teacher) {
          students.filter(s => s.section === teacher.sectionHandled).forEach(s => {
            const parent = parents.find(p => p.child === s.name);
            if (parent) {
              const opt = document.createElement('option');
              opt.value = parent.username;
              opt.innerText = parent.name;
              parentSelect.appendChild(opt);
            }
          });
        }
        section.appendChild(parentSelect);
      }
      
      if (tab === 'Teacher Chat' && role === 'parent') {
        section.innerHTML += '<label>Select Teacher:</label>';
        const teacherSelect = document.createElement('select');
        teacherSelect.id = 'chatTeacherSelect';
        
        const parent = parents.find(p => p.child === currentUser);
        if (parent) {
          const child = students.find(s => s.name === parent.child);
          if (child) {
            teachers.filter(t => t.sectionHandled === child.section).forEach(t => {
              const opt = document.createElement('option');
              opt.value = t.username;
              opt.innerText = t.name;
              teacherSelect.appendChild(opt);
            });
          }
        }
        section.appendChild(teacherSelect);
      }
      
      const chatbox = document.createElement('div');
      chatbox.id = 'chatbox';
      chatbox.className = 'chatbox';
      chatbox.innerHTML = '<p>💬 Chat messages will appear here...</p>';
      section.appendChild(chatbox);
      
      const input = document.createElement('input');
      input.type = 'text';
      input.id = 'chatInput';
      input.placeholder = 'Type your message...';
      section.appendChild(input);
      
      const sendBtn = document.createElement('button');
      sendBtn.innerHTML = '<i class="fas fa-paper-plane"></i> Send';
      sendBtn.onclick = function() { sendChatMessage(tab); };
      section.appendChild(sendBtn);
    }
    
    // My Info
    if (tab === 'My Info') {
      section.innerHTML = '<h3>👤 My Information</h3>';
      
      let user = null;
      
      if (role === 'student') {
        user = students.find(s => s.name === currentUser);
      } else if (role === 'teacher') {
        user = teachers.find(t => t.name === currentUser);
      } else if (role === 'parent') {
        user = parents.find(p => p.child === currentUser);
      } else if (role === 'admin') {
        user = adminAccount;
      }
      
      if (user) {
        section.innerHTML += '<div class="profile-card">' +
          '<div class="profile-photo">' +
          '<img id="profilePic" src="' + (user.pic || '') + '" alt="Profile Photo" onerror="this.src=\'https://via.placeholder.com/120\'">' +
          '</div>' +
          '<h3>' + user.name + '</h3>' +
          '<p>' + (user.section || user.sectionHandled || user.position || 'User') + '</p>' +
          '</div>';
        
        section.innerHTML += '<div style="text-align:center;margin-bottom:20px;">' +
          '<input type="file" id="uploadPic" accept="image/*" style="width:auto;">' +
          '<button onclick="uploadProfilePhoto()" style="width:auto;background:linear-gradient(135deg, #8B0000 0%, #003366 100%);color:white;padding:10px 20px;">📷 Upload Photo</button>' +
          '</div>';
        
        const detailsDiv = document.createElement('div');
        detailsDiv.className = 'profile-details';
        
        let detailsHTML = '';
        if (user.id) detailsHTML += '<div class="detail-row"><span class="detail-label">🆔 ID:</span><span class="detail-value">' + user.id + '</span></div>';
        if (user.username) detailsHTML += '<div class="detail-row"><span class="detail-label">👤 Username:</span><span class="detail-value">' + user.username + '</span></div>';
        if (user.section) detailsHTML += '<div class="detail-row"><span class="detail-label">🏫 Section:</span><span class="detail-value">' + user.section + '</span></div>';
        if (user.sectionHandled) detailsHTML += '<div class="detail-row"><span class="detail-label">🏫 Section Handled:</span><span class="detail-value">' + user.sectionHandled + '</span></div>';
        if (user.track) detailsHTML += '<div class="detail-row"><span class="detail-label">📚 Track:</span><span class="detail-value">' + user.track + '</span></div>';
        if (user.strand) detailsHTML += '<div class="detail-row"><span class="detail-label">🎯 Strand:</span><span class="detail-value">' + user.strand + '</span></div>';
        if (user.gradeLevel) detailsHTML += '<div class="detail-row"><span class="detail-label">📖 Grade Level:</span><span class="detail-value">' + user.gradeLevel + '</span></div>';
        if (user.position) detailsHTML += '<div class="detail-row"><span class="detail-label">💼 Position:</span><span class="detail-value">' + user.position + '</span></div>';
        
        detailsDiv.innerHTML = detailsHTML;
        section.appendChild(detailsDiv);
      } else {
        section.innerHTML += '<p>❌ User information not found.</p>';
      }
    }
    
    // Bulletin Board
    if (tab === 'Bulletin Board') {
      section.innerHTML = '<h3>📢 Bulletin Board</h3>';
      
      const board = document.createElement('div');
      bulletinBoard.forEach((msg, index) => {
        const msgDiv = document.createElement('div');
        msgDiv.style.padding = '18px';
        msgDiv.style.borderBottom = '2px solid #ddd';
        msgDiv.style.marginBottom = '12px';
        msgDiv.style.borderRadius = '8px';
        msgDiv.style.background = '#f8f9fa';
        msgDiv.innerHTML = '<p>' + msg + '</p>';
        
        if (role === 'teacher' || role === 'admin') {
          const deleteBtn = document.createElement('button');
          deleteBtn.innerHTML = '<i class="fas fa-trash"></i> Delete';
          deleteBtn.style.width = 'auto';
          deleteBtn.style.background = '#dc3545';
          deleteBtn.style.color = 'white';
          deleteBtn.style.padding = '8px 15px';
          deleteBtn.onclick = function() {
            bulletinBoard.splice(index, 1);
            saveData();
            loadSection('Bulletin Board');
          };
          msgDiv.appendChild(deleteBtn);
        }
        
        board.appendChild(msgDiv);
      });
      section.appendChild(board);
      
      if (role === 'teacher' || role === 'admin') {
        const newMsg = document.createElement('input');
        newMsg.id = 'newAnnouncement';
        newMsg.placeholder = 'Type new announcement...';
        section.appendChild(newMsg);
        
        const addBtn = document.createElement('button');
        addBtn.innerHTML = '<i class="fas fa-plus"></i> Add Announcement';
        addBtn.style.background = 'linear-gradient(135deg, #8B0000 0%, #003366 100%)';
        addBtn.style.color = 'white';
        addBtn.onclick = function() {
          if (newMsg.value.trim()) {
            bulletinBoard.push(newMsg.value.trim());
            saveData();
            loadSection('Bulletin Board');
          }
        };
        section.appendChild(addBtn);
      }
    }
    
    // Admin Functions
    if (role === 'admin') {
      // Student Approval
      if (tab === 'Student Approval') {
        section.innerHTML = '<h3>✅ Approve Students</h3>';
        const pendingStudents = students.filter(s => !s.approved);
        
        if (pendingStudents.length === 0) {
          section.innerHTML += '<p>✅ No pending approvals.</p>';
        } else {
          pendingStudents.forEach(s => {
            const div = document.createElement('div');
            div.style.padding = '18px';
            div.style.border = '2px solid #ddd';
            div.style.marginBottom = '12px';
            div.style.borderRadius = '10px';
            div.style.background = '#fff3cd';
            div.innerHTML = '<p><strong>👤 Name:</strong> ' + s.name + '</p>' +
              '<p><strong>🆔 ID:</strong> ' + s.id + '</p>' +
              '<p><strong>🏫 Section:</strong> ' + s.section + '</p>' +
              '<button onclick="approveStudent(\'' + s.id + '\')" style="background:#28a745;color:white;width:auto;padding:12px 24px;margin-right:10px;">✅ Approve</button>' +
              '<button onclick="deleteStudent(\'' + s.id + '\')" style="background:#dc3545;color:white;width:auto;padding:12px 24px;">🗑️ Delete</button>';
            section.appendChild(div);
          });
        }
      }
      
      // Create Teacher
      if (tab === 'Create Teacher') {
        section.innerHTML = '<h3>👨‍🏫 Create Teacher Account</h3>';
        section.innerHTML += '<input type="text" id="newTeacherName" placeholder="👤 Full Name">' +
          '<input type="text" id="newTeacherID" placeholder="🆔 Teacher ID">' +
          '<input type="text" id="newTeacherPosition" placeholder="💼 Position">' +
          '<input type="text" id="newTeacherSection" placeholder="🏫 Section Handled">' +
          '<input type="text" id="newTeacherUsername" placeholder="👤 Username">' +
          '<input type="password" id="newTeacherPassword" placeholder="🔒 Password">' +
          '<button onclick="createTeacher()" style="background:linear-gradient(135deg, #8B0000 0%, #003366 100%);color:white;padding:14px;">👨‍🏫 Create Teacher</button>';
      }
      
      // All Students
      if (tab === 'All Students') {
        section.innerHTML = '<h3>👨‍🎓 All Students</h3>';
        
        const printControls = document.createElement('div');
        printControls.className = 'print-controls';
        printControls.innerHTML = '<h4>🖨️ Print ID Cards</h4>' +
          '<p>Check the students you want to print, then click Print Selected.</p>' +
          '<label><input type="checkbox" id="selectAllStudents" onchange="toggleSelectAllStudents()" style="width:auto;"> ✅ Select All</label><br><br>' +
          '<button onclick="printSelectedIDs()" style="background:#28a745;color:white;width:auto;padding:12px 24px;">🖨️ Print Selected</button>';
        section.appendChild(printControls);
        
        const filterSection = document.createElement('select');
        filterSection.id = 'filterSection';
        filterSection.innerHTML = "<option value='all'>📋 All Sections</option>";
        const sections = [...new Set(students.map(s => s.section))];
        sections.forEach(sec => {
          const opt = document.createElement('option');
          opt.value = sec;
          opt.innerText = sec;
          filterSection.appendChild(opt);
        });
        section.appendChild(filterSection);
        
        const studentsContainer = document.createElement('div');
        studentsContainer.id = 'studentsContainer';
        section.appendChild(studentsContainer);
        
        filterSection.onchange = function() {
          renderStudentsBySection(studentsContainer, this.value);
        };
        
        renderStudentsBySection(studentsContainer, 'all');
      }
      
      // Parent Accounts
      if (tab === 'Parent Accounts') {
        section.innerHTML = '<h3>👪 Parent Accounts</h3>';
        section.innerHTML += '<p>📝 These credentials are auto-generated when students sign up.</p>';
        
        const filterSection = document.createElement('select');
        filterSection.id = 'filterParentSection';
        filterSection.innerHTML = "<option value='all'>📋 All Sections</option>";
        const sections = [...new Set(students.map(s => s.section))];
        sections.forEach(sec => {
          const opt = document.createElement('option');
          opt.value = sec;
          opt.innerText = sec;
          filterSection.appendChild(opt);
        });
        section.appendChild(filterSection);
        
        const parentContainer = document.createElement('div');
        parentContainer.id = 'parentContainer';
        section.appendChild(parentContainer);
        
        filterSection.onchange = function() {
          renderParentAccounts(parentContainer, this.value);
        };
        
        renderParentAccounts(parentContainer, 'all');
      }
      
      // Manage Users
      if (tab === 'Manage Users') {
        section.innerHTML = '<h3>⚙️ Manage Users</h3>';
        
        section.innerHTML += '<h4>👨‍🎓 Students</h4>';
        const studentsTable = document.createElement('table');
        studentsTable.innerHTML = '<tr><th>Name</th><th>ID</th><th>Section</th><th>Approved</th><th>Action</th></tr>';
        students.forEach(s => {
          const tr = document.createElement('tr');
          tr.innerHTML = '<td>' + s.name + '</td><td>' + s.id + '</td><td>' + s.section + '</td><td>' + (s.approved ? '✅' : '⏳') + '</td>' +
            '<td><button onclick="deleteStudent(\'' + s.id + '\')" style="background:#dc3545;color:white;width:auto;padding:6px 12px;">🗑️ Delete</button></td>';
          studentsTable.appendChild(tr);
        });
        section.appendChild(studentsTable);
        
        section.innerHTML += '<h4 style="margin-top:25px;">👨‍🏫 Teachers</h4>';
        const teachersTable = document.createElement('table');
        teachersTable.innerHTML = '<tr><th>Name</th><th>ID</th><th>Section</th><th>Action</th></tr>';
        teachers.forEach(t => {
          const tr = document.createElement('tr');
          tr.innerHTML = '<td>' + t.name + '</td><td>' + t.id + '</td><td>' + t.sectionHandled + '</td>' +
            '<td><button onclick="deleteTeacher(\'' + t.id + '\')" style="background:#dc3545;color:white;width:auto;padding:6px 12px;">🗑️ Delete</button></td>';
          teachersTable.appendChild(tr);
        });
        section.appendChild(teachersTable);
      }
      
      // Library Management
      if (tab === 'Library Management') {
        section.innerHTML = '<h3>📖 Library Management</h3>';
        
        section.innerHTML += '<button class="btn btn-primary mb-2" onclick="showAddBookModal()"><i class="fas fa-plus"></i> Add Book</button>';
        
        const libraryContainer = document.createElement('div');
        libraryContainer.id = 'libraryContainer';
        section.appendChild(libraryContainer);
        
        renderLibraryBooks(libraryContainer);
      }
      
      // Data Backup
      if (tab === 'Data Backup') {
        section.innerHTML = '<h3>💾 Data Backup</h3>';
        
        section.innerHTML += `
          <div class="backup-option">
            <div class="backup-icon"><i class="fas fa-download"></i></div>
            <div class="backup-info">
              <h4>Backup Data</h4>
              <p>Download all school data as JSON file</p>
            </div>
            <button class="btn btn-primary" onclick="backupData()"><i class="fas fa-download"></i> Backup</button>
          </div>
          
          <div class="backup-option">
            <div class="backup-icon"><i class="fas fa-upload"></i></div>
            <div class="backup-info">
              <h4>Restore Data</h4>
              <p>Restore school data from backup file</p>
            </div>
            <input type="file" id="restoreFile" accept=".json" style="width:auto;">
            <button class="btn btn-warning" onclick="restoreData()"><i class="fas fa-upload"></i> Restore</button>
          </div>
          
          <div class="backup-option">
            <div class="backup-icon"><i class="fas fa-trash"></i></div>
            <div class="backup-info">
              <h4>Clear All Data</h4>
              <p>Delete all data and reset to default</p>
            </div>
            <button class="btn btn-danger" onclick="clearAllData()"><i class="fas fa-trash"></i> Clear</button>
          </div>
        `;
      }
      
      // Data Export
      if (tab === 'Data Export') {
        section.innerHTML = '<h3>📤 Data Export</h3>';
        
        section.innerHTML += '<p>Export school data in various formats:</p>';
        
        const exportOptions = document.createElement('div');
        exportOptions.className = 'export-options';
        exportOptions.innerHTML = `
          <div class="export-btn" onclick="exportData('students')">
            <i class="fas fa-users"></i>
            <span>Students</span>
          </div>
          <div class="export-btn" onclick="exportData('teachers')">
            <i class="fas fa-chalkboard-teacher"></i>
            <span>Teachers</span>
          </div>
          <div class="export-btn" onclick="exportData('grades')">
            <i class="fas fa-chart-bar"></i>
            <span>Grades</span>
          </div>
          <div class="export-btn" onclick="exportData('attendance')">
            <i class="fas fa-calendar-check"></i>
            <span>Attendance</span>
          </div>
          <div class="export-btn" onclick="exportData('all')">
            <i class="fas fa-database"></i>
            <span>All Data</span>
          </div>
        `;
        section.appendChild(exportOptions);
      }
    }
    
    // My Planner
    if (tab === 'My Planner' && (role === 'teacher' || role === 'student')) {
      section.innerHTML = '<h3>📆 My Planner</h3>';
      
      if (!plannerData[currentUser]) {
        plannerData[currentUser] = { daily: [], weekly: [], monthly: [] };
      }
      
      const plannerContainer = document.createElement('div');
      plannerContainer.className = 'planner-container';
      
      // Daily Goals
      const dailySection = document.createElement('div');
      dailySection.className = 'planner-section';
      dailySection.innerHTML = '<h4>📅 Daily Goals</h4>';
      plannerData[currentUser].daily.forEach((goal, index) => {
        const item = document.createElement('div');
        item.className = 'planner-item' + (goal.completed ? ' completed' : '');
        item.innerHTML = '<input type="checkbox"' + (goal.completed ? ' checked' : '') + ' onchange="togglePlannerGoal(\'daily\', ' + index + ')">' +
          '<span class="goal-text">' + goal.text + '</span>' +
          '<span class="goal-time">' + (goal.time || '') + '</span>' +
          '<button class="alarm-btn" onclick="setAlarm(\'' + goal.time + '\')">⏰</button>' +
          '<button onclick="deletePlannerGoal(\'daily\', ' + index + ')" style="width:auto;background:#dc3545;color:white;padding:6px 10px;">×</button>';
        dailySection.appendChild(item);
      });
      dailySection.innerHTML += '<input type="text" id="dailyGoalInput" placeholder="Add daily goal..." style="width:55%;">' +
        '<input type="time" id="dailyGoalTime" style="width:auto;">' +
        '<button onclick="addPlannerGoal(\'daily\')" style="width:auto;background:#28a745;color:white;">➕ Add</button>';
      plannerContainer.appendChild(dailySection);
      
      // Weekly Goals
      const weeklySection = document.createElement('div');
      weeklySection.className = 'planner-section';
      weeklySection.innerHTML = '<h4>📆 Weekly Goals</h4>';
      plannerData[currentUser].weekly.forEach((goal, index) => {
        const item = document.createElement('div');
        item.className = 'planner-item' + (goal.completed ? ' completed' : '');
        item.innerHTML = '<input type="checkbox"' + (goal.completed ? ' checked' : '') + ' onchange="togglePlannerGoal(\'weekly\', ' + index + ')">' +
          '<span class="goal-text">' + goal.text + '</span>' +
          '<span class="goal-time">' + (goal.time || '') + '</span>' +
          '<button onclick="deletePlannerGoal(\'weekly\', ' + index + ')" style="width:auto;background:#dc3545;color:white;padding:6px 10px;">×</button>';
        weeklySection.appendChild(item);
      });
      weeklySection.innerHTML += '<input type="text" id="weeklyGoalInput" placeholder="Add weekly goal..." style="width:55%;">' +
        '<input type="date" id="weeklyGoalDate" style="width:auto;">' +
        '<button onclick="addPlannerGoal(\'weekly\')" style="width:auto;background:#28a745;color:white;">➕ Add</button>';
      plannerContainer.appendChild(weeklySection);
      
      // Monthly Goals
      const monthlySection = document.createElement('div');
      monthlySection.className = 'planner-section';
      monthlySection.innerHTML = '<h4>📆 Monthly Goals</h4>';
      plannerData[currentUser].monthly.forEach((goal, index) => {
        const item = document.createElement('div');
        item.className = 'planner-item' + (goal.completed ? ' completed' : '');
        item.innerHTML = '<input type="checkbox"' + (goal.completed ? ' checked' : '') + ' onchange="togglePlannerGoal(\'monthly\', ' + index + ')">' +
          '<span class="goal-text">' + goal.text + '</span>' +
          '<span class="goal-time">' + (goal.time || '') + '</span>' +
          '<button onclick="deletePlannerGoal(\'monthly\', ' + index + ')" style="width:auto;background:#dc3545;color:white;padding:6px 10px;">×</button>';
        monthlySection.appendChild(item);
      });
      monthlySection.innerHTML += '<input type="text" id="monthlyGoalInput" placeholder="Add monthly goal..." style="width:55%;">' +
        '<input type="date" id="monthlyGoalDate" style="width:auto;">' +
        '<button onclick="addPlannerGoal(\'monthly\')" style="width:auto;background:#28a745;color:white;">➕ Add</button>';
      plannerContainer.appendChild(monthlySection);
      
      section.appendChild(plannerContainer);
    }
    
    // My Mood
    if (tab === 'My Mood' && role === 'student') {
      section.innerHTML = '<h3>🤗 My Mood - AI Companion</h3>';
      section.innerHTML += '<p>Share how you\'re feeling and I\'ll help you feel better!</p>';
      
      const moodDiv = document.createElement('div');
      moodDiv.className = 'mood-selector';
      moodDiv.innerHTML = '<button class="mood-btn" onclick="selectMood(\'😊\')">😊</button>' +
        '<button class="mood-btn" onclick="selectMood(\'😢\')">😢</button>' +
        '<button class="mood-btn" onclick="selectMood(\'😠\')">😠</button>' +
        '<button class="mood-btn" onclick="selectMood(\'😰\')">😰</button>' +
        '<button class="mood-btn" onclick="selectMood(\'😴\')">😴</button>' +
        '<button class="mood-btn" onclick="selectMood(\'🤗\')">🤗</button>';
      section.appendChild(moodDiv);
      
      const chatContainer = document.createElement('div');
      chatContainer.className = 'mood-chat-container';
      
      const chatbox = document.createElement('div');
      chatbox.id = 'moodChatbox';
      chatbox.className = 'chatbox';
      chatbox.style.background = '#f0f8ff';
      chatbox.innerHTML = '<div class="chat-message chat-ai"><strong>🤗 AI Companion:</strong> Hi! How are you feeling today? You can select a mood above or just tell me what\'s on your mind.</div>';
      chatContainer.appendChild(chatbox);
      
      const inputArea = document.createElement('div');
      inputArea.className = 'input-area';
      
      const input = document.createElement('input');
      input.type = 'text';
      input.id = 'moodInput';
      input.placeholder = 'Tell me what\'s on your mind...';
      inputArea.appendChild(input);
      
      const sendBtn = document.createElement('button');
      sendBtn.innerHTML = '<i class="fas fa-paper-plane"></i> Share';
      sendBtn.style.background = '#6c5ce7';
      sendBtn.style.color = 'white';
      sendBtn.onclick = function() { sendMoodMessage(); };
      inputArea.appendChild(sendBtn);
      
      chatContainer.appendChild(inputArea);
      section.appendChild(chatContainer);
      
      section.innerHTML += '<div style="margin-top:18px;padding:15px;background:#fff3cd;border-radius:8px;font-size:13px;">' +
        '<strong>💡 Tips:</strong> Talk about your feelings! I\'m here to listen and help.' +
        '</div>';
    }
    
    // Assignments
    if (tab === 'Assignments' || tab === 'Child Assignments') {
      section.innerHTML = '<h3>📝 Assignments</h3>';
      
      let studentName = currentUser;
      if (role === 'parent') {
        const parent = parents.find(p => p.child === currentUser);
        if (parent) {
          const child = students.find(s => s.name === parent.child);
          if (child) studentName = child.name;
        }
      }
      
      if (role === 'teacher') {
        section.innerHTML += '<button class="btn btn-primary mb-2" onclick="showAddAssignmentModal()"><i class="fas fa-plus"></i> Add Assignment</button>';
      }
      
      const assignmentsList = assignments.filter(a => {
        if (role === 'teacher') return true;
        if (role === 'student') return a.student === currentUser;
        if (role === 'parent') return a.student === studentName;
        return false;
      });
      
      if (assignmentsList.length === 0) {
        section.innerHTML += '<p>📭 No assignments found.</p>';
      } else {
        assignmentsList.forEach(a => {
          const isUrgent = new Date(a.dueDate) < new Date() && !a.submitted;
          const isSoon = new Date(a.dueDate) - new Date() < 3 * 24 * 60 * 60 * 1000;
          
          const card = document.createElement('div');
          card.className = 'assignment-card' + (isUrgent ? ' urgent' : '') + (a.submitted ? ' completed' : '');
          card.innerHTML = `
            <div class="assignment-header">
              <div>
                <div class="assignment-title">${a.title}</div>
                <span class="assignment-subject">${a.subject}</span>
              </div>
              <div class="assignment-due ${isUrgent ? 'overdue' : isSoon ? 'soon' : ''}">
                <i class="fas fa-calendar-alt"></i> Due: ${a.dueDate}
              </div>
            </div>
            <div class="assignment-desc">${a.description}</div>
            <div class="assignment-actions">
              <span class="assignment-points">📊 ${a.points} points</span>
              ${!a.submitted && role === 'student' ? '<button class="btn btn-success btn-sm" onclick="submitAssignment(\'' + a.id + '\')"><i class="fas fa-check"></i> Submit</button>' : ''}
              ${a.submitted ? '<span class="text-success"><i class="fas fa-check-circle"></i> Submitted</span>' : ''}
              ${role === 'teacher' ? '<button class="btn btn-danger btn-sm" onclick="deleteAssignment(\'' + a.id + '\')"><i class="fas fa-trash"></i></button>' : ''}
            </div>
          `;
          section.appendChild(card);
        });
      }
    }
    
    // Learning Materials
    if (tab === 'Learning Materials') {
      section.innerHTML = '<h3>📚 Learning Materials</h3>';
      
      if (role === 'teacher') {
        section.innerHTML += '<button class="btn btn-primary mb-2" onclick="showAddMaterialModal()"><i class="fas fa-plus"></i> Add Material</button>';
      }
      
      if (learningMaterials.length === 0) {
        section.innerHTML += '<p>📭 No learning materials available.</p>';
      } else {
        learningMaterials.forEach(m => {
          const card = document.createElement('div');
          card.className = 'material-card';
          card.innerHTML = `
            <div class="material-icon"><i class="fas fa-file-alt"></i></div>
            <div class="material-info">
              <div class="material-title">${m.title}</div>
              <div class="material-meta">📚 ${m.subject} | 👤 ${m.uploadedBy} | 📅 ${m.date}</div>
              <div class="material-desc">${m.description}</div>
              <button class="btn btn-outline btn-sm mt-1" onclick="downloadMaterial('${m.id}')"><i class="fas fa-download"></i> Download</button>
            </div>
          `;
          section.appendChild(card);
        });
      }
    }
    
    // Quiz/Exam
    if (tab === 'Quiz/Exam') {
      section.innerHTML = '<h3>✍️ Quiz/Exam</h3>';
      
      section.innerHTML += '<p>Select a quiz to take:</p>';
      
      const quizList = [
        {id: 'quiz1', title: '3I\'s - Research Basics', subject: '3I\'s', questions: 10, time: 15},
        {id: 'quiz2', title: 'Genchem 2 - Chemical Bonding', subject: 'Genchem 2', questions: 15, time: 20},
        {id: 'quiz3', title: 'Perdev - Self-Awareness', subject: 'Perdev', questions: 10, time: 10}
      ];
      
      quizList.forEach(q => {
        const card = document.createElement('div');
        card.className = 'card';
        card.innerHTML = `
          <h4>${q.title}</h4>
          <p>📚 ${q.subject} | ❓ ${q.questions} questions | ⏱️ ${q.time} minutes</p>
          <button class="btn btn-primary" onclick="startQuiz('${q.id}')"><i class="fas fa-play"></i> Start Quiz</button>
        `;
        section.appendChild(card);
      });
    }
    
    // Syllabus
    if (tab === 'Syllabus') {
      section.innerHTML = '<h3>📋 Syllabus</h3>';
      
      const subjectSelect = document.createElement('select');
      subjectSelect.id = 'syllabusSubjectSelect';
      subjects.forEach(sub => {
        const opt = document.createElement('option');
        opt.value = sub;
        opt.innerText = sub;
        subjectSelect.appendChild(opt);
      });
      section.appendChild(subjectSelect);
      
      const syllabusContainer = document.createElement('div');
      syllabusContainer.id = 'syllabusContainer';
      section.appendChild(syllabusContainer);
      
      subjectSelect.onchange = function() {
        renderSyllabus(syllabusContainer, this.value);
      };
      
      renderSyllabus(syllabusContainer, subjects[0]);
      
      if (role === 'teacher' || role === 'admin') {
        section.innerHTML += '<h4 class="mt-2">Add/Edit Syllabus</h4>';
        section.innerHTML += '<input type="text" id="syllabusTopic" placeholder="Topic">' +
          '<input type="text" id="syllabusWeeks" placeholder="Weeks (e.g., 1-2)">' +
          '<button class="btn btn-primary" onclick="addSyllabusTopic()">Add Topic</button>';
      }
    }
    
    // School Calendar
    if (tab === 'School Calendar') {
      section.innerHTML = '<h3>📅 School Calendar</h3>';
      
      if (role === 'admin') {
        section.innerHTML += '<button class="btn btn-primary mb-2" onclick="showAddEventModal()"><i class="fas fa-plus"></i> Add Event</button>';
      }
      
      const calendarContainer = document.createElement('div');
      calendarContainer.className = 'calendar-container';
      calendarContainer.innerHTML = `
        <div class="calendar-header">
          <div class="calendar-nav">
            <button class="btn btn-outline btn-icon" onclick="changeMonth(-1)"><i class="fas fa-chevron-left"></i></button>
            <span class="calendar-month" id="calendarMonth"></span>
            <button class="btn btn-outline btn-icon" onclick="changeMonth(1)"><i class="fas fa-chevron-right"></i></button>
          </div>
          <button class="btn btn-outline" onclick="goToToday()">Today</button>
        </div>
        <div class="calendar-grid" id="calendarGrid"></div>
      `;
      section.appendChild(calendarContainer);
      
      renderCalendar();
    }
    
    // Library
    if (tab === 'Library' && role === 'student') {
      section.innerHTML = '<h3>📖 Library</h3>';
      
      const searchBox = document.createElement('div');
      searchBox.className = 'search-box';
      searchBox.innerHTML = '<i class="fas fa-search"></i><input type="text" id="librarySearch" placeholder="Search books..." oninput="searchLibrary()">';
      section.appendChild(searchBox);
      
      const libraryContainer = document.createElement('div');
      libraryContainer.id = 'libraryContainer';
      section.appendChild(libraryContainer);
      
      renderLibraryBooks(libraryContainer);
    }
    
    // Fees
    if (tab === 'Fees' || (tab === 'Child Fees' && role === 'parent')) {
      section.innerHTML = '<h3>💰 Fees & Payments</h3>';
      
      let studentName = currentUser;
      if (role === 'parent') {
        const parent = parents.find(p => p.child === currentUser);
        if (parent) {
          const child = students.find(s => s.name === parent.child);
          if (child) studentName = child.name;
        }
      }
      
      const studentFees = feesData[studentName] || [];
      const totalAmount = studentFees.reduce((sum, f) => sum + f.amount, 0);
      const totalPaid = studentFees.reduce((sum, f) => sum + f.paid, 0);
      const totalDue = totalAmount - totalPaid;
      
      section.innerHTML += `
        <div class="payment-summary">
          <h3>💳 Payment Summary</h3>
          <div class="payment-row">
            <span>Total Fees:</span>
            <span>₱${totalAmount.toLocaleString()}</span>
          </div>
          <div class="payment-row">
            <span>Paid:</span>
            <span>₱${totalPaid.toLocaleString()}</span>
          </div>
          <div class="payment-row payment-total">
            <span>Balance Due:</span>
            <span>₱${totalDue.toLocaleString()}</span>
          </div>
        </div>
      `;
      
      studentFees.forEach(fee => {
        const feeItem = document.createElement('div');
        feeItem.className = 'fee-item';
        feeItem.innerHTML = `
          <div class="fee-info">
            <div class="fee-icon"><i class="fas fa-file-invoice-dollar"></i></div>
            <div class="fee-details">
              <h4>${fee.name}</h4>
              <p>Due: ${fee.dueDate}</p>
            </div>
          </div>
          <div class="fee-amount ${fee.paid >= fee.amount ? 'paid' : 'unpaid'}">
            ₱${fee.paid} / ₱${fee.amount}
          </div>
        `;
        section.appendChild(feeItem);
      });
      
      if (role === 'admin') {
        section.innerHTML += '<h4 class="mt-2">Manage Fees</h4>';
        section.innerHTML += '<input type="text" id="feeName" placeholder="Fee Name">' +
          '<input type="number" id="feeAmount" placeholder="Amount">' +
          '<input type="date" id="feeDueDate">' +
          '<button class="btn btn-primary" onclick="addFee()">Add Fee</button>';
      }
    }
    
    // Notifications
    if (tab === 'Notifications') {
      section.innerHTML = '<h3>🔔 Notifications</h3>';
      
      if (notifications.length === 0) {
        section.innerHTML += '<p>📭 No notifications.</p>';
      } else {
        notifications.forEach(n => {
          const item = document.createElement('div');
          item.className = 'notification-item' + (n.read ? '' : ' unread');
          item.innerHTML = `
            <div class="notification-icon ${n.type}"><i class="fas fa-bell"></i></div>
            <div class="notification-content">
              <div class="notification-title">${n.title}</div>
              <div class="notification-message">${n.message}</div>
              <div class="notification-time">${n.time}</div>
            </div>
          `;
          section.appendChild(item);
        });
        
        if (role === 'admin') {
          section.innerHTML += '<h4 class="mt-2">Send Notification</h4>';
          section.innerHTML += '<input type="text" id="notifTitle" placeholder="Title">' +
            '<textarea id="notifMessage" placeholder="Message"></textarea>' +
            '<select id="notifType"><option value="info">Info</option><option value="success">Success</option><option value="warning">Warning</option><option value="danger">Important</option></select>' +
            '<button class="btn btn-primary" onclick="sendNotification()">Send to All</button>';
        }
      }
    }
    
    // Emergency Numbers
    if (tab === 'Emergency Numbers') {
      section.innerHTML = '<h3>🚨 Emergency Numbers</h3>';
      const numbers = [
        {name: '🚔 PNP DUMINGAG', num: '099859558677'},
        {name: '🔥 BFP DUMINGAG', num: '09300459871'},
        {name: '🏛️ LGU DUMINGAG', num: '09482121024'},
        {name: '🆘 MDRRMO DUMINGAG', num: '09098046609'},
        {name: '📞 DSWD Makabata Helpline', num: '1383'}
      ];
      numbers.forEach(n => {
        const div = document.createElement('div');
        div.style.margin = '12px 0';
        div.innerHTML = '<a href="tel:' + n.num + '" style="display:block;padding:18px;background:linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);border-radius:10px;border-left:5px solid #dc3545;text-decoration:none;color:#333;transition:all 0.3s;">' +
          '<strong>' + n.name + '</strong><br>' + n.num + '</a>';
        section.appendChild(div);
      });
    }
    
    // School Map
    if (tab === 'School Map') {
      section.innerHTML = '<h3>🗺️ School Map</h3>';
      
      const mapContainer = document.createElement('div');
      mapContainer.className = 'school-map-container';
      mapContainer.innerHTML = '<img src="https://via.placeholder.com/800x600?text=DSHS+School+Map" alt="School Map" style="max-width:100%;border-radius:10px;box-shadow:0 4px 15px rgba(0,0,0,0.2);">';
      section.appendChild(mapContainer);
    }
    
    content.appendChild(section);
  }
  
  //========= RENDER FUNCTIONS ======
  
  function renderAttendanceCalendar(container, studentName) {
    const existingCalendar = document.getElementById('attendanceCalendar');
    if (existingCalendar) existingCalendar.remove();
    
    const calendar = document.createElement('div');
    calendar.id = 'attendanceCalendar';
    calendar.className = 'attendance-calendar';
    
    const days = ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'];
    days.forEach(day => {
      const div = document.createElement('div');
      div.className = 'attendance-day header';
      div.innerText = day;
      calendar.appendChild(div);
    });
    
    const dateInput = document.querySelector('input[type="month"]');
    const selectedDate = dateInput ? dateInput.value : new Date().toISOString().split('T')[0].substring(0, 7);
    const yearMonth = selectedDate.split('-');
    const year = yearMonth[0];
    const month = yearMonth[1];
    
    const daysInMonth = new Date(year, month, 0).getDate();
    const firstDay = new Date(year, month - 1, 1).getDay();
    
    for (let i = 0; i < firstDay; i++) {
      const div = document.createElement('div');
      div.className = 'attendance-day';
      div.style.background = '#f9f9f9';
      calendar.appendChild(div);
    }
    
    for (let day = 1; day <= daysInMonth; day++) {
      const dateStr = year + '-' + month.padStart(2, '0') + '-' + day.toString().padStart(2, '0');
      const div = document.createElement('div');
      div.className = 'attendance-day';
      div.innerText = day;
      
      const status = attendanceData[studentName] ? attendanceData[studentName][dateStr] : null;
      if (status === 'P') {
        div.classList.add('present');
        div.innerHTML += ' ✅';
      } else if (status === 'A') {
        div.classList.add('absent');
        div.innerHTML += ' ❌';
      }
      
      div.onclick = function() {
        if (role === 'teacher' || role === 'admin') {
          const currentStatus = attendanceData[studentName] ? attendanceData[studentName][dateStr] : null;
          if (currentStatus === 'P') {
            attendanceData[studentName][dateStr] = 'A';
          } else if (currentStatus === 'A') {
            delete attendanceData[studentName][dateStr];
          } else {
            attendanceData[studentName][dateStr] = 'P';
          }
          saveData();
          renderAttendanceCalendar(container, studentName);
        }
      };
      
      calendar.appendChild(div);
    }
    
    container.appendChild(calendar);
    
    if (role !== 'teacher') {
      const legend = document.createElement('div');
      legend.className = 'attendance-legend';
      legend.style.display = 'block';
      legend.innerHTML = '<h4>📋 Legend</h4><p style="color:green;">✅ Present</p><p style="color:red;">❌ Absent</p>';
      container.appendChild(legend);
    }
  }
  
  function renderGradesTable(container, studentName) {
    const existingTable = document.getElementById('gradesTable');
    if (existingTable) existingTable.remove();
    
    const table = document.createElement('table');
    table.id = 'gradesTable';
    table.innerHTML = '<tr><th>📚 Subject</th><th>Q1</th><th>Q2</th><th>Q3</th><th>Q4</th><th>Average</th></tr>';
    
    let totalQ1 = 0, totalQ2 = 0, totalQ3 = 0, totalQ4 = 0;
    let count = 0;
    
    subjects.forEach(sub => {
      const tr = document.createElement('tr');
      const data = gradesData[studentName] ? gradesData[studentName][sub] : {q1: 0, q2: 0, q3: 0, q4: 0};
      const avg = (data.q1 + data.q2 + data.q3 + data.q4) / 4;
      totalQ1 += data.q1;
      totalQ2 += data.q2;
      totalQ3 += data.q3;
      totalQ4 += data.q4;
      count++;
      
      const editable = (role === 'teacher' || role === 'admin') ? 'contenteditable' : '';
      const onblur = (role === 'teacher' || role === 'admin') ? ' onblur="updateGrade(\'' + studentName + '\', \'' + sub + '\', this.dataset.quarter, this.innerText)"' : '';
      
      tr.innerHTML = '<td>' + sub + '</td>' +
        '<td ' + editable + onblur + ' data-quarter="q1">' + data.q1 + '</td>' +
        '<td ' + editable + onblur + ' data-quarter="q2">' + data.q2 + '</td>' +
        '<td ' + editable + onblur + ' data-quarter="q3">' + data.q3 + '</td>' +
        '<td ' + editable + onblur + ' data-quarter="q4">' + data.q4 + '</td>' +
        '<td><strong>' + avg.toFixed(2) + '</strong></td>';
      table.appendChild(tr);
    });
    
    const avgQ1 = count > 0 ? totalQ1 / count : 0;
    const avgQ2 = count > 0 ? totalQ2 / count : 0;
    const avgQ3 = count > 0 ? totalQ3 / count : 0;
    const avgQ4 = count > 0 ? totalQ4 / count : 0;
    const overallAvg = (avgQ1 + avgQ2 + avgQ3 + avgQ4) / 4;
    
    const avgRow = document.createElement('tr');
    avgRow.innerHTML = '<td><strong>📉 Average</strong></td>' +
      '<td><strong>' + avgQ1.toFixed(2) + '</strong></td>' +
      '<td><strong>' + avgQ2.toFixed(2) + '</strong></td>' +
      '<td><strong>' + avgQ3.toFixed(2) + '</strong></td>' +
      '<td><strong>' + avgQ4.toFixed(2) + '</strong></td>' +
      '<td><strong>' + overallAvg.toFixed(2) + '</strong></td>';
    table.appendChild(avgRow);
    
    container.appendChild(table);
  }
  
  function renderStudentsBySection(container, sectionFilter) {
    container.innerHTML = '';
    
    let filteredStudents = students;
    if (sectionFilter !== 'all') {
      filteredStudents = students.filter(s => s.section === sectionFilter);
    }
    
    filteredStudents.forEach(s => {
      const idCard = document.createElement('div');
      idCard.className = 'id-card';
      idCard.innerHTML = '<input type="checkbox" class="id-card-checkbox" data-student-id="' + s.id + '">' +
        '<div class="id-card-header"><h3 style="margin:0;">🎓 DUMINGAG SENIOR HIGH SCHOOL</h3><p style="margin:0;font-size:11px;">Student ID Card</p></div>' +
        '<div class="id-card-photo"><img src="' + (s.pic || 'https://via.placeholder.com/80') + '" alt="Photo" onerror="this.src=\'https://via.placeholder.com/80\'"></div>' +
        '<div class="id-card-info"><p><strong>Name:</strong> ' + s.name + '</p><p><strong>ID No:</strong> ' + s.id + '</p>' +
        '<p><strong>Section:</strong> ' + s.section + '</p><p><strong>Track:</strong> ' + s.track + '</p>' +
        '<p><strong>Strand:</strong> ' + s.strand + '</p><p><strong>Grade:</strong> ' + s.gradeLevel + '</p></div>' +
        '<div class="id-card-footer">🎓 Dumingag Senior High School - Dumingag, Zamboanga del Sur</div>' +
        '<div id="qr-' + s.id + '" style="text-align:center;margin-top:12px;"></div>';
      
      container.appendChild(idCard);
      
      setTimeout(() => {
        new QRCode(document.getElementById('qr-' + s.id), {
          text: s.name + '-' + s.id,
          width: 65,
          height: 65
        });
      }, 100);
    });
  }
  
  function renderParentAccounts(container, sectionFilter) {
    container.innerHTML = '';
    
    let parentAccounts = JSON.parse(localStorage.getItem('dshs_parentAccounts')) || [];
    
    let filteredAccounts = parentAccounts;
    if (sectionFilter !== 'all') {
      filteredAccounts = parentAccounts.filter(p => p.section === sectionFilter);
    }
    
    if (filteredAccounts.length === 0) {
      container.innerHTML = '<p>❌ No parent accounts found.</p>';
      return;
    }
    
    filteredAccounts.forEach(p => {
      const card = document.createElement('div');
      card.className = 'parent-account-card';
      card.innerHTML = '<h4>👤 ' + p.studentName + '</h4>' +
        '<p><strong>🆔 Student ID:</strong> ' + p.studentId + '</p>' +
        '<p><strong>🏫 Section:</strong> ' + p.section + '</p>' +
        '<div class="credentials">' +
        '<p><strong>👨‍💼 Parent Username:</strong> ' + p.parentUsername + '</p>' +
        '<p><strong>🔑 Parent Password:</strong> ' + p.parentPassword + '</p>' +
        '</div>';
      container.appendChild(card);
    });
  }
  
  function renderLibraryBooks(container) {
    container.innerHTML = '';
    
    libraryBooks.forEach(book => {
      const card = document.createElement('div');
      card.className = 'library-book';
      card.innerHTML = `
        <div class="book-cover"><i class="fas fa-book"></i></div>
        <div class="book-info">
          <div class="book-title">${book.title}</div>
          <div class="book-author">by ${book.author}</div>
          <div class="book-meta">
            <span>📚 ${book.category}</span>
            <span>📖 ${book.copies} copies</span>
          </div>
          <span class="book-status ${book.status}">${book.status.charAt(0).toUpperCase() + book.status.slice(1)}</span>
          ${book.status === 'available' && role === 'student' ? '<button class="btn btn-primary btn-sm mt-1" onclick="borrowBook(' + book.id + ')">📚 Borrow</button>' : ''}
        </div>
      `;
      container.appendChild(card);
    });
  }
  
  function renderSyllabus(container, subject) {
    container.innerHTML = '';
    
    const syllabusSection = document.createElement('div');
    syllabusSection.className = 'syllabus-section';
    syllabusSection.innerHTML = '<h4>' + subject + ' Syllabus</h4>';
    
    const topics = syllabusData[subject] || [];
    
    if (topics.length === 0) {
      syllabusSection.innerHTML += '<p>No syllabus available for this subject.</p>';
    } else {
      const topicsDiv = document.createElement('div');
      topicsDiv.className = 'syllabus-topics';
      
      topics.forEach((topic, index) => {
        const topicDiv = document.createElement('div');
        topicDiv.className = 'syllabus-topic';
        topicDiv.innerHTML = '<span class="syllabus-topic-icon"><i class="fas fa-book"></i></span>' +
          '<span class="syllabus-topic-title">' + topic.topic + '</span>' +
          '<span class="syllabus-topic-weeks">Week ' + topic.weeks + '</span>' +
          (role === 'teacher' || role === 'admin' ? '<button class="btn btn-danger btn-sm" onclick="deleteSyllabusTopic(\'' + subject + '\', ' + index + ')">×</button>' : '');
        topicsDiv.appendChild(topicDiv);
      });
      
      syllabusSection.appendChild(topicsDiv);
    }
    
    container.appendChild(syllabusSection);
  }
  
  let currentCalendarDate = new Date();
  
  function renderCalendar() {
    const monthNames = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'];
    const year = currentCalendarDate.getFullYear();
    const month = currentCalendarDate.getMonth();
    
    document.getElementById('calendarMonth').innerText = monthNames[month] + ' ' + year;
    
    const grid = document.getElementById('calendarGrid');
    grid.innerHTML = '';
    
    const days = ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'];
    days.forEach(day => {
      const div = document.createElement('div');
      div.className = 'calendar-day-header';
      div.innerText = day;
      grid.appendChild(div);
    });
    
    const firstDay = new Date(year, month, 1).getDay();
    const daysInMonth = new Date(year, month + 1, 0).getDate();
    const today = new Date();
    
    for (let i = 0; i < firstDay; i++) {
      const div = document.createElement('div');
      div.className = 'calendar-day other-month';
      grid.appendChild(div);
    }
    
    for (let day = 1; day <= daysInMonth; day++) {
      const dateStr = year + '-' + (month + 1).toString().padStart(2, '0') + '-' + day.toString().padStart(2, '0');
      const div = document.createElement('div');
      div.className = 'calendar-day';
      
      if (day === today.getDate() && month === today.getMonth() && year === today.getFullYear()) {
        div.classList.add('today');
      }
      
      const events = calendarEvents.filter(e => e.date === dateStr);
      if (events.length > 0) {
        div.classList.add('has-event');
      }
      
      div.innerHTML = '<div class="calendar-day-number">' + day + '</div>';
      
      if (events.length > 0) {
        const dotsDiv = document.createElement('div');
        events.forEach(e => {
          const dot = document.createElement('div');
          dot.className = 'calendar-event-dot';
          dot.style.background = e.color || '#003366';
          dotsDiv.appendChild(dot);
        });
        div.appendChild(dotsDiv);
        
        const eventList = document.createElement('div');
        eventList.className = 'calendar-event-list';
        events.forEach(e => {
          eventList.innerHTML += '<div style="padding:5px;border-left:3px solid ' + (e.color || '#003366') + ';">' + e.title + '</div>';
        });
        div.appendChild(eventList);
      }
      
      grid.appendChild(div);
    }
  }
  
  function changeMonth(delta) {
    currentCalendarDate.setMonth(currentCalendarDate.getMonth() + delta);
    renderCalendar();
  }
  
  function goToToday() {
    currentCalendarDate = new Date();
    renderCalendar();
  }
  
  //========= HELPER FUNCTIONS ======
  
  function toggleSelectAllStudents() {
    const selectAll = document.getElementById('selectAllStudents');
    const checkboxes = document.querySelectorAll('.id-card-checkbox');
    checkboxes.forEach(cb => cb.checked = selectAll.checked);
  }
  
  function printSelectedIDs() {
    const checkboxes = document.querySelectorAll('.id-card-checkbox:checked');
    if (checkboxes.length === 0) {
      showToast('Please select at least one student to print!', 'warning');
      return;
    }
    window.print();
  }
  
  function approveStudent(id) {
    const student = students.find(s => s.id === id);
    if (student) {
      student.approved = true;
      saveData();
      showToast(student.name + ' has been approved!', 'success');
      loadSection('Student Approval');
    }
  }
  
  function deleteStudent(id) {
    const student = students.find(s => s.id === id);
    if (student) {
      if (confirm('Are you sure you want to delete ' + student.name + '?')) {
        students = students.filter(s => s.id !== id);
        delete gradesData[student.name];
        delete attendanceData[student.name];
        saveData();
        showToast(student.name + ' has been deleted.', 'success');
        loadSection('Student Approval');
      }
    }
  }
  
  function deleteTeacher(id) {
    const teacher = teachers.find(t => t.id === id);
    if (teacher) {
      if (confirm('Are you sure you want to delete ' + teacher.name + '?')) {
        teachers = teachers.filter(t => t.id !== id);
        saveData();
        showToast(teacher.name + ' has been deleted.', 'success');
        loadSection('Manage Users');
      }
    }
  }
  
  function createTeacher() {
    const name = document.getElementById('newTeacherName').value.trim();
    const id = document.getElementById('newTeacherID').value.trim();
    const position = document.getElementById('newTeacherPosition').value.trim();
    const section = document.getElementById('newTeacherSection').value.trim();
    const username = document.getElementById('newTeacherUsername').value.trim();
    const password = document.getElementById('newTeacherPassword').value.trim();
    
    if (!name || !username || !password || !section) {
      showToast('Please fill in all required fields!', 'danger');
      return;
    }
    
    if (teachers.find(t => t.username === username)) {
      showToast('Username already exists!', 'danger');
      return;
    }
    
    teachers.push({name, id, position, sectionHandled: section, username, password: secureHash(password)});
    saveData();
    showToast('Teacher account created successfully!', 'success');
    
    ['newTeacherName', 'newTeacherID', 'newTeacherPosition', 'newTeacherSection', 'newTeacherUsername', 'newTeacherPassword'].forEach(id => {
      document.getElementById(id).value = '';
    });
  }
  
  function updateSubject(index, newValue) {
    const oldValue = subjects[index];
    subjects[index] = newValue;
    
    if (scheduleTimes[oldValue]) {
      scheduleTimes[newValue] = scheduleTimes[oldValue];
      delete scheduleTimes[oldValue];
    }
    
    students.forEach(s => {
      if (gradesData[s.name] && gradesData[s.name][oldValue] !== undefined) {
        gradesData[s.name][newValue] = gradesData[s.name][oldValue];
        delete gradesData[s.name][oldValue];
      }
    });
    
    saveData();
  }
  
  function updateScheduleTime(subject, time) {
    scheduleTimes[subject] = time;
    saveData();
  }
  
  function deleteSubject(index) {
    const subject = subjects[index];
    subjects.splice(index, 1);
    delete scheduleTimes[subject];
    
    students.forEach(s => {
      if (gradesData[s.name]) {
        delete gradesData[s.name][subject];
      }
    });
    
    saveData();
    loadSection('Subject Schedule');
  }
  
  function addSubject() {
    const name = document.getElementById('newSubjectName').value.trim();
    const time = document.getElementById('newSubjectTime').value.trim();
    
    if (!name) {
      showToast('Please enter a subject name!', 'warning');
      return;
    }
    
    if (subjects.includes(name)) {
      showToast('Subject already exists!', 'danger');
      return;
    }
    
    subjects.push(name);
    scheduleTimes[name] = time || 'TBA';
    
    students.forEach(s => {
      if (!gradesData[s.name]) gradesData[s.name] = {};
      gradesData[s.name][name] = {q1: 0, q2: 0, q3: 0, q4: 0};
    });
    
    saveData();
    loadSection('Subject Schedule');
  }
  
  function updateGrade(student, subject, quarter, newGrade) {
    const grade = parseInt(newGrade);
    if (isNaN(grade) || grade < 0 || grade > 100) {
      showToast('Grade must be between 0 and 100.', 'danger');
      loadSection('Grades');
      return;
    }
    
    if (!gradesData[student]) gradesData[student] = {};
    if (!gradesData[student][subject]) gradesData[student][subject] = {q1: 0, q2: 0, q3: 0, q4: 0};
    gradesData[student][subject][quarter] = grade;
    saveData();
  }
  
  function uploadProfilePhoto() {
    const fileInput = document.getElementById('uploadPic');
    if (!fileInput.files || !fileInput.files[0]) {
      showToast('Please select a photo first!', 'warning');
      return;
    }
    
    const reader = new FileReader();
    reader.onload = function(e) {
      const photoData = e.target.result;
      
      if (role === 'student') {
        const user = students.find(s => s.name === currentUser);
        if (user) { user.pic = photoData; saveData(); document.getElementById('profilePic').src = photoData; showToast('Photo uploaded!', 'success'); }
      } else if (role === 'teacher') {
        const user = teachers.find(t => t.name === currentUser);
        if (user) { user.pic = photoData; saveData(); document.getElementById('profilePic').src = photoData; showToast('Photo uploaded!', 'success'); }
      } else if (role === 'parent') {
        const user = parents.find(p => p.child === currentUser);
        if (user) { user.pic = photoData; saveData(); document.getElementById('profilePic').src = photoData; showToast('Photo uploaded!', 'success'); }
      } else if (role === 'admin') {
        adminAccount.pic = photoData; saveData(); document.getElementById('profilePic').src = photoData; showToast('Photo uploaded!', 'success'); }
    };
    reader.readAsDataURL(fileInput.files[0]);
  }
  
  function sendChatMessage(tab) {
    const input = document.getElementById('chatInput');
    const chatbox = document.getElementById('chatbox');
    const message = input.value.trim();
    
    if (!message) {
      showToast('Please type a message!', 'warning');
      return;
    }
    
    const timestamp = new Date().toLocaleString();
    chatbox.innerHTML += '<p><strong>' + currentUser + ':</strong> ' + message + ' <small style="color:#888;">(' + timestamp + ')</small></p>';
    chatbox.scrollTop = chatbox.scrollHeight;
    input.value = '';
  }
  
  //========= PLANNER FUNCTIONS ======
  
  function addPlannerGoal(type) {
    const input = document.getElementById(type + 'GoalInput');
    const timeInput = document.getElementById(type + 'GoalTime') || document.getElementById(type + 'GoalDate');
    
    if (!input.value.trim()) {
      showToast('Please enter a goal!', 'warning');
      return;
    }
    
    if (!plannerData[currentUser]) plannerData[currentUser] = {daily: [], weekly: [], monthly: []};
    
    plannerData[currentUser][type].push({
      text: input.value.trim(),
      time: timeInput ? timeInput.value : '',
      completed: false
    });
    
    saveData();
    loadSection('My Planner');
  }
  
  function togglePlannerGoal(type, index) {
    plannerData[currentUser][type][index].completed = !plannerData[currentUser][type][index].completed;
    saveData();
    loadSection('My Planner');
  }
  
  function deletePlannerGoal(type, index) {
    plannerData[currentUser][type].splice(index, 1);
    saveData();
    loadSection('My Planner');
  }
  
  function setAlarm(time) {
    if (!time) {
      showToast('No time set for this goal!', 'info');
      return;
    }
    showToast('Alarm set for ' + time, 'info');
  }
  
  //========= MY MOOD FUNCTIONS ======

let selectedMood = '';

function selectMood(mood) {
  selectedMood = mood;
  document.querySelectorAll('.mood-btn').forEach(btn => {
    btn.classList.toggle('selected', btn.innerText === mood);
  });
  const chatbox = document.getElementById('moodChatbox');
  chatbox.innerHTML += '<div class="chat-message chat-user"><strong>👤 You:</strong> ' + mood + '</div>';
  chatbox.scrollTop = chatbox.scrollHeight;
  getAIResponse('I feel ' + mood);
}

function sendMoodMessage() {
  const input = document.getElementById('moodInput');
  const message = input.value.trim();
  if (!message && !selectedMood) {
    showToast('Please select a mood or type a message!', 'warning');
    return;
  }
  const chatbox = document.getElementById('moodChatbox');
  if (message) {
    chatbox.innerHTML += '<div class="chat-message chat-user"><strong>👤 You:</strong> ' + message + '</div>';
    chatbox.scrollTop = chatbox.scrollHeight;
    input.value = '';
    getAIResponse(message);
  }
}

function getAIResponse(message) {
  const chatbox = document.getElementById('moodChatbox');
  chatbox.innerHTML += '<div class="chat-message chat-ai" id="typingIndicator"><em>💭 Thinking...</em></div>';
  chatbox.scrollTop = chatbox.scrollHeight;
  setTimeout(() => {
    const typingIndicator = document.getElementById('typingIndicator');
    if (typingIndicator) typingIndicator.remove();
    const response = getSupportiveResponse(message);
    chatbox.innerHTML += '<div class="chat-message chat-ai"><strong>🤗 AI Companion:</strong> ' + response + '</div>';
    chatbox.scrollTop = chatbox.scrollHeight;
  }, 1000);
}

function getSupportiveResponse(message) {
  const lowerMessage = message.toLowerCase();
  if (lowerMessage.includes('happy') || lowerMessage.includes('good') || lowerMessage.includes('great') || lowerMessage.includes('excited') || lowerMessage.includes('😊')) {
    return "That's wonderful! 🎉 I'm so glad you're feeling good! Keep that positive energy going!";
  }
  if (lowerMessage.includes('sad') || lowerMessage.includes('depressed') || lowerMessage.includes('unhappy') || lowerMessage.includes('down') || lowerMessage.includes('😢')) {
    return "I'm here for you. 💙 It's okay to feel sad sometimes. Would you like to talk about what's making you feel this way?";
  }
  if (lowerMessage.includes('angry') || lowerMessage.includes('mad') || lowerMessage.includes('frustrated') || lowerMessage.includes('😠')) {
    return "I understand you're feeling angry. 😤 Take a deep breath... Inhale for 4 seconds, hold for 7, exhale for 8.";
  }
  if (lowerMessage.includes('anxious') || lowerMessage.includes('nervous') || lowerMessage.includes('worried') || lowerMessage.includes('stressed') || lowerMessage.includes('😰')) {
    return "It's okay to feel anxious sometimes. 🌸 Try: Take deep breaths, Write down your worries, Talk to someone you trust.";
  }
  if (lowerMessage.includes('tired') || lowerMessage.includes('sleepy') || lowerMessage.includes('exhausted') || lowerMessage.includes('😴')) {
    return "You sound tired! 😴 Make sure you're getting enough sleep - teens need 8-10 hours. Take breaks when studying!";
  }
  const responses = [
    "Thank you for sharing that with me. 💙 I'm here to listen.",
    "I hear you. 🌟 Would you like some suggestions on how to cope?",
    "Thanks for opening up to me. 💜 You're very brave!",
    "Your feelings are valid. 💙 Keep going!"
  ];
  return responses[Math.floor(Math.random() * responses.length)];
}

//========= SEMESTER/QUARTER SELECTORS ======

function selectSemester(sem, btn) {
  document.querySelectorAll('.sem-btn').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
  const quarterSelector = document.getElementById('quarterSelector');
  if (quarterSelector) {
    if (sem === 1) {
      quarterSelector.innerHTML = '<button class="quarter-btn active" onclick="selectQuarter(1, this)">1st Quarter</button><button class="quarter-btn" onclick="selectQuarter(2, this)">2nd Quarter</button>';
    } else {
      quarterSelector.innerHTML = '<button class="quarter-btn active" onclick="selectQuarter(3, this)">3rd Quarter</button><button class="quarter-btn" onclick="selectQuarter(4, this)">4th Quarter</button>';
    }
  }
}

function selectQuarter(quarter, btn) {
  document.querySelectorAll('.quarter-btn').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
}

//========= ASSIGNMENTS FUNCTIONS ======

function showAddAssignmentModal() {
  const subjectOptions = subjects.map(s => `<option value="${s}">${s}</option>`).join('');
  showModal('Add Assignment', '<input type="text" id="assignmentTitle" placeholder="Title"><select id="assignmentSubject">' + subjectOptions + '</select><input type="date" id="assignmentDueDate"><textarea id="assignmentDesc" placeholder="Description"></textarea><input type="number" id="assignmentPoints" placeholder="Points">', [{text: '<i class="fas fa-plus"></i> Add', class: 'btn btn-primary', onclick: 'addAssignment()'}, {text: 'Cancel', class: 'btn btn-outline', onclick: 'closeAllModals()'}]);
}

function addAssignment() {
  const title = document.getElementById('assignmentTitle').value.trim();
  const subject = document.getElementById('assignmentSubject').value;
  const dueDate = document.getElementById('assignmentDueDate').value;
  const description = document.getElementById('assignmentDesc').value.trim();
  const points = parseInt(document.getElementById('assignmentPoints').value) || 10;
  if (!title || !dueDate) {
    showToast('Please fill required fields!', 'warning');
    return;
  }
  const assignment = { id: 'A' + Date.now(), title, subject, dueDate, description, points, student: role === 'student' ? currentUser : null, submitted: false, dateCreated: new Date().toISOString().split('T')[0] };
  assignments.push(assignment);
  saveData();
  closeAllModals();
  showToast('Assignment added!', 'success');
  loadSection('Assignments');
}

function submitAssignment(id) {
  const assignment = assignments.find(a => a.id === id);
  if (assignment) {
    assignment.submitted = true;
    assignment.submittedDate = new Date().toISOString().split('T')[0];
    saveData();
    showToast('Assignment submitted!', 'success');
    loadSection('Assignments');
  }
}

function deleteAssignment(id) {
  if (confirm('Delete this assignment?')) {
    assignments = assignments.filter(a => a.id !== id);
    saveData();
    loadSection('Assignments');
  }
}

//========= LEARNING MATERIALS FUNCTIONS ======

function showAddMaterialModal() {
  const subjectOptions = subjects.map(s => `<option value="${s}">${s}</option>`).join('');
  showModal('Add Learning Material', '<input type="text" id="materialTitle" placeholder="Title"><select id="materialSubject">' + subjectOptions + '</select><textarea id="materialDesc" placeholder="Description"></textarea><input type="file" id="materialFile">', [{text: '<i class="fas fa-plus"></i> Add', class: 'btn btn-primary', onclick: 'addMaterial()'}, {text: 'Cancel', class: 'btn btn-outline', onclick: 'closeAllModals()'}]);
}

function addMaterial() {
  const title = document.getElementById('materialTitle').value.trim();
  const subject = document.getElementById('materialSubject').value;
  const description = document.getElementById('materialDesc').value.trim();
  if (!title) {
    showToast('Please enter a title!', 'warning');
    return;
  }
  const material = { id: 'M' + Date.now(), title, subject, description, uploadedBy: currentUser, date: new Date().toISOString().split('T')[0], fileName: 'material.pdf' };
  learningMaterials.push(material);
  saveData();
  closeAllModals();
  showToast('Material added!', 'success');
  loadSection('Learning Materials');
}

function downloadMaterial(id) {
  const material = learningMaterials.find(m => m.id === id);
  if (material) {
    showToast('Download started: ' + material.title, 'info');
  }
}

//========= QUIZ/EXAM FUNCTIONS ======

function startQuiz(quizId) {
  showModal('Quiz', '<p>You are about to start this quiz. Are you ready?</p><div class="quiz-timer"><i class="fas fa-clock"></i> Time limit: 15 minutes</div>', [{text: '<i class="fas fa-play"></i> Start', class: 'btn btn-primary', onclick: 'startQuizQuestions()'}, {text: 'Cancel', class: 'btn btn-outline', onclick: 'closeAllModals()'}]);
}

function startQuizQuestions() {
  closeAllModals();
  showToast('Quiz started! Good luck!', 'info');
}

//========= CALENDAR FUNCTIONS ======

function showAddEventModal() {
  showModal('Add Calendar Event', '<input type="text" id="eventTitle" placeholder="Event Title"><input type="date" id="eventDate"><input type="color" id="eventColor" value="#003366"><input type="text" id="eventDesc" placeholder="Description">', [{text: '<i class="fas fa-plus"></i> Add', class: 'btn btn-primary', onclick: 'addCalendarEvent()'}, {text: 'Cancel', class: 'btn btn-outline', onclick: 'closeAllModals()'}]);
}

function addCalendarEvent() {
  const title = document.getElementById('eventTitle').value.trim();
  const date = document.getElementById('eventDate').value;
  const color = document.getElementById('eventColor').value;
  const description = document.getElementById('eventDesc').value.trim();
  if (!title || !date) {
    showToast('Please fill required fields!', 'warning');
    return;
  }
  calendarEvents.push({id: 'E' + Date.now(), title, date, color, description});
  saveData();
  closeAllModals();
  showToast('Event added!', 'success');
  renderCalendar();
}

let currentCalendarDate = new Date();

function renderCalendar() {
  const monthNames = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'];
  const year = currentCalendarDate.getFullYear();
  const month = currentCalendarDate.getMonth();
  document.getElementById('calendarMonth').innerText = monthNames[month] + ' ' + year;
  const grid = document.getElementById('calendarGrid');
  grid.innerHTML = '';
  const days = ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'];
  days.forEach(day => {
    const div = document.createElement('div');
    div.className = 'calendar-day-header';
    div.innerText = day;
    grid.appendChild(div);
  });
  const firstDay = new Date(year, month, 1).getDay();
  const daysInMonth = new Date(year, month + 1, 0).getDate();
  const today = new Date();
  for (let i = 0; i < firstDay; i++) {
    const div = document.createElement('div');
    div.className = 'calendar-day other-month';
    grid.appendChild(div);
  }
  for (let day = 1; day <= daysInMonth; day++) {
    const dateStr = year + '-' + (month + 1).toString().padStart(2, '0') + '-' + day.toString().padStart(2, '0');
    const div = document.createElement('div');
    div.className = 'calendar-day';
    if (day === today.getDate() && month === today.getMonth() && year === today.getFullYear()) {
      div.classList.add('today');
    }
    const events = calendarEvents.filter(e => e.date === dateStr);
    if (events.length > 0) {
      div.classList.add('has-event');
    }
    div.innerHTML = '<div class="calendar-day-number">' + day + '</div>';
    if (events.length > 0) {
      const dotsDiv = document.createElement('div');
      events.forEach(e => {
        const dot = document.createElement('div');
        dot.className = 'calendar-event-dot';
        dot.style.background = e.color || '#003366';
        dotsDiv.appendChild(dot);
      });
      div.appendChild(dotsDiv);
      const eventList = document.createElement('div');
      eventList.className = 'calendar-event-list';
      events.forEach(e => {
        eventList.innerHTML += '<div style="padding:5px;border-left:3px solid ' + (e.color || '#003366') + ';">' + e.title + '</div>';
      });
      div.appendChild(eventList);
    }
    grid.appendChild(div);
  }
}

function changeMonth(delta) {
  currentCalendarDate.setMonth(currentCalendarDate.getMonth() + delta);
  renderCalendar();
}

function goToToday() {
  currentCalendarDate = new Date();
  renderCalendar();
}

//========= SYLLABUS FUNCTIONS ======

function addSyllabusTopic() {
  const topic = document.getElementById('syllabusTopic').value.trim();
  const weeks = document.getElementById('syllabusWeeks').value.trim();
  const subjectSelect = document.getElementById('syllabusSubjectSelect');
  const subject = subjectSelect ? subjectSelect.value : subjects[0];
  if (!topic || !weeks) {
    showToast('Please fill all fields!', 'warning');
    return;
  }
  if (!syllabusData[subject]) syllabusData[subject] = [];
  syllabusData[subject].push({topic, weeks});
  saveData();
  document.getElementById('syllabusTopic').value = '';
  document.getElementById('syllabusWeeks').value = '';
  renderSyllabus(document.getElementById('syllabusContainer'), subject);
  showToast('Topic added!', 'success');
}

function deleteSyllabusTopic(subject, index) {
  if (syllabusData[subject]) {
    syllabusData[subject].splice(index, 1);
    saveData();
    renderSyllabus(document.getElementById('syllabusContainer'), subject);
    showToast('Topic deleted!', 'success');
  }
}

//========= LIBRARY FUNCTIONS ======

function showAddBookModal() {
  showModal('Add Book', '<input type="text" id="bookTitle" placeholder="Book Title"><input type="text" id="bookAuthor" placeholder="Author"><input type="text" id="bookCategory" placeholder="Category"><input type="number" id="bookCopies" placeholder="Number of Copies" value="1">', [{text: '<i class="fas fa-plus"></i> Add', class: 'btn btn-primary', onclick: 'addBook()'}, {text: 'Cancel', class: 'btn btn-outline', onclick: 'closeAllModals()'}]);
}

function addBook() {
  const title = document.getElementById('bookTitle').value.trim();
  const author = document.getElementById('bookAuthor').value.trim();
  const category = document.getElementById('bookCategory').value.trim();
  const copies = parseInt(document.getElementById('bookCopies').value) || 1;
  if (!title) {
    showToast('Please enter book title!', 'warning');
    return;
  }
  libraryBooks.push({id: libraryBooks.length + 1, title, author, category, status: 'available', copies});
  saveData();
  closeAllModals();
  showToast('Book added!', 'success');
  loadSection('Library Management');
}

function borrowBook(bookId) {
  const book = libraryBooks.find(b => b.id === bookId);
  if (book && book.status === 'available') {
    book.status = 'borrowed';
    book.borrowedBy = currentUser;
    book.borrowDate = new Date().toISOString().split('T')[0];
    saveData();
    showToast('Book borrowed! Return by next week.', 'success');
    loadSection('Library');
  }
}

function searchLibrary() {
  const query = document.getElementById('librarySearch').value.toLowerCase();
  const filtered = libraryBooks.filter(b => b.title.toLowerCase().includes(query) || b.author.toLowerCase().includes(query) || b.category.toLowerCase().includes(query));
  renderLibraryBooksFiltered(filtered);
}

function renderLibraryBooksFiltered(books) {
  const container = document.getElementById('libraryContainer');
  container.innerHTML = '';
  books.forEach(book => {
    const card = document.createElement('div');
    card.className = 'library-book';
    card.innerHTML = '<div class="book-cover"><i class="fas fa-book"></i></div><div class="book-info"><div class="book-title">' + book.title + '</div><div class="book-author">by ' + book.author + '</div><div class="book-meta"><span>📚 ' + book.category + '</span><span>📖 ' + book.copies + ' copies</span></div><span class="book-status ' + book.status + '">' + book.status.charAt(0).toUpperCase() + book.status.slice(1) + '</span>' + (book.status === 'available' && role === 'student' ? '<button class="btn btn-primary btn-sm mt-1" onclick="borrowBook(' + book.id + ')">📚 Borrow</button>' : '') + '</div>';
    container.appendChild(card);
  });
}

//========= FEES FUNCTIONS ======

function addFee() {
  const name = document.getElementById('feeName').value.trim();
  const amount = parseInt(document.getElementById('feeAmount').value);
  const dueDate = document.getElementById('feeDueDate').value;
  if (!name || !amount || !dueDate) {
    showToast('Please fill all fields!', 'warning');
    return;
  }
  students.forEach(s => {
    if (!feesData[s.name]) feesData[s.name] = [];
    feesData[s.name].push({id: Date.now(), name, amount, paid: 0, dueDate});
  });
  saveData();
  showToast('Fee added for all students!', 'success');
  loadSection('Fees');
}

//========= NOTIFICATIONS FUNCTIONS ======

function sendNotification() {
  const title = document.getElementById('notifTitle').value.trim();
  const message = document.getElementById('notifMessage').value.trim();
  const type = document.getElementById('notifType').value;
  if (!title || !message) {
    showToast('Please fill all fields!', 'warning');
    return;
  }
  const notif = {id: 'N' + Date.now(), title, message, type, time: new Date().toLocaleString(), read: false};
  notifications.unshift(notif);
  saveData();
  showToast('Notification sent!', 'success');
  loadSection('Notifications');
}

//========= DATA BACKUP/RESTORE FUNCTIONS ======

function backupData() {
  const data = {students, teachers, parents, subjects, scheduleTimes, gradesData, attendanceData, bulletinBoard, plannerData, assignments, learningMaterials, calendarEvents, libraryBooks, feesData, syllabusData};
  const blob = new Blob([JSON.stringify(data, null, 2)], {type: 'application/json'});
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = 'dshs_backup_' + new Date().toISOString().split('T')[0] + '.json';
  a.click();
  URL.revokeObjectURL(url);
  showToast('Backup downloaded!', 'success');
}

function restoreData() {
  const fileInput = document.getElementById('restoreFile');
  if (!fileInput.files || !fileInput.files[0]) {
    showToast('Please select a backup file!', 'warning');
    return;
  }
  const reader = new FileReader();
  reader.onload = function(e) {
    try {
      const data = JSON.parse(e.target.result);
      if (data.students) { students = data.students; localStorage.setItem('dshs_students', JSON.stringify(students)); }
      if (data.teachers) { teachers = data.teachers; localStorage.setItem('dshs_teachers', JSON.stringify(teachers)); }
      if (data.parents) { parents = data.parents; localStorage.setItem('dshs_parents', JSON.stringify(parents)); }
      if (data.gradesData) { gradesData = data.gradesData; localStorage.setItem('dshs_gradesData', JSON.stringify(gradesData)); }
      if (data.attendanceData) { attendanceData = data.attendanceData; localStorage.setItem('dshs_attendanceData', JSON.stringify(attendanceData)); }
      if (data.assignments) { assignments = data.assignments; localStorage.setItem('dshs_assignments', JSON.stringify(assignments)); }
      if (data.calendarEvents) { calendarEvents = data.calendarEvents; localStorage.setItem('dshs_calendarEvents', JSON.stringify(calendarEvents)); }
      if (data.libraryBooks) { libraryBooks = data.libraryBooks; localStorage.setItem('dshs_libraryBooks', JSON.stringify(libraryBooks)); }
      if (data.feesData) { feesData = data.feesData; localStorage.setItem('dshs_feesData', JSON.stringify(feesData)); }
      showToast('Data restored successfully!', 'success');
      location.reload();
    } catch (err) {
      showToast('Invalid backup file!', 'danger');
    }
  };
  reader.readAsText(fileInput.files[0]);
}

function clearAllData() {
  if (confirm('⚠️ This will delete ALL data! Are you sure?')) {
    if (confirm('This action cannot be undone! Continue?')) {
      localStorage.clear();
      showToast('All data cleared!', 'success');
      setTimeout(() => location.reload(), 1500);
    }
  }
}

//========= DATA EXPORT FUNCTIONS ======

function exportData(type) {
  let data, filename;
  switch(type) {
    case 'students':
      data = students;
      filename = 'students.json';
      break;
    case 'teachers':
      data = teachers;
      filename = 'teachers.json';
      break;
    case 'grades':
      data = gradesData;
      filename = 'grades.json';
      break;
    case 'attendance':
      data = attendanceData;
      filename = 'attendance.json';
      break;
    case 'all':
      data = {students, teachers, parents, gradesData, attendanceData};
      filename = 'dshs_all_data.json';
      break;
    default:
      return;
  }
  const blob = new Blob([JSON.stringify(data, null, 2)], {type: 'application/json'});
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = filename;
  a.click();
  URL.revokeObjectURL(url);
  showToast('Exported: ' + filename, 'success');
}

//========= WINDOW ONLOAD ======

window.onload = function() {
  saveData();
  if (getSession()) {
    showToast('Session restored', 'info');
  }
};
</script>
</body>
</html>
