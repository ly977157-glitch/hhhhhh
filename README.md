<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>باي تكسي</title>
<script src="https://www.gstatic.com/firebasejs/10.8.0/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.8.0/firebase-auth-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.8.0/firebase-database-compat.js"></script>
<script>
var firebaseConfig = {
    apiKey: "AIzaSyBDoHq1vPgK99Tnep9gtzdBbQM05_h2ADU",
    authDomain: "bay-9be2a.firebaseapp.com",
    databaseURL: "https://bay-9be2a-default-rtdb.firebaseio.com",
    projectId: "bay-9be2a",
    storageBucket: "bay-9be2a.firebasestorage.app",
    messagingSenderId: "941883528154",
    appId: "1:941883528154:web:e628a67330b7779086a6e3"
};
firebase.initializeApp(firebaseConfig);
var auth = firebase.auth();
var db = firebase.database();
</script>
<style>
* { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Segoe UI', Tahoma, sans-serif; }
body { background: linear-gradient(135deg, #667eea, #764ba2); min-height: 100vh; }
.login-page { display: flex; justify-content: center; align-items: center; min-height: 100vh; padding: 20px; }
.login-box { width: 100%; max-width: 400px; background: white; border-radius: 20px; padding: 40px 30px; box-shadow: 0 20px 60px rgba(0,0,0,0.3); }
.login-box h1 { color: #667eea; text-align: center; margin-bottom: 30px; font-size: 32px; }
.login-box input { width: 100%; padding: 15px 20px; margin-bottom: 15px; border: 2px solid #e0e0e0; border-radius: 12px; font-size: 16px; outline: none; }
.login-box input:focus { border-color: #667eea; }
.login-box button { width: 100%; padding: 15px; border: none; border-radius: 12px; font-size: 16px; font-weight: bold; cursor: pointer; margin-bottom: 10px; }
.login-box .btn-primary { background: linear-gradient(135deg, #667eea, #764ba2); color: white; }
.login-box .btn-secondary { background: #f0f0f0; color: #333; }
.login-box .link { text-align: center; margin-top: 15px; color: #666; }
.login-box .link a { color: #667eea; cursor: pointer; text-decoration: underline; font-weight: bold; }
.login-box .error { color: #e74c3c; font-size: 14px; margin-bottom: 10px; text-align: center; display: none; }
.login-box .success { color: #4caf50; font-size: 14px; margin-bottom: 10px; text-align: center; display: none; }
.home-page { display: none; min-height: 100vh; background: #f5f5f5; }
.home-page.active { display: block; }
.home-header { background: linear-gradient(135deg, #667eea, #764ba2); color: white; padding: 30px 20px; text-align: center; }
.home-header .avatar { width: 80px; height: 80px; background: rgba(255,255,255,0.2); border-radius: 50%; margin: 0 auto 15px; display: flex; align-items: center; justify-content: center; font-size: 40px; }
.home-header h2 { font-size: 24px; margin-bottom: 5px; }
.home-header p { opacity: 0.9; font-size: 14px; }
.menu-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; padding: 20px; }
.menu-item { background: white; border-radius: 16px; padding: 25px 15px; text-align: center; box-shadow: 0 2px 10px rgba(0,0,0,0.08); cursor: pointer; }
.menu-item .icon { font-size: 32px; margin-bottom: 10px; }
.menu-item h3 { color: #333; font-size: 16px; margin-bottom: 5px; }
.menu-item p { color: #999; font-size: 12px; }
.bottom-nav { position: fixed; bottom: 0; left: 0; right: 0; background: white; display: flex; justify-content: space-around; padding: 10px 0; box-shadow: 0 -2px 10px rgba(0,0,0,0.1); }
.bottom-nav button { background: none; border: none; color: #999; font-size: 12px; cursor: pointer; padding: 5px 15px; }
.bottom-nav button.active { color: #667eea; }
.bottom-nav button .nav-icon { font-size: 24px; display: block; margin-bottom: 3px; }
.content-page { display: none; padding: 20px; padding-bottom: 80px; }
.content-page.active { display: block; }
.page-title { font-size: 22px; color: #333; margin-bottom: 20px; text-align: center; }
.profile-card { background: white; border-radius: 16px; padding: 20px; margin-bottom: 15px; box-shadow: 0 2px 10px rgba(0,0,0,0.08); }
.profile-card h3 { color: #667eea; font-size: 16px; margin-bottom: 15px; }
.profile-row { display: flex; justify-content: space-between; padding: 12px 0; border-bottom: 1px solid #f0f0f0; }
.profile-row:last-child { border-bottom: none; }
.profile-row .label { color: #666; font-size: 14px; }
.profile-row .value { color: #333; font-size: 14px; font-weight: bold; }
.setting-item { background: white; border-radius: 12px; padding: 15px 20px; margin-bottom: 10px; display: flex; justify-content: space-between; align-items: center; box-shadow: 0 2px 8px rgba(0,0,0,0.05); cursor: pointer; }
.setting-item .setting-left { display: flex; align-items: center; gap: 12px; }
.setting-item .setting-icon { font-size: 20px; }
.setting-item .setting-text { color: #333; font-size: 15px; }
.setting-item .setting-arrow { color: #999; font-size: 18px; }
.logout-btn { background: #ffebee; color: #e74c3c; border: none; width: 100%; padding: 15px; border-radius: 12px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 20px; }
.toast { position: fixed; top: 20px; left: 50%; transform: translateX(-50%) translateY(-100px); background: #333; color: white; padding: 15px 25px; border-radius: 12px; transition: transform 0.3s; z-index: 1000; font-size: 14px; }
.toast.show { transform: translateX(-50%) translateY(0); }
.loading { position: fixed; top: 0; left: 0; right: 0; bottom: 0; background: rgba(255,255,255,0.9); display: none; justify-content: center; align-items: center; z-index: 999; }
.loading.active { display: flex; }
.loading-spinner { width: 50px; height: 50px; border: 4px solid #f0f0f0; border-top-color: #667eea; border-radius: 50%; animation: spin 1s linear infinite; }
@keyframes spin { to { transform: rotate(360deg); } }
</style>
</head>
<body>

<div class="loading" id="loadingOverlay"><div class="loading-spinner"></div></div>

<div class="login-page" id="loginPage">
    <div class="login-box">
        <h1>🚕 باي تكسي</h1>
        <div class="error" id="loginError"></div>
        <input type="email" id="loginEmail" placeholder="البريد الإلكتروني">
        <input type="password" id="loginPassword" placeholder="كلمة المرور">
        <button class="btn-primary" onclick="login()">تسجيل الدخول</button>
        <button class="btn-secondary" onclick="showRegister()">إنشاء حساب جديد</button>
    </div>
</div>

<div class="login-page" id="registerPage" style="display:none;">
    <div class="login-box">
        <h1>🚕 إنشاء حساب</h1>
        <div class="error" id="regError"></div>
        <div class="success" id="regSuccess"></div>
        <input type="text" id="regName" placeholder="الاسم الكامل">
        <input type="email" id="regEmail" placeholder="البريد الإلكتروني">
        <input type="password" id="regPassword" placeholder="كلمة المرور (6 أحرف فأكثر)">
        <button class="btn-primary" onclick="register()">إنشاء الحساب</button>
        <div class="link"><a onclick="showLogin()">لدي حساب بالفعل</a></div>
    </div>
</div>

<div class="home-page" id="homePage">
    <div class="home-header">
        <div class="avatar">👤</div>
        <h2 id="userName">مرحباً 👋</h2>
        <p id="userEmail">مستخدم باي تكسي</p>
    </div>
    <div class="menu-grid" id="mainMenu">
        <div class="menu-item" onclick="showPage('ridesPage')"><div class="icon">🚕</div><h3>حجز رحلة</h3><p>اطلب تكسي الآن</p></div>
        <div class="menu-item" onclick="showPage('historyPage')"><div class="icon">📋</div><h3>سجل الرحلات</h3><p>رحلاتك السابقة</p></div>
        <div class="menu-item" onclick="showPage('profilePage')"><div class="icon">👤</div><h3>الملف الشخصي</h3><p>معلوماتك</p></div>
        <div class="menu-item" onclick="showPage('settingsPage')"><div class="icon">⚙️</div><h3>الإعدادات</h3><p>تخصيص التطبيق</p></div>
    </div>
    <div class="content-page" id="ridesPage"><h2 class="page-title">🚕 حجز رحلة</h2><div class="profile-card"><h3>اختر نوع الرحلة</h3><div class="menu-item" style="margin-bottom:10px; text-align:right;"><div class="icon">🚗</div><h3>اقتصادية - 25 ر.س</h3><p>سيارة عادية 4 مقاعد</p></div><div class="menu-item" style="margin-bottom:10px; text-align:right;"><div class="icon">🚙</div><h3>عائلية - 45 ر.س</h3><p>سيارة كبيرة 7 مقاعد</p></div><div class="menu-item" style="text-align:right;"><div class="icon">🚕</div><h3>فاخرة - 80 ر.س</h3><p>سيارة فاخرة 4 مقاعد</p></div></div><button class="logout-btn" onclick="backToHome()">⬅️ رجوع</button></div>
    <div class="content-page" id="historyPage"><h2 class="page-title">📋 سجل الرحلات</h2><div class="profile-card"><div class="profile-row"><span class="label">📍 من</span><span class="value">شارع الملك فهد</span></div><div class="profile-row"><span class="label">📍 إلى</span><span class="value">الرياض بارك</span></div><div class="profile-row"><span class="label">💰 السعر</span><span class="value">25 ر.س</span></div><div class="profile-row"><span class="label">📅 التاريخ</span><span class="value">20 مايو 2026</span></div></div><button class="logout-btn" onclick="backToHome()">⬅️ رجوع</button></div>
    <div class="content-page" id="profilePage"><h2 class="page-title">👤 الملف الشخصي</h2><div class="profile-card"><h3>المعلومات الشخصية</h3><div class="profile-row"><span class="label">الاسم</span><span class="value" id="profileName">-</span></div><div class="profile-row"><span class="label">البريد الإلكتروني</span><span class="value" id="profileEmail">-</span></div><div class="profile-row"><span class="label">رقم الهاتف</span><span class="value">05xxxxxxxx</span></div><div class="profile-row"><span class="label">عدد الرحلات</span><span class="value" id="profileRides">0</span></div></div><button class="logout-btn" onclick="backToHome()">⬅️ رجوع</button></div>
    <div class="content-page" id="settingsPage"><h2 class="page-title">⚙️ الإعدادات</h2><div class="setting-item"><div class="setting-left"><span class="setting-icon">🔔</span><span class="setting-text">الإشعارات</span></div><span class="setting-arrow">←</span></div><div class="setting-item"><div class="setting-left"><span class="setting-icon">🌙</span><span class="setting-text">الوضع الليلي</span></div><span class="setting-arrow">←</span></div><div class="setting-item"><div class="setting-left"><span class="setting-icon">🌍</span><span class="setting-text">اللغة</span></div><span class="
