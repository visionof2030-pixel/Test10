<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>أداة التقارير التعليمية | وزارة التعليم</title>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<!-- مكتبة html2canvas و html2pdf -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
<!-- مكتبة html2pdf.js -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
<style>
:root {
  --primary: #083024;
  --primary-light: #0a4030;
  --secondary: #059669;
  --secondary-dark: #047857;
  --whatsapp: #25D366;
  --telegram: #0088cc;
  --light: #f8fafc;
  --dark: #1f2937;
  --gray: #6b7280;
  --light-gray: #e5e7eb;
  --danger: #dc2626;
  --success: #059669;
  --warning: #d97706;
  --border-radius: 8px;
  --box-shadow: 0 2px 4px -1px rgba(0, 0, 0, 0.1);
  --box-shadow-hover: 0 5px 10px -3px rgba(0, 0, 0, 0.1);
  --transition: all 0.2s ease;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  -webkit-tap-highlight-color: transparent;
}

body {
  font-family: 'Cairo', sans-serif;
  background: linear-gradient(135deg, #f0f9ff 0%, #e0f2fe 100%);
  color: var(--dark);
  line-height: 1.6;
  min-height: 100vh;
  padding: 0;
  overflow-x: hidden;
}

/* تحسينات للأجهزة المحمولة */
@media (max-width: 768px) {
  body {
    font-size: 14px;
    -webkit-text-size-adjust: 100%;
  }
}

.container {
  max-width: 100%;
  margin: 0 auto;
  padding: 10px;
}

/* الهيدر مع خلفية شعار وزارة التعليم */
.header {
  background: white url('https://i.ibb.co/kVWFFwhW/9-C92-E57-B-23-FA-479-D-A024-1-D5-F871-B4-F8-D.png') center/contain no-repeat;
  border-radius: var(--border-radius);
  box-shadow: var(--box-shadow);
  padding: 10px 15px;
  margin-bottom: 10px;
  display: flex;
  flex-direction: column;
  gap: 10px;
  border-right: 3px solid var(--primary);
  position: relative;
  min-height: 100px;
}

.header::before {
  content: '';
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background: rgba(255, 255, 255, 0.9);
  border-radius: var(--border-radius);
  z-index: 1;
}

.header > * {
  position: relative;
  z-index: 2;
}

.header-top {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 8px;
}

.header-bottom {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

@media (max-width: 480px) {
  .header-top {
    flex-direction: column;
    text-align: center;
  }
  
  .header-bottom {
    flex-direction: column;
  }
}

.logo-section {
  display: flex;
  align-items: center;
  gap: 10px;
}

.logo-icon {
  width: 40px;
  height: 40px;
  background: linear-gradient(135deg, var(--primary), var(--primary-light));
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-size: 20px;
  flex-shrink: 0;
}

.logo-text h1 {
  font-size: 16px;
  font-weight: 700;
  color: var(--dark);
  margin-bottom: 2px;
  line-height: 1.2;
}

.logo-text p {
  font-size: 12px;
  color: var(--gray);
  line-height: 1.3;
}

/* زر القائمة للجوال */
.mobile-menu-btn {
  display: none;
  background: none;
  border: none;
  color: var(--primary);
  font-size: 20px;
  cursor: pointer;
  padding: 5px;
}

@media (max-width: 768px) {
  .mobile-menu-btn {
    display: block;
  }
}

/* شريط التنقل السفلي للجوال */
.mobile-nav {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  background: white;
  box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.1);
  z-index: 1000;
  padding: 8px 5px;
  display: none;
  justify-content: space-around;
  backdrop-filter: blur(10px);
}

@media (max-width: 768px) {
  .mobile-nav {
    display: flex;
  }
  
  .container {
    padding-bottom: 70px;
  }
}

.nav-btn {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 3px;
  background: none;
  border: none;
  color: var(--gray);
  font-size: 10px;
  padding: 5px 3px;
  cursor: pointer;
  flex: 1;
  min-width: 0;
  transition: var(--transition);
}

.nav-btn.active {
  color: var(--primary);
}

.nav-btn i {
  font-size: 14px;
}

.nav-btn:hover {
  transform: translateY(-2px);
}

/* المحتوى الرئيسي */
.main-content {
  display: grid;
  grid-template-columns: 1fr;
  gap: 10px;
}

@media (min-width: 1024px) {
  .main-content {
    grid-template-columns: 1fr 300px;
  }
}

/* لوحة التحكم - تصميم متجاوب */
.control-panel {
  background: white;
  border-radius: var(--border-radius);
  box-shadow: var(--box-shadow);
  padding: 15px;
  height: fit-content;
  position: sticky;
  top: 10px;
}

@media (max-width: 1024px) {
  .control-panel {
    position: static;
    order: 2;
  }
}

/* القوالب السريعة */
.quick-templates {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
  gap: 8px;
  margin-bottom: 15px;
}

@media (max-width: 480px) {
  .quick-templates {
    grid-template-columns: 1fr;
  }
}

.template-btn {
  background: white;
  border: 1px solid var(--light-gray);
  border-radius: 6px;
  padding: 8px;
  cursor: pointer;
  transition: var(--transition);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 6px;
  text-align: center;
  min-height: 70px;
  justify-content: center;
}

.template-btn:hover {
  border-color: var(--primary);
  transform: translateY(-1px);
  box-shadow: var(--box-shadow-hover);
}

.template-btn i {
  font-size: 16px;
  color: var(--primary);
}

.template-btn span {
  font-size: 11px;
  font-weight: 500;
}

/* أزرار العمل */
.action-buttons {
  display: flex;
  flex-direction: column;
  gap: 8px;
  margin-top: 15px;
}

.action-btn {
  padding: 10px;
  border: none;
  border-radius: 6px;
  font-family: 'Cairo', sans-serif;
  font-size: 13px;
  font-weight: 600;
  cursor: pointer;
  transition: var(--transition);
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 6px;
}

.action-btn-primary {
  background: linear-gradient(135deg, var(--primary), var(--primary-light));
  color: white;
}

.action-btn-primary:hover {
  transform: translateY(-1px);
  box-shadow: var(--box-shadow-hover);
}

.action-btn-secondary {
  background: white;
  color: var(--primary);
  border: 1px solid var(--primary);
}

.action-btn-secondary:hover {
  background: var(--primary);
  color: white;
}

.action-btn-success {
  background: linear-gradient(135deg, var(--success), var(--secondary-dark));
  color: white;
}

.action-btn-success:hover {
  transform: translateY(-1px);
  box-shadow: var(--box-shadow-hover);
}

.action-btn-whatsapp {
  background: linear-gradient(135deg, var(--whatsapp), #128C7E);
  color: white;
}

.action-btn-whatsapp:hover {
  transform: translateY(-1px);
  box-shadow: var(--box-shadow-hover);
}

/* نموذج الإدخال */
.form-container {
  background: white;
  border-radius: var(--border-radius);
  box-shadow: var(--box-shadow);
  overflow: hidden;
}

.form-header {
  background: linear-gradient(135deg, var(--primary), var(--primary-light));
  color: white;
  padding: 12px 15px;
}

.form-header h2 {
  font-size: 16px;
  font-weight: 600;
  display: flex;
  align-items: center;
  gap: 8px;
}

.form-content {
  padding: 15px;
}

/* تحسينات للحقول في الجوال */
.form-section {
  margin-bottom: 15px;
}

.form-section-title {
  font-size: 14px;
  font-weight: 600;
  color: var(--dark);
  margin-bottom: 10px;
  padding-bottom: 5px;
  border-bottom: 1px solid var(--light-gray);
  display: flex;
  align-items: center;
  gap: 6px;
}

.form-section-title i {
  color: var(--primary);
  font-size: 14px;
}

.form-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 10px;
}

@media (max-width: 768px) {
  .form-grid {
    grid-template-columns: 1fr;
  }
}

.form-group {
  margin-bottom: 10px;
}

.form-label {
  display: block;
  font-size: 12px;
  font-weight: 600;
  color: var(--dark);
  margin-bottom: 5px;
  display: flex;
  align-items: center;
  gap: 6px;
}

.form-label i {
  color: var(--primary);
  font-size: 12px;
}

.form-control {
  width: 100%;
  padding: 8px 10px;
  border: 1px solid var(--light-gray);
  border-radius: 6px;
  font-family: 'Cairo', sans-serif;
  font-size: 13px;
  color: var(--dark);
  transition: var(--transition);
  background: white;
  -webkit-appearance: none;
}

/* تحسينات للحقول الصغيرة على الجوال */
@media (max-width: 480px) {
  .form-control {
    padding: 10px 12px;
    font-size: 16px;
  }
  
  select.form-control {
    font-size: 16px;
  }
}

.form-control:focus {
  outline: none;
  border-color: var(--primary);
  box-shadow: 0 0 0 2px rgba(8, 48, 36, 0.1);
}

/* منطقة المحتوى - تصميم متجاوب */
.content-section {
  margin-bottom: 15px;
}

.content-box {
  background: rgba(255, 255, 255, 0.9);
  border: 1px solid var(--light-gray);
  border-radius: 6px;
  padding: 10px;
  margin-bottom: 10px;
}

.content-box-title {
  font-size: 13px;
  font-weight: 600;
  color: var(--primary);
  margin-bottom: 8px;
  display: flex;
  align-items: center;
  gap: 6px;
  padding-bottom: 5px;
  border-bottom: 1px solid rgba(8, 48, 36, 0.1);
}

.content-box-title i {
  font-size: 14px;
}

.content-box textarea {
  width: 100%;
  min-height: 100px;
  border: 1px solid #e5e7eb;
  border-radius: 4px;
  padding: 8px;
  font-family: 'Cairo', sans-serif;
  font-size: 13px;
  line-height: 1.5;
  resize: vertical;
  background: #f9fafb;
}

.content-box textarea:focus {
  outline: none;
  border-color: var(--primary);
  background: white;
}

.char-count {
  font-size: 11px;
  color: var(--gray);
  text-align: left;
  margin-top: 5px;
}

/* تحسينات للمربعات على الجوال */
@media (max-width: 768px) {
  .content-box textarea {
    min-height: 80px;
    font-size: 14px;
  }
}

/* منطقة رفع الصور */
.upload-section {
  margin-top: 15px;
}

.upload-area {
  border: 1px dashed var(--light-gray);
  border-radius: 6px;
  padding: 12px;
  text-align: center;
  cursor: pointer;
  transition: var(--transition);
  margin-bottom: 10px;
  background: #f9fafb;
}

.upload-area:hover {
  border-color: var(--primary);
  background: #f3f4f6;
}

.upload-area i {
  font-size: 30px;
  color: var(--primary);
  margin-bottom: 6px;
}

.upload-area p {
  color: var(--gray);
  margin-bottom: 3px;
  font-size: 13px;
}

.upload-area small {
  font-size: 11px;
  color: var(--gray);
}

.image-preview {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
  gap: 8px;
  margin-top: 10px;
}

@media (max-width: 480px) {
  .image-preview {
    grid-template-columns: repeat(2, 1fr);
  }
}

.preview-image {
  position: relative;
  border-radius: 6px;
  overflow: hidden;
  height: 80px;
  box-shadow: 0 1px 3px rgba(0,0,0,0.1);
}

.preview-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.remove-image {
  position: absolute;
  top: 3px;
  left: 3px;
  background: rgba(220, 38, 38, 0.9);
  color: white;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: var(--transition);
  font-size: 10px;
}

.remove-image:hover {
  background: var(--danger);
}

/* التوقيعات */
.signatures-section {
  background: #f9fafb;
  border-radius: 6px;
  padding: 12px;
  margin-top: 15px;
}

.signatures-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 12px;
}

@media (max-width: 480px) {
  .signatures-grid {
    grid-template-columns: 1fr;
  }
}

.signature-field {
  text-align: center;
}

.signature-input {
  width: 100%;
  padding: 8px;
  border: 1px solid var(--light-gray);
  border-radius: 6px;
  font-family: 'Cairo', sans-serif;
  font-size: 13px;
  text-align: center;
  background: white;
  margin-top: 5px;
}

/* نافذة المعاينة */
.preview-overlay {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background: rgba(0, 0, 0, 0.9);
  display: none;
  align-items: center;
  justify-content: center;
  z-index: 2000;
  padding: 10px;
  backdrop-filter: blur(5px);
}

.preview-container {
  background: white;
  border-radius: var(--border-radius);
  width: 100%;
  max-width: 700px;
  max-height: 85vh;
  overflow-y: auto;
  position: relative;
  animation: slideIn 0.3s ease;
}

@keyframes slideIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.preview-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px 15px;
  background: linear-gradient(135deg, var(--primary), var(--primary-light));
  color: white;
  position: sticky;
  top: 0;
  z-index: 1;
}

.close-preview {
  background: none;
  border: none;
  color: white;
  font-size: 18px;
  cursor: pointer;
  padding: 4px;
  width: 30px;
  height: 30px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.close-preview:hover {
  background: rgba(255, 255, 255, 0.2);
}

/* تصميم التقرير للطباعة */
.report-content {
  padding: 15px;
  font-family: 'Cairo', sans-serif;
  max-width: 700px;
  margin: 0 auto;
  page-break-inside: avoid;
  font-size: 12px;
}

/* رسائل التنبيه */
.alert {
  padding: 8px 10px;
  border-radius: 6px;
  margin-bottom: 10px;
  display: flex;
  align-items: center;
  gap: 6px;
  font-size: 12px;
  animation: fadeIn 0.3s ease;
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(-8px); }
  to { opacity: 1; transform: translateY(0); }
}

.alert-success {
  background: #d1fae5;
  color: #065f46;
  border-right: 3px solid var(--success);
}

.alert-warning {
  background: #fef3c7;
  color: #92400e;
  border-right: 3px solid var(--warning);
}

.alert-error {
  background: #fee2e2;
  color: #991b1b;
  border-right: 3px solid var(--danger);
}

.alert-info {
  background: #dbeafe;
  color: #1e40af;
  border-right: 3px solid var(--primary);
}

/* شاشة التحميل */
.loading-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.9);
  display: none;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  z-index: 3000;
  color: white;
  font-size: 16px;
  text-align: center;
  padding: 15px;
}

.loading-spinner {
  width: 40px;
  height: 40px;
  border: 2px solid rgba(255, 255, 255, 0.3);
  border-top-color: white;
  border-radius: 50%;
  animation: spin 1s linear infinite;
  margin-bottom: 15px;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}

/* تحسينات للتمرير */
::-webkit-scrollbar {
  width: 6px;
}

::-webkit-scrollbar-track {
  background: #f1f1f1;
  border-radius: 3px;
}

::-webkit-scrollbar-thumb {
  background: var(--primary);
  border-radius: 3px;
}

::-webkit-scrollbar-thumb:hover {
  background: var(--primary-light);
}

/* طباعة التقرير */
@media print {
  body * {
    visibility: hidden;
  }
  
  .preview-container,
  .preview-container * {
    visibility: visible;
  }
  
  .preview-container {
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    max-width: 100%;
    box-shadow: none;
    border-radius: 0;
    max-height: none;
    overflow: visible;
  }
  
  .preview-header {
    display: none;
  }
  
  .report-content {
    padding: 10px;
    max-width: 100%;
    font-size: 11px;
  }
  
  .action-buttons,
  .mobile-nav,
  .header {
    display: none !important;
  }
}

/* تحسينات للوضع الأفقي */
@media (max-height: 500px) and (orientation: landscape) {
  .mobile-nav {
    display: none;
  }
  
  .container {
    padding-bottom: 15px;
  }
}

/* إضافة مسافات أصغر بين العناصر */
.form-group + .form-group {
  margin-top: 5px;
}

/* تحسينات للعناصر الصغيرة */
.form-control::placeholder {
  font-size: 11px;
}

textarea.form-control::placeholder {
  font-size: 11px;
}

.signature-input::placeholder {
  font-size: 11px;
}

/* تحسين التباعد العام */
.form-content > * {
  margin-bottom: 8px;
}

/* تحسينات للهواتف الصغيرة */
@media (max-width: 360px) {
  .container {
    padding: 5px;
  }
  
  .header {
    padding: 8px 10px;
    min-height: 80px;
  }
  
  .logo-icon {
    width: 35px;
    height: 35px;
    font-size: 18px;
  }
  
  .logo-text h1 {
    font-size: 14px;
  }
  
  .logo-text p {
    font-size: 11px;
  }
}

/* زر مساعدة */
.help-btn {
  position: fixed;
  bottom: 80px;
  left: 15px;
  background: var(--primary);
  color: white;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 22px;
  cursor: pointer;
  z-index: 1001;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  transition: var(--transition);
}

.help-btn:hover {
  transform: scale(1.1);
  box-shadow: 0 6px 16px rgba(0, 0, 0, 0.2);
}

@media (max-width: 768px) {
  .help-btn {
    bottom: 70px;
    width: 45px;
    height: 45px;
    font-size: 20px;
  }
}
</style>
</head>
<body>
<div class="container">
  <!-- الهيدر -->
  <header class="header">
    <div class="header-top">
      <div class="logo-section">
        <div class="logo-icon">
          <i class="fas fa-graduation-cap"></i>
        </div>
        <div class="logo-text">
          <h1>أداة التقارير التعليمية</h1>
          <p>وزارة التعليم - نظام إعداد التقارير الذكي</p>
        </div>
      </div>
      <button class="mobile-menu-btn" onclick="toggleMenu()">
        <i class="fas fa-bars"></i>
      </button>
    </div>
    
    <div class="header-bottom">
      <div class="alert alert-success">
        <i class="fas fa-check-circle"></i>
        <span>جميع البيانات مؤمنة ومشفرة</span>
      </div>
      <div class="alert alert-info">
        <i class="fas fa-mobile-alt"></i>
        <span>متوافق مع جميع الأجهزة</span>
      </div>
    </div>
  </header>

  <!-- المحتوى الرئيسي -->
  <div class="main-content">
    <!-- نموذج الإدخال -->
    <main class="form-container">
      <div class="form-header">
        <h2><i class="fas fa-edit"></i> إعداد تقرير جديد</h2>
      </div>

      <div class="form-content">
        <!-- معلومات المدرسة -->
        <div class="form-section">
          <h3 class="form-section-title">
            <i class="fas fa-school"></i>
            معلومات المدرسة
          </h3>
          <div class="form-grid">
            <div class="form-group">
              <label class="form-label">
                <i class="fas fa-university"></i>
                اسم المدرسة
              </label>
              <input type="text" class="form-control" id="school-name" 
                     placeholder="أدخل اسم المدرسة الكامل" required>
            </div>
            
            <div class="form-group">
              <label class="form-label">
                <i class="fas fa-map-marker-alt"></i>
                إدارة التعليم
              </label>
              <select class="form-control" id="education-department">
                <option value="">اختر إدارة التعليم</option>
                <option value="الرياض">الإدارة العامة للتعليم بمنطقة الرياض</option>
                <option value="مكة">الإدارة العامة للتعليم بمنطقة مكة المكرمة</option>
                <option value="الشرقية">الإدارة العامة للتعليم بالمنطقة الشرقية</option>
                <option value="المدينة">الإدارة العامة للتعليم بمنطقة المدينة المنورة</option>
              </select>
            </div>
          </div>
        </div>

        <!-- معلومات التقرير -->
        <div class="form-section">
          <h3 class="form-section-title">
            <i class="fas fa-info-circle"></i>
            معلومات التقرير
          </h3>
          <div class="form-grid">
            <div class="form-group">
              <label class="form-label">
                <i class="fas fa-file-alt"></i>
                نوع التقرير
              </label>
              <select class="form-control" id="report-type">
                <option value="نشاط إثرائي">نشاط إثرائي</option>
                <option value="خطة علاجية">خطة علاجية</option>
                <option value="تقرير تقويمي">تقرير تقويمي</option>
                <option value="تقرير متابعة">تقرير متابعة</option>
              </select>
            </div>
            
            <div class="form-group">
              <label class="form-label">
                <i class="fas fa-calendar"></i>
                الفصل الدراسي
              </label>
              <select class="form-control" id="semester">
                <option value="الأول">الفصل الدراسي الأول</option>
                <option value="الثاني">الفصل الدراسي الثاني</option>
                <option value="الصيفي">الفصل الصيفي</option>
              </select>
            </div>
            
            <div class="form-group">
              <label class="form-label">
                <i class="fas fa-users"></i>
                الصف
              </label>
              <input type="text" class="form-control" id="class-level" 
                     placeholder="مثال: الثالث الثانوي">
            </div>
            
            <div class="form-group">
              <label class="form-label">
                <i class="fas fa-book"></i>
                المادة الدراسية
              </label>
              <input type="text" class="form-control" id="subject" 
                     placeholder="مثال: أحياء">
            </div>
          </div>
          
          <div class="form-grid">
            <div class="form-group">
              <label class="form-label">
                <i class="fas fa-user-friends"></i>
                الفئة المستهدفة
              </label>
              <input type="text" class="form-control" id="target-audience" 
                     placeholder="مثال: الطلاب المتميزون">
            </div>
            
            <div class="form-group">
              <label class="form-label">
                <i class="fas fa-hashtag"></i>
                العدد
              </label>
              <input type="number" class="form-control" id="participants-count" 
                     placeholder="مثال: 15">
            </div>
            
            <div class="form-group">
              <label class="form-label">
                <i class="fas fa-map-marker"></i>
                مكان التنفيذ
              </label>
              <input type="text" class="form-control" id="location" 
                     placeholder="مثال: مختبر البحث">
            </div>
          </div>
        </div>

        <!-- المحتوى الرئيسي -->
        <div class="content-section">
          <div class="content-box">
            <div class="content-box-title">
              <i class="fas fa-bullseye"></i>
              الهدف التربوي
            </div>
            <textarea class="form-control" id="educational-goal" 
                      placeholder="اكتب الهدف التربوي هنا..." 
                      rows="3" required maxlength="500"></textarea>
            <div class="char-count"><span id="goal-chars">0</span>/500 حرف</div>
          </div>
        </div>

        <div class="content-section">
          <div class="content-box">
            <div class="content-box-title">
              <i class="fas fa-tasks"></i>
              خطوات التنفيذ
            </div>
            <textarea id="implementation-steps" 
                      placeholder="اكتب خطوات التنفيذ هنا..." 
                      rows="4" maxlength="500"></textarea>
            <div class="char-count"><span id="steps-chars">0</span>/500 حرف</div>
          </div>
        </div>

        <div class="content-section">
          <div class="content-box">
            <div class="content-box-title">
              <i class="fas fa-chart-line"></i>
              النتائج المتحققة
            </div>
            <textarea id="achieved-results" 
                      placeholder="اكتب النتائج المتحققة هنا..." 
                      rows="4" maxlength="500"></textarea>
            <div class="char-count"><span id="results-chars">0</span>/500 حرف</div>
          </div>
        </div>

        <div class="content-section">
          <div class="content-box">
            <div class="content-box-title">
              <i class="fas fa-thumbs-up"></i>
              نقاط القوة
            </div>
            <textarea id="strengths" 
                      placeholder="اكتب نقاط القوة هنا..." 
                      rows="3" maxlength="500"></textarea>
            <div class="char-count"><span id="strengths-chars">0</span>/500 حرف</div>
          </div>
        </div>

        <div class="content-section">
          <div class="content-box">
            <div class="content-box-title">
              <i class="fas fa-comments"></i>
              التوصيات والمقترحات
            </div>
            <textarea id="recommendations" 
                      placeholder="اكتب التوصيات والمقترحات هنا..." 
                      rows="3" maxlength="500"></textarea>
            <div class="char-count"><span id="recommendations-chars">0</span>/500 حرف</div>
          </div>
        </div>

        <div class="content-section">
          <div class="content-box">
            <div class="content-box-title">
              <i class="fas fa-lightbulb"></i>
              نقاط التحسين
            </div>
            <textarea id="improvements" 
                      placeholder="اكتب نقاط التحسين هنا..." 
                      rows="3" maxlength="500"></textarea>
            <div class="char-count"><span id="improvements-chars">0</span>/500 حرف</div>
          </div>
        </div>

        <!-- الصور التوثيقية -->
        <div class="upload-section">
          <h3 class="form-section-title">
            <i class="fas fa-images"></i>
            الصور التوثيقية (صورتين كحد أقصى)
          </h3>
          
          <div class="upload-area" onclick="document.getElementById('image-upload').click()">
            <i class="fas fa-cloud-upload-alt"></i>
            <p>انقر أو اسحب الصور هنا</p>
            <small>يسمح بصورتين كحد أقصى (JPEG, PNG)</small>
          </div>
          
          <input type="file" id="image-upload" accept="image/*" multiple 
                 style="display: none" onchange="handleImageUpload(this)">
          
          <div class="image-preview" id="image-preview"></div>
        </div>

        <!-- التوقيعات -->
        <div class="signatures-section">
          <h3 class="form-section-title">
            <i class="fas fa-signature"></i>
            التوقيعات
          </h3>
          
          <div class="signatures-grid">
            <div class="signature-field">
              <label class="form-label">
                <i class="fas fa-chalkboard-teacher"></i>
                اسم المعلم
              </label>
              <input type="text" class="signature-input" id="teacher-name" 
                     placeholder="أدخل اسمك الكامل" required>
            </div>
            
            <div class="signature-field">
              <label class="form-label">
                <i class="fas fa-user-tie"></i>
                اسم المدير
              </label>
              <input type="text" class="signature-input" id="principal-name" 
                     placeholder="اسم مدير المدرسة">
            </div>
          </div>
        </div>
      </div>
    </main>

    <!-- لوحة التحكم -->
    <aside class="control-panel">
      <h3 class="form-section-title">
        <i class="fas fa-magic"></i>
        قوالب جاهزة
      </h3>
      
      <div class="quick-templates">
        <button class="template-btn" onclick="loadTemplate(1)">
          <i class="fas fa-star"></i>
          <span>نشاط إثرائي</span>
        </button>
        
        <button class="template-btn" onclick="loadTemplate(2)">
          <i class="fas fa-heart"></i>
          <span>خطة علاجية</span>
        </button>
        
        <button class="template-btn" onclick="loadTemplate(3)">
          <i class="fas fa-lightbulb"></i>
          <span>نشاط إبداعي</span>
        </button>
        
        <button class="template-btn" onclick="loadTemplate(4)">
          <i class="fas fa-chart-bar"></i>
          <span>تقرير تقويمي</span>
        </button>
      </div>
      
      <h3 class="form-section-title">
        <i class="fas fa-cogs"></i>
        أدوات التحكم
      </h3>
      
      <div class="action-buttons">
        <button class="action-btn action-btn-primary" onclick="showPreview()">
          <i class="fas fa-eye"></i>
          معاينة التقرير
        </button>
        
        <button class="action-btn action-btn-success" onclick="printReport()">
          <i class="fas fa-print"></i>
          طباعة التقرير
        </button>
        
        <button class="action-btn action-btn-whatsapp" onclick="shareAsPDF()">
          <i class="fab fa-whatsapp"></i>
          إرسال PDF عبر واتساب
        </button>
        
        <button class="action-btn action-btn-secondary" onclick="downloadAsPDF()">
          <i class="fas fa-download"></i>
          تحميل PDF
        </button>
        
        <button class="action-btn action-btn-secondary" onclick="saveDraft()">
          <i class="fas fa-save"></i>
          حفظ كمسودة
        </button>
        
        <button class="action-btn" style="background: #ef4444; color: white;" onclick="clearForm()">
          <i class="fas fa-trash"></i>
          مسح النموذج
        </button>
      </div>
      
      <div class="alert alert-warning" style="margin-top: 12px;">
        <i class="fas fa-info-circle"></i>
        <span>يتم الحفظ تلقائياً في ذاكرة المتصفح</span>
      </div>
    </aside>
  </div>
</div>

<!-- شريط التنقل السفلي للجوال -->
<nav class="mobile-nav">
  <button class="nav-btn active" onclick="scrollToTop()">
    <i class="fas fa-home"></i>
    <span>الرئيسية</span>
  </button>
  
  <button class="nav-btn" onclick="showPreview()">
    <i class="fas fa-eye"></i>
    <span>معاينة</span>
  </button>
  
  <button class="nav-btn" onclick="printReport()">
    <i class="fas fa-print"></i>
    <span>طباعة</span>
  </button>
  
  <button class="nav-btn" onclick="shareAsPDF()">
    <i class="fab fa-whatsapp"></i>
    <span>واتساب</span>
  </button>
</nav>

<!-- زر المساعدة -->
<button class="help-btn" onclick="showHelp()">
  <i class="fas fa-question"></i>
</button>

<!-- نافذة المعاينة -->
<div class="preview-overlay" id="preview-overlay">
  <div class="preview-container">
    <div class="preview-header">
      <h3><i class="fas fa-file-pdf"></i> معاينة التقرير</h3>
      <button class="close-preview" onclick="hidePreview()">
        <i class="fas fa-times"></i>
      </button>
    </div>
    <div class="report-content" id="report-content">
      <!-- محتوى التقرير -->
    </div>
  </div>
</div>

<!-- نافذة المساعدة -->
<div class="preview-overlay" id="help-overlay">
  <div class="preview-container" style="max-width: 500px;">
    <div class="preview-header">
      <h3><i class="fas fa-question-circle"></i> المساعدة والدعم</h3>
      <button class="close-preview" onclick="hideHelp()">
        <i class="fas fa-times"></i>
      </button>
    </div>
    <div style="padding: 20px;">
      <h4 style="color: var(--primary); margin-bottom: 15px;">كيفية استخدام الأداة:</h4>
      
      <div style="margin-bottom: 15px;">
        <div style="display: flex; align-items: flex-start; gap: 10px; margin-bottom: 10px;">
          <i class="fas fa-edit" style="color: var(--primary);"></i>
          <div>
            <strong>1. تعبئة النموذج:</strong>
            <p style="font-size: 13px; color: var(--gray);">املأ جميع الحقول المطلوبة لتوليد التقرير</p>
          </div>
        </div>
        
        <div style="display: flex; align-items: flex-start; gap: 10px; margin-bottom: 10px;">
          <i class="fas fa-eye" style="color: var(--primary);"></i>
          <div>
            <strong>2. المعاينة:</strong>
            <p style="font-size: 13px; color: var(--gray);">استعرض التقرير قبل الطباعة أو الحفظ</p>
          </div>
        </div>
        
        <div style="display: flex; align-items: flex-start; gap: 10px; margin-bottom: 10px;">
          <i class="fas fa-print" style="color: var(--primary);"></i>
          <div>
            <strong>3. الطباعة:</strong>
            <p style="font-size: 13px; color: var(--gray);">اطبع التقرير مباشرة على طابعتك</p>
          </div>
        </div>
        
        <div style="display: flex; align-items: flex-start; gap: 10px; margin-bottom: 10px;">
          <i class="fab fa-whatsapp" style="color: var(--whatsapp);"></i>
          <div>
            <strong>4. المشاركة:</strong>
            <p style="font-size: 13px; color: var(--gray);">شارك التقرير كـ PDF عبر الواتساب</p>
          </div>
        </div>
      </div>
      
      <div class="alert alert-info">
        <i class="fas fa-lightbulb"></i>
        <span>لأفضل تجربة، استخدم المتصفح على أحدث إصدار</span>
      </div>
    </div>
  </div>
</div>

<!-- شاشة التحميل -->
<div class="loading-overlay" id="loading-overlay">
  <div class="loading-spinner"></div>
  <p id="loading-text">جاري إنشاء التقرير...</p>
</div>

<script>
// بيانات التطبيق
const templates = {
  1: {
    name: "نشاط إثرائي",
    type: "نشاط إثرائي",
    goal: "تنمية مهارات التفكير النقدي والإبداعي لدى الطلاب المتميزين من خلال أنشطة متقدمة تحفز الابتكار وتطور القدرات البحثية.",
    steps: `1. اختيار الطلاب الموهوبين بناءً على معايير محددة
2. عقد ورش عمل متخصصة في التفكير الإبداعي
3. تنفيذ مشاريع بحثية مصغرة
4. تنظيم مسابقات علمية محفزة
5. متابعة وتقييم فردي لكل طالب`,
    results: `• تطوير 8 مشاريع بحثية مبتكرة
• تحسن ملحوظ في مهارات التحليل بنسبة 40%
• مشاركة ناجحة في المسابقات المحلية
• زيادة الثقة العلمية لدى الطلاب`,
    recommendations: `• توسيع نطاق البرنامج ليشمل المزيد من الطلاب
• تدريب معلمين متخصصين في الإثراء العلمي
• إنشاء مكتبة مصادر رقمية متخصصة
• توثيق التجارب الناجحة ونشرها`,
    strengths: `• تفاعل الطلاب الإيجابي مع الأنشطة
• تنوع الأساليب التعليمية المستخدمة
• توافر الموارد التعليمية المساعدة
• دعم إدارة المدرسة للبرنامج`,
    improvements: `• زيادة وقت الأنشطة العملية
• توفير المزيد من الأجهزة التقنية
• تطوير أدوات تقييم أكثر شمولية
• تعزيز الشراكة مع أولياء الأمور`,
    target: "الطلاب المتميزون",
    subject: "أحياء",
    classLevel: "الثالث الثانوي",
    count: "15",
    location: "مختبر البحث"
  },
  2: {
    name: "خطة علاجية",
    type: "خطة علاجية",
    goal: "معالجة الصعوبات القرائية والكتابية لدى الطلاب المتأخرين دراسياً وتحسين مهاراتهم الأساسية في اللغة العربية.",
    steps: `1. تشخيص فردي للصعوبات التعليمية
2. تصميم خطط علاجية مخصصة
3. جلسات علاجية مكثفة أسبوعياً
4. استخدام وسائل تعليمية مساعدة
5. متابعة أسرية وتقييم دوري`,
    results: `• تحسن مهارات القراءة بنسبة 65%
• تحسن مهارات الكتابة بنسبة 55%
• زيادة مشاركة الطلاب في الفصل
• تحسن الثقة بالنفس لدى الطلاب`,
    recommendations: `• تطوير أدوات تشخيص أكثر دقة
• تدريب فرق علاجية متخصصة
• إنشاء بنك أنشطة علاجية
• تعزيز الشراكة مع أولياء الأمور`,
    strengths: `• البرنامج الفردي المخصص
• استخدام وسائل تعليمية متنوعة
• المتابعة المستمرة للطلاب
• التعاون مع أولياء الأمور`,
    improvements: `• زيادة عدد الجلسات العلاجية
• توفير مختبر لغوي متكامل
• تدريب أكثر تخصصاً للمعلمين
• تطوير مواد تعليمية إضافية`,
    target: "الطلاب المتأخرين دراسياً",
    subject: "اللغة العربية",
    classLevel: "الأول متوسط",
    count: "8",
    location: "قاعة مصادر التعلم"
  },
  3: {
    name: "نشاط إبداعي",
    type: "نشاط إثرائي",
    goal: "تنمية المهارات التقنية والبرمجية لدى الطلاب الموهوبين وتهيئتهم لمتطلبات العصر الرقمي.",
    steps: `1. تدريب على أساسيات البرمجة
2. ورش عمل في التصميم الرقمي
3. مشاريع تقنية تطبيقية
4. مسابقات برمجية
5. زيارات ميدانية لشركات تقنية`,
    results: `• تصميم 12 موقعاً إلكترونياً تعليمياً
• تطوير 5 تطبيقات تعليمية
• فوز في مسابقات برمجية محلية
• اكتشاف مواهب تقنية واعدة`,
    recommendations: `• توفير معامل حاسوب متطورة
• تأهيل مدربين في المجال التقني
• إنشاء نادي تقني مدرسي
• شراكات مع مؤسسات تقنية`,
    strengths: `• حماس الطلاب للتقنية
• توافر الأجهزة الحديثة
• دعم المجتمع المحلي
• نجاح المشاريع التطبيقية`,
    improvements: `• تحديث الأجهزة بشكل دوري
• زيادة ساعات التدريب
• تنويع المجالات التقنية
• تعزيز الجانب العملي`,
    target: "الطلاب المهتمين بالتكنولوجيا",
    subject: "الحاسب الآلي",
    classLevel: "الثاني ثانوي",
    count: "12",
    location: "معمل الحاسب الآلي"
  },
  4: {
    name: "تقرير تقويمي",
    type: "تقرير تقويمي",
    goal: "تقويم أداء الطلاب في نهاية الفصل الدراسي وتحديد مستوى تحقيق الأهداف التعليمية.",
    steps: `1. إعداد اختبارات تقويمية شاملة
2. تحليل نتائج الاختبارات
3. مقابلات فردية مع الطلاب
4. دراسة مؤشرات الأداء
5. تقييم المنهج الدراسي`,
    results: `• تحقيق 85% من الطلاب للمستوى المطلوب
• تحسن في متوسط الدرجات بنسبة 15%
• ارتفاع مؤشر الرضا عن التعليم
• تحديد نقاط القوة والضعف`,
    recommendations: `• تطوير استراتيجيات التدريس
• تحسين الوسائل التعليمية
• تنويع أساليب التقويم
• تعزيز التعلم الذاتي`,
    strengths: `• شمولية عملية التقويم
• موضوعية النتائج
• مشاركة الطلاب في التقييم
• دقة التحليل الإحصائي`,
    improvements: `• تطوير أدوات قياس أكثر دقة
• زيادة فترات التقويم
• تدريب المعلمين على التقويم
• تحليل نتائج أكثر تفصيلاً`,
    target: "جميع طلاب الصف",
    subject: "الرياضيات",
    classLevel: "الثالث متوسط",
    count: "30",
    location: "الفصل الدراسي"
  }
};

let uploadedImages = [];

// تحديث عداد الأحرف
function updateCharCount(textareaId, counterId) {
  const textarea = document.getElementById(textareaId);
  const counter = document.getElementById(counterId);
  
  if (!textarea || !counter) return;
  
  textarea.addEventListener('input', function() {
    const chars = this.value.length;
    counter.textContent = chars;
    
    if (chars > 500) {
      this.value = this.value.substring(0, 500);
      counter.textContent = 500;
      counter.style.color = '#dc2626';
    } else {
      counter.style.color = '#6b7280';
    }
  });
  
  // التهيئة الأولية
  const initialChars = textarea.value.length;
  counter.textContent = initialChars;
  if (initialChars > 500) {
    counter.style.color = '#dc2626';
  }
}

// تحميل القالب
function loadTemplate(templateId) {
  const template = templates[templateId];
  if (!template) return;
  
  // تعبئة الحقول
  document.getElementById('report-type').value = template.type;
  document.getElementById('educational-goal').value = template.goal;
  document.getElementById('implementation-steps').value = template.steps;
  document.getElementById('achieved-results').value = template.results;
  document.getElementById('strengths').value = template.strengths;
  document.getElementById('recommendations').value = template.recommendations;
  document.getElementById('improvements').value = template.improvements;
  document.getElementById('target-audience').value = template.target;
  document.getElementById('subject').value = template.subject;
  document.getElementById('class-level').value = template.classLevel;
  document.getElementById('participants-count').value = template.count;
  document.getElementById('location').value = template.location;
  
  // تحديث عداد الأحرف
  ['educational-goal', 'implementation-steps', 'achieved-results', 
   'strengths', 'recommendations', 'improvements'].forEach((id, index) => {
    updateCharCount(id, ['goal-chars', 'steps-chars', 'results-chars', 
                        'strengths-chars', 'recommendations-chars', 
                        'improvements-chars'][index]);
  });
  
  // إضافة قيم افتراضية
  if (!document.getElementById('school-name').value) {
    document.getElementById('school-name').value = "مدرسة التجربة النموذجية";
  }
  if (!document.getElementById('teacher-name').value) {
    document.getElementById('teacher-name').value = "أحمد محمد علي";
  }
  if (!document.getElementById('principal-name').value) {
    document.getElementById('principal-name').value = "خالد بن عبدالله السليم";
  }
  if (!document.getElementById('education-department').value) {
    document.getElementById('education-department').value = "الرياض";
  }
  
  showAlert(`تم تحميل قالب "${template.name}" بنجاح`, 'success');
}

// مسح النموذج
function clearForm() {
  if (!confirm('هل أنت متأكد من رغبتك في مسح جميع البيانات؟')) return;
  
  const fields = [
    'school-name', 'target-audience', 'educational-goal',
    'implementation-steps', 'achieved-results', 'recommendations',
    'teacher-name', 'principal-name', 'subject', 'strengths', 'improvements',
    'class-level', 'participants-count', 'location'
  ];
  
  fields.forEach(fieldId => {
    const element = document.getElementById(fieldId);
    if (element) element.value = '';
  });
  
  // مسح الصور
  uploadedImages = [];
  const preview = document.getElementById('image-preview');
  if (preview) preview.innerHTML = '';
  const uploadInput = document.getElementById('image-upload');
  if (uploadInput) uploadInput.value = '';
  
  // إعادة تعيين القوائم المنسدلة
  const departmentSelect = document.getElementById('education-department');
  if (departmentSelect) departmentSelect.value = '';
  
  const reportType = document.getElementById('report-type');
  if (reportType) reportType.value = 'نشاط إثرائي';
  
  const semester = document.getElementById('semester');
  if (semester) semester.value = 'الأول';
  
  // تحديث عداد الأحرف
  ['educational-goal', 'implementation-steps', 'achieved-results', 
   'strengths', 'recommendations', 'improvements'].forEach((id, index) => {
    updateCharCount(id, ['goal-chars', 'steps-chars', 'results-chars', 
                        'strengths-chars', 'recommendations-chars', 
                        'improvements-chars'][index]);
  });
  
  showAlert('تم مسح جميع البيانات بنجاح', 'success');
}

// رفع الصور
function handleImageUpload(input) {
  const files = Array.from(input.files).slice(0, 2);
  const preview = document.getElementById('image-preview');
  
  if (!preview) return;
  
  if (files.length > 2) {
    showAlert('يمكنك رفع صورتين كحد أقصى', 'error');
    input.value = '';
    return;
  }
  
  uploadedImages = [];
  preview.innerHTML = '';
  
  files.forEach((file, index) => {
    if (!file.type.match('image.*')) {
      showAlert('يرجى رفع ملفات صور فقط', 'error');
      return;
    }
    
    if (file.size > 5 * 1024 * 1024) {
      showAlert('حجم الصورة يجب أن يكون أقل من 5MB', 'error');
      return;
    }
    
    const reader = new FileReader();
    reader.onload = function(e) {
      uploadedImages.push({
        data: e.target.result,
        name: file.name
      });
      
      const imgDiv = document.createElement('div');
      imgDiv.className = 'preview-image';
      imgDiv.innerHTML = `
        <img src="${e.target.result}" alt="صورة ${index + 1}">
        <div class="remove-image" onclick="removeImage(${index})">
          <i class="fas fa-times"></i>
        </div>
      `;
      preview.appendChild(imgDiv);
    };
    reader.readAsDataURL(file);
  });
  
  if (files.length > 0) {
    showAlert(`تم رفع ${files.length} صورة بنجاح`, 'success');
  }
}

// إزالة صورة
function removeImage(index) {
  uploadedImages.splice(index, 1);
  const preview = document.getElementById('image-preview');
  if (!preview) return;
  
  preview.innerHTML = '';
  
  uploadedImages.forEach((img, i) => {
    const imgDiv = document.createElement('div');
    imgDiv.className = 'preview-image';
    imgDiv.innerHTML = `
      <img src="${img.data}" alt="صورة ${i + 1}">
      <div class="remove-image" onclick="removeImage(${i})">
        <i class="fas fa-times"></i>
      </div>
    `;
    preview.appendChild(imgDiv);
  });
}

// عرض المعاينة
function showPreview() {
  const data = collectFormData();
  
  if (!validateForm()) {
    showAlert('الرجاء تعبئة الحقول المطلوبة (اسم المدرسة، الهدف التربوي، اسم المعلم)', 'error');
    return;
  }
  
  buildPreviewContent(data);
  document.getElementById('preview-overlay').style.display = 'flex';
  document.body.style.overflow = 'hidden';
}

// إخفاء المعاينة
function hidePreview() {
  document.getElementById('preview-overlay').style.display = 'none';
  document.body.style.overflow = 'auto';
}

// عرض المساعدة
function showHelp() {
  document.getElementById('help-overlay').style.display = 'flex';
  document.body.style.overflow = 'hidden';
}

// إخفاء المساعدة
function hideHelp() {
  document.getElementById('help-overlay').style.display = 'none';
  document.body.style.overflow = 'auto';
}

// الطباعة المباشرة - النسخة المصلحة
function printReport() {
  const data = collectFormData();
  
  if (!validateForm()) {
    showAlert('الرجاء تعبئة الحقول المطلوبة قبل الطباعة', 'error');
    return;
  }
  
  showLoading('جاري إعداد التقرير للطباعة...');
  
  try {
    // إنشاء محتوى HTML للتقرير
    const reportHTML = createReportHTML(data);
    
    // إنشاء نافذة جديدة للطباعة
    const printWindow = window.open('', '_blank', 'width=800,height=600');
    
    if (!printWindow) {
      hideLoading();
      showAlert('تم منع النافذة المنبثقة. الرجاء السماح بالنوافذ المنبثقة لهذا الموقع.', 'error');
      return;
    }
    
    printWindow.document.write(`
      <!DOCTYPE html>
      <html dir="rtl" lang="ar">
      <head>
        <meta charset="UTF-8">
        <title>تقرير - ${data.school}</title>
        <style>
          @import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap');
          * { margin: 0; padding: 0; box-sizing: border-box; }
          body { 
            font-family: 'Cairo', sans-serif; 
            padding: 20px;
            background: white;
            color: #1f2937;
          }
          .print-container { max-width: 800px; margin: 0 auto; }
          .header { 
            text-align: center; 
            margin-bottom: 30px; 
            padding-bottom: 20px; 
            border-bottom: 3px solid #083024;
            background: url('https://i.ibb.co/kVWFFwhW/9-C92-E57-B-23-FA-479-D-A024-1-D5-F871-B4-F8-D.png') center/contain no-repeat;
            background-size: 200px;
            position: relative;
            min-height: 120px;
            padding-top: 30px;
          }
          .header::before {
            content: '';
            position: absolute;
            top: 0;
            right: 0;
            bottom: 0;
            left: 0;
            background: rgba(255, 255, 255, 0.9);
          }
          .header > * { position: relative; z-index: 2; }
          h1 { color: #083024; font-size: 24px; margin-bottom: 10px; }
          h2 { color: #1f2937; font-size: 18px; margin-bottom: 5px; }
          h3 { color: #6b7280; font-size: 16px; margin-bottom: 10px; }
          .info-grid { 
            display: grid; 
            grid-template-columns: repeat(3, 1fr); 
            gap: 10px; 
            margin-bottom: 20px; 
          }
          .info-box {
            border: 1px solid #083024;
            border-radius: 6px;
            padding: 10px;
            text-align: center;
            font-size: 14px;
            background: white;
          }
          .info-box strong { display: block; color: #083024; margin-bottom: 5px; }
          .section { margin-bottom: 25px; }
          .section-title { 
            color: #083024; 
            font-size: 18px; 
            margin-bottom: 15px; 
            padding-bottom: 8px; 
            border-bottom: 2px solid #083024; 
          }
          .section-content { 
            background: #f9fafb; 
            padding: 15px; 
            border-radius: 8px; 
            white-space: pre-line;
            line-height: 1.8;
          }
          .grid-2 { 
            display: grid; 
            grid-template-columns: 1fr 1fr; 
            gap: 20px; 
            margin-bottom: 20px; 
          }
          .signatures { 
            display: flex; 
            justify-content: space-around; 
            margin-top: 40px; 
            padding-top: 20px; 
            border-top: 1px solid #d1d5db; 
          }
          .signature-box { text-align: center; }
          .signature-line { 
            width: 150px; 
            height: 1px; 
            background: #083024; 
            margin: 10px auto; 
          }
          .date { 
            text-align: center; 
            color: #6b7280; 
            margin-top: 10px; 
            font-size: 14px; 
          }
          @media print {
            body { padding: 10px; }
            .header { background-size: 150px; min-height: 100px; padding-top: 20px; }
            .section-title { font-size: 16px; }
          }
        </style>
      </head>
      <body>
        <div class="print-container">
          ${reportHTML}
        </div>
        <script>
          // الطباعة تلقائياً بعد تحميل الصفحة
          window.onload = function() {
            setTimeout(function() {
              window.print();
              window.onafterprint = function() {
                window.close();
              };
            }, 1000);
          };
        <\/script>
      </body>
      </html>
    `);
    
    printWindow.document.close();
    
    // إخفاء شاشة التحميل
    hideLoading();
    showAlert('تم فتح نافذة الطباعة بنجاح', 'success');
    
  } catch (error) {
    hideLoading();
    console.error('خطأ في الطباعة:', error);
    showAlert('حدث خطأ أثناء الطباعة. الرجاء المحاولة مرة أخرى.', 'error');
  }
}

// إنشاء HTML للتقرير
function createReportHTML(data) {
  const hijriDate = getHijriDate();
  const currentDate = new Date().toLocaleDateString('ar-SA');
  
  return `
    <div class="header">
      <h1>وزارة التعليم</h1>
      <h2>${data.department || 'وزارة التعليم'}</h2>
      <h3>${data.school}</h3>
      <div class="date">${currentDate} - ${hijriDate}</div>
    </div>
    
    <div class="info-grid">
      <div class="info-box">
        <strong>الفصل الدراسي</strong>
        ${data.semester}
      </div>
      <div class="info-box">
        <strong>الصف</strong>
        ${data.classLevel || 'غير محدد'}
      </div>
      <div class="info-box">
        <strong>المادة</strong>
        ${data.subject || 'غير محدد'}
      </div>
    </div>
    
    <div class="info-grid">
      <div class="info-box">
        <strong>نوع التقرير</strong>
        ${data.type || 'نشاط إثرائي'}
      </div>
      <div class="info-box">
        <strong>الفئة المستهدفة</strong>
        ${data.target || 'غير محدد'}
      </div>
      <div class="info-box">
        <strong>العدد</strong>
        ${data.count || 'غير محدد'}
      </div>
    </div>
    
    <div class="section">
      <div class="section-title">الهدف التربوي</div>
      <div class="section-content">${data.goal || 'لم يتم تحديد الهدف التربوي'}</div>
    </div>
    
    <div class="grid-2">
      <div class="section">
        <div class="section-title">خطوات التنفيذ</div>
        <div class="section-content">${data.steps || 'لم يتم تحديد خطوات التنفيذ'}</div>
      </div>
      <div class="section">
        <div class="section-title">النتائج المتحققة</div>
        <div class="section-content">${data.results || 'لم يتم تحديد النتائج'}</div>
      </div>
    </div>
    
    <div class="grid-2">
      <div class="section">
        <div class="section-title">نقاط القوة</div>
        <div class="section-content">${data.strengths || 'لم يتم تحديد نقاط القوة'}</div>
      </div>
      <div class="section">
        <div class="section-title">التوصيات والمقترحات</div>
        <div class="section-content">${data.recommendations || 'لم يتم تحديد توصيات'}</div>
      </div>
    </div>
    
    <div class="section">
      <div class="section-title">نقاط التحسين</div>
      <div class="section-content">${data.improvements || 'لم يتم تحديد نقاط التحسين'}</div>
    </div>
    
    ${uploadedImages.length > 0 ? `
      <div class="section">
        <div class="section-title">الصور التوثيقية</div>
        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-top: 15px;">
          ${uploadedImages.map(img => `
            <div style="border: 1px solid #d1d5db; border-radius: 8px; overflow: hidden; height: 200px;">
              <img src="${img.data}" style="width: 100%; height: 100%; object-fit: cover;" alt="صورة توثيقية">
            </div>
          `).join('')}
        </div>
      </div>
    ` : ''}
    
    <div class="signatures">
      ${data.teacher ? `
        <div class="signature-box">
          <div style="font-weight: 600; margin-bottom: 5px;">المعلم</div>
          <div class="signature-line"></div>
          <div>${data.teacher}</div>
        </div>
      ` : ''}
      
      ${data.principal ? `
        <div class="signature-box">
          <div style="font-weight: 600; margin-bottom: 5px;">مدير المدرسة</div>
          <div class="signature-line"></div>
          <div>${data.principal}</div>
        </div>
      ` : ''}
    </div>
  `;
}

// تحميل التقرير كـ PDF باستخدام html2pdf
async function downloadAsPDF() {
  const data = collectFormData();
  
  if (!validateForm()) {
    showAlert('الرجاء تعبئة الحقول المطلوبة قبل إنشاء PDF', 'error');
    return;
  }
  
  showLoading('جاري إنشاء ملف PDF...');
  
  try {
    // إنشاء عنصر مؤقت لمعاينة PDF
    const tempDiv = document.createElement('div');
    tempDiv.style.position = 'absolute';
    tempDiv.style.left = '-9999px';
    tempDiv.style.top = '-9999px';
    tempDiv.style.width = '800px';
    tempDiv.style.padding = '20px';
    tempDiv.style.background = 'white';
    tempDiv.style.fontFamily = "'Cairo', sans-serif";
    tempDiv.dir = 'rtl';
    
    // إضافة المحتوى إلى العنصر المؤقت
    tempDiv.innerHTML = createReportHTML(data);
    
    // إضافة العنصر إلى الصفحة
    document.body.appendChild(tempDiv);
    
    // تهيئة خيارات html2pdf
    const options = {
      margin: [15, 15],
      filename: `تقرير_${data.school}_${new Date().toISOString().split('T')[0]}.pdf`,
      image: { type: 'jpeg', quality: 0.98 },
      html2canvas: { 
        scale: 2,
        useCORS: true,
        logging: false,
        allowTaint: true
      },
      jsPDF: { 
        unit: 'mm', 
        format: 'a4', 
        orientation: 'portrait',
        compress: true
      }
    };
    
    // إنشاء PDF
    await html2pdf().set(options).from(tempDiv).save();
    
    // إزالة العنصر المؤقت
    document.body.removeChild(tempDiv);
    
    hideLoading();
    showAlert('تم تحميل ملف PDF بنجاح', 'success');
    
  } catch (error) {
    hideLoading();
    console.error('خطأ في إنشاء PDF:', error);
    showAlert('حدث خطأ أثناء إنشاء ملف PDF', 'error');
  }
}

// إرسال التقرير عبر واتساب كـ PDF
async function shareAsPDF() {
  const data = collectFormData();
  
  if (!validateForm()) {
    showAlert('الرجاء تعبئة الحقول المطلوبة قبل المشاركة', 'error');
    return;
  }
  
  showLoading('جاري إعداد التقرير للمشاركة عبر واتساب...');
  
  try {
    // إنشاء عنصر مؤقت لمعاينة PDF
    const tempDiv = document.createElement('div');
    tempDiv.style.position = 'absolute';
    tempDiv.style.left = '-9999px';
    tempDiv.style.top = '-9999px';
    tempDiv.style.width = '800px';
    tempDiv.style.padding = '20px';
    tempDiv.style.background = 'white';
    tempDiv.style.fontFamily = "'Cairo', sans-serif";
    tempDiv.dir = 'rtl';
    
    // إضافة المحتوى إلى العنصر المؤقت
    tempDiv.innerHTML = createReportHTML(data);
    
    // إضافة العنصر إلى الصفحة
    document.body.appendChild(tempDiv);
    
    // إنشاء PDF أولاً
    const options = {
      margin: [15, 15],
      filename: `تقرير_${data.school}.pdf`,
      image: { type: 'jpeg', quality: 0.98 },
      html2canvas: { 
        scale: 2,
        useCORS: true,
        logging: false
      },
      jsPDF: { 
        unit: 'mm', 
        format: 'a4', 
        orientation: 'portrait'
      }
    };
    
    // إنشاء PDF كـ blob
    const pdfOutput = await html2pdf().set(options).from(tempDiv).output('blob');
    
    // إزالة العنصر المؤقت
    document.body.removeChild(tempDiv);
    
    // إنشاء رابط لـ blob
    const pdfBlobUrl = URL.createObjectURL(pdfOutput);
    
    // إنشاء نص للرسالة
    let message = `📋 *تقرير تعليمي*\n\n`;
    message += `🏫 *المدرسة:* ${data.school}\n`;
    message += `📍 *الإدارة:* ${data.department || 'غير محدد'}\n`;
    message += `📄 *نوع التقرير:* ${data.type || 'نشاط إثرائي'}\n`;
    message += `📚 *الفصل:* ${data.semester}\n`;
    message += `👥 *الصف:* ${data.classLevel || 'غير محدد'}\n`;
    message += `📖 *المادة:* ${data.subject || 'غير محدد'}\n\n`;
    message += `🎯 *الهدف التربوي:*\n${data.goal.substring(0, 100)}${data.goal.length > 100 ? '...' : ''}\n\n`;
    message += `📝 *تم إنشاء التقرير بتاريخ:* ${new Date().toLocaleDateString('ar-SA')}\n`;
    message += `📎 *التقرير مرفق كملف PDF*`;
    
    // إنشاء رابط الواتساب مع الرسالة
    const encodedMessage = encodeURIComponent(message);
    const whatsappURL = `https://wa.me/?text=${encodedMessage}`;
    
    // في متصفحات حديثة يمكن محاولة مشاركة الملف
    if (navigator.share && navigator.canShare) {
      try {
        const file = new File([pdfOutput], `تقرير_${data.school}.pdf`, { type: 'application/pdf' });
        
        if (navigator.canShare({ files: [file] })) {
          await navigator.share({
            title: `تقرير ${data.school}`,
            text: message,
            files: [file]
          });
          
          hideLoading();
          showAlert('تم مشاركة التقرير بنجاح', 'success');
          return;
        }
      } catch (shareError) {
        console.log('مشاركة الملف غير مدعومة، استخدام رابط الواتساب التقليدي');
      }
    }
    
    // فتح نافذة جديدة للواتساب
    const whatsappWindow = window.open(whatsappURL, '_blank');
    
    // بعد ثانية، حاول فتح نافذة لتحميل PDF
    setTimeout(() => {
      if (whatsappWindow && !whatsappWindow.closed) {
        // فتح نافذة جديدة لتحميل PDF
        const downloadWindow = window.open(pdfBlobUrl, '_blank');
        
        // توجيه المستخدم لتحميل الملف وإرساله يدوياً
        setTimeout(() => {
          showAlert('يرجى تحميل ملف PDF من النافذة المنبثقة وإرساله عبر واتساب', 'info');
        }, 1000);
      } else {
        // إذا تم منع النوافذ المنبثقة، عرض خيارات بديلة
        const shouldDownload = confirm('يرجى السماح بالنوافذ المنبثقة لمشاركة PDF. هل تريد تحميل الملف بدلاً من ذلك؟');
        if (shouldDownload) {
          const link = document.createElement('a');
          link.href = pdfBlobUrl;
          link.download = `تقرير_${data.school}.pdf`;
          link.click();
          showAlert('تم تحميل ملف PDF. يمكنك إرساله يدوياً عبر واتساب', 'success');
        }
      }
    }, 1000);
    
    hideLoading();
    
  } catch (error) {
    hideLoading();
    console.error('خطأ في المشاركة:', error);
    showAlert('حدث خطأ أثناء المشاركة عبر واتساب', 'error');
  }
}

// الحصول على التاريخ الهجري
function getHijriDate() {
  const now = new Date();
  const date = now.getDate().toString().padStart(2, '0');
  const month = (now.getMonth() + 1).toString().padStart(2, '0');
  const year = now.getFullYear();
  
  // تقريب للتاريخ الهجري (ليست دقيقة لكنها كافية)
  const hijriYear = Math.floor((year - 622) * 1.0307);
  
  const hijriMonths = [
    'محرم', 'صفر', 'ربيع الأول', 'ربيع الثاني', 
    'جمادى الأولى', 'جمادى الآخرة', 'رجب', 'شعبان', 
    'رمضان', 'شوال', 'ذو القعدة', 'ذو الحجة'
  ];
  
  const currentHijriMonth = hijriMonths[now.getMonth()];
  return `${date} ${currentHijriMonth} ${hijriYear} هـ`;
}

// حفظ المسودة
function saveDraft() {
  const data = collectFormData();
  
  try {
    localStorage.setItem('report_draft', JSON.stringify({
      ...data,
      images: uploadedImages,
      timestamp: new Date().toISOString()
    }));
    
    showAlert('تم حفظ المسودة بنجاح في ذاكرة المتصفح', 'success');
  } catch (e) {
    showAlert('حدث خطأ أثناء حفظ المسودة', 'error');
  }
}

// تحميل المسودة
function loadDraft() {
  try {
    const draft = JSON.parse(localStorage.getItem('report_draft'));
    if (!draft) return;
    
    if (confirm('تم العثور على مسودة محفوظة. هل تريد تحميلها؟')) {
      const fields = {
        'school-name': draft.school || '',
        'education-department': draft.department || '',
        'target-audience': draft.target || '',
        'subject': draft.subject || '',
        'educational-goal': draft.goal || '',
        'implementation-steps': draft.steps || '',
        'achieved-results': draft.results || '',
        'recommendations': draft.recommendations || '',
        'strengths': draft.strengths || '',
        'improvements': draft.improvements || '',
        'teacher-name': draft.teacher || '',
        'principal-name': draft.principal || '',
        'class-level': draft.classLevel || '',
        'participants-count': draft.count || '',
        'location': draft.location || '',
        'report-type': draft.type || 'نشاط إثرائي',
        'semester': draft.semester || 'الأول'
      };
      
      Object.entries(fields).forEach(([id, value]) => {
        const element = document.getElementById(id);
        if (element) element.value = value;
      });
      
      if (draft.images && draft.images.length > 0) {
        uploadedImages = draft.images;
        updateImagePreview();
      }
      
      // تحديث عداد الأحرف
      ['educational-goal', 'implementation-steps', 'achieved-results', 
       'strengths', 'recommendations', 'improvements'].forEach((id, index) => {
        updateCharCount(id, ['goal-chars', 'steps-chars', 'results-chars', 
                            'strengths-chars', 'recommendations-chars', 
                            'improvements-chars'][index]);
      });
      
      showAlert('تم تحميل المسودة بنجاح', 'success');
    }
  } catch (e) {
    console.error('خطأ في تحميل المسودة:', e);
  }
}

// تحديث معاينة الصور
function updateImagePreview() {
  const preview = document.getElementById('image-preview');
  if (!preview) return;
  
  preview.innerHTML = '';
  
  uploadedImages.forEach((img, i) => {
    const imgDiv = document.createElement('div');
    imgDiv.className = 'preview-image';
    imgDiv.innerHTML = `
      <img src="${img.data}" alt="صورة ${i + 1}">
      <div class="remove-image" onclick="removeImage(${i})">
        <i class="fas fa-times"></i>
      </div>
    `;
    preview.appendChild(imgDiv);
  });
}

// جمع بيانات النموذج
function collectFormData() {
  const getDepartmentName = (value) => {
    const departments = {
      'الرياض': 'الإدارة العامة للتعليم بمنطقة الرياض',
      'مكة': 'الإدارة العامة للتعليم بمنطقة مكة المكرمة',
      'الشرقية': 'الإدارة العامة للتعليم بالمنطقة الشرقية',
      'المدينة': 'الإدارة العامة للتعليم بمنطقة المدينة المنورة'
    };
    return departments[value] || value;
  };

  return {
    department: getDepartmentName(document.getElementById('education-department')?.value || ''),
    school: document.getElementById('school-name')?.value.trim() || '',
    type: document.getElementById('report-type')?.value || '',
    semester: document.getElementById('semester')?.value || '',
    classLevel: document.getElementById('class-level')?.value.trim() || '',
    subject: document.getElementById('subject')?.value.trim() || '',
    target: document.getElementById('target-audience')?.value.trim() || '',
    count: document.getElementById('participants-count')?.value.trim() || '',
    location: document.getElementById('location')?.value.trim() || '',
    goal: document.getElementById('educational-goal')?.value.trim() || '',
    steps: document.getElementById('implementation-steps')?.value.trim() || '',
    results: document.getElementById('achieved-results')?.value.trim() || '',
    strengths: document.getElementById('strengths')?.value.trim() || '',
    recommendations: document.getElementById('recommendations')?.value.trim() || '',
    improvements: document.getElementById('improvements')?.value.trim() || '',
    teacher: document.getElementById('teacher-name')?.value.trim() || '',
    principal: document.getElementById('principal-name')?.value.trim() || ''
  };
}

// التحقق من صحة البيانات
function validateForm() {
  const data = collectFormData();
  const requiredFields = ['school', 'goal', 'teacher'];
  
  for (const field of requiredFields) {
    if (!data[field]) {
      return false;
    }
  }
  
  return true;
}

// بناء محتوى التقرير للمعاينة
function buildPreviewContent(data) {
  const content = document.getElementById('report-content');
  if (!content) return;
  
  // استخدام نفس قالب الطباعة ولكن للمعاينة
  content.innerHTML = createReportHTML(data);
}

// عرض شاشة التحميل
function showLoading(text = 'جاري التحميل...') {
  document.getElementById('loading-text').textContent = text;
  document.getElementById('loading-overlay').style.display = 'flex';
  document.body.style.overflow = 'hidden';
}

// إخفاء شاشة التحميل
function hideLoading() {
  document.getElementById('loading-overlay').style.display = 'none';
  document.body.style.overflow = 'auto';
}

// عرض التنبيهات
function showAlert(message, type = 'info') {
  const alert = document.createElement('div');
  alert.className = `alert alert-${type}`;
  alert.innerHTML = `
    <i class="fas fa-${type === 'success' ? 'check-circle' : 
                      type === 'warning' ? 'exclamation-triangle' : 
                      type === 'error' ? 'times-circle' : 'info-circle'}"></i>
    <span>${message}</span>
  `;
  
  const container = document.querySelector('.container');
  if (container) {
    container.prepend(alert);
    
    setTimeout(() => {
      if (alert.parentNode) {
        alert.remove();
      }
    }, 5000);
  }
}

// وظائف القائمة الجوال
function scrollToTop() {
  window.scrollTo({ top: 0, behavior: 'smooth' });
  setActiveNavBtn(0);
}

function setActiveNavBtn(index) {
  const navBtns = document.querySelectorAll('.nav-btn');
  navBtns.forEach((btn, i) => {
    if (i === index) {
      btn.classList.add('active');
    } else {
      btn.classList.remove('active');
    }
  });
}

function toggleMenu() {
  const controlPanel = document.querySelector('.control-panel');
  if (controlPanel) {
    controlPanel.style.display = controlPanel.style.display === 'none' ? 'block' : 'none';
  }
}

// إغلاق التنبيه بالنقر
document.addEventListener('click', function(e) {
  if (e.target.closest('.alert')) {
    e.target.closest('.alert').remove();
  }
});

// إغلاق المعاينة بالزر ESC
document.addEventListener('keydown', function(e) {
  if (e.key === 'Escape') {
    hidePreview();
    hideHelp();
  }
});

// إغلاق المعاينة بالنقر خارجها
const previewOverlay = document.getElementById('preview-overlay');
if (previewOverlay) {
  previewOverlay.addEventListener('click', function(e) {
    if (e.target === this) {
      hidePreview();
    }
  });
}

const helpOverlay = document.getElementById('help-overlay');
if (helpOverlay) {
  helpOverlay.addEventListener('click', function(e) {
    if (e.target === this) {
      hideHelp();
    }
  });
}

// تحسين تجربة اللمس
document.addEventListener('DOMContentLoaded', function() {
  // تحميل المسودة عند البدء
  loadDraft();
  
  // تحديث عداد الأحرف
  ['educational-goal', 'implementation-steps', 'achieved-results', 
   'strengths', 'recommendations', 'improvements'].forEach((id, index) => {
    updateCharCount(id, ['goal-chars', 'steps-chars', 'results-chars', 
                        'strengths-chars', 'recommendations-chars', 
                        'improvements-chars'][index]);
  });
  
  // تعيين القيم الافتراضية إذا لم تكن موجودة
  const schoolNameInput = document.getElementById('school-name');
  if (schoolNameInput && !schoolNameInput.value) {
    schoolNameInput.value = "مدرسة التجربة النموذجية";
  }
  
  // إضافة مستمعين للأزرار في الجوال
  const navBtns = document.querySelectorAll('.nav-btn');
  navBtns.forEach((btn, index) => {
    btn.addEventListener('click', () => setActiveNavBtn(index));
  });
  
  // الترحيب
  setTimeout(() => {
    showAlert('مرحباً بك في نظام إعداد التقارير التعليمية', 'success');
  }, 1000);
});

// دعم سحب وإفلات الصور
const uploadArea = document.querySelector('.upload-area');
if (uploadArea) {
  uploadArea.addEventListener('dragover', (e) => {
    e.preventDefault();
    uploadArea.style.borderColor = '#083024';
    uploadArea.style.background = '#f3f4f6';
  });

  uploadArea.addEventListener('dragleave', () => {
    uploadArea.style.borderColor = '';
    uploadArea.style.background = '';
  });

  uploadArea.addEventListener('drop', (e) => {
    e.preventDefault();
    uploadArea.style.borderColor = '';
    uploadArea.style.background = '';
    
    const files = Array.from(e.dataTransfer.files);
    const input = document.getElementById('image-upload');
    
    if (input) {
      // إنشاء DataTransfer object لتعيين الملفات
      const dataTransfer = new DataTransfer();
      files.slice(0, 2).forEach(file => dataTransfer.items.add(file));
      input.files = dataTransfer.files;
      
      handleImageUpload(input);
    }
  });
}
</script>
</body>
</html>