<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>DSHS School System</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
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
  }
  
  * {
    box-sizing: border-box;
  }
  
  body { 
    margin: 0; 
    min-height: 70vh; 
    background: url(https://i.ibb.co/XxJDdGth/your-image.png) center center / cover no-repeat fixed; 
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  }
  
  .signup-link { color: var(--main-blue); font-weight: bold; cursor: pointer; }
  .signup-link:hover { text-decoration: underline; }
  
  input, button, textarea, select { 
    width: 100%; 
    padding: 12px; 
    margin-top: 8px; 
    box-sizing: border-box; 
    font-size: 14px;
    border: 2px solid #ddd;
    border-radius: 6px;
    transition: border-color 0.3s;
  }
  
  input:focus, textarea:focus, select:focus {
    border-color: var(--main-blue);
    outline: none;
  }
  
  button { 
    cursor: pointer; 
    border-radius: 6px; 
    font-weight: bold;
    transition: all 0.3s;
  }
  
  button:hover {
    transform: translateY(-2px);
    box-shadow: 0 4px 8px rgba(0,0,0,0.2);
  }
  
  /*------ COLLAPSIBLE MENU BUTTON ------*/
  .toggle-btn { 
    background: linear-gradient(135deg, var(--main-red) 0%, var(--main-blue) 100%); 
    color: white; 
    font-size: 18px; 
    border: none; 
    position: fixed; 
    top: 12px; 
    left: 12px; 
    z-index: 1000; 
    padding: 10px 14px; 
    border-radius: 8px;
    cursor: pointer;
    display: flex;
    align-items: center;
    gap: 8px;
    box-shadow: 0 4px 15px rgba(0,0,0,0.3);
    transition: all 0.3s;
  }
  
  .toggle-btn:hover { 
    background: linear-gradient(135deg, #660000 0%, #002244 100%);
    transform: scale(1.05);
  }
  
  .toggle-btn .icon { 
    font-size: 22px; 
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  .toggle-btn .text {
    display: none;
    white-space: nowrap;
  }
  
  .toggle-btn:hover .text {
    display: block;
  }
  
  .login { 
    height: 100vh; 
    display: flex; 
    justify-content: center; 
    align-items: center; 
    padding: 20px;
  }
  
  .box { 
    background: rgba(255,255,255,0.98); 
    padding: 40px; 
    width: 100%; 
    max-width: 420px; 
    border-radius: 15px; 
    box-shadow: 0 15px 40px rgba(0,0,0,0.3); 
    text-align: center; 
    border-top: 5px solid var(--main-red);
  }
  
  .box h2 {
    color: var(--main-blue);
    margin-bottom: 25px;
  }
  
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
  
  .menu-header p {
    margin: 5px 0 0 0;
    font-size: 13px;
    opacity: 0.9;
  }
  
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
  
  .menu button .tab-icon {
    font-size: 20px;
    width: 30px;
    text-align: center;
  }
  
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
  
  .section { 
    background: white; 
    padding: 25px; 
    border-radius: 12px; 
    width: 100%; 
    max-width: 850px; 
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
  
  table { 
    border-collapse: collapse; 
    width: 100%; 
    margin-top: 20px; 
    overflow-x: auto;
  }
  table, th, td { 
    border: 1px solid #dee2e6; 
    text-align: center; 
    padding: 12px; 
  }
  th { 
    background: linear-gradient(135deg, var(--main-red) 0%, var(--main-blue) 100%); 
    color: white; 
    font-weight: bold;
  }
  
  tr:nth-child(even) {
    background-color: #f8f9fa;
  }
  
  tr:hover {
    background-color: #e9ecef;
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
  
  .id-card-info strong { 
    color: var(--sub-yellow); 
  }
  
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
  
  .attendance-day:hover {
    transform: scale(1.1);
    border-color: var(--main-blue);
  }
  
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
  
  .attendance-day.header:hover {
    transform: none;
  }
  
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
  
  .subject-item input[type="text"] { 
    flex: 1; 
    min-width: 140px; 
    margin: 0; 
  }
  
  .planner-container { 
    max-height: 450px; 
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
  
  .planner-item:hover {
    border-color: var(--main-blue);
  }
  
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
  
  .planner-item .goal-text { 
    flex: 1; 
    min-width: 180px; 
  }
  
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
  
  .attendance-legend { 
    display: none; /* Hidden for teacher */
  }
  
  .performance-box {
    background: linear-gradient(135deg, var(--main-red) 0%, var(--main-blue) 100%); 
    color: white;
    padding: 25px;
    border-radius: 12px;
    margin: 20px 0;
    text-align: center;
    box-shadow: 0 6px 20px rgba(0,0,0,0.2);
  }
  
  .performance-box h3 {
    color: var(--sub-yellow);
    margin-top: 0;
  }
  
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
  
  .stat-number { 
    font-size: 32px; 
    font-weight: bold; 
    color: var(--sub-yellow);
  }
  
  .stat-label { 
    font-size: 13px; 
    opacity: 0.9; 
    margin-top: 5px;
  }
  
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
  
  .school-welcome h2 {
    margin: 0 0 10px 0;
    color: var(--sub-yellow);
  }
  
  .school-welcome p {
    margin: 0;
    opacity: 0.95;
  }
  
  /*------ PROFILE CARD FOR MY INFO ------*/
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
  
  .profile-card h3 {
    color: var(--sub-yellow);
    margin: 0 0 5px 0;
  }
  
  .profile-card p {
    margin: 5px 0;
    opacity: 0.9;
  }
  
  .profile-details {
    background: white;
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
  
  .profile-details .detail-row:last-child {
    border-bottom: none;
  }
  
  .profile-details .detail-label {
    font-weight: bold;
    color: var(--main-blue);
  }
  
  .profile-details .detail-value {
    color: var(--main-gray);
  }
  
  /*------ RESPONSIVE MOOD CHAT ------*/
  .mood-chat-container {
    max-width: 600px;
    margin: 0 auto;
  }
  
  .mood-chat-container .chatbox {
    height: 400px;
  }
  
  .mood-chat-container .input-area {
    display: flex;
    gap: 10px;
    margin-top: 15px;
  }
  
  .mood-chat-container .input-area input {
    flex: 1;
    margin: 0;
  }
  
  .mood-chat-container .input-area button {
    width: auto;
    white-space: nowrap;
  }
  
  @media (max-width: 768px) {
    .menu { 
      width: 85%; 
      max-width: 340px; 
    }
    
    .section { 
      padding: 18px; 
      margin-top: 12px; 
    }
    
    .schedule-box div { flex: 1 1 100%; }
    
    table { 
      display: block; 
      overflow-x: auto; 
      white-space: nowrap; 
    }
    
    .id-card { 
      max-width: 100%; 
      margin: 12px 0; 
    }
    
    .mood-selector {
      gap: 12px;
    }
    
    .mood-btn {
      width: 60px;
      height: 60px;
      font-size: 28px;
    }
    
    .header {
      padding-left: 55px;
      font-size: 15px;
    }
    
    .toggle-btn {
      padding: 8px 12px;
      font-size: 14px;
    }
    
    .box {
      padding: 25px;
    }
    
    .stat-number {
      font-size: 26px;
    }
    
    .mood-chat-container .chatbox {
      height: 300px;
    }
    
    .mood-chat-container .input-area {
      flex-direction: column;
    }
    
    .mood-chat-container .input-area button {
      width: 100%;
    }
  }
  
  @media print {
    .menu, .toggle-btn, .header, .print-controls, .menu-overlay {
      display: none !important;
    }
    
    .id-card { 
      break-inside: avoid; 
      page-break-inside: avoid; 
      border: 3px solid #000; 
      display: inline-block;
      margin: 10px;
    }
    
    .content {
      padding: 0;
    }
    
    .section {
      box-shadow: none;
      padding: 10px;
      border: none;
    }
  }
</style>
<script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
<script src="https://unpkg.com/html5-qrcode/html5-qrcode.min.js"></script>
</head>
<body>
  
  <div class="login-wrapper">
    <img src="https://i.ibb.co/F4DpWS4d/logo.png" alt="DSHS Logo" style="display:block; margin: 45px auto 8px; width:200px;">
  </div>

<div class="login" id="login">
  <div class="box">
    <h2>🎓 Login</h2>
    <input type="text" id="loginUsername" placeholder="👤 Username">
    <div class="pass-wrapper">
      <input type="password" id="loginPassword" placeholder="🔒 Password">
      <span onclick="togglePassword()">👁️</span>
    </div>
    <button onclick="login()" style="background: linear-gradient(135deg, var(--main-red) 0%, var(--main-blue) 100%); color: white; padding: 14px; font-size: 16px;">🚀 Login</button>
    <p id="msg"></p>
    <p style="font-size: 13px; margin-top: 12px;">Don't have an account yet? <span class="signup-link" onclick="showSignup()">Sign up!</span></p>
  </div>
</div>

<div class="login" id="signup" style="display:none;">
  <div class="box">
    <h2>📝 Student Sign Up</h2>
    <input type="text" id="signupName" placeholder="👤 Full Name">
    <input type="text" id="signupID" placeholder="🆔 Student I.D">
    <input type="text" id="signupSection" placeholder="🏫 Section">
    <input type="text" id="signupTrack" placeholder="📚 Track">
    <input type="text" id="signupStrand" placeholder="🎯 Strand">
    <input type="text" id="signupGradeLevel" placeholder="📖 Grade Level">
    <input type="text" id="signupUsername" placeholder="👤 Username">
    <input type="password" id="signupPass" placeholder="🔒 Password">
    <button onclick="submitSignup()" style="background: linear-gradient(135deg, var(--main-red) 0%, var(--main-blue) 100%); color: white; padding: 14px; font-size: 16px;">✅ Create Account</button>
    <button onclick="clearSignup()" style="background: var(--main-gray); color: white;">🔄 Clear</button>
    <p style="font-size: 13px; margin-top: 12px;">Already have an account? <span class="signup-link" onclick="showLogin()">Login</span></p>
  </div>
</div>

<div class="dashboard" id="dashboard">
  <button class="toggle-btn" id="toggleBtn" onclick="toggleMenu()">
    <span class="icon">☰</span>
    <span class="text">Menu</span>
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
      <div class="section"><h3>👋 Welcome</h3><p>Select an option from the menu to get started.</p></div>
    </div>
  </div>
</div>

<script>
  //------ HASH PASSWORD ------
function simpleHash(str){
  let hash = 0;
  for(let i=0;i<str.length;i++){
    const char = str.charCodeAt(i);
    hash = ((hash<<5)-hash)+char;
    hash = hash & hash;
  }
  return hash.toString();
}

//------ DATA ------
let role="", currentUser="";
let students = JSON.parse(localStorage.getItem('students')) || [
  {name:"Jibdel",id:"ST001",section:"12-A",track:"Academic",strand:"STEM",gradeLevel:"12",username:"jibdel",password:simpleHash("1234"),approved:true,pic:""},
  {name:"Viennes",id:"ST002",section:"12-B",track:"Academic",strand:"ABM",gradeLevel:"12",username:"viennes",password:simpleHash("5678"),approved:true,pic:""},
  {name:"Jurl",id:"ST003",section:"12-C",track:"Academic",strand:"STEM",gradeLevel:"12",username:"jurl",password:simpleHash("abcd"),approved:true,pic:""}
];
let teachers = JSON.parse(localStorage.getItem('teachers')) || [
  {name:"Mr. Smith",id:"TE001",position:"Teacher III",sectionHandled:"12-A",username:"teacher1",password:simpleHash("teach123")}
];
let parents = JSON.parse(localStorage.getItem('parents')) || [
  {name:"Parent of Jibdel",child:"Jibdel",username:"parentSt001",password:simpleHash("par123")}
];
let subjects = JSON.parse(localStorage.getItem('subjects')) || ["3I's","Genchem 2","P6 2","Perdev","CPAR","Entrepreneurship"];
let scheduleTimes = JSON.parse(localStorage.getItem('scheduleTimes')) || {"3I's":"8:00-9:00","Genchem 2":"9:00-10:00","P6 2":"10:00-11:00","Perdev":"11:45-12:30","CPAR":"12:30-1:00","Entrepreneurship":"1:00-2:00"};
let gradesData = JSON.parse(localStorage.getItem('gradesData')) || {};
if(Object.keys(gradesData).length===0){
  students.forEach(function(s){
    gradesData[s.name]={};
    subjects.forEach(function(sub){ gradesData[s.name][sub]=Math.floor(Math.random()*21)+80; });
  });
}
let attendanceData = JSON.parse(localStorage.getItem('attendanceData')) || {};
if(Object.keys(attendanceData).length===0){
  students.forEach(function(s){ attendanceData[s.name]={}; });
}
let bulletinBoard = JSON.parse(localStorage.getItem('bulletinBoard')) || ["Welcome to the DSHS School System!"];
let plannerData = JSON.parse(localStorage.getItem('plannerData')) || {};
let adminAccount = {name:"Administrator", username:"admin", password:simpleHash("admin123")};
  
  //------ SAVE ------
function saveData(){
  try{
    localStorage.setItem('students', JSON.stringify(students));
    localStorage.setItem('teachers', JSON.stringify(teachers));
    localStorage.setItem('parents', JSON.stringify(parents));
    localStorage.setItem('subjects', JSON.stringify(subjects));
    localStorage.setItem('scheduleTimes', JSON.stringify(scheduleTimes));
    localStorage.setItem('gradesData', JSON.stringify(gradesData));
    localStorage.setItem('attendanceData', JSON.stringify(attendanceData));
    localStorage.setItem('bulletinBoard', JSON.stringify(bulletinBoard));
    localStorage.setItem('plannerData', JSON.stringify(plannerData));
  } catch(e){ alert("Storage error."); }
}

//------ TOGGLE MENU ------
function toggleMenu(){
  const menu = document.getElementById("menu");
  const overlay = document.getElementById("menuOverlay");
  
  menu.classList.toggle("show");
  overlay.classList.toggle("show");
}

//------ PASSWORD TOGGLE ------
function togglePassword(){
  const p=document.getElementById("loginPassword");
  p.type=(p.type==="password")?"text":"password";
}

//------ LOGIN ------
function login(){
  const username=document.getElementById("loginUsername").value.trim();
  const pass=simpleHash(document.getElementById("loginPassword").value);
  let found=false;

  if(username===adminAccount.username && pass===adminAccount.password){ role="admin"; currentUser=adminAccount.name; found=true; }
  teachers.forEach(function(t){ if(username===t.username && pass===t.password){ role="teacher"; currentUser=t.name; found=true; }});
  students.forEach(function(s){ if(username===s.username && pass===s.password){ if(s.approved){ role="student"; currentUser=s.name; found=true; } else { document.getElementById("msg").innerText="Account not approved yet"; return; } }});
  parents.forEach(function(p){ if(username===p.username && pass===p.password){ role="parent"; currentUser=p.child; found=true; }});

  if(!found){ document.getElementById("msg").innerText="Invalid login or not approved yet"; return; }
  document.getElementById("login").style.display="none";
  document.getElementById("signup").style.display="none";
  document.getElementById("dashboard").style.display="block";
  loadDashboard();
}

//------ DASHBOARD ------
function loadDashboard(){
  document.getElementById("roleTitle").innerText = role.toUpperCase()+" DASHBOARD";
  const menu=document.getElementById("menu"); menu.innerHTML="";
  
  let items = [
    {name: "Attendance", icon: "📅"},
    {name: "Subject Schedule", icon: "📚"},
    {name: "My Info", icon: "👤"},
    {name: "Bulletin Board", icon: "📢"},
    {name: "School Map", icon: "🗺️"}
  ];
  
  if(role==="teacher") {
    items = [
      {name: "Attendance", icon: "📅"},
      {name: "Subject Schedule", icon: "📚"},
      {name: "My Info", icon: "👤"},
      {name: "Bulletin Board", icon: "📢"},
      {name: "Grades", icon: "📊"},
      {name: "Parent Chat", icon: "💬"},
      {name: "My Planner", icon: "📝"},
      {name: "Emergency Numbers", icon: "🚨"},
      {name: "School Map", icon: "🗺️"}
    ];
  }
  else if(role==="student") {
    items = [
      {name: "Attendance", icon: "📅"},
      {name: "Subject Schedule", icon: "📚"},
      {name: "My Info", icon: "👤"},
      {name: "Bulletin Board", icon: "📢"},
      {name: "Grades", icon: "📊"},
      {name: "QR Code", icon: "🔳"},
      {name: "My Mood", icon: "😊"},
      {name: "My Planner", icon: "📝"},
      {name: "Emergency Numbers", icon: "🚨"},
      {name: "School Map", icon: "🗺️"}
    ];
  }
  else if(role==="parent") {
    items = [
      {name: "Child Attendance", icon: "📅"},
      {name: "Child Grades", icon: "📊"},
      {name: "Child Schedule", icon: "📚"},
      {name: "My Info", icon: "👤"},
      {name: "Bulletin Board", icon: "📢"},
      {name: "Teacher Chat", icon: "💬"},
      {name: "Emergency Numbers", icon: "🚨"},
      {name: "School Map", icon: "🗺️"}
    ];
  }
  else if(role==="admin") {
    items = [
      {name: "Student Approval", icon: "✅"},
      {name: "Create Teacher", icon: "👨‍🏫"},
      {name: "All Students", icon: "👨‍🎓"},
      {name: "Parent Accounts", icon: "👪"},
      {name: "Manage Users", icon: "⚙️"},
      {name: "Bulletin Board", icon: "📢"},
      {name: "Emergency Numbers", icon: "🚨"},
      {name: "School Map", icon: "🗺️"}
    ];
  }

  menu.innerHTML = '<div class="menu-header"><h3>🎓 DSHS Menu</h3><p>👤 ' + currentUser + '</p></div>';
  
  items.forEach(function(item){
    const btn=document.createElement("button");
    btn.innerHTML = '<span class="tab-icon">' + item.icon + '</span> ' + item.name;
    btn.onclick=function() {
      toggleMenu();
      loadSection(item.name);
    };
    menu.appendChild(btn);
  });

  const logoutBtn=document.createElement("button"); 
  logoutBtn.innerHTML = '<span class="tab-icon">⬅</span> Logout'; 
  logoutBtn.className="logout"; 
  logoutBtn.onclick=function() {
    toggleMenu();
    logout();
  }; 
  menu.appendChild(logoutBtn);
}

//------ LOGOUT ------
function logout(){
  role=""; currentUser="";
  document.getElementById("dashboard").style.display="none";
  document.getElementById("login").style.display="flex";
  document.getElementById("menu").classList.remove("show");
  document.getElementById("menuOverlay").classList.remove("show");
}

//------ SHOW SIGNUP/LOGIN ------
function showSignup(){ document.getElementById("login").style.display="none"; document.getElementById("signup").style.display="flex"; }
function showLogin(){ document.getElementById("signup").style.display="none"; document.getElementById("login").style.display="flex"; }
function clearSignup(){ ["signupName","signupID","signupSection","signupTrack","signupStrand","signupGradeLevel","signupUsername","signupPass"].forEach(function(id){ document.getElementById(id).value=""; }); }

//------ SUBMIT SIGNUP ------
function submitSignup(){
  let name=document.getElementById("signupName").value.trim();
  let id=document.getElementById("signupID").value.trim();
  let section=document.getElementById("signupSection").value.trim();
  let track=document.getElementById("signupTrack").value.trim();
  let strand=document.getElementById("signupStrand").value.trim();
  let gradeLevel=document.getElementById("signupGradeLevel").value.trim();
  let username=document.getElementById("signupUsername").value.trim();
  let password=document.getElementById("signupPass").value.trim();
  if(!name||!id||!section||!track||!strand||!gradeLevel||!username||!password){ alert("All fields required!"); return; }
  if(password.length<6){ alert("Password must be at least 6 characters!"); return; }
  if(students.find(function(s){ return s.username===username; }) || students.find(function(s){ return s.id===id; })){ alert("Username or ID already exists!"); return; }

  // Generate parent account automatically
  let parentUsername = "parent" + id;
  let parentPassword = Math.random().toString(36).slice(-6);
  
  students.push({name,id,section,track,strand,gradeLevel,username,password:simpleHash(password),approved:false,pic:""});
  gradesData[name]={}; subjects.forEach(function(sub){ gradesData[name][sub]=0; });
  attendanceData[name]={};
  
  // Create parent account automatically
  parents.push({
    name: "Parent of " + name,
    child: name,
    username: parentUsername,
    password: simpleHash(parentPassword)
  });
  
  // Store parent credentials for admin to see
  let parentAccounts = JSON.parse(localStorage.getItem('parentAccounts')) || [];
  parentAccounts.push({
    studentName: name,
    studentId: id,
    section: section,
    parentUsername: parentUsername,
    parentPassword: parentPassword
  });
  localStorage.setItem('parentAccounts', JSON.stringify(parentAccounts));
  
  saveData();
  alert("Signup successful! Wait for admin approval.\n\nParent Account:\nUsername: " + parentUsername + "\nPassword: " + parentPassword);
  clearSignup(); showLogin();
}
  
  //------ LOAD SECTION ------
function loadSection(tab){
  const content=document.getElementById("content");
  content.innerHTML="";
  const section=document.createElement("div"); section.className="section";

  //------ ATTENDANCE ------
  if(tab==="Attendance" || tab==="Child Attendance"){
    section.innerHTML="<h3>📅 Attendance</h3>";
    
    let studentName = currentUser;
    if(role === "teacher") {
      const selectStudent = document.createElement("select");
      selectStudent.id = "attendanceStudentSelect";
      const teacher = teachers.find(function(t){ return t.name === currentUser; });
      students.filter(function(s){ return s.section === teacher.sectionHandled; }).forEach(function(s){
        const opt = document.createElement("option");
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
    } else if(role === "parent") {
      const selectStudent = document.createElement("select");
      selectStudent.id = "attendanceStudentSelect";
      const parent = parents.find(function(p){ return p.child === currentUser; });
      if(parent) {
        const child = students.find(function(s){ return s.name === parent.child; });
        if(child) {
          const opt = document.createElement("option");
          opt.value = child.name;
          opt.innerText = child.name;
          selectStudent.appendChild(opt);
          studentName = child.name;
        }
      }
      section.appendChild(selectStudent);
    }
    
    const dateInput = document.createElement("input");
    dateInput.type = "month";
    dateInput.value = new Date().toISOString().split("T")[0].substring(0, 7);
    section.appendChild(dateInput);
    
    const qrDiv = document.createElement("div");
    qrDiv.id = "scanner-container";
    section.appendChild(qrDiv);
    
    const resultDiv = document.createElement("div");
    resultDiv.id = "scanner-result";
    section.appendChild(resultDiv);
    
    content.appendChild(section);
    
    renderAttendanceCalendar(section, studentName);
    
    //------ QR SCANNER FOR TEACHERS ------
    if(role === "teacher") {
      const scannerDiv = document.createElement("div");
      scannerDiv.id = "qr-scanner";
      scannerDiv.className = "qr-scanner-container";
      scannerDiv.style.marginTop = "20px";
      section.appendChild(scannerDiv);
      
      const scannerResult = document.createElement("div");
      scannerResult.id = "scanner-result";
      scannerResult.className = "scanner-result";
      scannerResult.style.display = "none";
      section.appendChild(scannerResult);
      
      setTimeout(function(){
        try {
          const html5QrCode = new Html5Qrcode("qr-scanner");
          html5QrCode.start(
            { facingMode: "environment" },
            { fps: 10, qrbox: 250 },
            function(decodedText){
              const parts = decodedText.split("-");
              const scannedStudent = parts[0];
              const today = new Date().toISOString().split("T")[0];
              
              if(attendanceData[scannedStudent]) {
                attendanceData[scannedStudent][today] = "P";
                saveData();
                const resultDiv = document.getElementById("scanner-result");
                resultDiv.style.display = "block";
                resultDiv.className = "scanner-result success";
                resultDiv.innerHTML = "✅ Marked " + scannedStudent + " present on " + today;
                renderAttendanceCalendar(section, studentName);
              }
              html5QrCode.stop();
            },
            function(errorMessage){}
          ).catch(function(err){
            console.log("Scanner error:", err);
            const scannerResult = document.getElementById("scanner-result");
            if(scannerResult) {
              scannerResult.style.display = "block";
              scannerResult.className = "scanner-result error";
              scannerResult.innerHTML = "❌ Camera access denied or not available";
            }
          });
        } catch(e) {
          console.log("Scanner initialization error:", e);
          const scannerResult = document.getElementById("scanner-result");
          if(scannerResult) {
            scannerResult.style.display = "block";
            scannerResult.className = "scanner-result error";
            scannerResult.innerHTML = "❌ QR Scanner not supported on this device";
          }
        }
      }, 500);
    }
  }
  
  //------ GRADES ------
  if(tab === "Grades" || tab === "Child Grades"){
    section.innerHTML = "<h3>📊 Grades</h3>";
    
    // Semester Selector
    const semSelector = document.createElement("div");
    semSelector.className = "sem-selector";
    semSelector.innerHTML = `
      <button class="sem-btn active" onclick="selectSemester(1, this)">1st Semester</button>
      <button class="sem-btn" onclick="selectSemester(2, this)">2nd Semester</button>
    `;
    section.appendChild(semSelector);
    
    // Quarter Selector
    const quarterSelector = document.createElement("div");
    quarterSelector.className = "quarter-selector";
    quarterSelector.id = "quarterSelector";
    quarterSelector.innerHTML = `
      <button class="quarter-btn active" onclick="selectQuarter(1, this)">1st Quarter</button>
      <button class="quarter-btn" onclick="selectQuarter(2, this)">2nd Quarter</button>
      <button class="quarter-btn" onclick="selectQuarter(3, this)">3rd Quarter</button>
      <button class="quarter-btn" onclick="selectQuarter(4, this)">4th Quarter</button>
    `;
    section.appendChild(quarterSelector);
    
    let studentName = currentUser;
    if(role === "teacher") {
      const selectStudent = document.createElement("select");
      selectStudent.id = "gradesStudentSelect";
      const teacher = teachers.find(function(t){ return t.name === currentUser; });
      students.filter(function(s){ return s.section === teacher.sectionHandled; }).forEach(function(s){
        const opt = document.createElement("option");
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
    } else if(role === "parent") {
      const parent = parents.find(function(p){ return p.child === currentUser; });
      if(parent) {
        const child = students.find(function(s){ return s.name === parent.child; });
        if(child) studentName = child.name;
      }
    }
    
    content.appendChild(section);
    renderGradesTable(section, studentName);
  }
  
  //------ SUBJECT SCHEDULE ------
  if(tab === "Subject Schedule" || tab === "Child Schedule"){
    section.innerHTML = "<h3>📚 Subject Schedule</h3>";
    
    let studentName = currentUser;
    if(role === "parent") {
      const parent = parents.find(function(p){ return p.child === currentUser; });
      if(parent) {
        const child = students.find(function(s){ return s.name === parent.child; });
        if(child) studentName = child.name;
      }
    }
    
    const scheduleBox = document.createElement("div");
    scheduleBox.className = "schedule-box";
    
    subjects.forEach(function(sub){
      const div = document.createElement("div");
      const time = scheduleTimes[sub] || "TBA";
      div.innerHTML = "<strong>" + sub + "</strong><br>" + time;
      scheduleBox.appendChild(div);
    });
    section.appendChild(scheduleBox);
    
    if(role === "teacher" || role === "admin") {
      section.innerHTML += "<h4>Manage Subjects</h4>";
      subjects.forEach(function(sub, index){
        const item = document.createElement("div");
        item.className = "subject-item";
        item.innerHTML = '<input type="text" value="' + sub + '" onchange="updateSubject(' + index + ', this.value)">' +
          '<input type="text" value="' + (scheduleTimes[sub] || '') + '" placeholder="Time" onchange="updateScheduleTime(\'' + sub + '\', this.value)">' +
          '<button onclick="deleteSubject(' + index + ')" style="width:auto;background:#dc3545;color:white;">🗑️ Delete</button>';
        section.appendChild(item);
      });
      
      const addDiv = document.createElement("div");
      addDiv.className = "subject-item";
      addDiv.innerHTML = '<input type="text" id="newSubjectName" placeholder="New Subject">' +
        '<input type="text" id="newSubjectTime" placeholder="Time">' +
        '<button onclick="addSubject()" style="width:auto;background:#28a745;color:white;">➕ Add</button>';
      section.appendChild(addDiv);
    }
  }

  //------ QR CODE ------
  if(tab === "QR Code" && role === "student"){
    section.innerHTML = "<h3>🔳 Your QR Code</h3>";
    
    // Get student info for QR code
    const student = students.find(function(s){ return s.name === currentUser; });
    const studentId = student ? student.id : "ST000";
    const studentSection = student ? student.section : "Unknown";
    
    const qrDiv = document.createElement("div");
    qrDiv.id = "qr-code";
    qrDiv.style.textAlign = "center";
    qrDiv.style.padding = "20px";
    section.appendChild(qrDiv);
    
    // Create QR code with student data
    const qrCodeData = currentUser + "-" + studentId + "-" + studentSection;
    new QRCode(qrDiv, {
      text: qrCodeData,
      width: 200,
      height: 200,
      colorDark: "#003366",
      colorLight: "#ffffff",
      correctLevel: QRCode.CorrectLevel.H
    });
    
    section.innerHTML += "<p style='text-align:center;margin-top:15px;'>📱 Scan this QR code for attendance</p>";
    
    //------ PERFORMANCE BOX ------
    const perfBox = document.createElement("div");
    perfBox.className = "performance-box";
    const totalDays = Object.keys(attendanceData[currentUser] || {}).length;
    const presentDays = Object.values(attendanceData[currentUser] || {}).filter(function(s){ return s === "P"; }).length;
    const absentDays = totalDays - presentDays;
    const percentage = totalDays > 0 ? Math.round((presentDays / totalDays) * 100) : 0;
    
    perfBox.innerHTML = "<h3>📈 Your Attendance Performance</h3>" +
      "<div class='performance-stats'>" +
      "<div class='stat-item'><div class='stat-number'>" + presentDays + "</div><div class='stat-label'>✅ Present</div></div>" +
      "<div class='stat-item'><div class='stat-number'>" + absentDays + "</div><div class='stat-label'>❌ Absent</div></div>" +
      "<div class='stat-item'><div class='stat-number'>" + percentage + "%</div><div class='stat-label'>📊 Rate</div></div>" +
      "</div>";
    section.appendChild(perfBox);
  }

  //------ CHAT ------
  if(tab === "Parent Chat" || tab === "Teacher Chat"){
    section.innerHTML = "<h3>💬 " + tab + "</h3>";
    
    if(tab === "Parent Chat" && role === "teacher") {
      section.innerHTML += "<label>Select Parent:</label>";
      const parentSelect = document.createElement("select");
      parentSelect.id = "chatParentSelect";
      
      const teacher = teachers.find(function(t){ return t.name === currentUser; });
      if(teacher) {
        students.filter(function(s){ return s.section === teacher.sectionHandled; }).forEach(function(s){
          const parent = parents.find(function(p){ return p.child === s.name; });
          if(parent) {
            const opt = document.createElement("option");
            opt.value = parent.username;
            opt.innerText = parent.name;
            parentSelect.appendChild(opt);
          }
        });
      }
      section.appendChild(parentSelect);
    }
    
    if(tab === "Teacher Chat" && role === "parent") {
      section.innerHTML += "<label>Select Teacher:</label>";
      const teacherSelect = document.createElement("select");
      teacherSelect.id = "chatTeacherSelect";
      
      const parent = parents.find(function(p){ return p.child === currentUser; });
      if(parent) {
        const child = students.find(function(s){ return s.name === parent.child; });
        if(child) {
          teachers.filter(function(t){ return t.sectionHandled === child.section; }).forEach(function(t){
            const opt = document.createElement("option");
            opt.value = t.username;
            opt.innerText = t.name;
            teacherSelect.appendChild(opt);
          });
        }
      }
      section.appendChild(teacherSelect);
    }
    
    const chatbox = document.createElement("div");
    chatbox.id = "chatbox";
    chatbox.className = "chatbox";
    chatbox.innerHTML = "<p>💬 Chat messages will appear here...</p>";
    section.appendChild(chatbox);
    
    const input = document.createElement("input");
    input.type = "text";
    input.id = "chatInput";
    input.placeholder = "Type your message...";
    section.appendChild(input);
    
    const sendBtn = document.createElement("button");
    sendBtn.innerText = "📤 Send";
    sendBtn.onclick = function() { sendChatMessage(tab); };
    section.appendChild(sendBtn);
  }

  //------ MY INFO ------
  if(tab === "My Info"){
    section.innerHTML = "<h3>👤 My Information</h3>";
    
    let user = null;
    
    if(role === "student") {
      user = students.find(function(s){ return s.name === currentUser; });
    } else if(role === "teacher") {
      user = teachers.find(function(t){ return t.name === currentUser; });
    } else if(role === "parent") {
      user = parents.find(function(p){ return p.child === currentUser; });
    } else if(role === "admin") {
      user = adminAccount;
    }
    
    if(user) {
      // Profile Card
      section.innerHTML += '<div class="profile-card">' +
        '<div class="profile-photo">' +
        '<img id="profilePic" src="' + (user.pic || '') + '" alt="Profile Photo" onerror="this.src=\'https://via.placeholder.com/120\'">' +
        '</div>' +
        '<h3>' + user.name + '</h3>' +
        '<p>' + (user.section || user.sectionHandled || user.position || 'User') + '</p>' +
        '</div>';
      
      // Upload Photo
      section.innerHTML += '<div style="text-align:center;margin-bottom:20px;">' +
        '<input type="file" id="uploadPic" accept="image/*" style="width:auto;">' +
        '<button onclick="uploadProfilePhoto()" style="width:auto;background:linear-gradient(135deg, #8B0000 0%, #003366 100%);color:white;padding:10px 20px;">📷 Upload Photo</button>' +
        '</div>';
      
      // Profile Details
      const detailsDiv = document.createElement("div");
      detailsDiv.className = "profile-details";
      
      let detailsHTML = "";
      if(user.id) detailsHTML += '<div class="detail-row"><span class="detail-label">🆔 ID:</span><span class="detail-value">' + user.id + '</span></div>';
      if(user.username) detailsHTML += '<div class="detail-row"><span class="detail-label">👤 Username:</span><span class="detail-value">' + user.username + '</span></div>';
      if(user.section) detailsHTML += '<div class="detail-row"><span class="detail-label">🏫 Section:</span><span class="detail-value">' + user.section + '</span></div>';
      if(user.sectionHandled) detailsHTML += '<div class="detail-row"><span class="detail-label">🏫 Section Handled:</span><span class="detail-value">' + user.sectionHandled + '</span></div>';
      if(user.track) detailsHTML += '<div class="detail-row"><span class="detail-label">📚 Track:</span><span class="detail-value">' + user.track + '</span></div>';
      if(user.strand) detailsHTML += '<div class="detail-row"><span class="detail-label">🎯 Strand:</span><span class="detail-value">' + user.strand + '</span></div>';
      if(user.gradeLevel) detailsHTML += '<div class="detail-row"><span class="detail-label">📖 Grade Level:</span><span class="detail-value">' + user.gradeLevel + '</span></div>';
      if(user.position) detailsHTML += '<div class="detail-row"><span class="detail-label">💼 Position:</span><span class="detail-value">' + user.position + '</span></div>';
      
      detailsDiv.innerHTML = detailsHTML;
      section.appendChild(detailsDiv);
    } else {
      section.innerHTML += "<p>❌ User information not found.</p>";
    }
  }

  //------ BULLETIN BOARD ------
  if(tab === "Bulletin Board"){
    section.innerHTML = "<h3>📢 Bulletin Board</h3>";
    
    const board = document.createElement("div");
    bulletinBoard.forEach(function(msg, index){
      const msgDiv = document.createElement("div");
      msgDiv.style.padding = "18px";
      msgDiv.style.borderBottom = "2px solid #ddd";
      msgDiv.style.marginBottom = "12px";
      msgDiv.style.borderRadius = "8px";
      msgDiv.style.background = "#f8f9fa";
      msgDiv.innerHTML = "<p>" + msg + "</p>";
      
      if(role === "teacher" || role === "admin") {
        const deleteBtn = document.createElement("button");
        deleteBtn.innerText = "🗑️ Delete";
        deleteBtn.style.width = "auto";
        deleteBtn.style.background = "#dc3545";
        deleteBtn.style.color = "white";
        deleteBtn.style.padding = "8px 15px";
        deleteBtn.onclick = function() {
          bulletinBoard.splice(index, 1);
          saveData();
          loadSection("Bulletin Board");
        };
        msgDiv.appendChild(deleteBtn);
      }
      
      board.appendChild(msgDiv);
    });
    section.appendChild(board);
    
    if(role === "teacher" || role === "admin") {
      const newMsg = document.createElement("input");
      newMsg.id = "newAnnouncement";
      newMsg.placeholder = "Type new announcement...";
      section.appendChild(newMsg);
      
      const addBtn = document.createElement("button");
      addBtn.innerText = "➕ Add Announcement";
      addBtn.style.background = "linear-gradient(135deg, #8B0000 0%, #003366 100%)";
      addBtn.style.color = "white";
      addBtn.onclick = function() {
        if(newMsg.value.trim()) {
          bulletinBoard.push(newMsg.value.trim());
          saveData();
          loadSection("Bulletin Board");
        }
      };
      section.appendChild(addBtn);
    }
  }
  
  //------ ADMIN FUNCTIONS ------
  if(role === "admin"){
    //------ STUDENT APPROVAL ------
    if(tab === "Student Approval"){
      section.innerHTML = "<h3>✅ Approve Students</h3>";
      const pendingStudents = students.filter(function(s){ return !s.approved; });
      
      if(pendingStudents.length === 0) {
        section.innerHTML += "<p>✅ No pending approvals.</p>";
      } else {
        pendingStudents.forEach(function(s){
          const div = document.createElement("div");
          div.style.padding = "18px";
          div.style.border = "2px solid #ddd";
          div.style.marginBottom = "12px";
          div.style.borderRadius = "10px";
          div.style.background = "#fff3cd";
          div.innerHTML = '<p><strong>👤 Name:</strong> ' + s.name + '</p>' +
            '<p><strong>🆔 ID:</strong> ' + s.id + '</p>' +
            '<p><strong>🏫 Section:</strong> ' + s.section + '</p>' +
            '<button onclick="approveStudent(\'' + s.id + '\')" style="background:#28a745;color:white;width:auto;padding:12px 24px;margin-right:10px;">✅ Approve</button>' +
            '<button onclick="deleteStudent(\'' + s.id + '\')" style="background:#dc3545;color:white;width:auto;padding:12px 24px;">🗑️ Delete</button>';
          section.appendChild(div);
        });
      }
    }
    
    //------ CREATE TEACHER ------
    if(tab === "Create Teacher"){
      section.innerHTML = "<h3>👨‍🏫 Create Teacher Account</h3>";
      section.innerHTML += '<input type="text" id="newTeacherName" placeholder="👤 Full Name">' +
        '<input type="text" id="newTeacherID" placeholder="🆔 Teacher ID">' +
        '<input type="text" id="newTeacherPosition" placeholder="💼 Position">' +
        '<input type="text" id="newTeacherSection" placeholder="🏫 Section Handled">' +
        '<input type="text" id="newTeacherUsername" placeholder="👤 Username">' +
        '<input type="password" id="newTeacherPassword" placeholder="🔒 Password">' +
        '<button onclick="createTeacher()" style="background:linear-gradient(135deg, #8B0000 0%, #003366 100%);color:white;padding:14px;">👨‍🏫 Create Teacher</button>';
    }
    
    //------ ALL STUDENTS (PRINT ID) ------
    if(tab === "All Students"){
      section.innerHTML = "<h3>👨‍🎓 All Students</h3>";
      
      const printControls = document.createElement("div");
      printControls.className = "print-controls";
      printControls.innerHTML = '<h4>🖨️ Print ID Cards</h4>' +
        '<p>Check the students you want to print, then click Print Selected.</p>' +
        '<label><input type="checkbox" id="selectAllStudents" onchange="toggleSelectAllStudents()" style="width:auto;"> ✅ Select All</label><br><br>' +
        '<button onclick="printSelectedIDs()" style="background:#28a745;color:white;width:auto;padding:12px 24px;">🖨️ Print Selected</button>';
      section.appendChild(printControls);
      
      const filterSection = document.createElement("select");
      filterSection.id = "filterSection";
      filterSection.innerHTML = "<option value='all'>📋 All Sections</option>";
      const sections = [...new Set(students.map(function(s){ return s.section; }))];
      sections.forEach(function(sec){
        const opt = document.createElement("option");
        opt.value = sec;
        opt.innerText = sec;
        filterSection.appendChild(opt);
      });
      section.appendChild(filterSection);
      
      const studentsContainer = document.createElement("div");
      studentsContainer.id = "studentsContainer";
      section.appendChild(studentsContainer);
      
      filterSection.onchange = function(){
        renderStudentsBySection(studentsContainer, this.value);
      };
      
      renderStudentsBySection(studentsContainer, "all");
    }
    
    //------ PARENT ACCOUNTS ------
    if(tab === "Parent Accounts"){
      section.innerHTML = "<h3>👪 Parent Accounts</h3>";
      section.innerHTML += "<p>📝 These credentials are auto-generated when students sign up.</p>";
      
      const filterSection = document.createElement("select");
      filterSection.id = "filterParentSection";
      filterSection.innerHTML = "<option value='all'>📋 All Sections</option>";
      const sections = [...new Set(students.map(function(s){ return s.section; }))];
      sections.forEach(function(sec){
        const opt = document.createElement("option");
        opt.value = sec;
        opt.innerText = sec;
        filterSection.appendChild(opt);
      });
      section.appendChild(filterSection);
      
      const parentContainer = document.createElement("div");
      parentContainer.id = "parentContainer";
      section.appendChild(parentContainer);
      
      filterSection.onchange = function(){
        renderParentAccounts(parentContainer, this.value);
      };
      
      renderParentAccounts(parentContainer, "all");
    }
    
    //------ MANAGE USERS ------
    if(tab === "Manage Users"){
      section.innerHTML = "<h3>⚙️ Manage Users</h3>";
      
      section.innerHTML += "<h4>👨‍🎓 Students</h4>";
      const studentsTable = document.createElement("table");
      studentsTable.innerHTML = "<tr><th>Name</th><th>ID</th><th>Section</th><th>Action</th></tr>";
      students.forEach(function(s){
        const tr = document.createElement("tr");
        tr.innerHTML = '<td>' + s.name + '</td><td>' + s.id + '</td><td>' + s.section + '</td>' +
          '<td><button onclick="deleteStudent(\'' + s.id + '\')" style="background:#dc3545;color:white;width:auto;padding:6px 12px;">🗑️ Delete</button></td>';
        studentsTable.appendChild(tr);
      });
      section.appendChild(studentsTable);
      
      section.innerHTML += "<h4 style='margin-top:25px;'>👨‍🏫 Teachers</h4>";
      const teachersTable = document.createElement("table");
      teachersTable.innerHTML = "<tr><th>Name</th><th>ID</th><th>Section</th><th>Action</th></tr>";
      teachers.forEach(function(t){
        const tr = document.createElement("tr");
        tr.innerHTML = '<td>' + t.name + '</td><td>' + t.id + '</td><td>' + t.sectionHandled + '</td>' +
          '<td><button onclick="deleteTeacher(\'' + t.id + '\')" style="background:#dc3545;color:white;width:auto;padding:6px 12px;">🗑️ Delete</button></td>';
        teachersTable.appendChild(tr);
      });
      section.appendChild(teachersTable);
    }
  }
  
  //------ MY PLANNER (TEACHER & STUDENT) ------
  if(tab === "My Planner" && (role === "teacher" || role === "student")){
    section.innerHTML = "<h3>📝 My Planner</h3>";
    
    if(!plannerData[currentUser]) {
      plannerData[currentUser] = { daily: [], weekly: [], monthly: [] };
    }
    
    const plannerContainer = document.createElement("div");
    plannerContainer.className = "planner-container";
    
    // Daily Goals
    const dailySection = document.createElement("div");
    dailySection.className = "planner-section";
    dailySection.innerHTML = "<h4>📅 Daily Goals</h4>";
    plannerData[currentUser].daily.forEach(function(goal, index){
      const item = document.createElement("div");
      item.className = "planner-item" + (goal.completed ? " completed" : "");
      item.innerHTML = '<input type="checkbox"' + (goal.completed ? " checked" : "") + ' onchange="togglePlannerGoal(\'daily\', ' + index + ')">' +
        '<span class="goal-text">' + goal.text + '</span>' +
        '<span class="goal-time">' + (goal.time || "") + '</span>' +
        '<button class="alarm-btn" onclick="setAlarm(\'' + goal.time + '\')">⏰</button>' +
        '<button onclick="deletePlannerGoal(\'daily\', ' + index + ')" style="width:auto;background:#dc3545;color:white;padding:6px 10px;">×</button>';
      dailySection.appendChild(item);
    });
    dailySection.innerHTML += '<input type="text" id="dailyGoalInput" placeholder="Add daily goal..." style="width:55%;">' +
      '<input type="time" id="dailyGoalTime" style="width:auto;">' +
      '<button onclick="addPlannerGoal(\'daily\')" style="width:auto;background:#28a745;color:white;">➕ Add</button>';
    plannerContainer.appendChild(dailySection);
    
    // Weekly Goals
    const weeklySection = document.createElement("div");
    weeklySection.className = "planner-section";
    weeklySection.innerHTML = "<h4>📆 Weekly Goals</h4>";
    plannerData[currentUser].weekly.forEach(function(goal, index){
      const item = document.createElement("div");
      item.className = "planner-item" + (goal.completed ? " completed" : "");
      item.innerHTML = '<input type="checkbox"' + (goal.completed ? " checked" : "") + ' onchange="togglePlannerGoal(\'weekly\', ' + index + ')">' +
        '<span class="goal-text">' + goal.text + '</span>' +
        '<span class="goal-time">' + (goal.time || "") + '</span>' +
        '<button onclick="deletePlannerGoal(\'weekly\', ' + index + ')" style="width:auto;background:#dc3545;color:white;padding:6px 10px;">×</button>';
      weeklySection.appendChild(item);
    });
    weeklySection.innerHTML += '<input type="text" id="weeklyGoalInput" placeholder="Add weekly goal..." style="width:55%;">' +
      '<input type="date" id="weeklyGoalDate" style="width:auto;">' +
      '<button onclick="addPlannerGoal(\'weekly\')" style="width:auto;background:#28a745;color:white;">➕ Add</button>';
    plannerContainer.appendChild(weeklySection);
    
    // Monthly Goals
    const monthlySection = document.createElement("div");
    monthlySection.className = "planner-section";
    monthlySection.innerHTML = "<h4>📆 Monthly Goals</h4>";
    plannerData[currentUser].monthly.forEach(function(goal, index){
      const item = document.createElement("div");
      item.className = "planner-item" + (goal.completed ? " completed" : "");
      item.innerHTML = '<input type="checkbox"' + (goal.completed ? " checked" : "") + ' onchange="togglePlannerGoal(\'monthly\', ' + index + ')">' +
        '<span class="goal-text">' + goal.text + '</span>' +
        '<span class="goal-time">' + (goal.time || "") + '</span>' +
        '<button onclick="deletePlannerGoal(\'monthly\', ' + index + ')" style="width:auto;background:#dc3545;color:white;padding:6px 10px;">×</button>';
      monthlySection.appendChild(item);
    });
    monthlySection.innerHTML += '<input type="text" id="monthlyGoalInput" placeholder="Add monthly goal..." style="width:55%;">' +
      '<input type="date" id="monthlyGoalDate" style="width:auto;">' +
      '<button onclick="addPlannerGoal(\'monthly\')" style="width:auto;background:#28a745;color:white;">➕ Add</button>';
    plannerContainer.appendChild(monthlySection);
    
    section.appendChild(plannerContainer);
  }
  
  //------ MY MOOD (AI CHAT FOR STUDENTS) ------
  if(tab === "My Mood" && role === "student"){
    section.innerHTML = "<h3>🤗 My Mood - AI Companion</h3>";
    section.innerHTML += "<p>Share how you're feeling and I'll help you feel better!</p>";
    
    // Mood selector
    const moodDiv = document.createElement("div");
    moodDiv.className = "mood-selector";
    moodDiv.innerHTML = '<button class="mood-btn" onclick="selectMood(\'😊\')">😊</button>' +
      '<button class="mood-btn" onclick="selectMood(\'😢\')">😢</button>' +
      '<button class="mood-btn" onclick="selectMood(\'😠\')">😠</button>' +
      '<button class="mood-btn" onclick="selectMood(\'😰\')">😰</button>' +
      '<button class="mood-btn" onclick="selectMood(\'😴\')">😴</button>' +
      '<button class="mood-btn" onclick="selectMood(\'🤗\')">🤗</button>';
    section.appendChild(moodDiv);
    
    // Chat container (responsive)
    const chatContainer = document.createElement("div");
    chatContainer.className = "mood-chat-container";
    
    const chatbox = document.createElement("div");
    chatbox.id = "moodChatbox";
    chatbox.className = "chatbox";
    chatbox.style.background = "#f0f8ff";
    chatbox.innerHTML = '<div class="chat-message chat-ai"><strong>🤗 AI Companion:</strong> Hi! How are you feeling today? You can select a mood above or just tell me what\'s on your mind.</div>';
    chatContainer.appendChild(chatbox);
    
    // Input area
    const inputArea = document.createElement("div");
    inputArea.className = "input-area";
    
    const input = document.createElement("input");
    input.type = "text";
    input.id = "moodInput";
    input.placeholder = "Tell me what's on your mind...";
    inputArea.appendChild(input);
    
    const sendBtn = document.createElement("button");
    sendBtn.innerText = "💬 Share";
    sendBtn.style.background = "#6c5ce7";
    sendBtn.style.color = "white";
    sendBtn.onclick = function() { sendMoodMessage(); };
    inputArea.appendChild(sendBtn);
    
    chatContainer.appendChild(inputArea);
    section.appendChild(chatContainer);
    
    section.innerHTML += '<div style="margin-top:18px;padding:15px;background:#fff3cd;border-radius:8px;font-size:13px;">' +
      '<strong>💡 Tips:</strong> Talk about your feelings! I\'m here to listen and help.' +
      '</div>';
  }
  
 //------ EMERGENCY NUMBERS ------
  if(tab === "Emergency Numbers"){
    section.innerHTML = "<h3>🚨 Emergency Numbers</h3>";
    const numbers = [
      {name:"🚔 PNP DUMINGAG", num:"099859558677"},
      {name:"🔥 BFP DUMINGAG", num:"09300459871"},
      {name:"🏛️ LGU DUMINGAG", num:"09482121024"},
      {name:"🆘 MDRRMO DUMINGAG", num:"09098046609"},
      {name:"📞 DSWD Makabata Helpline", num:"1383"}
    ];
    numbers.forEach(function(n){
      const div = document.createElement("div");
      div.style.margin = "12px 0";
      div.innerHTML = '<a href="tel:' + n.num + '" style="display:block;padding:18px;background:linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);border-radius:10px;border-left:5px solid #dc3545;text-decoration:none;color:#333;transition:all 0.3s;">' +
        '<strong>' + n.name + '</strong><br>' + n.num + '</a>';
      section.appendChild(div);
    });
  }
  
  //------ SCHOOL MAP ------
  if(tab === "School Map"){
    section.innerHTML = "<h3>🗺️ School Map</h3>";
    
    const mapContainer = document.createElement("div");
    mapContainer.className = "school-map-container";
    mapContainer.innerHTML = `
      <img src="https://ibb.co/hxG306gd" alt="DSHS School Map" style="max-width:100%;border-radius:10px;box-shadow:0 4px 15px rgba(0,0,0,0.2);">
    `;
    section.appendChild(mapContainer);
  }
  
  content.appendChild(section);
}
  
//------ RENDER ATTENDANCE CALENDAR ------
function renderAttendanceCalendar(container, studentName) {
  const existingCalendar = document.getElementById("attendanceCalendar");
  if(existingCalendar) existingCalendar.remove();
  
  const calendar = document.createElement("div");
  calendar.id = "attendanceCalendar";
  calendar.className = "attendance-calendar";
  
  const days = ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"];
  days.forEach(function(day){
    const div = document.createElement("div");
    div.className = "attendance-day header";
    div.innerText = day;
    calendar.appendChild(div);
  });
  
  const dateInput = document.querySelector('input[type="month"]');
  const selectedDate = dateInput ? dateInput.value : new Date().toISOString().split("T")[0].substring(0, 7);
  const yearMonth = selectedDate.split("-");
  const year = yearMonth[0];
  const month = yearMonth[1];
  
  const daysInMonth = new Date(year, month, 0).getDate();
  const firstDay = new Date(year, month - 1, 1).getDay();
  
  for(let i = 0; i < firstDay; i++) {
    const div = document.createElement("div");
    div.className = "attendance-day";
    div.style.background = "#f9f9f9";
    calendar.appendChild(div);
  }
  
  for(let day = 1; day <= daysInMonth; day++) {
    const dateStr = year + "-" + month.padStart(2, '0') + "-" + day.toString().padStart(2, '0');
    const div = document.createElement("div");
    div.className = "attendance-day";
    div.innerText = day;
    
    const status = attendanceData[studentName] ? attendanceData[studentName][dateStr] : null;
    if(status === "P") {
      div.classList.add("present");
      div.innerHTML += " ✅";
    } else if(status === "A") {
      div.classList.add("absent");
      div.innerHTML += " ❌";
    }
    
    div.onclick = function(){
      if(role === "teacher" || role === "admin") {
        const currentStatus = attendanceData[studentName] ? attendanceData[studentName][dateStr] : null;
        if(currentStatus === "P") {
          attendanceData[studentName][dateStr] = "A";
        } else if(currentStatus === "A") {
          delete attendanceData[studentName][dateStr];
        } else {
          attendanceData[studentName][dateStr] = "P";
        }
        saveData();
        renderAttendanceCalendar(container, studentName);
      }
    };
    
    calendar.appendChild(div);
  }
  
  container.appendChild(calendar);
  
  // Only show legend for non-teacher roles
  if(role !== "teacher") {
    const legend = document.createElement("div");
    legend.className = "attendance-legend";
    legend.style.display = "block";
    legend.innerHTML = "<h4>📋 Legend</h4>" +
      "<p style='color:green;'>✅ Present</p>" +
      "<p style='color:red;'>❌ Absent</p>" +
      "<p style='font-size:12px;color:#666;margin-top:10px;'>👁️ View only</p>";
    container.appendChild(legend);
  }
}

//------ RENDER GRADES TABLE ------
function renderGradesTable(container, studentName) {
  const existingTable = document.getElementById("gradesTable");
  if(existingTable) existingTable.remove();
  
  const table = document.createElement("table");
  table.id = "gradesTable";
  table.innerHTML = "<tr><th>📚 Subject</th><th>📊 Grade</th><th>📈 Status</th></tr>";
  
  let total = 0;
  let count = 0;
  
  subjects.forEach(function(sub){
    const tr = document.createElement("tr");
    const grade = gradesData[studentName] ? gradesData[studentName][sub] : 0;
    total += grade;
    count++;
    
    let status = "✅ Passing";
    if(grade < 75) status = "⚠️ Needs Improvement";
    
    const editable = (role === "teacher" || role === "admin") ? "contenteditable" : "";
    const onblur = (role === "teacher" || role === "admin") ? " onblur=\"updateGrade('" + studentName + "', '" + sub + "', this.innerText)\"" : "";
    
    tr.innerHTML = "<td>" + sub + "</td><td " + editable + onblur + ">" + grade + "</td><td style='color:" + (grade >= 75 ? 'green' : 'red') + "'>" + status + "</td>";
    table.appendChild(tr);
  });
  
  const avgRow = document.createElement("tr");
  avgRow.innerHTML = "<td><strong>📉 Average</strong></td><td><strong>" + (count > 0 ? (total / count).toFixed(2) : 0) + "</strong></td><td></td>";
  table.appendChild(avgRow);
  
  container.appendChild(table);
}

//------ RENDER STUDENTS BY SECTION (WITH CHECKBOXES) ------
function renderStudentsBySection(container, sectionFilter) {
  container.innerHTML = "";
  
  let filteredStudents = students;
  if(sectionFilter !== "all") {
    filteredStudents = students.filter(function(s){ return s.section === sectionFilter; });
  }
  
  filteredStudents.forEach(function(s){
    const idCard = document.createElement("div");
    idCard.className = "id-card";
    idCard.innerHTML = '<input type="checkbox" class="id-card-checkbox" data-student-id="' + s.id + '">' +
      '<div class="id-card-header"><h3 style="margin:0;">🎓 DUMINGAG SENIOR HIGH SCHOOL</h3><p style="margin:0;font-size:11px;">Student ID Card</p></div>' +
      '<div class="id-card-photo"><img src="' + (s.pic || 'https://via.placeholder.com/80') + '" alt="Photo" onerror="this.src=\'https://via.placeholder.com/80\'"></div>' +
      '<div class="id-card-info"><p><strong>Name:</strong> ' + s.name + '</p><p><strong>ID No:</strong> ' + s.id + '</p>' +
      '<p><strong>Section:</strong> ' + s.section + '</p><p><strong>Track:</strong> ' + s.track + '</p>' +
      '<p><strong>Strand:</strong> ' + s.strand + '</p><p><strong>Grade:</strong> ' + s.gradeLevel + '</p></div>' +
      '<div class="id-card-footer">🎓 Dumingag Senior High School - Dumingag, Zamboanga del Sur</div>' +
      '<div id="qr-' + s.id + '" style="text-align:center;margin-top:12px;"></div>';
    
    container.appendChild(idCard);
    
    setTimeout(function(){
      new QRCode(document.getElementById("qr-" + s.id), {
        text: s.name + "-" + s.id,
        width: 65,
        height: 65
      });
    }, 100);
  });
}

//------ RENDER PARENT ACCOUNTS ------
function renderParentAccounts(container, sectionFilter) {
  container.innerHTML = "";
  
  let parentAccounts = JSON.parse(localStorage.getItem('parentAccounts')) || [];
  
  let filteredAccounts = parentAccounts;
  if(sectionFilter !== "all") {
    filteredAccounts = parentAccounts.filter(function(p){ return p.section === sectionFilter; });
  }
  
  if(filteredAccounts.length === 0) {
    container.innerHTML = "<p>❌ No parent accounts found.</p>";
    return;
  }
  
  filteredAccounts.forEach(function(p){
    const card = document.createElement("div");
    card.className = "parent-account-card";
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

//------ TOGGLE SELECT ALL STUDENTS ------
function toggleSelectAllStudents() {
  const selectAll = document.getElementById("selectAllStudents");
  const checkboxes = document.querySelectorAll(".id-card-checkbox");
  checkboxes.forEach(function(cb){
    cb.checked = selectAll.checked;
  });
}

//------ PRINT SELECTED IDS ------
function printSelectedIDs() {
  const checkboxes = document.querySelectorAll(".id-card-checkbox:checked");
  if(checkboxes.length === 0) {
    alert("⚠️ Please select at least one student to print!");
    return;
  }
  window.print();
}

//------ APPROVE STUDENT ------
function approveStudent(id) {
  const student = students.find(function(s){ return s.id === id; });
  if(student) {
    student.approved = true;
    saveData();
    alert("✅ " + student.name + " has been approved!");
    loadSection("Student Approval");
  }
}

//------ DELETE STUDENT ------
function deleteStudent(id) {
  const student = students.find(function(s){ return s.id === id; });
  if(student) {
    if(confirm("⚠️ Are you sure you want to delete " + student.name + "?")) {
      students = students.filter(function(s){ return s.id !== id; });
      delete gradesData[student.name];
      delete attendanceData[student.name];
      saveData();
      alert("🗑️ " + student.name + " has been deleted.");
      loadSection("Student Approval");
    }
  }
}

//------ DELETE TEACHER ------
function deleteTeacher(id) {
  const teacher = teachers.find(function(t){ return t.id === id; });
  if(teacher) {
    if(confirm("⚠️ Are you sure you want to delete " + teacher.name + "?")) {
      teachers = teachers.filter(function(t){ return t.id !== id; });
      saveData();
      alert("🗑️ " + teacher.name + " has been deleted.");
      loadSection("Manage Users");
    }
  }
}

//------ CREATE TEACHER ------
function createTeacher() {
  const name = document.getElementById("newTeacherName").value.trim();
  const id = document.getElementById("newTeacherID").value.trim();
  const position = document.getElementById("newTeacherPosition").value.trim();
  const section = document.getElementById("newTeacherSection").value.trim();
  const username = document.getElementById("newTeacherUsername").value.trim();
  const password = document.getElementById("newTeacherPassword").value.trim();
  
  if(!name || !username || !password || !section) {
    alert("⚠️ Please fill in all required fields!");
    return;
  }
  
  if(teachers.find(function(t){ return t.username === username; })) {
    alert("❌ Username already exists!");
    return;
  }
  
  teachers.push({
    name: name,
    id: id,
    position: position,
    sectionHandled: section,
    username: username,
    password: simpleHash(password)
  });
  
  saveData();
  alert("✅ Teacher account created successfully!");
  
  document.getElementById("newTeacherName").value = "";
  document.getElementById("newTeacherID").value = "";
  document.getElementById("newTeacherPosition").value = "";
  document.getElementById("newTeacherSection").value = "";
  document.getElementById("newTeacherUsername").value = "";
  document.getElementById("newTeacherPassword").value = "";
}
  
//------ UPDATE SUBJECT ------
function updateSubject(index, newValue) {
  const oldValue = subjects[index];
  subjects[index] = newValue;
  
  if(scheduleTimes[oldValue]) {
    scheduleTimes[newValue] = scheduleTimes[oldValue];
    delete scheduleTimes[oldValue];
  }
  
  students.forEach(function(s){
    if(gradesData[s.name] && gradesData[s.name][oldValue] !== undefined) {
      gradesData[s.name][newValue] = gradesData[s.name][oldValue];
      delete gradesData[s.name][oldValue];
    }
  });
  
  saveData();
}

//------ UPDATE SCHEDULE TIME ------
function updateScheduleTime(subject, time) {
  scheduleTimes[subject] = time;
  saveData();
}

//------ DELETE SUBJECT ------
function deleteSubject(index) {
  const subject = subjects[index];
  subjects.splice(index, 1);
  delete scheduleTimes[subject];
  
  students.forEach(function(s){
    if(gradesData[s.name]) {
      delete gradesData[s.name][subject];
    }
  });
  
  saveData();
  loadSection("Subject Schedule");
}

//------ ADD SUBJECT ------
function addSubject() {
  const name = document.getElementById("newSubjectName").value.trim();
  const time = document.getElementById("newSubjectTime").value.trim();
  
  if(!name) {
    alert("⚠️ Please enter a subject name!");
    return;
  }
  
  if(subjects.includes(name)) {
    alert("❌ Subject already exists!");
    return;
  }
  
  subjects.push(name);
  scheduleTimes[name] = time || "TBA";
  
  students.forEach(function(s){
    if(!gradesData[s.name]) gradesData[s.name] = {};
    gradesData[s.name][name] = 0;
  });
  
  saveData();
  loadSection("Subject Schedule");
}

//------ UPDATE GRADE ------
function updateGrade(student, subject, newGrade) {
  const grade = parseInt(newGrade);
  if(isNaN(grade) || grade < 0 || grade > 100) {
    alert("⚠️ Grade must be between 0 and 100.");
    loadSection("Grades");
    return;
  }
  
  if(!gradesData[student]) gradesData[student] = {};
  gradesData[student][subject] = grade;
  saveData();
}

//------ UPLOAD PROFILE PHOTO ------
function uploadProfilePhoto() {
  const fileInput = document.getElementById("uploadPic");
  if(!fileInput.files || !fileInput.files[0]) {
    alert("⚠️ Please select a photo first!");
    return;
  }
  
  const reader = new FileReader();
  reader.onload = function(e){
    const photoData = e.target.result;
    
    if(role === "student") {
      const user = students.find(function(s){ return s.name === currentUser; });
      if(user) {
        user.pic = photoData;
        saveData();
        document.getElementById("profilePic").src = photoData;
        alert("✅ Photo uploaded successfully!");
      }
    } else if(role === "teacher") {
      const user = teachers.find(function(t){ return t.name === currentUser; });
      if(user) {
        user.pic = photoData;
        saveData();
        document.getElementById("profilePic").src = photoData;
        alert("✅ Photo uploaded successfully!");
      }
    } else if(role === "parent") {
      const user = parents.find(function(p){ return p.child === currentUser; });
      if(user) {
        user.pic = photoData;
        saveData();
        document.getElementById("profilePic").src = photoData;
        alert("✅ Photo uploaded successfully!");
      }
    } else if(role === "admin") {
      adminAccount.pic = photoData;
      saveData();
      document.getElementById("profilePic").src = photoData;
      alert("✅ Photo uploaded successfully!");
    }
  };
  reader.readAsDataURL(fileInput.files[0]);
}

//------ SEND CHAT MESSAGE ------
function sendChatMessage(tab) {
  const input = document.getElementById("chatInput");
  const chatbox = document.getElementById("chatbox");
  const message = input.value.trim();
  
  if(!message) {
    alert("⚠️ Please type a message!");
    return;
  }
  
  const timestamp = new Date().toLocaleString();
  chatbox.innerHTML += "<p><strong>" + currentUser + ":</strong> " + message + " <small style='color:#888;'>(" + timestamp + ")</small></p>";
  chatbox.scrollTop = chatbox.scrollHeight;
  input.value = "";
}

//------ PLANNER FUNCTIONS ------
function addPlannerGoal(type) {
  const input = document.getElementById(type + "GoalInput");
  const timeInput = document.getElementById(type + "GoalTime") || document.getElementById(type + "GoalDate");
  
  if(!input.value.trim()) {
    alert("⚠️ Please enter a goal!");
    return;
  }
  
  if(!plannerData[currentUser]) {
    plannerData[currentUser] = { daily: [], weekly: [], monthly: [] };
  }
  
  plannerData[currentUser][type].push({
    text: input.value.trim(),
    time: timeInput ? timeInput.value : "",
    completed: false
  });
  
  saveData();
  loadSection("My Planner");
}

function togglePlannerGoal(type, index) {
  plannerData[currentUser][type][index].completed = !plannerData[currentUser][type][index].completed;
  saveData();
  loadSection("My Planner");
}

function deletePlannerGoal(type, index) {
  plannerData[currentUser][type].splice(index, 1);
  saveData();
  loadSection("My Planner");
}

function setAlarm(time) {
  if(!time) {
    alert("⏰ No time set for this goal!");
    return;
  }
  alert("🔔 Alarm set for " + time + "\n\nNote: Browser notifications must be enabled for actual alerts.");
}

//------ MY MOOD AI CHAT FUNCTIONS ------
let selectedMood = "";

function selectMood(mood) {
  selectedMood = mood;
  
  const buttons = document.querySelectorAll(".mood-btn");
  buttons.forEach(function(btn) {
    if(btn.innerText === mood) {
      btn.classList.add("selected");
    } else {
      btn.classList.remove("selected");
    }
  });
  
  const chatbox = document.getElementById("moodChatbox");
  chatbox.innerHTML += '<div class="chat-message chat-user"><strong>👤 You:</strong> ' + mood + '</div>';
  chatbox.scrollTop = chatbox.scrollHeight;
  
  getAIResponse("I feel " + mood);
}

function sendMoodMessage() {
  const input = document.getElementById("moodInput");
  const message = input.value.trim();
  
  if(!message && !selectedMood) {
    alert("⚠️ Please select a mood or type a message!");
    return;
  }
  
  const chatbox = document.getElementById("moodChatbox");
  
  if(message) {
    chatbox.innerHTML += '<div class="chat-message chat-user"><strong>👤 You:</strong> ' + message + '</div>';
    chatbox.scrollTop = chatbox.scrollHeight;
    input.value = "";
    
    getAIResponse(message);
  }
}

function getAIResponse(message) {
  const chatbox = document.getElementById("moodChatbox");
  
  chatbox.innerHTML += '<div class="chat-message chat-ai" id="typingIndicator"><em>💭 Thinking...</em></div>';
  chatbox.scrollTop = chatbox.scrollHeight;
  
  setTimeout(function() {
    const typingIndicator = document.getElementById("typingIndicator");
    if(typingIndicator) typingIndicator.remove();
    
    const response = getSupportiveResponse(message);
    chatbox.innerHTML += '<div class="chat-message chat-ai"><strong>🤗 AI Companion:</strong> ' + response + '</div>';
    chatbox.scrollTop = chatbox.scrollHeight;
  }, 1000);
}

function getSupportiveResponse(message) {
  const lowerMessage = message.toLowerCase();
  
  if(lowerMessage.includes("😊") || lowerMessage.includes("happy") || lowerMessage.includes("good") || lowerMessage.includes("great") || lowerMessage.includes("excited") || lowerMessage.includes("love")) {
    return "That's wonderful! 🎉 I'm so glad you're feeling good! Keep that positive energy going! Remember to share your happiness with others too!";
  }
  
  if(lowerMessage.includes("😢") || lowerMessage.includes("sad") || lowerMessage.includes("depressed") || lowerMessage.includes("unhappy") || lowerMessage.includes("down") || lowerMessage.includes("crying") || lowerMessage.includes("hurt")) {
    return "I'm here for you. 💙 It's okay to feel sad sometimes. Would you like to talk about what's making you feel this way? Remember, you're not alone. Consider talking to a trusted teacher or counselor.";
  }
  
  if(lowerMessage.includes("😠") || lowerMessage.includes("angry") || lowerMessage.includes("mad") || lowerMessage.includes("frustrated") || lowerMessage.includes("annoyed") || lowerMessage.includes("hate")) {
    return "I understand you're feeling angry. 😤 Take a deep breath... Inhale for 4 seconds, hold for 7, exhale for 8. Would you like to talk about what's frustrating you?";
  }
  
  if(lowerMessage.includes("😰") || lowerMessage.includes("anxious") || lowerMessage.includes("nervous") || lowerMessage.includes("worried") || lowerMessage.includes("stressed") || lowerMessage.includes("scared") || lowerMessage.includes("fear")) {
    return "It's okay to feel anxious sometimes. 🌸 Try these tips:\n\n1. Take deep breaths\n2. Write down your worries\n3. Talk to someone you trust\n\nRemember, one step at a time. You can get through this!";
  }
  
  if(lowerMessage.includes("😴") || lowerMessage.includes("tired") || lowerMessage.includes("sleepy") || lowerMessage.includes("exhausted") || lowerMessage.includes("fatigued") || lowerMessage.includes("sleep")) {
    return "You sound tired! 😴 Make sure you're getting enough sleep - teens need 8-10 hours. Take breaks when studying, stay hydrated, and don't forget to rest. Your health comes first!";
  }
  
  if(lowerMessage.includes("🤗") || lowerMessage.includes("love") || lowerMessage.includes("grateful") || lowerMessage.includes("thankful") || lowerMessage.includes("blessed")) {
    return "That's a beautiful feeling! 💕 Gratitude is so important for mental health. Consider writing down 3 things you're grateful for each day. You're amazing!";
  }
  
  const responses = [
    "Thank you for sharing that with me. 💙 I'm here to listen. Do you want to talk more about it?",
    "I hear you. 🌸 Remember, it's okay to not be okay. Would you like some suggestions on how to cope?",
    "Thanks for opening up to me. 💜 You're very brave. Is there anything specific you'd like to talk about?",
    "I appreciate you sharing your feelings. 💙 Would you like me to share some helpful tips?",
    "Your feelings are valid. 🌟 You're doing great by talking about them. Keep going!"
  ];
  
  return responses[Math.floor(Math.random() * responses.length)];
}

//------ SEMESTER AND QUARTER SELECTORS ------
function selectSemester(sem, btn) {
  const buttons = document.querySelectorAll(".sem-btn");
  buttons.forEach(function(b) {
    b.classList.remove("active");
  });
  btn.classList.add("active");
  
  const quarterSelector = document.getElementById("quarterSelector");
  if(quarterSelector) {
    if(sem === 1) {
      quarterSelector.innerHTML = `
        <button class="quarter-btn active" onclick="selectQuarter(1, this)">1st Quarter</button>
        <button class="quarter-btn" onclick="selectQuarter(2, this)">2nd Quarter</button>
      `;
    } else {
      quarterSelector.innerHTML = `
        <button class="quarter-btn active" onclick="selectQuarter(3, this)">3rd Quarter</button>
        <button class="quarter-btn" onclick="selectQuarter(4, this)">4th Quarter</button>
      `;
    }
  }
}

function selectQuarter(quarter, btn) {
  const buttons = document.querySelectorAll(".quarter-btn");
  buttons.forEach(function(b) {
    b.classList.remove("active");
  });
  btn.classList.add("active");
  
  console.log("Selected Quarter: " + quarter);
}

//------ INITIALIZE ON PAGE LOAD ------
window.onload = function() {
  saveData();
};
</script>
</body>
</html>
