<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>أداة إصدار التقارير والشواهد</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;500;600;700;800&display=swap');
*{margin:0;padding:0;box-sizing:border-box;}
html,body{font-family:'Cairo',sans-serif;background: linear-gradient(135deg, #f0f9f6 0%, #e8f4f0 50%, #d4ebe2 100%);direction:rtl;overflow-x:hidden;min-height:100vh;-webkit-text-size-adjust:100%;-ms-text-size-adjust:100%;}
.wrapper{max-width:850px;margin:auto;padding:15px;width:100%;}

/* شريط الأخبار العلوي - محسن للأجهزة المحمولة */
.top-marquee{
position:fixed;top:0;left:0;right:0;width:100%;background:linear-gradient(135deg, #022e22 0%, #044a35 100%);color:#fff;
padding:10px 5px;font-size:12px;z-index:300;overflow:hidden;height:45px;
white-space:nowrap;border-bottom:3px solid #ffd166;box-shadow:0 4px 12px rgba(2, 46, 34, 0.25);
display:flex;align-items:center;
}
.marquee-inner{
display:inline-block;
padding-left:2%;
animation:newsScroll 30s linear infinite;
color:#e8f4f0;font-weight:500;
}
@keyframes newsScroll{
0%{transform:translateX(-100%);}
100%{transform:translateX(100%);}
}
.top-marquee:hover .marquee-inner{animation-play-state:paused;}

/* شريط التحكم العلوي - متجاوب تماماً */
.control-bar{
position:fixed;top:45px;left:0;right:0;width:100%;z-index:250;
background:linear-gradient(135deg, #ffffff 0%, #f5fcf9 100%);
padding:10px 10px;display:flex;flex-wrap:wrap;justify-content:space-between;align-items:center;
box-shadow:0 4px 15px rgba(4, 74, 53, 0.12);border-bottom:2px solid #d0e6de;
backdrop-filter:blur(5px);
gap:8px;
}

.execution-text{
color:#044a35;font-size:13px;font-weight:800;
padding:6px 12px;background:linear-gradient(135deg, #e8f4f0 0%, #d4ebe2 100%);
border-radius:8px;border-right:4px solid #ffd166;
display:flex;align-items:center;gap:8px;
box-shadow:0 3px 8px rgba(6, 109, 77, 0.15);
position:relative;overflow:hidden;
flex-shrink:0;
}
.execution-text::before{
content:'';position:absolute;top:0;right:0;width:100%;height:100%;
background:linear-gradient(90deg, transparent, rgba(255,255,255,0.3), transparent);
transform:translateX(-100%);animation:shine 3s infinite;
}
@keyframes shine{100%{transform:translateX(100%);}}
.execution-text i{color:#066d4d;font-size:14px;}

.btn-group{
display:flex;flex-wrap:wrap;gap:8px;justify-content:center;align-items:center;
}

button.main-btn{
background:linear-gradient(135deg, #066d4d 0%, #05553d 100%);color:#fff;border:none;
padding:10px 12px;font-size:12px;border-radius:10px;cursor:pointer;min-width:auto;
transition:all 0.3s ease;font-weight:600;position:relative;overflow:hidden;
box-shadow:0 4px 10px rgba(6, 109, 77, 0.25);display:flex;flex-direction:column;align-items:center;gap:4px;
border:1px solid rgba(255,255,255,0.1);flex:1 1 auto;max-width:130px;
}
button.main-btn::after{
content:'';position:absolute;top:0;left:0;width:100%;height:100%;
background:linear-gradient(90deg, transparent, rgba(255,255,255,0.1), transparent);
transform:translateX(-100%);
}
button.main-btn:hover::after{animation:buttonShine 0.6s;}
@keyframes buttonShine{100%{transform:translateX(100%);}}
button.main-btn:hover{
background:linear-gradient(135deg, #05553d 0%, #044a35 100%);transform:translateY(-3px);
box-shadow:0 6px 15px rgba(6, 109, 77, 0.35);
}
button.main-btn:active{transform:translateY(-1px);}

.btn-icon{font-size:16px;}
.btn-text{font-size:11px;font-weight:700;}

/* زر حفظ بيانات المعلم خاص */
#saveTeacherBtn{background:linear-gradient(135deg, #2a7b5e 0%, #1e6b4f 100%);}
#saveTeacherBtn:hover{background:linear-gradient(135deg, #1e6b4f 0%, #15563f 100%);}

/* زر الدعم الفني */
#supportBtn{background:linear-gradient(135deg, #5a67d8 0%, #4c51bf 100%);}
#supportBtn:hover{background:linear-gradient(135deg, #4c51bf 0%, #434190 100%);}

/* تحسين واجهة الإدخال */
.input-section{
background:#ffffff;padding:20px;border-radius:18px;margin-top:160px;
border:2px solid #e0f0ea;box-shadow:0 8px 25px rgba(4, 74, 53, 0.1);
position:relative;overflow:hidden;
}
.input-section::before{
content:'';position:absolute;top:0;right:0;width:100%;height:4px;
background:linear-gradient(to left, #066d4d, #ffd166);
}

.input-section h2{
color:#044a35;font-size:20px;margin-bottom:25px;padding-bottom:15px;
border-bottom:3px solid #e0f0ea;text-align:center;font-weight:800;
position:relative;
}
.input-section h2::after{
content:'';position:absolute;bottom:-3px;right:0;width:100px;height:3px;
background:linear-gradient(to left, #066d4d, #ffd166);border-radius:2px;
}

.form-group{margin-bottom:20px;}
.form-group label{
font-size:14px;font-weight:700;margin-bottom:8px;display:block;color:#083024;
display:flex;align-items:center;gap:10px;padding-right:8px;
position:relative;
}
.form-group label i{
color:#066d4d;font-size:15px;background:#f0f9f6;padding:6px;border-radius:8px;
border:1px solid #d4ebe2;
}

.form-group label::before{
content:'';width:8px;height:8px;background:#ffd166;border-radius:50%;
display:inline-block;margin-left:6px;box-shadow:0 0 6px #ffd166;
}

input,select,textarea{
width:100%;padding:12px;margin-top:6px;border:2px solid #d4ebe2;border-radius:10px;
font-size:14px;background:#f9fcfb;transition:all 0.3s;font-family:'Cairo', sans-serif;
color:#083024;box-shadow:inset 0 2px 5px rgba(0,0,0,0.05);-webkit-appearance:none;
}
input:focus,select:focus,textarea:focus{
outline:none;border-color:#066d4d;box-shadow:0 0 0 3px rgba(6,109,77,0.15), inset 0 2px 5px rgba(0,0,0,0.05);
background:#ffffff;transform:translateY(-2px);
}
textarea{height:100px;resize:none;overflow:hidden;line-height:1.6;}

.auto-buttons{display:flex;gap:10px;margin-top:10px;}
.auto-btn{
flex:1;padding:10px;background:linear-gradient(135deg, #f0f9f6 0%, #e0f0ea 100%);
border:2px solid #b8d9cd;color:#066d4d;border-radius:10px;font-size:13px;cursor:pointer;
font-weight:700;transition:all 0.3s;display:flex;align-items:center;justify-content:center;gap:8px;
position:relative;overflow:hidden;
}
.auto-btn:hover{
background:linear-gradient(135deg, #e0f0ea 0%, #d0e6de 100%);border-color:#066d4d;
transform:translateY(-2px);box-shadow:0 4px 10px rgba(6, 109, 77, 0.2);
}
.auto-btn:active{transform:translateY(0);}
.auto-btn i{font-size:13px;}

.form-row{
display:grid;grid-template-columns:1fr 1fr;gap:15px;
}

/* تلميحات للأزرار */
button[title] {
position: relative;
}
button[title]:hover::after {
content: attr(title);
position: absolute;
bottom: calc(100% + 10px);
right: 50%;
transform: translateX(50%);
background: rgba(4, 58, 42, 0.95);
color: white;
padding: 8px 12px;
border-radius: 8px;
font-size: 11px;
white-space: nowrap;
z-index: 1000;
border: 1px solid #044a35;
box-shadow: 0 4px 12px rgba(0,0,0,0.15);
max-width:200px;
}
button[title]:hover::before {
content: '';
position: absolute;
bottom: calc(100% + 2px);
right: 50%;
transform: translateX(50%);
border: 6px solid transparent;
border-top-color: rgba(4, 58, 42, 0.95);
z-index: 1000;
}

/* تصميم خاص لأزرار PDF وواتساب */
#pdfBtn{background:linear-gradient(135deg, #d9534f 0%, #c9302c 100%);}
#pdfBtn:hover{background:linear-gradient(135deg, #c9302c 0%, #ac2925 100%);}

#whatsappBtn{background:linear-gradient(135deg, #25D366 0%, #128C7E 100%);}
#whatsappBtn:hover{background:linear-gradient(135deg, #128C7E 0%, #075E54 100%);}

#clearBtn{background:linear-gradient(135deg, #f0ad4e 0%, #ec971f 100%);}
#clearBtn:hover{background:linear-gradient(135deg, #ec971f 0%, #d58512 100%);}

/* إشعارات */
.notification {
position: fixed;
top: 110px;
right: 10px;
left: 10px;
background: linear-gradient(135deg, #066d4d 0%, #044a35 100%);
color: white;
padding: 12px 18px;
border-radius: 10px;
box-shadow: 0 6px 20px rgba(4, 74, 53, 0.3);
z-index: 1000;
display: flex;
align-items: center;
gap: 10px;
font-weight: 600;
transform: translateX(150%);
transition: transform 0.4s cubic-bezier(0.68, -0.55, 0.27, 1.55);
border-right: 5px solid #ffd166;
text-align:center;
justify-content:center;
}
.notification.show {
transform: translateX(0);
}
.notification i {
font-size: 18px;
}

/* نافذة الدعم الفني */
.support-modal {
display: none;
position: fixed;
top: 0;
left: 0;
right: 0;
bottom: 0;
background-color: rgba(0, 0, 0, 0.7);
z-index: 1001;
justify-content: center;
align-items: center;
padding: 15px;
}

.support-content {
background: white;
border-radius: 15px;
padding: 25px;
width: 100%;
max-width: 500px;
box-shadow: 0 15px 35px rgba(0, 0, 0, 0.2);
position: relative;
max-height: 90vh;
overflow-y: auto;
}

.support-header {
display: flex;
justify-content: space-between;
align-items: center;
margin-bottom: 20px;
padding-bottom: 15px;
border-bottom: 2px solid #e0f0ea;
}

.support-header h3 {
color: #044a35;
font-size: 20px;
font-weight: 800;
}

.close-support {
background: none;
border: none;
font-size: 24px;
color: #066d4d;
cursor: pointer;
width: 30px;
height: 30px;
display: flex;
align-items: center;
justify-content: center;
border-radius: 50%;
transition: all 0.3s;
}

.close-support:hover {
background-color: #e8f4f0;
}

.support-form .form-group {
margin-bottom: 20px;
}

.support-actions {
display: flex;
gap: 15px;
margin-top: 25px;
}

.support-action-btn {
flex: 1;
padding: 14px;
border-radius: 10px;
border: none;
color: white;
font-weight: 700;
font-size: 14px;
cursor: pointer;
display: flex;
align-items: center;
justify-content: center;
gap: 10px;
transition: all 0.3s;
box-shadow: 0 4px 10px rgba(0,0,0,0.15);
}

.email-btn {
background: linear-gradient(135deg, #d44646 0%, #b52a2a 100%);
}

.email-btn:hover {
background: linear-gradient(135deg, #b52a2a 0%, #9c1f1f 100%);
transform: translateY(-3px);
}

.whatsapp-support-btn {
background: linear-gradient(135deg, #25D366 0%, #128C7E 100%);
}

.whatsapp-support-btn:hover {
background: linear-gradient(135deg, #128C7E 0%, #075E54 100%);
transform: translateY(-3px);
}

.support-info {
background: #f8fdfa;
border-radius: 10px;
padding: 15px;
margin-top: 20px;
border-right: 4px solid #ffd166;
}

.support-info p {
margin-bottom: 8px;
font-size: 14px;
color: #044a35;
}

.support-info i {
color: #066d4d;
margin-left: 8px;
}

/* تحسينات للأجهزة المحمولة */
@media (max-width: 768px) {
.control-bar {
top: 45px;
padding: 8px;
flex-direction: column;
gap: 10px;
height: auto;
}

.execution-text {
font-size: 12px;
padding: 5px 10px;
width: 100%;
justify-content: center;
}

.btn-group {
width: 100%;
justify-content: space-between;
gap: 6px;
}

button.main-btn {
padding: 8px 10px;
font-size: 11px;
min-width: 0;
max-width: 100%;
flex: 1 1 calc(50% - 6px);
}

.btn-icon {
font-size: 14px;
}

.btn-text {
font-size: 10px;
}

.input-section {
margin-top: 130px;
padding: 15px;
border-radius: 15px;
}

.input-section h2 {
font-size: 18px;
margin-bottom: 20px;
}

.form-row {
grid-template-columns: 1fr;
gap: 15px;
}

.notification {
top: 100px;
padding: 10px 15px;
font-size: 14px;
}

.support-content {
padding: 20px;
max-height: 85vh;
}

.support-actions {
flex-direction: column;
}

.support-action-btn {
width: 100%;
}
}

@media (max-width: 480px) {
.top-marquee {
font-size: 11px;
padding: 8px 5px;
height: 40px;
}

.marquee-inner {
animation-duration: 35s;
}

button.main-btn {
padding: 7px 8px;
font-size: 10px;
flex: 1 1 calc(50% - 4px);
}

.btn-icon {
font-size: 12px;
}

.btn-text {
font-size: 9px;
}

.input-section {
margin-top: 120px;
padding: 12px;
}

input, select, textarea {
padding: 10px;
font-size: 13px;
}

.form-group label {
font-size: 13px;
}

.form-group label i {
font-size: 13px;
padding: 5px;
}

.auto-btn {
padding: 8px;
font-size: 12px;
}

.support-header h3 {
font-size: 18px;
}

.support-action-btn {
padding: 12px;
font-size: 13px;
}
}

@media (max-width: 320px) {
button.main-btn {
flex: 1 1 100%;
margin-bottom: 4px;
}

.btn-group {
gap: 4px;
}

.input-section {
margin-top: 110px;
}
}

/* iPhone X/XS/11 Pro/12 mini/13 mini - ارتفاع الشاشة */
@media only screen and (device-width: 375px) and (device-height: 812px) and (-webkit-device-pixel-ratio: 3) {
.top-marquee {
padding-top: env(safe-area-inset-top);
height: calc(45px + env(safe-area-inset-top));
}

.control-bar {
top: calc(45px + env(safe-area-inset-top));
}
}

/* iPhone 12/13/14 - ارتفاع الشاشة */
@media only screen and (device-width: 390px) and (device-height: 844px) and (-webkit-device-pixel-ratio: 3) {
.top-marquee {
padding-top: env(safe-area-inset-top);
height: calc(45px + env(safe-area-inset-top));
}

.control-bar {
top: calc(45px + env(safe-area-inset-top));
}
}

/* iPhone 12/13/14 Pro Max - شاشات كبيرة */
@media only screen and (device-width: 428px) and (device-height: 926px) and (-webkit-device-pixel-ratio: 3) {
.top-marquee {
padding-top: env(safe-area-inset-top);
height: calc(45px + env(safe-area-inset-top));
}

.control-bar {
top: calc(45px + env(safe-area-inset-top));
}
}

/* قسم PDF - تم التعديل لضمان ظهوره بشكل صحيح */
#report-content{
width:100%;margin:20px auto;background:#ffffff !important;
-webkit-print-color-adjust: exact !important;
print-color-adjust: exact !important;
}

.header{
background:#083024 !important;padding:8px;min-height:140px;position:relative;color:#fff !important;text-align:center;overflow:hidden;
display:flex;align-items:center;justify-content:center;
-webkit-print-color-adjust: exact !important;
print-color-adjust: exact !important;
}
.header img{width:155px;}

.header-school-title{
position:absolute;bottom:36px;right:8px;font-size:12px;font-weight:600;
color:#ffffff !important;
}
.header-school{
position:absolute;bottom:20px;right:8px;font-size:12px;font-weight:700;
color:#ffffff !important;
}
.header-education{
position:absolute;bottom:8px;left:50%;transform:translateX(-50%);font-size:11px;font-weight:700;
color:#d7f2ea !important;
}
.header-date-box{
position:absolute;top:6px;left:10px;font-size:11px;text-align:right;line-height:1.3;
color:#ffffff !important;
}

.info-grid{
display:grid;grid-template-columns:repeat(4,1fr);
gap:4px;margin-top:10px;
}
.info-grid2{
display:grid;grid-template-columns:repeat(3,1fr);
gap:4px;margin-bottom:8px;margin-top:10px;
}

.info-box{
background:#e8f2ee !important;border-radius:6px;height:34px;
display:flex;flex-direction:column;justify-content:center;align-items:center;
border:1px solid rgba(6,109,77,0.3) !important;
-webkit-print-color-adjust: exact !important;
print-color-adjust: exact !important;
}
.info-title{
font-size:9px;font-weight:700;color:#083024 !important;
-webkit-print-color-adjust: exact !important;
print-color-adjust: exact !important;
}
.info-value{
font-size:10px;font-weight:700;color:#000000 !important;
-webkit-print-color-adjust: exact !important;
print-color-adjust: exact !important;
}

.objective-box{
background:#f3f9f6 !important;border:1px solid rgba(6,109,77,0.35) !important;
padding:6px 10px;border-radius:8px;margin-bottom:10px;
min-height:120px;max-height:120px;overflow:hidden;
-webkit-print-color-adjust: exact !important;
print-color-adjust: exact !important;
}
.objective-title{
text-align:center;font-size:14px;font-weight:700;
color:#083024 !important;
}
.objective-content{
font-size:13px;line-height:1.6;
color:#000000 !important;
}

.report-row{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin:12px 0;}
.report-box{
background:#ffffff !important;border-radius:8px;padding:6px;
border:1px solid rgba(6,109,77,0.35) !important;min-height:130px;max-height:130px;overflow:hidden;
-webkit-print-color-adjust: exact !important;
print-color-adjust: exact !important;
}
.report-box-title{
text-align:center;font-size:13px;font-weight:700;
color:#083024 !important;
}
.report-box-content{
font-size:13px;line-height:1.6;
color:#000000 !important;
}

.image-evidence-grid{display:grid;grid-template-columns:1fr 1fr;gap:8px;}
.image-box{
min-height:140px;max-height:140px;border:1px dashed #066d4d !important;border-radius:8px;
display:flex;align-items:center;justify-content:center;background:#ffffff !important;
font-size:12px;color:#666 !important;overflow:hidden;
-webkit-print-color-adjust: exact !important;
print-color-adjust: exact !important;
}
.image-box img{max-width:100%;max-height:100%;object-fit:contain;}

.signature-section{margin-top:20px;display:grid;grid-template-columns:1fr 1fr;gap:20px;}
.signature-box{
text-align:center;font-size:12px;
color:#083024 !important;font-weight:700;
}
.signature-line{
margin-top:6px;border-top:1px solid #083024 !important;width:80%;margin:auto;
}
.footer{
text-align:center;font-size:10px;padding:6px;margin-top:20px;
background:#083024 !important;color:#fff !important;
-webkit-print-color-adjust: exact !important;
print-color-adjust: exact !important;
}

/* لضمان ظهور الألوان في PDF */
.pdf-export * {
    -webkit-print-color-adjust: exact !important;
    print-color-adjust: exact !important;
    color-adjust: exact !important;
}

/* منع التكبير التلقائي على iOS */
input, select, textarea {
font-size: 16px !important;
}
@media screen and (-webkit-min-device-pixel-ratio:0) {
  select,
  textarea,
  input {
    font-size: 16px !important;
  }
}
</style>
</head>

<body>

<div class="top-marquee">
<div class="marquee-inner">
<i class="fas fa-bullhorn" style="margin-left:10px;"></i>
اختر نوع التقرير المطلوب، ثم اضغط زر التعبئة لكل بند ليظهر النص الجاهز، وواصل الضغط لتبديل الصياغة حتى تجد الأنسب. عدّل النصوص عند الحاجة، وأدخل أي تقرير جديد يدوياً إذا لم يكن ضمن القائمة
</div>
</div>

<div class="control-bar">
<div class="execution-text">
<i class="fas fa-user-tie"></i>
تنفيذ : المعلم فهد الخالدي
</div>
<div class="btn-group">
<button class="main-btn" id="saveTeacherBtn" onclick="saveTeacherData()" title="حفظ بيانات إدارة التعليم، اسم المدرسة، الصف، المادة، المستهدفون، المكان">
<i class="fas fa-chalkboard-teacher btn-icon"></i>
<span class="btn-text">حفظ بيانات المعلم</span>
</button>
<button class="main-btn" id="supportBtn" onclick="openSupportModal()" title="الدعم الفني والتواصل مع المطور">
<i class="fas fa-headset btn-icon"></i>
<span class="btn-text">الدعم الفني</span>
</button>
<button class="main-btn" id="clearBtn" onclick="clearData()" title="مسح جميع البيانات المدخلة">
<i class="fas fa-trash-alt btn-icon"></i>
<span class="btn-text">مسح</span>
</button>
<button class="main-btn" id="pdfBtn" onclick="downloadPDF()" title="تحويل التقرير إلى PDF وتنزيله">
<i class="fas fa-file-pdf btn-icon"></i>
<span class="btn-text">تنزيل PDF</span>
</button>
<button class="main-btn" id="whatsappBtn" onclick="sharePDFWhatsApp()" title="مشاركة التقرير عبر واتساب">
<i class="fab fa-whatsapp btn-icon"></i>
<span class="btn-text">مشاركة واتساب</span>
</button>
</div>
</div>

<!-- إشعارات -->
<div class="notification" id="saveNotification">
<i class="fas fa-check-circle"></i>
<span>تم حفظ بيانات المعلم بنجاح!</span>
</div>

<!-- نافذة الدعم الفني -->
<div class="support-modal" id="supportModal">
<div class="support-content">
<div class="support-header">
<h3><i class="fas fa-headset" style="margin-left:10px;"></i>الدعم الفني</h3>
<button class="close-support" onclick="closeSupportModal()">×</button>
</div>

<div class="support-form">
<div class="form-group">
<label for="supportName"><i class="fas fa-user"></i>الاسم الكامل</label>
<input type="text" id="supportName" placeholder="أدخل اسمك الكامل">
</div>

<div class="form-group">
<label for="supportPhone"><i class="fas fa-phone"></i>رقم التواصل</label>
<input type="tel" id="supportPhone" placeholder="أدخل رقم الجوال أو الهاتف">
</div>

<div class="form-group">
<label for="supportIssue"><i class="fas fa-exclamation-circle"></i>تفاصيل المشكلة</label>
<textarea id="supportIssue" rows="4" placeholder="صف مشكلتك بالتفصيل..."></textarea>
</div>

<div class="support-info">
<p><i class="fas fa-envelope"></i>البريد الإلكتروني: iFahadenglish@gmail.com</p>
<p><i class="fab fa-whatsapp"></i>واتساب: +966597077245</p>
</div>

<div class="support-actions">
<button class="support-action-btn email-btn" onclick="sendEmailSupport()">
<i class="fas fa-envelope"></i>مراسلة عبر البريد
</button>
<button class="support-action-btn whatsapp-support-btn" onclick="sendWhatsAppSupport()">
<i class="fab fa-whatsapp"></i>مراسلة عبر واتساب
</button>
</div>
</div>
</div>
</div>

<div class="wrapper">
<div class="input-section">
  
  <h2><i class="fas fa-tools" style="margin-left:10px;"></i>أداة إصدار التقارير التربوية</h2>
  
  <div class="form-group">
    <label><i class="fas fa-university"></i>إدارة التعليم</label>
    <select id="education" oninput="updateReport()">
      <option>الإدارة العامة للتعليم بمنطقة مكة المكرمة</option>
      <option>الإدارة العامة للتعليم بمنطقة الرياض</option>
      <option>الإدارة العامة للتعليم بمنطقة المدينة المنورة</option>
      <option>الإدارة العامة للتعليم بالمنطقة الشرقية</option>
      <option>الإدارة العامة للتعليم بمنطقة القصيم</option>
      <option>الإدارة العامة للتعليم بمنطقة عسير</option>
      <option>الإدارة العامة للتعليم بمنطقة تبوك</option>
      <option>الإدارة العامة للتعليم بمنطقة حائل</option>
      <option>الإدارة العامة للتعليم بمنطقة الحدود الشمالية</option>
      <option>الإدارة العامة للتعليم بمنطقة جازان</option>
      <option>الإدارة العامة للتعليم بمنطقة نجران</option>
      <option>الإدارة العامة للتعليم بمنطقة الباحة</option>
      <option>الإدارة العامة للتعليم بمنطقة الجوف</option>
      <option>الإدارة العامة للتعليم بمحافظة الأحساء</option>
      <option>الإدارة العامة للتعليم بمحافظة الطائف</option>
      <option>الإدارة العامة للتعليم بمحافظة جدة</option>
    </select>
  </div>
  
  <div class="form-group">
    <label><i class="fas fa-school"></i>اسم المدرسة</label>
    <input id="school" value="سعيد بن العاص" placeholder="أدخل اسم المدرسة" oninput="updateReport()">
  </div>
  
  <div class="form-group">
    <label><i class="fas fa-file-alt"></i>اسم التقرير</label>
    <select id="reportType" oninput="handleReportType()">
      <option>تقرير نشاط إثرائي</option>
      <option>تقرير خطة علاجية</option>
      <option>تقرير تكريم المتميزين</option>
      <option>تقرير أنشطة صفية</option>
      <option>تقرير خطة أسبوعية</option>
      <option>تقرير توزيع المنهج</option>
      <option>تقرير حصة النشاط</option>
      <option>تقرير تنفيذ إذاعة مدرسية</option>
      <option>تقرير تبادل الزيارات</option>
      <option>تقرير مجتمعات التعلم</option>
      <option>تقرير تنفيذ درس تطبيقي</option>
      <option>تقرير حضور دورات وورش تدريبية</option>
      <option>تقرير التواصل مع ولي الأمر</option>
      <option>تقرير إشعار ولي الأمر عن مستوى ابنه</option>
      <option>تقرير حضور اجتماع أولياء الأمور</option>
      <option>تقرير تفعيل الخطة الأسبوعية</option>
      <option>تقرير درس تم تنفيذه</option>
      <option>تقرير تعليم تعاوني بين الطلاب</option>
      <option>تقرير تصنيف الطلاب</option>
      <option>تقرير تحفيز الطلاب</option>
      <option>تقرير كشف المتابعة</option>
      <option>تقرير توزيع وقت الحصة</option>
      <option>تقرير تنفيذ اختبار تحسن</option>
      <option>تقرير المشاركات بين الطلاب</option>
      <option>تقرير سجل الخطط العلاجية</option>
      <option>تقرير سجل رعاية الموهوبين</option>
      <option>تقرير تفعيل المنصات التعليمية</option>
      <option>تقرير المجتمعات المهنية</option>
      <option>تقرير الورش التدريبية التي قدمتها</option>
      <option>تقرير الإشراف اليومي</option>
      <option>تقرير الاحتفال باليوم الوطني</option>
      <option>تقرير المبادرات والابتكار</option>
      <option>تقرير حل مشكلة تربوية</option>
      <option>تقرير توظيف الذكاء الاصطناعي</option>
      <option>تقرير الفصول المقلوبة</option>
      <option>تقرير تطوير البيئة الصفية</option>
      <option>تقرير الوسائل التعليمية المبتكرة</option>
      <option>تقرير المناوبة والفسحة</option>
      <option>تقرير سجل التواصل مع أولياء الأمور</option>
      <option>تقرير جرد المختبرات وغرف المصادر</option>
      <option>تقرير إدارة الأزمات</option>
      <option>تقرير نقل أثر التدريب</option>
      <option>تقرير المعلم الصغير</option>
      <option>تقرير إدارة الاجتماعات</option>
      <option>تقرير الاختبارات الذكية</option>
      <option>تقرير المحتوى الرقمي المنتج</option>
      <option>تقرير تعزيز السلوك الإيجابي</option>
      <option>تقرير سجل الدرجات الإلكتروني</option>
      <option>تقرير مقارنة السلاسل الزمنية</option>
      <option>تقرير سجل التغذية الراجعة من الطلاب</option>
      <option>تقرير البحث الإجرائي</option>
      <option>تقرير معرفة الميول والاتجاهات</option>
      <option>تقرير عضوية لجنة التميز والجودة</option>
      <option>تقرير عضوية لجنة التدقيق</option>
      <option>تقرير رعاية الطلاب المتأخرين دراسيًا</option>
      <option>تقرير دراسة حالة</option>
      <option>تقرير تحليل النتائج</option>
      <option>تقرير تفعيل حصص النشاط</option>
      <option>تقرير التدريب على الاختبارات المعيارية</option>
      <option>تقرير مبادرة تطوعية</option>
      <option>تقرير التحليل الاحتياجات التدريبية</option>
      <option>تقرير تصميم الوحدات التعليمية</option>
      <option>تقرير إعداد المواد التعليمية</option>
      <option>تقرير تخطيط المشاريع التعليمية</option>
      <option>تقرير تطوير المناهج الإثرائية</option>
      <option>تقرير إعداد بنك الأسئلة</option>
      <option>تقرير تصميم الأنشطة اللاصفية</option>
      <option>تقرير تخطيط الرحلات التعليمية</option>
      <option>تقرير تحليل نتائج الاختبارات التشخيصية</option>
      <option>تقرير مؤشرات الأداء التعليمي</option>
      <option>تقرير تقييم المخرجات التعليمية</option>
      <option>تقرير قياس الأثر التعليمي</option>
      <option>تقرير تحليل الاختبارات التحصيلية</option>
      <option>تقرير تقييم المشاريع الطلابية</option>
      <option>تقرير تقييم الأداء العملي</option>
      <option>تقرير تقييم المحافظ الإلكترونية</option>
      <option>تقرير المشاركة في المؤتمرات التعليمية</option>
      <option>تقرير حضور الندوات العلمية</option>
      <option>تقرير متابعة الدورات العالمية</option>
      <option>تقرير المشاركة في البحث التربوي</option>
      <option>تقرير التدريب على المناهج الحديثة</option>
      <option>تقرير التطوير المهني المستمر</option>
      <option>تقرير الشراكات المهنية</option>
      <option>تقرير تفعيل الفصول الافتراضية</option>
      <option>تقرير إنتاج المحتوى الرقمي</option>
      <option>تقرير استخدام أنظمة إدارة التعلم</option>
      <option>تقرير التقييم الإلكتروني</option>
      <option>تقرير التعليم المدمج</option>
      <option>تقرير الواقع المعزز في التعليم</option>
      <option>تقرير التعليم عن بعد</option>
      <option>تقرير الألعاب التعليمية الرقمية</option>
      <option>تقرير إدارة الوقت في الصف</option>
      <option>تقرير تنظيم البيئة الصفية</option>
      <option>تقرير إجراءات السلامة في الصف</option>
      <option>تقرير إدارة الموارد التعليمية</option>
      <option>تقرير نظام الحوافز والمكافآت</option>
      <option>تقرير إدارة السلوك الصفي</option>
      <option>تقرير التنويع في التقييم</option>
      <option>تقرير تطبيق التعلم القائم على المشاريع</option>
      <option>تقرير التعلم القائم على حل المشكلات</option>
      <option>تقرير التعلم التعاوني</option>
      <option>تقرير التعلم الذاتي الموجه</option>
      <option>تقرير العروض العملية</option>
      <option>تقرير الزيارات الميدانية</option>
      <option>تقرير الأنشطة التفاعلية</option>
      <option>تقرير برنامج الدعم النفسي</option>
      <option>تقرير الرعاية الصحية في المدرسة</option>
      <option>تقرير دعم الطلاب ذوي الإعاقة</option>
      <option>أخرى</option>
    </select>
    <input id="reportTypeInput" placeholder="أدخل اسم التقرير" oninput="updateReport()" style="display:none;margin-top:8px;">
  </div>
  
  <div class="form-row">
    <div class="form-group">
      <label><i class="fas fa-chalkboard-teacher"></i>صفة المعلّم</label>
      <select id="teacherType" oninput="updateReport()">
        <option selected>المعلم</option>
        <option>المعلمة</option>
      </select>
    </div>
    
    <div class="form-group">
      <label><i class="fas fa-user"></i>اسم المعلّم</label>
      <input id="teacher" value="فهد الخالدي" placeholder="اسم المعلم" oninput="updateReport()">
    </div>
  </div>
  
  <div class="form-row">
    <div class="form-group">
      <label><i class="fas fa-user-tie"></i>صفة المدير</label>
      <select id="principalType" oninput="updateReport()">
        <option selected>المدير</option>
        <option>المديرة</option>
      </select>
    </div>
    
    <div class="form-group">
      <label><i class="fas fa-user-cog"></i>اسم المدير</label>
      <input id="principal" value="نايف اللحياني" placeholder="اسم مدير المدرسة" oninput="updateReport()">
    </div>
  </div>
  
  <div class="form-row">
    <div class="form-group">
      <label><i class="fas fa-users-class"></i>الصف</label>
      <input id="grade" placeholder="مثال: ٥/٣" oninput="updateReport()">
    </div>
    
    <div class="form-group">
      <label><i class="fas fa-calendar-alt"></i>الفصل الدراسي</label>
      <select id="term" oninput="updateReport()">
        <option></option><option>الأول</option><option>الثاني</option>
      </select>
    </div>
  </div>
  
  <div class="form-group">
    <label><i class="fas fa-book"></i>المادة</label>
    <input id="subject" placeholder="مثال: لغتي – علوم – رياضيات" oninput="updateReport()">
  </div>
  
  <div class="form-row">
    <div class="form-group">
      <label><i class="fas fa-bullseye"></i>المستهدفون</label>
      <input id="target" placeholder="مثال: جميع طلاب الصف" oninput="updateReport()">
    </div>
    
    <div class="form-group">
      <label><i class="fas fa-user-check"></i>عدد الحضور</label>
      <input id="count" placeholder="مثال: ٢٥ طالب" oninput="updateReport()">
    </div>
  </div>
  
  <div class="form-group">
    <label><i class="fas fa-map-marker-alt"></i>مكان التنفيذ</label>
    <input id="place" placeholder="مثال: داخل الصف – المختبر" oninput="updateReport()">
  </div>
  
  <div class="form-group">
    <label><i class="fas fa-flag"></i>الهدف التربوي</label>
    <textarea id="goal" placeholder="أدخل الهدف التربوي" oninput="updateReport()"></textarea>
    <div class="auto-buttons"><button class="auto-btn" onclick="autoFill('goal')"><i class="fas fa-magic"></i>تعبئة ذكية</button></div>
  </div>
  
  <div class="form-group">
    <label><i class="fas fa-file-signature"></i>نبذة مختصرة</label>
    <textarea id="summary" placeholder="أدخل نبذة مختصرة" oninput="updateReport()"></textarea>
    <div class="auto-buttons"><button class="auto-btn" onclick="autoFill('summary')"><i class="fas fa-magic"></i>تعبئة ذكية</button></div>
  </div>
  
  <div class="form-group">
    <label><i class="fas fa-tasks"></i>إجراءات التنفيذ</label>
    <textarea id="steps" placeholder="كيف تم تنفيذ النشاط؟" oninput="updateReport()"></textarea>
    <div class="auto-buttons"><button class="auto-btn" onclick="autoFill('steps')"><i class="fas fa-magic"></i>تعبئة ذكية</button></div>
  </div>
  
  <div class="form-group">
    <label><i class="fas fa-chess-board"></i>الاستراتيجيات</label>
    <textarea id="strategies" placeholder="ما هي الاستراتيجيات" oninput="updateReport()"></textarea>
    <div class="auto-buttons"><button class="auto-btn" onclick="autoFill('strategies')"><i class="fas fa-magic"></i>تعبئة ذكية</button></div>
  </div>
  
  <div class="form-row">
    <div class="form-group">
      <label><i class="fas fa-thumbs-up"></i>نقاط القوة</label>
      <textarea id="strengths" placeholder="نقاط القوة" oninput="updateReport()"></textarea>
      <div class="auto-buttons"><button class="auto-btn" onclick="autoFill('strengths')"><i class="fas fa-magic"></i>تعبئة ذكية</button></div>
    </div>
    
    <div class="form-group">
      <label><i class="fas fa-tools"></i>نقاط التحسين</label>
      <textarea id="improve" placeholder="نقاط تحتاج تطوير" oninput="updateReport()"></textarea>
      <div class="auto-buttons"><button class="auto-btn" onclick="autoFill('improve')"><i class="fas fa-magic"></i>تعبئة ذكية</button></div>
    </div>
  </div>
  
  <div class="form-group">
    <label><i class="fas fa-lightbulb"></i>التوصيات</label>
    <textarea id="recomm" placeholder="توصيات مستقبلية" oninput="updateReport()"></textarea>
    <div class="auto-buttons"><button class="auto-btn" onclick="autoFill('recomm')"><i class="fas fa-magic"></i>تعبئة ذكية</button></div>
  </div>
  
  <div class="form-row">
    <div class="form-group">
      <label><i class="fas fa-camera"></i>الصورة 1</label>
      <input type="file" accept="image/*" placeholder="ارفع صورة" onchange="loadImage(this,'imgBox1')">
    </div>
    
    <div class="form-group">
      <label><i class="fas fa-camera"></i>الصورة 2</label>
      <input type="file" accept="image/*" placeholder="ارفع صورة" onchange="loadImage(this,'imgBox2')">
    </div>
  </div>

</div>
</div>

<!-- قسم PDF المعدل -->
<div id="report-content" class="wrapper pdf-export" style="display:none;">

<div class="header">
<img src="https://i.ibb.co/1fc5gB6v/9-C92-E57-B-23-FA-479-D-A024-1-D5-F871-B4-F8-D.png">
<div class="header-school-title">اسم المدرسة</div>
<div class="header-school" id="schoolBox"></div>
<div class="header-education" id="educationBox"></div>
<div class="header-date-box">
<span id="hDate"></span><br>
<span id="gDate"></span>
</div>
</div>

<div class="info-grid">
<div class="info-box"><div class="info-title">الفصل</div><div class="info-value" id="termBox"></div></div>
<div class="info-box"><div class="info-title">الصف</div><div class="info-value" id="gradeBox"></div></div>
<div class="info-box"><div class="info-title">المادة</div><div class="info-value" id="subjectBox"></div></div>
<div class="info-box"><div class="info-title">التقرير</div><div class="info-value" id="reportTypeBox"></div></div>
</div>

<div class="info-grid2">
<div class="info-box"><div class="info-title">المستهدفون</div><div class="info-value" id="targetBox"></div></div>
<div class="info-box"><div class="info-title">العدد</div><div class="info-value" id="countBox"></div></div>
<div class="info-box"><div class="info-title">المكان</div><div class="info-value" id="placeBox"></div></div>
</div>

<div class="objective-box"><div class="objective-title">الهدف التربوي</div><div class="objective-content" id="goalBox"></div></div>

<div class="report-row">
<div class="report-box"><div class="report-box-title">النبذة</div><div class="report-box-content" id="summaryBox"></div></div>
<div class="report-box"><div class="report-box-title">إجراءات التنفيذ</div><div class="report-box-content" id="stepsBox"></div></div>
</div>

<div class="report-row">
<div class="report-box"><div class="report-box-title">الاستراتيجيات</div><div class="report-box-content" id="strategiesBox"></div></div>
<div class="report-box"><div class="report-box-title">نقاط القوة</div><div class="report-box-content" id="strengthsBox"></div></div>
</div>

<div class="report-row">
<div class="report-box"><div class="report-box-title">نقاط التحسين</div><div class="report-box-content" id="improveBox"></div></div>
<div class="report-box"><div class="report-box-title">التوصيات</div><div class="report-box-content" id="recommBox"></div></div>
</div>

<div class="image-evidence-grid">
<div class="image-box" id="imgBox1">صورة توثيقية ١</div>
<div class="image-box" id="imgBox2">صورة توثيقية ٢</div>
</div>

<div class="signature-section">
<div class="signature-box"><div id="teacherTypeBox"></div><span id="teacherBox"></span><div class="signature-line"></div></div>
<div class="signature-box"><div id="principalTypeBox"></div><span id="principalBox"></span><div class="signature-line"></div></div>
</div>

<div class="footer">وزارة التعليم – المملكة العربية السعودية</div>
</div>

<script>
// كائن يحتوي على النصوص الذكية لكل نوع تقرير
const autoTextsByReportType = {
    'تقرير نشاط إثرائي': {
        goal: [
            "تنمية مهارات التفكير وتنشيط الإبداع وتحقيق مشاركة فعالة ودعم التعاون بين الطلاب وتنمية مهارات حل المشكلات وصقل شخصية الطالب.",
            "تحسين قدرات الطلاب في المتابعة الفاعلة أثناء الدروس وتطوير قدرتهم على التعبير وصياغة الأفكار وتعزيز روح العمل التعاوني داخل الصف.",
            "تعزيز مهارات التواصل وبناء الثقة بالقدرات الذاتية لدى الطلاب من خلال أنشطة تعليمية محفزة تمكّنهم من تطبيق ما تعلموه بصورة فعّالة.",
            "تنمية التفكير التحليلي والابتكار لدى الطلاب وتحقيق مستويات عالية من المشاركة عبر استراتيجيات فعّالة تحقق نواتج تعلم قوية.",
            "تطوير مهارات البحث والاستقصاء لدى الطلاب وتهيئتهم لاستخدام مصادر تعلم متنوعة بصورة إيجابية ومستقلّة."
        ],
        summary: [
            "تم تنفيذ النشاط داخل الصف بطريقة تفاعلية بمشاركة جميع الطلاب مما عزز من التعلم التعاوني وساهم في اكتساب مهارات جديدة.",
            "شارك الطلاب بفعالية كبيرة وظهر لديهم اهتمام واضح في تقديم أفكارهم وتطبيق الأنشطة المطلوبة خلال الدرس.",
            "كان النشاط محفزًا للطلاب وساعد في رفع مستوى الفهم لديهم وربط المحتوى التعليمي بالواقع العملي.",
            "أظهر الطلاب تفاعلًا ممتازًا مع خطوات النشاط مما ساعد على تحقيق الأهداف المخطط لها بصورة واضحة.",
            "ساهم النشاط في زيادة الدافعية لدى الطلاب وتعزيز روح المنافسة الإيجابية بينهم داخل الصف."
        ],
        steps: [
            "بدأت الحصة بشرح أهداف النشاط ثم تقسيم الطلاب إلى مجموعات والعمل على تنفيذ المهام مع تقديم الإرشادات اللازمة.",
            "توجيه الطلاب أثناء تنفيذ النشاط وتقديم التغذية الراجعة الفورية لضمان وضوح المهام وتعزيز التعلم الفاعل.",
            "استخدام أساليب متنوعة لإشراك الطلاب ومتابعة تقدمهم داخل المجموعات مع تشجيعهم على تبادل الأفكار.",
            "تقديم الدعم للطلاب أثناء النشاط مع الحرص على مشاركة الجميع في إنجاز المهمة المطلوبة.",
            "اختتام النشاط بنقاش مفتوح حول النتائج ومراجعة أهم ما تم التوصل إليه خلال الدرس."
        ],
        strategies: [
            "استراتيجية التعلم التعاوني لتنمية روح التعاون بين الطلاب وتعزيز العمل الجماعي.",
            "استراتيجية العصف الذهني لتحفيز الإبداع وتدريب الطلاب على تطوير حلول جديدة.",
            "استراتيجية التعلم النشط لجذب انتباه الطلاب وتفعيل مشاركتهم داخل الصف.",
            "المناقشة الصفية لزيادة التفاعل وتحسين مهارات التواصل بين الطلاب.",
            "استخدام الوسائط التعليمية المتنوعة لدعم التعلم وتحقيق فهم أعمق للدرس."
        ],
        strengths: [
            "تفاعل ممتاز من الطلاب أثناء تنفيذ النشاط وظهور مهارات التعاون بوضوح.",
            "مستوى جيد من التنظيم داخل الصف وإدارة فعّالة للوقت خلال النشاط.",
            "اهتمام واضح من الطلاب بتنفيذ التعليمات وتحقيق الهدف التعليمي.",
            "وجود رغبة قوية لدى الطلاب في المشاركة وتبادل الأفكار داخل المجموعات.",
            "تحسن واضح في الفهم لدى أغلب الطلاب وتطبيق فعّال للمحتوى."
        ],
        improve: [
            "زيادة وقت النشاط لضمان مشاركة أكبر لكل الطلاب وتحقيق أفضل النتائج.",
            "الحرص على دعم الطلاب المتعثرين ومنحهم فرصًا إضافية للمشاركة وتحسين مستوياتهم.",
            "التوسع في استخدام الأنشطة التطبيقية لرفع قدرة الطلاب على توظيف المعرفة.",
            "التدرج في تقديم المهام لتناسب مستويات الطلاب المختلفة بصورة أفضل.",
            "التركيز على تحفيز الطلاب الأقل تفاعلًا ودعمهم بالتوجيه المناسب."
        ],
        recomm: [
            "الاستمرار في تطبيق الأنشطة التفاعلية التي تعزز التعلم النشط داخل الصف.",
            "توظيف الوسائل التقنية بفاعلية أكبر لجذب انتباه الطلاب وتعزيز مشاركتهم.",
            "العمل على تطوير استراتيجيات جديدة ومتنوعة تلائم قدرات جميع الطلاب.",
            "تحفيز الطلاب على البحث والاستكشاف في محتوى الدروس المستقبلية.",
            "التركيز على تعزيز الثقة لدى الطلاب وتشجيع المبادرات التعليمية."
        ]
    },
    'تقرير خطة علاجية': {
        goal: [
            "معالجة الضعف الدراسي لدى الطلاب المتأخرين ورفع مستواهم التحصيلي من خلال برامج علاجية مكثفة ومتخصصة تتناسب مع احتياجاتهم.",
            "تحسين مهارات الطلاب الأساسية في القراءة والكتابة والحساب عبر أنشطة علاجية فردية وجماعية تستهدف نقاط الضعف المحددة.",
            "بناء الثقة النفسية لدى الطلاب المتأخرين دراسياً وتشجيعهم على المشاركة الفاعلة في العملية التعليمية وتحسين دافعيتهم للتعلم.",
            "تحديد الفجوات التعليمية لدى الطلاب وتصميم خطط علاجية فردية تعالج نقاط الضعف وتطور نقاط القوة لدى كل طالب على حدة.",
            "تعزيز المهارات الأساسية للطلاب المتأخرين وتمكينهم من اللحاق بزملائهم من خلال برامج دعم وعلاج ممنهجة ومتابعة مستمرة."
        ],
        summary: [
            "تم تطبيق خطة علاجية لعدد من الطلاب المتأخرين دراسياً باستخدام أنشطة متنوعة تركز على المهارات الأساسية.",
            "شارك الطلاب في جلسات علاجية فردية وجماعية ساعدت في تحسين مستواهم الدراسي بشكل ملحوظ.",
            "شهدت الخطة العلاجية تفاعلاً جيداً من الطلاب مع تحسن في أدائهم الدراسي وزيادة في ثقتهم بأنفسهم.",
            "تم تنفيذ أنشطة علاجية مكثفة ساهمت في سد الفجوات التعليمية لدى الطلاب المتأخرين دراسياً.",
            "أظهر الطلاب تحسناً كبيراً في المهارات الأساسية بعد تطبيق الخطة العلاجية المخصصة لهم."
        ],
        steps: [
            "تحديد الطلاب المتأخرين دراسياً وتحليل نقاط ضعفهم من خلال الاختبارات التشخيصية والملاحظة الصفية.",
            "تصميم أنشطة علاجية فردية وجماعية تناسب مستوى كل طالب واحتياجاته التعليمية الخاصة.",
            "تنفيذ جلسات علاجية منتظمة مع متابعة تقدم الطلاب وتقييم أدائهم بشكل دوري.",
            "استخدام وسائل تعليمية مساعدة وألعاب تعليمية لجعل الجلسات العلاجية أكثر جاذبية وفعالية.",
            "تسجيل ملاحظات عن تقدم كل طالب وتعديل الخطة العلاجية حسب الحاجة لضمان تحقيق الأهداف."
        ],
        strategies: [
            "التعليم التفريقي لتلبية احتياجات الطلاب المختلفة وفق قدراتهم ومستوياتهم.",
            "التعلم التعاوني بين الطلاب لتعزيز الثقة وتبادل الخبرات بينهم.",
            "استخدام الوسائل البصرية والسمعية لتسهيل فهم المفاهيم الصعبة.",
            "التكرار والتدرج في تقديم المهارات لضمان استيعابها بشكل كامل.",
            "التغذية الراجعة الفورية لتصحيح الأخطاء وتعزيز الإجابات الصحيحة."
        ],
        strengths: [
            "التزام الطلاب بالحضور والمشاركة في الجلسات العلاجية بنشاط واهتمام.",
            "تحسن ملحوظ في مهارات القراءة والكتابة لدى معظم الطلاب المستهدفين.",
            "تفاعل إيجابي من أولياء الأمور مع الخطة العلاجية ومتابعتهم لأبنائهم.",
            "تنوع الأنشطة العلاجية مما ساهم في استمرار دافعية الطلاب للتعلم.",
            "ملاحظة زيادة الثقة بالنفس لدى الطلاب وتحسن اتجاهاتهم نحو المادة."
        ],
        improve: [
            "زيادة وقت الجلسات العلاجية لضمان تحقيق نتائج أفضل للطلاب.",
            "توفير المزيد من الوسائل التعليمية المساعدة لتطوير الخطة العلاجية.",
            "زيادة التنسيق مع أولياء الأمور لمتابعة الطلاب خارج المدرسة.",
            "تنويع أساليب التقويم لقياس التقدم بدقة أكبر.",
            "تخصيص وقت أكبر للطلاب الذين يعانون من صعوبات تعلم شديدة."
        ],
        recomm: [
            "الاستمرار في تطبيق الخطط العلاجية للطلاب المتأخرين دراسياً.",
            "تطوير بنك أنشطة علاجية متنوعة لمواجهة الصعوبات المختلفة.",
            "تدريب المعلمين على استراتيجيات التعامل مع الطلاب المتأخرين.",
            "تعزيز الشراكة مع أولياء الأمور لتحقيق نتائج مستدامة.",
            "تخصيص ميزانية للمواد التعليمية الداعمة للخطط العلاجية."
        ]
    },
    'تقرير تكريم المتميزين': {
        goal: [
            "تحفيز الطلاب المتميزين وتكريمهم لجهودهم وتفوقهم الدراسي مما يعزز روح التنافس الإيجابي ويشجع الآخرين على التحسين.",
            "تعزيز الثقة بالنفس لدى الطلاب المتفوقين وتقدير جهودهم المتميزة لتحفيزهم على الاستمرار في التفوق والإبداع.",
            "تشجيع ثقافة التميز والإنجاز بين الطلاب من خلال تكريم المتفوقين وتقديمهم كنماذج يحتذى بها في المدرسة.",
            "تعزيز الانتماء للمدرسة وتحفيز جميع الطلاب على بذل الجهد للتفوق من خلال تكريم زملائهم المتميزين.",
            "بناء بيئة مدرسية محفزة ترعى المواهب وتشجع التفوق الدراسي والسلوكي من خلال برامج التكريم والتشجيع."
        ],
        summary: [
            "تم تكريم مجموعة من الطلاب المتميزين في الحفل المدرسي تقديراً لتفوقهم الدراسي وسلوكهم المثالي.",
            "شهد الحفل تكريم الطلاب المتفوقين بحضور أولياء الأمور والهيئة التعليمية مما كان له أثر إيجابي كبير.",
            "تم تنظيم حفل تكريم للطلاب المتميزين الذين حققوا نتائج متميزة في الاختبارات والفعاليات المدرسية.",
            "شارك في الحفل طلاب متميزون في مختلف المجالات الدراسية والأنشطة اللاصفية.",
            "شكل حفل التكريم دفعة معنوية قوية للطلاب المتفوقين وحافزاً لزملائهم للوصول إلى التميز."
        ],
        steps: [
            "تحديد معايير التميز والتفوق الدراسي والسلوكي لاختيار الطلاب المكرمين.",
            "اختيار الطلاب المتفوقين بناءً على نتائجهم الدراسية وسلوكهم وإنجازاتهم المختلفة.",
            "تحضير الحفل وتجهيز الشهادات والهدايا التكريمية للطلاب المتميزين.",
            "دعوة أولياء أمور الطلاب المكرمين للمشاركة في حفل التكريم.",
            "تنظيم الحفل وتقديم الكلمات التكريمية وتسليم الشهادات والهدايا للطلاب."
        ],
        strategies: [
            "التكريم العلني للطلاب المتفوقين لتعزيز ثقتهم بنفسهم وتحفيز الآخرين.",
            "التنويع في أساليب التكريم ليشمل المجالات الدراسية والأنشطة المختلفة.",
            "إشراك أولياء الأمور في حفل التكريم لتعزيز الشراكة مع الأسرة.",
            "توثيق حفل التكريم بالصور والفيديوهات لنشر ثقافة التميز.",
            "ربط التكريم بمعايير واضحة ومعلنة للطلاب لتحقيق العدالة والشفافية."
        ],
        strengths: [
            "تفاعل كبير من الطلاب المكرمين وأولياء أمورهم مع حفل التكريم.",
            "تنظيم ممتاز للحفل وحضور لافت من جميع أطراف المجتمع المدرسي.",
            "تنوع معايير التكريم ليشمل الجوانب الدراسية والسلوكية والإبداعية.",
            "أثر إيجابي واضح على دافعية الطلاب للتفوق والتميز في المستقبل.",
            "نجاح الحفل في تحقيق أهدافه التربوية والتشجيعية للطلاب."
        ],
        improve: [
            "توسيع دائرة التكريم ليشمل المزيد من الطلاب في المرات القادمة.",
            "زيادة الميزانية المخصصة للهدايا التكريمية لتكون أكثر جاذبية.",
            "تضمين فعاليات وأنشطة ترفيهية أكثر تنوعاً خلال حفل التكريم.",
            "تطوير معايير التكريم لتشمل مجالات إبداعية جديدة ومتنوعة.",
            "تحسين عملية التواصل مع أولياء الأمور ودعوتهم للمشاركة."
        ],
        recomm: [
            "الاستمرار في تنظيم حفلات التكريم بشكل دوري كل فصل دراسي.",
            "تطوير نظام حوافز ومكافآت متنوعة للطلاب المتميزين.",
            "إنشاء لوحة شرف دائمة لأسماء الطلاب المتفوقين في المدرسة.",
            "تعميم فكرة التكريم على المستوى الصفي ليشمل جميع الطلاب.",
            "توثيق أفضل الممارسات في التكريم ونشرها بين المدارس الأخرى."
        ]
    },
    'تقرير أنشطة صفية': {
        goal: [
            "تنمية المهارات العلمية والعملية لدى الطلاب من خلال أنشطة صفية تفاعلية تربط بين النظرية والتطبيق في بيئة تعليمية جاذبة.",
            "تعزيز الفهم العميق للمفاهيم الدراسية عبر أنشطة تطبيقية صفية تشجع الاكتشاف والتجربة والمشاركة الفاعلة للطلاب.",
            "تحسين مهارات التواصل والتعاون بين الطلاب من خلال أنشطة صفية جماعية تعزز العمل المشترك وتبادل الأفكار والخبرات.",
            "تنمية التفكير الناقد والإبداعي لدى الطلاب عبر أنشطة صفية تحفز التساؤل والاستقصاء وحل المشكلات بطرق مبتكرة.",
            "ربط المنهج الدراسي بالحياة العملية من خلال أنشطة صفية تطبيقية تجعل التعلم أكثر واقعية ومرتبطاً بتجارب الطلاب اليومية."
        ],
        summary: [
            "تم تنفيذ أنشطة صفية متنوعة في حصص المادة ساهمت في زيادة تفاعل الطلاب مع المحتوى الدراسي.",
            "شهدت الحصص تطبيق أنشطة عملية جماعية وفردية عززت فهم الطلاب للمفاهيم العلمية.",
            "تفاعل الطلاب بشكل إيجابي مع الأنشطة الصفية مما ساهم في تحقيق الأهداف التعليمية المخطط لها.",
            "تم تنفيذ أنشطة تعليمية مبتكرة داخل الصف ساعدت على تكوين بيئة تعليمية نشطة ومحفزة.",
            "أظهر الطلاب حماساً كبيراً للمشاركة في الأنشطة الصفية التي ربطت بين الجانب النظري والعملي."
        ],
        steps: [
            "تخطيط الأنشطة الصفية المناسبة لأهداف الدرس ومستوى الطلاب.",
            "تجهيز الأدوات والمواد اللازمة لتنفيذ الأنشطة داخل الصف.",
            "تقسيم الطلاب إلى مجموعات وتوضيح التعليمات والأدوار لكل مجموعة.",
            "متابعة تنفيذ الطلاب للأنشطة وتقديم التوجيه والدعم عند الحاجة.",
            "مناقشة نتائج الأنشطة مع الطلاب وتلخيص أهم النقاط المستفادة."
        ],
        strategies: [
            "التعلم النشط القائم على المشاركة الفاعلة للطالب في العملية التعليمية.",
            "التعلم التعاوني من خلال العمل في مجموعات صغيرة لتحقيق هدف مشترك.",
            "استراتيجية الاكتشاف الموجه لتنمية مهارات الاستقصاء والبحث.",
            "التعلم بالمشاريع الصغيرة لربط المعرفة بالتطبيق العملي.",
            "استخدام الوسائل التعليمية المتنوعة لدعم الأنشطة الصفية."
        ],
        strengths: [
            "تفاعل الطلاب الكبير مع الأنشطة الصفية ومشاركتهم الفاعلة فيها.",
            "تنوع الأنشطة مما ساهم في استمرار انتباه واهتمام الطلاب.",
            "تحسن ملحوظ في فهم المفاهيم الصعبة بعد تطبيق الأنشطة العملية.",
            "تنظيم جيد للوقت خلال الحصة مما سمح بتنفيذ جميع الأنشطة المخطط لها.",
            "ملاحظة زيادة دافعية الطلاب للتعلم وتحسن أدائهم الدراسي."
        ],
        improve: [
            "زيادة الوقت المخصص للأنشطة الصفية لتحقيق نتائج أفضل.",
            "توفير المزيد من الوسائل والأدوات التعليمية الداعمة للأنشطة.",
            "تدريب الطلاب على العمل الجماعي ومهارات التواصل بشكل أفضل.",
            "تطوير أنشطة تتناسب مع الفروق الفردية بين الطلاب.",
            "تحسين التخطيط المسبق للأنشطة لضمان تنفيذها بسلاسة."
        ],
        recomm: [
            "الاستمرار في تطبيق الأنشطة الصفية التفاعلية في جميع الدروس.",
            "تطوير بنك أنشطة صفية متنوعة لجميع وحدات المنهج الدراسي.",
            "تدريب المعلمين على تصميم وتنفيذ الأنشطة الصفية الفعالة.",
            "تخصيص جزء من الميزانية لدعم الأنشطة الصفية بالمستلزمات.",
            "توثيق التجارب الناجحة في الأنشطة الصفية ونشرها بين المعلمين."
        ]
    },
    
  "تقرير خطة أسبوعية": {
    "goal": [
      "تنظيم خطة أسبوعية فعالة تعزز تقدم الطلاب الأكاديمي وتحقق أهداف تعلم متدرجة تدعم تنمية المهارات المختلفة وتحسن الاستيعاب.",
      "تحقيق تكامل بين الدروس خلال الأسبوع مع ربط خبرات الطلاب التعليمية وتقديم تعلم منظم يجمع بين التطبيق والمراجعة والتحسين المستمر.",
      "رفع جودة العملية التعليمية عبر تخطيط أسبوعي يضمن وضوح الأهداف وتحقيق مشاركة فعالة وتقدم حقيقي في مهارات الطلاب التحصيلية.",
      "دعم استيعاب الطلاب للمحتوى بتوزيع متوازن للدروس أسبوعياً يمنع تراكم المهام ويحسن قدرة الطلاب على التعلم دون ضغط كبير.",
      "تطبيق خطة أسبوعية مرنة تراعي الفروق الفردية وتقدم فرصاً متنوعة للتعلم مما يعزز الفهم ويزيد فاعلية المشاركة داخل الصف."
    ],
    "summary": [
      "تنفيذ خطة أسبوعية متوازنة تلبي احتياج الطلاب. تعزيز الفاعلية وتحسين الأداء خلال جميع الدروس.",
      "خطة أسبوعية منظمة تسهم في رفع الفهم. متابعة مستمرة لتحقيق أهداف تعلم دقيقة.",
      "تنفيذ الدروس وفق جدول مخطط مسبقاً. وتحقيق مشاركة فاعلة داخل بيئة صف محفزة.",
      "تنظيم المحتوى الدراسي بما يناسب قدرات الطلاب. متابعة النتائج وتحفيز التقدم التعليمي.",
      "إدارة زمنية ممتازة للدروس والمهمات. تحسين التعلم وزيادة استيعاب المفاهيم."
    ],
    "steps": [
      "تحديد أهداف الأسبوع وتوزيع الدروس. متابعة الدافعية وتقديم التغذية الراجعة.",
      "تنظيم المهام ومراقبة مشاركات الطلاب. تحسين الأداء عبر دعم مستمر يومياً.",
      "إعداد خطة تفصيلية تناسب جميع المستويات. وتحديثها عند الحاجة باستمرار.",
      "تطبيق أنشطة مناسبة تعزز الفهم والتفكير. مراجعة مستمرة لقياس تحقيق الأهداف.",
      "تنسيق الدروس بما يتماشى مع الوقت المتاح. معالجة نقاط الضعف فور ظهورها."
    ],
    "strategies": [
      "تنويع أساليب التعلم مع تفاعل نشط. تعزيز التعاون بين الطلاب داخل المجموعات.",
      "استراتيجيات مشاركة تحفز الطلاب دائماً. أنشطة تطبيقية ترفع مستوى التركيز.",
      "دمج التقنية في تنفيذ المهام اليومية. وتحفيز المناقشة بين جميع الطلاب.",
      "تطبيق أسئلة تفكير عليا داخل الدروس. وتمكين الطلاب من البحث والاستنتاج.",
      "توظيف تعلم تشاركي يعزز مهارات تواصل. واستخدام أمثلة واقعية لربط المحتوى."
    ],
    "strengths": [
      "تنفيذ منظم يشجع الطلاب على التعلم. وارتفاع ملحوظ في مستويات المشاركة دائماً.",
      "تحسن فهم المفاهيم لدى الطلاب جميعاً. إدارة صفية فعالة تحقق الأهداف المخططة.",
      "وضوح التوجيهات يساعد بتحسين النتائج. واستجابة سريعة من الطلاب للمهام.",
      "تفاعل جماعي متميز أثناء تنفيذ الدروس. ثقة متزايدة بتنفيذ الأنشطة التعليمية.",
      "تقليل الفاقد بتطبيق خطة أسبوعية. تعزيز الاستيعاب ومحافظة على تركيز الطلاب."
    ],
    "improve": [
      "زيادة الوسائل المتنوعة لتحفيز الطلاب. وتقديم دعم أكبر للمتعثرين مباشرة.",
      "تنظيم أنشطة إضافية ترفع دافعية الطلاب. وتخصيص وقت أطول لتطبيق المحتوى.",
      "تنويع الممارسات الصفية التي تعالج الفروق. والتركيز على مهارات التفكير العليا.",
      "تطوير المتابعة الفردية للطلاب باستمرار. ورفع مستوى المراجعين الأقل تقدماً.",
      "تعزيز التدريب الذاتي خارج وقت الدراسة. وزيادة متابعة تنفيذ الخطة أسبوعياً."
    ],
    "recomm": [
      "الاستمرار بتطبيق خطة تعليم أسبوعية. توظيف التقنية لدعم تعلم أكثر فعالية.",
      "زيادة التعاون بين الطلاب باستخدام أنشطة. ونشر ثقافة التعلم الذاتي دائماً.",
      "تحديث الخطة بناء على التغذية الراجعة. وتطوير طرق التطبيق باستمرار دائم.",
      "تخصيص وقت إضافي للمراجعة الدورية. ودعم التعلم في البيئات غير الصفية.",
      "تطوير بنك أنشطة متنوعة أسبوعياً. وتحسين التواصل مع الأسرة للمتابعة."
    ]
  },

  "تقرير توزيع المنهج": {
    "goal": [
      "تنظيم تقديم المنهج خلال الفصل بشكل يضمن تسلسل المحتوى، وتحسين فهم الطلاب، وتحقيق نواتج تعلم واضحة تدعم التقدم الدراسي.",
      "تحقيق توزيع زمني عادل لوحدات المنهج بما يناسب قدرات الطلاب، ويضمن الوصول إلى الإتقان مع مراعاة الفروق الفردية باستمرار.",
      "رفع جودة التعليم عبر جدول تدريسي متوازن ينسق بين الشرح والتطبيق والمراجعة ويضمن تقدماً تعلمياً ثابتاً للطلاب.",
      "تعزيز استيعاب الطلاب للمفاهيم من خلال توزيع منطقي يقلل ضغط الدروس ويزيد ثبات المعرفة وتحسن الأداء الدراسي.",
      "إدارة الوقت الدراسي بكفاءة عالية من خلال توزيع وحدات المنهج بترتيب يسهم في الفهم التدريجي المرتبط بنتائج تقييم واضحة."
    ],
    "summary": [
      "تنظيم توزيع المنهج وفق خطة دقيقة. متابعة التحصيل وتدارك أي ضعف سريعاً.",
      "توزيع المحتوى بأيام متوازنة ومستهدفة. رفع الاستيعاب وتحسين مستوى الطلاب.",
      "تحسين سير الدروس داخل الأسابيع المحددة. تحقيق فهم عميق ومتابعة فعّالة دائماً.",
      "إدارة المحتوى لإتاحة فرص تطبيق مستمرة. ضمان سير المنهج دون تأخير ملحوظ.",
      "ترتيب وحدات المنهج يرفع مستوى الفهم. تعزيز ثبات التعلم بصورة متواصلة."
    ],
    "steps": [
      "تحليل وحدات المنهج وتحديد الأولويات. وتقسيم الدروس على الأسابيع بدقة.",
      "متابعة التطبيق وتقييم تقدم الطلاب. وتعديل الجدول عند الحاجة فوراً.",
      "موازنة المهام اليومية بما يناسب قدرات. وتطبيق استراتيجيات تعلم مستمر.",
      "تنسيق المراجعات وفق الخطة الزمنية. وتوفير الوقت لتعزيز المفاهيم الصعبة.",
      "توظيف نشاطات تطبيقية داعمة للمحتوى. ومتابعة أثرها على تحسن الأداء."
    ],
    "strategies": [
      "تنويع طرق الشرح وتحسين التواصل. استخدام مراجعات دورية داعمة للتعلم.",
      "تعلم نشط يعزز مشاركة الطلاب جميعاً. وتوظيف التقنية لرفع التفاعل داخل الصف.",
      "ربط الدروس بخبرات حياتية قريبة. وتحفيز التفكير بالأسئلة المفتوحة والأنشطة.",
      "إدارة فعّالة للوقت داخل الدروس دائماً. وتحقيق إنجاز حقيقي للمحتوى التعليمي.",
      "استراتيجيات تضمن وصول المعلومات للجميع. ومتابعة المخرجات بقياس واضح وصحيح."
    ],
    "strengths": [
      "تسلسل رائع في تقديم موضوعات المنهج. توافق جيد مع قدرات الطلاب الدراسية.",
      "إدارة عملية للدروس تمنع التشتت. ودافعية أفضل لدى الطلاب للتعلم.",
      "زيادة فهم المفاهيم الأساسية للطلاب. وتحسن تدريجي في التحصيل الأكاديمي.",
      "تحقيق تغطية شاملة للمحتوى المطلوب. ومتابعة تقدم مستمرة تحقق الأهداف.",
      "وضوح التوقعات أمام الطلاب دائماً. مما يعزز المشاركة والثقة بالتعلم."
    ],
    "improve": [
      "زيادة الأنشطة التطبيقية ضمن الدروس. وتوفير وقت إضافي للمراجعات الدورية.",
      "تطوير طرق لمعالجة صعوبات التعلم. وإعادة ضبط الخطة عند الحاجة دوماً.",
      "تحفيز الطلاب الأقل أداء عبر دعم. فردي إضافي وبرامج متابعة دقيقة.",
      "زيادة التنسيق بين جميع المعلمين. وتعزيز الشراكة لتحسين النتائج العامة.",
      "رفع مستوى التفاعل داخل الدروس. وتخفيف العبء في بعض الأسابيع المزدحمة."
    ],
    "recomm": [
      "تحديث خطة التوزيع باستمرار دقيق. والاستفادة من التغذية الراجعة المهنية.",
      "تعزيز المراجعة في نهاية كل وحدة. وتحسين آليات قياس مستوى الفهم.",
      "زيادة الأنشطة العملية الداعمة للمحتوى. وتوظيف موارد تعلم إضافية ممتازة.",
      "إشراك الطلاب في تقييم التخطيط. وتنمية مسؤوليتهم عن تعلم مستمر.",
      "التأكيد على تعاون الأسرة بالمتابعة. للمساعدة في تثبيت واستيعاب المحتوى."
    ]
  },

  "تقرير حصة النشاط": {
    "goal": [
      "تعزيز مهارات الإبداع والتعاون من خلال تنفيذ أنشطة تفاعلية داخل الصف تشجع الطلاب على الحوار والعمل الجماعي وتحسين الذات.",
      "تنمية قدرات الطلاب على التفكير الحر والاستقصاء عبر أنشطة تعليمية ممتعة تدعم شخصياتهم وتزيد من قدرتهم على التفاعل.",
      "رفع مستوى المشاركة الفعالة بين الطلاب من خلال أنشطة جماعية تتيح تبادل الآراء وتحقيق أهداف تعلم عملية تطبيقية.",
      "تحسين مهارات الطلاب الاجتماعية عبر تشجيعهم على المشاركة في أنشطة محفزة ترفع الثقة وتدعم التواصل الإيجابي بينهم.",
      "تطوير شخصية الطلاب من خلال مواقف تعليمية تعزز المنافسة الإيجابية وتحسن تعاونهم داخل البيئة الصفية بفاعلية عالية."
    ],
    "summary": [
      "تنفيذ نشاط تعليمي ممتع يعزز التواصل. ويدعم التفاعل الفعّال بين الطلاب دائماً.",
      "نشاط تفاعلي داخل الصف يزيد المشاركة. وينمي مهارات الطلاب بشكل رائع.",
      "أنشطة تعاونية جذابة ترفع الحماس. وتحسن التواصل بين الطلاب بصورة أفضل.",
      "استخدام أنشطة محفزة تدعم التفكير. وزيادة الإبداع داخل البيئة الصفية.",
      "ربط نشاطات ممتعة بالمحتوى الدراسي. وتحسين فهم الطلاب بطرق جديدة."
    ],
    "steps": [
      "تحديد الهدف من النشاط بدقة مناسبة. تقسيم الطلاب لمجموعات بمهمات واضحة.",
      "شرح خطوات النشاط للطلاب بوضوح جيد. متابعة الأداء وتقديم دعم فوري.",
      "إتاحة فرص مشاركة لجميع الأفراد دوماً. وتبادل منظم للأفكار بداخل الصف.",
      "مراقبة تقدم كل مجموعة باستمرار دائم. تحفيز الطلاب لتحقيق أهداف النشاط.",
      "ختام النشاط بنقاش لتبادل الخبرات. تقييم الإنجاز وتحسين الأداء لاحقاً."
    ],
    "strategies": [
      "التعلم النشط لتحسين مشاركة الطلاب. عصف ذهني يدعم توليد أفكار مبتكرة.",
      "استخدام التعلم التعاوني باستمرار داخل الصف. وتحسين العمل الجماعي بفاعلية.",
      "أنشطة بحث واستكشاف تنمي التفكير. تطوير المهارات بطرق تطبيقية ممتعة.",
      "تعلم قائم على المشاريع الصغيرة دائماً. تحفيز الطلاب لإيجاد حلول للمشكلات.",
      "استراتيجيات تواصل فعالة تدعم الحوار. استخدام تقنيات تعليم تزيد التفاعل."
    ],
    "strengths": [
      "مشاركة عالية من أغلب الطلاب دائماً. تعاون مشجع داخل مجموعات التعلم.",
      "تحسن واضح في مهارات التفكير لديهم. تفاعل ممتاز مع محتوى النشاط.",
      "جو تعليمي محفز يدعم الإبداع. تنظيم رائع لإدارة وقت النشاط.",
      "أداء جماعي مميز يظهر قدرات جديدة. مساهمة واضحة في تطوير المهارات.",
      "زيادة دافعية الطلاب لتجربة المزيد. وانسجام كبير أثناء العمل المشترك."
    ],
    "improve": [
      "زيادة الوقت المخصص للنشاط دائماً. دعم أكبر للطلاب الأقل مشاركة.",
      "تعزيز توظيف الوسائل التعليمية الحديثة. وتدريب الطلاب على التعاون.",
      "تنويع المهام لتناسب جميع القدرات. وتوجيه إضافي للمجموعات المتعثرة.",
      "توسيع الأنشطة التطبيقية داخل الصف. تحسين متابعة تقدم كل طالب.",
      "التدرج بشكل أفضل في صعوبة النشاط. ضمان مشاركة فعّالة من الجميع."
    ],
    "recomm": [
      "الاستمرار باستخدام الأنشطة التفاعلية المميزة. وتوظيف التقنية في التعلم دائماً.",
      "زيادة الأنشطة التطبيقية في الدروس المقبلة. وتحفيز الطلاب على الإبداع أكثر.",
      "مشاركة الطلاب في تصميم الأنشطة المقبلة. وبناء ثقة أكبر بقدراتهم التعليمية.",
      "تطوير فعاليات متنوعة تعزز التعاون المستمر. وتدعم المهارات الاجتماعية للطلاب.",
      "تحسين التنسيق بين المعلم والمجموعات دائماً. وضمان تعلم ممتع داخل الصف."
    ]
  },

  "تقرير تنفيذ إذاعة مدرسية": {
    "goal": [
      "تنمية مهارات الإلقاء وتعزيز الثقة بالنفس من خلال مشاركة الطلاب في الإذاعة المدرسية وتقديم محتوى هادف يرسخ القيم الإيجابية.",
      "تحسين التواصل اللغوي لدى الطلاب عبر فقرات إذاعية متنوعة تعزز الجرأة في الحديث وتنمّي قدراتهم الأدائية والإبداعية داخل المدرسة.",
      "دعم بناء الشخصية الطلابية عبر مشاركات إذاعية محفزة تقوي العلاقات الاجتماعية وتزيد الوعي بالقضايا التربوية والثقافية المهمة.",
      "تفعيل دور الطلاب الإعلامي بتمكينهم من إعداد وتقديم برامج إذاعية تساهم في نشر المعرفة وغرس السلوك الإيجابي بالمدرسة.",
      "تطوير روح القيادة لدى الطلاب من خلال تحمّل مسؤولية تنفيذ البرنامج الإذاعي ورفع مستوى المشاركة التربوية الهادفة."
    ],
    "summary": [
      "تنفيذ إذاعة مدرسية مميزة تزيد التفاعل. مشاركة طلابية رائعة في تقديم فقرات مفيدة.",
      "برنامج إذاعي متكامل يرفع الحماس. محتوى هادف يساهم بنشر قيم إيجابية.",
      "إلقاء متميز من الطلاب المشاركين. حضور جيد وتفاعل ملحوظ منذ البداية.",
      "تنظيم رائع لفقرات البرنامج بالكامل. وانضباط واضح أثناء تقديم الإذاعة.",
      "تنوع الفقرات يمنح الطلاب فرصة. لإظهار مواهبهم التعليمية والإبداعية."
    ],
    "steps": [
      "اختيار موضوع إذاعي يناسب الطلاب. إعداد فقرات تقدم محتوى تربوياً هادفاً.",
      "تدريب الطلاب على أساليب الإلقاء. متابعة وضبط الأداء قبل التنفيذ.",
      "تنظيم البرنامج وفق تسلسل مناسب. توزيع الأدوار ودعم المشاركين دائماً.",
      "تنفيذ الإذاعة أمام الجمهور الصباحي. تعزيز الثقة وتشجيع الجرأة بالكلام.",
      "تقديم تغذية راجعة لتحسين الأداء. وتطوير مهارات المشاركين مستقبلاً."
    ],
    "strategies": [
      "توظيف مهارات الإلقاء والتقديم الشفهي. فقرات مؤثرة تجذب انتباه الحضور.",
      "التعاون بين الطلاب أثناء التدريب. دعم القدرات وتبادل الخبرات الإذاعية.",
      "استخدام مؤثرات صوتية ملائمة للعرض. تعزيز القوة التعبيرية داخل الفقرات.",
      "تعلم قائم على الأداء العملي دائماً. تعزيز الثقة من خلال الممارسة الفعلية.",
      "تنويع الفقرات لزيادة الحماس الطلابي. إشراك أكبر عدد من المشاركين الجدد."
    ],
    "strengths": [
      "تحسن كبير بمهارات الإلقاء الشفهي. وجرأة واضحة لدى الطلاب المشاركين.",
      "التزام الحضور بمتابعة الفقرات كاملة. تفاعل ممتاز مع محتوى الإذاعة.",
      "تنظيم رائع للوقت أثناء التنفيذ. وتجانس مستمر بين جميع الفقرات.",
      "قدرة الطلاب على الإبداع والتأثير. تقديم متميز للرسالة التربوية المقررة.",
      "تحقيق أهداف البرنامج الإذاعي بالكامل. وزيادة الوعي بالقيم المدرسية."
    ],
    "improve": [
      "زيادة عدد المتحدثين بالفقرات المقبلة. وتدريبهم على تحسين الأداء المستمر.",
      "تنويع الموضوعات المطروحة يومياً. مع متابعة مردودها على الطلاب.",
      "استثمار التقنية لإنشاء فقرات مرئية. وتحفيز الطلاب على الإبداع دائماً.",
      "توفير مساحة مشاركة أكبر للجمهور. وتعزيز النقاش بعد البرنامج مباشرة.",
      "إضافة تقييم رقمي لأداء المشاركين. وقياس الأثر التربوي بوضوح."
    ],
    "recomm": [
      "استمرار تنفيذ إذاعات يومية هادفة. لتوسيع مشاركة الطلاب في المدرسة.",
      "تنمية مهارات التقديم لجميع الطلاب. وتشجيعهم عبر تحفيزات مناسبة دائماً.",
      "تطوير محتوى يركز على السلوكيات. ويسهم في نشر القيم الإيجابية داخل المدرسة.",
      "تنظيم مسابقات خاصة بالإلقاء الإذاعي. واكتشاف مواهب جديدة متميزة.",
      "توثيق أفضل الفقرات وعرضها لاحقاً. لتحفيز الطلاب على إنتاج محتوى هادف."
    ]
  },

  "تقرير تبادل الزيارات": {
    "goal": [
      "تحسين جودة التعليم من خلال تبادل الخبرات الصفية بين المعلمين مما يعزز تطوير الممارسات التدريسية ورفع مستوى أداء الطلاب التعليمي.",
      "دعم النمو المهني للمعلمين بزيارات منظمة تهدف لتحليل الدروس وملاحظة الاستراتيجيات وتبادل الخبرات الميدانية الناجحة.",
      "تحقيق شراكة تربوية مستمرة عبر زيارات مهنية تعزز التعاون بين المعلمين وتسهم بتحسين الأداء داخل البيئة التعليمية.",
      "رفع مستوى الوعي بأساليب التدريس الحديثة من خلال حضور دروس متنوعة وتطبيق أفضل الممارسات داخل الفصول.",
      "توظيف التغذية الراجعة البنّاءة لتطوير الأداء التدريسي مما يضمن جودة أعلى في التعلم ومخرجات أفضل للطلاب."
    ],
    "summary": [
      "زيارة صفية مهنية تهدف لتبادل خبرات. استفادة واضحة للمعلمين المشاركين.",
      "تحليل لممارسات التدريس المطبقة فعلاً. وتطوير نقاط التحسين بشكل مباشر.",
      "تنفيذ زيارة مفيدة تزيد التواصل. وتحقق فائدة أكاديمية للجميع دائماً.",
      "مشاركة معرفية جيدة بين الزملاء. تعزيز التعاون ورفع الأداء تدريجياً.",
      "زيارات تربوية منهجية مستمرة. تضمن تحسناً في طرق التدريس."
    ],
    "steps": [
      "تحديد أهداف الزيارة ومجالات الملاحظة. حضور الدرس وتوثيق الملاحظات.",
      "تحليل الأداء التدريسي بعناية مستمرة. تقديم تغذية راجعة بناءة للمعلم.",
      "متابعة تطبيق التوصيات داخل الصف. تقييم النتائج بعد فترة محددة.",
      "تعزيز تبادل الخبرات والممارسات. وتشجيع التعاون بين الزملاء دائماً.",
      "بناء خطة تطويرية تفصيلية لاحقاً. وضمان تحقيق أثر إيجابي مستمر."
    ],
    "strategies": [
      "إدارة نقاش مفتوح بعد الزيارة مباشرة. تحليل أداء المعلم وتحسينه.",
      "مقارنة الاستراتيجيات وفق معايير واضحة. اختيار المناسب للفصل المدرسي.",
      "تبادل أفضل الممارسات التربوية دائماً. تعزيز مهارات المعلم التعليمية.",
      "جلسات تدريب مشتركة بعد الزيارة. دعم التطوير داخل البيئة المدرسية.",
      "توظيف نتائج التحليل لتطوير الدروس. ومتابعة الأداء بشكل مستمر."
    ],
    "strengths": [
      "تعاون كبير بين أعضاء الهيئة التدريسية. مشاركة فعالة داخل الزيارة.",
      "وعي متزايد بأهمية تبادل الخبرات. وتطبيق ممارسات جديدة مباشرة.",
      "تطوير مستمر لاستراتيجيات التدريس. تحسين ملحوظ بمهارات المعلمين.",
      "نتائج إيجابية أبرزها تحسين الطلاب. استجابة ملحوظة داخل الفصل.",
      "زيادة الثقة بين المعلمين دائماً. تنمية مهنية مستدامة وشاملة."
    ],
    "improve": [
      "رفع عدد الزيارات المهنية لاحقاً. وتحسين تنظيم التوقيت دائماً.",
      "توفير متابعة أوضح بعد الزيارة. لتحقق أثر تربوي مستدام مستقبلاً.",
      "إتاحة مشاركة أكبر للمعلمين الجدد. دعم مهني مبكر ومكثف للجميع.",
      "زيادة التنوع بالاستراتيجيات الملاحظة. لضمان رفع الاستفادة بشكل رائع.",
      "توثيق خطط التحسين بفاعلية أعلى. ومشاركة مخرجاتها مع الجميع."
    ],
    "recomm": [
      "الاستمرار بزيارات مهنية منظمة فعالة. ودعم نشر الخبرات داخل المدرسة.",
      "تشجيع الزيارات المتبادلة بين مدارس. لرفع جودة التعليم في المنطقة.",
      "إعداد برامج تطوير مستمرة للمعلمين. تواكب أحدث استراتيجيات التدريس.",
      "تخصيص وقت كافٍ للمتابعة الفعلية. وتحقيق نتائج ملموسة للطلاب.",
      "تنظيم ورش تفاعلية بعد الزيارات. لتسريع تطوير المهارات التدريسية."
    ]
  },

  "تقرير مجتمعات التعلم": {
    "goal": [
      "تعزيز التعاون المهني بين المعلمين من خلال مجتمعات تعلم تسهم في تطوير الخطط التعليمية وتحسين جودة التدريس ورفع مستوى الطلاب بشكل مستمر.",
      "بناء ثقافة مهنية قائمة على تبادل الخبرات ومناقشة التحديات وتطوير أساليب التعليم وتحسين المخرجات الصفية.",
      "تفعيل مجتمعات تعلم مستدامة تركز على تحسين الأداء التدريسي وتطوير الخطط بما يتناسب مع احتياجات الطلاب التعليمية.",
      "توفير بيئة مهنية داعمة تسمح للمعلمين بتحسين الأداء ومشاركة التجارب الناجحة ورفع مستوى الكفاءة التعليمية.",
      "تعزيز التعلم المستمر بين المعلمين من خلال اجتماعات تربوية تعزز التعاون وتدعم تقدم الطلاب في جميع الجوانب."
    ],
    "summary": [
      "اجتماع مهني لتبادل خبرات تطويرية. تحسين الأداء داخل العملية التعليمية.",
      "تعلم تعاوني مهني مستمر وفعّال. دعم خطط التدريس ومتابعة الطلاب.",
      "جلسات نقاش تربوية ذات أثر إيجابي. تعزيز العمل الجماعي داخل المدرسة.",
      "تواصل تربوي يحسن خطط تعليمية. مشاركة أفكار لممارسات متميزة.",
      "تنظيم اجتماعات مهنية منتظمة جداً. تحقيق تطوير دائم للمعلمين."
    ],
    "steps": [
      "تحديد أهداف الاجتماع بوضوح جيد. مناقشة خطط تعليم تعزز التفاعل.",
      "عرض تجارب ناجحة من الميدان. تحليل أثرها على تعلم الطلاب.",
      "تبادل حلول لمشكلات موجودة سابقاً. وتوثيق النقاط المهمة بالكامل.",
      "متابعة تطبيق التوصيات عملياً دوماً. تقييم أثرها أثناء تنفيذ الدروس.",
      "إعداد تقارير مهنية بعد اللقاء. وتحديث الخطط وفق مجريات العمل."
    ],
    "strategies": [
      "مجموعات نقاش ترفع جودة التعليم. مشاركة أفكار وتحليل تجارب ناجحة.",
      "استراتيجيات تطوير عبر تعاون مستمر. تحسين الأداء بشكل تدريجي دائماً.",
      "تطبيق ممارسات فعالة داخل الصف. نقل الخبرات بين الزملاء باستمرار.",
      "تدريب مهني يعتمد على المشاركة. رفع كفاءة المعلمين بشكل ممتاز.",
      "توظيف تغذية راجعة دقيقة مباشرة. وتحسين نتائج الطلاب باستمرار."
    ],
    "strengths": [
      "تفاعل إيجابي بين المعلمين دائماً. دعم كبير لتطوير الاستراتيجيات.",
      "أفكار تربوية جديدة متبادلة. وحرص واضح على تحسين التعلم.",
      "تنظيم ممتاز للاجتماعات المهنية. مشاركة نشطة من الجميع.",
      "تحقيق نتائج إيجابية سريعة. تحسن ملحوظ لدى الطلاب.",
      "زيادة الثقة داخل الفريق التربوي. تعاون كبير يعزز التطوير."
    ],
    "improve": [
      "إضافة ممارسات تطبيقية مستمرة دائماً. متابعة النتائج في كل فصل.",
      "تنويع موضوعات اللقاءات المهنية. لتلبية احتياجات متنوعة فعلياً.",
      "توفير وقت أطول للنقاش التحليلي. لتحقيق أكبر قدر من الفائدة.",
      "جمع بيانات حول أثر الاجتماعات. تقييم تقدم أداء التدريس مستمر.",
      "التوسع بمشاركة مدرسين جدد دائماً. دعم المبتدئين مهنياً بقوة."
    ],
    "recomm": [
      "الاستمرار في تفعيل مجتمعات تعلم. ودعم تبادل الخبرات الناجحة دائماً.",
      "تنظيم ورش عمل تطويرية بانتظام. تعزيز الإنتاجية داخل المدرسة.",
      "توظيف التقنية لإدارة الاجتماعات. وتوثيق مخرجاتها فورياً.",
      "تطوير نماذج تقييم لكل لقاء. لضمان تحقيق أفضل النتائج.",
      "تعزيز روح الفريق بين الأعضاء. وتقدير المساهمات الفعالة للجميع."
    ]
  },
  
  "تقرير تنفيذ درس تطبيقي": {
    "goal": [
      "تطبيق استراتيجيات تدريس حديثة أمام الزملاء لدعم الخبرات المهنية وتحسين جودة التعليم ورفع مستوى التفاعل داخل الصف لتحقيق تعلم فعّال.",
      "تحسين قدرة المعلمين على تبادل الممارسات الناجحة من خلال عرض دروس تطبيقية تعزز الاحترافية وتحسن مخرجات الطلاب التعليمية.",
      "توسيع المعرفة المهنية لدى المعلمين عبر دروس تجريبية تبرز أساليب التدريس الحديثة وتزيد المشاركة الفعلية للطلاب بالصف.",
      "تحفيز المعلمين على الابتكار في التدريس من خلال دروس تطبيقية تركز على التعلم النشط وتطوير مهارات التفكير لدى الطلبة.",
      "توثيق ممارسات تدريسية فعالة عبر تنفيذ دروس تطبيقية منظمة ترفع من جودة الفهم ودافعية الطلاب نحو التعلم المستمر."
    ],
    "summary": [
      "درس تطبيقي يعزز فهم الطلاب دائماً. مشاركة فاعلة تمنحهم الثقة داخل الصف.",
      "تنفيذ درس تجريبي بطرائق متعددة. استراتيجيات فعالة ترفع التفاعل جيداً.",
      "تجربة تطبيقية متميزة تزيد الدافعية. وتحقق نتائج إيجابية داخل القاعة.",
      "عرض درس يركز على نشاط الطلاب. إدارة صفية مميزة طوال التنفيذ.",
      "تنظيم رائع للدرس التطبيقي اليوم. واستجابة متقدمة من الطلاب."
    ],
    "steps": [
      "تخطيط للدرس باستراتيجيات متقدمة. إعداد وسائل تحقق أهداف التطبيق.",
      "توضيح الأهداف أمام الطلاب جيداً. تقديم محتوى بطرق تعليم تفاعلية.",
      "توزيع أنشطة تعزز مهارات التفكير. تطوير خبرات التعلم عبر النقاش.",
      "مراقبة الأداء أثناء تنفيذ الدرس. وتقديم دعم مستمر متواصل للجميع.",
      "تقييم نتائج التعلم بعد النشاط. تعديل أساليب مقترحة للتحسين."
    ],
    "strategies": [
      "تعلم نشط يدعم فاعلية المشاركة. توظيف أنشطة تطبيقية متنوعة دائماً.",
      "مجموعات عمل تنمي مهارات الطلاب. تواصل مستمر داخل بيئة صفية.",
      "استقصاء وأسئلة تحفز العقل. تعزيز قدرات التفكير العليا فوراً.",
      "التعلم عبر المشاريع الصغيرة الهادفة. ربط محتوى الدرس بالواقع عملياً.",
      "استخدام التقنية داخل الحصة لديها. رفع استيعاب الطلاب بشكل أكبر."
    ],
    "strengths": [
      "ارتفاع مستوى الحماس لدى الطلاب. تفاعل ممتاز أثناء النشاطات كلياً.",
      "إدارة وقت متوازنة تماماً للدرس. تحقيق أهداف تطبيقية واضحة جيداً.",
      "إبداع كبير لدى الطلاب الجادين. أفكار مبتكرة تعرض باستمرار رائع.",
      "تجاوب سريع مع الأسئلة المتقدمة. ثقة ممتازة بالقدرات التعليمية.",
      "تنظيم رائع لأدوار الطلاب دائماً. مشاركة عادلة وجهود قوية."
    ],
    "improve": [
      "زيادة أنشطة تساعد المتأخرين. تقديم دعم إضافي أثناء الحصة.",
      "تنويع أكبر في الوسائل المعينة. رفع جودة العروض التعليمية جداً.",
      "وقت أكثر لمناقشة التحديات. تطوير فهم أعمق للموضوع.",
      "زيادة فرص العمل التعاوني أكثر. تشجيع المشاركة دون تردد.",
      "تحسين متابعة مستويات الطلاب. وتقويم مستمر داخل الدرس."
    ],
    "recomm": [
      "تطبيق دروس تنفيذية متكررة جيداً. تعميم الممارسات التي تنجح كثيراً.",
      "تشجيع الزملاء على الحضور دوماً. مشاركة خبرات ميدانية قيّمة جداً.",
      "إضافة تقييم يحدد نقاط القوة. تطوير خطة تخص تحسين بعض الجوانب.",
      "تحسين استخدام التقنية بالتدريس. دعم تطور تطبيق أدوات التعلم.",
      "تشجيع إبداع الطلاب باستمرار. تحفيز قدراتهم على التفكير دوماً."
    ]
  },

  "تقرير حضور دورات وورش تدريبية": {
    "goal": [
      "تطوير مهارات المعلم المهنية من خلال دورات تدريبية تعزز قدرته على توظيف أساليب تعليم حديثة وتحسين أدائه بما يرفع جودة التعلم.",
      "دعم التطوير الذاتي المستمر لدى المعلمين عبر برامج تدريبية تساعد في تحسين الاستراتيجيات وتحقيق نتائج إيجابية بالصف.",
      "رفع كفاءة عملية التدريس من خلال حضور ورش متنوعة تزيد المعرفة وتوسع خبرات المعلم الميدانية والتقنية.",
      "تعزيز النمو المهني للمعلمين بتطبيق مكتسبات التدريب داخل الصف وتحسين ممارساتهم التعليمية بصورة مستمرة.",
      "تمكين المعلمين من استخدام طرق مبتكرة عبر ورش تدريبية تعالج تحديات التدريس وترفع مستوى التحفيز لدى الطلاب."
    ],
    "summary": [
      "تدريب مهني تطويري يزيد جودة التعليم. اكتساب خبرات تدعم التدريس فعلياً.",
      "ورشة تدريبية ترفع المهارات التدريسية. تحفيز أكبر للتعلم المستمر واقعياً.",
      "برامج تدريبية تطور قدرات المعلم. تحسين واضح في العمليات التعليمية.",
      "تدريب مفيد يعزز الإبداع التدريسي دائماً. دعم قوي للممارسات الصفية.",
      "ورشة متقدمة تقوي الأداء داخل الصف. استراتيجيات حديثة قابلة للتطبيق."
    ],
    "steps": [
      "التسجيل المسبق وحضور التدريب. توثيق الأهداف لتطبيقها جيداً لاحقاً.",
      "مناقشة مفاهيم مهمة أثناء التدريب. وتحويلها لأساليب تعليم فاعلة فعلاً.",
      "تطبيق أفكار جديدة داخل الصف. تحليل أثرها وتحسينها مستقبلاً.",
      "المشاركة بنشاط في جميع الفقرات. تبادل تجارب عملية مع الزملاء.",
      "متابعة توصيات التدريب بالتطبيق. والبحث عن فرص تطوير إضافية."
    ],
    "strategies": [
      "توظيف التعلم التعاوني ضمن التدريب. رفع مهارات التواصل بين الحضور.",
      "ورش تطبيقية تعزز مهارات التدريس. مشاركة أفكار وتجارب حقيقية.",
      "تعلم يعتمد على حل المشكلات دوماً. توجيه ميداني يعزز الفائدة.",
      "استخدام تقنيات حديثة بالتدريب. دعم التحول الرقمي في التدريس.",
      "تنفيذ أنشطة متقدمة مستمرة. رفع جودة الخبرات المهنية فعلاً."
    ],
    "strengths": [
      "زيادة وعي المعلم بطرق التدريس. تحسن فعلي بالأداء داخل الصف.",
      "تحفيز العمل الجماعي للتطوير. مشاركة نشطة بكثير من الجلسات.",
      "استفادة واضحة من محتوى التدريب. انتقال فعلي للممارسات الناجحة.",
      "إبداع أكبر في تقديم الدروس. واستخدام أساليب تدريس حديثة.",
      "ارتفاع الثقة بقدرات المعلم دائماً. تقدم ملحوظ على نتائج الطلاب."
    ],
    "improve": [
      "تكثيف التدريب التخصصي المتقدم. ومتابعة أثره بالميدان فعلياً.",
      "إضافة ورش تطبيقية أكثر تفصيلاً. تعميق فهم التقنيات التعليمية.",
      "تقوية الربط بين التدريب والصف. دعم مستمر لقياس الأثر الحاصل.",
      "تنويع محتوى الورش التدريبية. لتغطية جميع المهارات التعليمية.",
      "تسريع تطبيق التقنيات الحديثة. متابعة مستويات الأداء دائماً."
    ],
    "recomm": [
      "المشاركة المستمرة في دورات تدريبية. دعم التحسين الوظيفي للمعلمين.",
      "نشر الخبرات المكتسبة لزملاء دائمين. مشاركة تطبيقات أثناء الدروس.",
      "تعزيز مهارات التفكير ببرامج تدريبية. رفع مستوى التخطيط الممتاز.",
      "تنظيم ورش تخصصية داخل المدرسة. تحسين الممارسات التعليمية جداً.",
      "استخدام تقييم أثر التدريب بدقة. تطوير مستمر للتنفيذ المباشر."
    ]
  },

  "تقرير التواصل مع ولي الأمر": {
    "goal": [
      "تعزيز التعاون بين المدرسة والأسرة عبر تواصل فعال يساعد في تحسين أداء الطالب الأكاديمي والسلوكي ويضمن دعماً تربوياً مستداماً.",
      "مشاركة ولي الأمر في معرفة مستوى ابنه التعليمي والسلوكي وتحفيزه على تقديم الدعم اللازم لتحسين النتائج.",
      "ضمان متابعة مستمرة للطالب وتعزيز دوره في العملية التعليمية من خلال تواصل منظم يحقق نتائج ملموسة في المستوى.",
      "تمكين ولي الأمر من فهم احتياجات ابنه الدراسية والسلوكية لاتخاذ خطوات مساندة تعزز تحسين مستواه وتطوير مهاراته.",
      "تحقيق شراكة تعليمية إيجابية بين المدرسة والأسرة تعزز دافعية الطالب وتدعم التقدم والتحصيل بشكل مستمر."
    ],
    "summary": [
      "تواصل هادف لشرح مستوى الطالب. دعم الأسرة يعزز التحسن الدراسي.",
      "اجتماع تربوي يوضح قدرات الطالب. حلول مشتركة لتحسين الأداء.",
      "جهود تواصل تدعم الطالب أكاديمياً. تعزيز الاهتمام داخل المنزل.",
      "محادثة بناءة مع ولي الأمر. رفع الوعي التعليمي بشكل مناسب.",
      "تبادل معلومات تساعد الطالب بالنجاح. متابعة أسرية تحقق نتائج."
    ],
    "steps": [
      "تحديد موعد للقاء ولي الأمر. مناقشة أداء الطالب بشكل مهني.",
      "عرض تقارير تبين مستوى الطالب. وتقديم نصائح تحسين مباشرة.",
      "شرح نقاط القوة في شخصية الطالب. وتحديد احتياجات تطوير فورية.",
      "وضع خطة متفق عليها مع الأسرة. متابعة تنفيذها أسبوعياً جيداً.",
      "الاتصال بانتظام لتقديم تحديثات. تعزيز التعاون لاستمرار التقدم."
    ],
    "strategies": [
      "استماع جيد لملاحظات ولي الأمر. تبادل آراء تدعم الطالب فعلياً.",
      "تواصل شفهي ورسمي منظم دائماً. تقارير متابعة تبين مستوى الطالب.",
      "تشجيع مشاركة الطالب بالمنزل. وترسيخ عادات علمية منتظمة.",
      "توعية الأسرة بطرق دعم مناسبة. تقوية التعاون التربوي للجميع.",
      "تقديم حلول تعليمية فعالة فعلاً. وقياس نتائجها كل أسبوع."
    ],
    "strengths": [
      "استجابة ممتازة من ولي الأمر. اهتمام واضح بمتابعة الابن.",
      "تحسن تدريجي بمستوى الطالب. تعاون كبير بين الأسرة والمدرسة.",
      "اندماج الطالب في أنشطته أكثر. ثقة أكبر أثناء التعلم دائماً.",
      "تعاون جيد يعزز المسؤولية. ويقوي السلوك الإيجابي يومياً.",
      "نتائج متابعة أدت لتحسن أكاديمي. دعم واضح لاستمرار الإنجاز."
    ],
    "improve": [
      "زيادة التواصل مع الأسرة مستقبلاً. وتكثيف المتابعة لكل طالب.",
      "تحسين التوجيه المنزلي المستمر. توفير وسائل دعم تربوية جديدة.",
      "زيادة المعلومات حول الضعف بالطالب. متابعة تقدم الأداء أسبوعياً.",
      "تخصيص وقت أطول للنقاش مفيد. وتحفيز الأسرة للمشاركة أكثر.",
      "تشجيع ولي الأمر للمراجعة أكثر. دعم الطالب بتدريبات مساندة."
    ],
    "recomm": [
      "تنشيط التواصل باستمرار ضروري. وتوحيد الجهود لتحسين المستوى.",
      "دعوة الأسرة لحضور اجتماعات مهمة. وتحسين الدعم التربوي دائماً.",
      "حماية التقدم بتحفيز متواصل جداً. والمتابعة الجادة لكل المهام.",
      "تشجيع الطالب على الالتزام دوماً. ودعم التعلم المستمر بالمنزل.",
      "اتباع خطط تطوير مشتركة تماماً. وقياس أثرها لتحقيق إنجاز."
    ]
  },

  "تقرير إشعار ولي الأمر عن مستوى ابنه": {
    "goal": [
      "إبلاغ ولي الأمر بمستوى ابنه التحصيلي والسلوكي لاتخاذ إجراءات داعمة تساعد في تحسين الأداء وتعزيز نقاط القوة التعليمية.",
      "رفع وعي الأسرة بمتطلبات نجاح الطالب وتقديم معلومات دقيقة تسهم في تحسين مشاركته داخل المدرسة.",
      "تعزيز التواصل بين المدرسة والمنزل لتحديد الجوانب التي تحتاج إلى تحسين وبناء خطة مشتركة لدعم الطالب مستقبلاً.",
      "تمكين الأسرة من تتبع تطور الطالب أكاديمياً وسلوكياً بشكل مستمر لتحقيق نتائج مرضية في التحصيل الدراسي.",
      "توفير إشعار رسمي يوضح مستوى الطالب الحالي ويدعم اتخاذ خطوات عملية لتحسين الأداء ورفع الدافعية التعليمية."
    ],
    "summary": [
      "إشعار رسمي يوضح مستوى الطالب. يساعد الأسرة على دعم التحسين.",
      "تواصل مكتوب يعزز التعاون الأسري. متابعة دقيقة لمستوى الابن.",
      "تنبيه مبكر عن الضعف الموجود. دعم الطالب بشكل فعال لاحقاً.",
      "تقرير يوضح نقاط القوة لديه. وتوصيات مناسبة لتحسين الأداء.",
      "معلومات أكاديمية مهمة للأسرة. تحفيز للطالب لمستوى أفضل."
    ],
    "steps": [
      "إصدار إشعار يبين مستوى الطالب. تسليم نسخة لولي الأمر مباشرة.",
      "شرح تفاصيل الأداء للطالب والأسرة. تحديد احتياجات تحسين واقعية.",
      "اقتراح طرق دعم تعليم مستهدف. متابعة المستجدات أسبوعياً أكيداً.",
      "توفير تغذية راجعة بعد الاختبارات. تطوير الأداء عبر خطوات عملية.",
      "جلسة متابعة عند الحاجة لاحقاً. تحديد تقدم الطالب بشكل دوري."
    ],
    "strategies": [
      "إشراك الأسرة بدعم الطالب. مراقبة دورية للأداء المدرسي دائماً.",
      "تقديم خطة علاجية بسيطة واضحة. متابعة التطبيق على مدار أسبوع.",
      "تشجيع مراجعة الدروس بلا توقف. رفع الدافعية بالمكافآت المناسبة.",
      "تعاون بين المدرسة والأسرة فعلياً. بناء ثقة أكبر بالتحسن دائماً.",
      "تحليل نتائج الاختبارات أولاً. تحسين نقاط الضعف بما يناسب."
    ],
    "strengths": [
      "زيادة اهتمام الأسرة بتحسن الابن. متابعة منتظمة لأداء الطالب.",
      "تحسن تدريجي في واجباته الصفية. اندماجه مع زملائه أكثر دائماً.",
      "وضوح دور الأسرة في التطوير. تحسن إيجابي بمستوى الحضور.",
      "تحمل الطالب مسؤولية أكبر فعلاً. وارتفاع جودة التكليفات الدراسية.",
      "استجابة الأبناء للمتابعة واضحة. نتائج إيجابية بالتحصيل مميزاً."
    ],
    "improve": [
      "زيادة التدريب المنزلي للطالب جيداً. وتعزيز القراءة والكتابة فعلاً.",
      "مراجعة الدروس بشكل مستمر جداً. متابعة الأسرة أسبوعياً بانتظام.",
      "زيادة النصائح للطالب دائماً. توفير وقت أطول للمراجعة.",
      "تكثيف الجلسات المساندة لاحقاً. متابعة التحسن سريعاً تفيد الطالب.",
      "تحسين وقت الطالب بالمنزل. والحد من الملهيات نهائياً."
    ],
    "recomm": [
      "الاستمرار بمتابعة تقدم الابن. وتحفيزه عند كل إنجاز جيد.",
      "زيادة التعاون بين الأسرة والمدرسة. دعم الطالب في جميع مهامه.",
      "تنمية مهارات الطالب الأساسية دوماً. تقديم خطط دعم بسيطة ومباشرة.",
      "تبني عادات دراسية مفيدة جداً. تحسين مستوى المتابعة الأكاديمية.",
      "رفع وعي الطالب بقدراته فعلاً. تعزيز الدافعية بشكل أكبر."
    ]
  }
}
// النصوص الافتراضية (للتقارير الأخرى)
const defaultTexts = {
    goal: ["الهدف التربوي"],
    summary: ["النبذة المختصرة"],
    steps: ["إجراءات التنفيذ"],
    strategies: ["الاستراتيجيات"],
    strengths: ["نقاط القوة"],
    improve: ["نقاط التحسين"],
    recomm: ["التوصيات"]
};

let counters = {goal:0,summary:0,steps:0,strategies:0,strengths:0,improve:0,recomm:0};
let currentReportType = "تقرير نشاط إثرائي";

function getCurrentTexts() {
    const reportType = document.getElementById('reportType').value;
    return autoTextsByReportType[reportType] || defaultTexts;
}

function autoFill(id){
    const texts = getCurrentTexts();
    if (texts[id] && texts[id].length > 0) {
        counters[id] = (counters[id] + 1) % texts[id].length;
        document.getElementById(id).value = texts[id][counters[id]];
        updateReport();
    } else {
        alert("لا توجد نصوص ذكية متاحة لهذا الحقل في التقرير الحالي");
    }
}

function handleReportType(){
    const reportType = document.getElementById('reportType').value;
    currentReportType = reportType;
    
    // إعادة تعيين العدادات عند تغيير نوع التقرير
    counters = {goal:0,summary:0,steps:0,strategies:0,strengths:0,improve:0,recomm:0};
    
    // إظهار/إخفاء حقل الإدخال للنوع "أخرى"
    document.getElementById('reportTypeInput').style.display = (reportType === "أخرى") ? "block" : "none";
    updateReport();
}

function updateReport(){
    document.getElementById('educationBox').innerText = document.getElementById('education').value;
    document.getElementById('schoolBox').innerText = document.getElementById('school').value;
    document.getElementById('termBox').innerText = document.getElementById('term').value;
    document.getElementById('gradeBox').innerText = document.getElementById('grade').value;
    document.getElementById('subjectBox').innerText = document.getElementById('subject').value;
    document.getElementById('targetBox').innerText = document.getElementById('target').value;
    document.getElementById('countBox').innerText = document.getElementById('count').value;
    document.getElementById('placeBox').innerText = document.getElementById('place').value;
    document.getElementById('teacherBox').innerText = document.getElementById('teacher').value;
    document.getElementById('principalBox').innerText = document.getElementById('principal').value;
    document.getElementById('teacherTypeBox').innerText = document.getElementById('teacherType').value;
    document.getElementById('principalTypeBox').innerText = document.getElementById('principalType').value;
    const reportType = document.getElementById('reportType').value;
    document.getElementById('reportTypeBox').innerText = (reportType === "أخرى") ? document.getElementById('reportTypeInput').value : reportType;
    document.getElementById('goalBox').innerText = document.getElementById('goal').value;
    document.getElementById('summaryBox').innerText = document.getElementById('summary').value;
    document.getElementById('stepsBox').innerText = document.getElementById('steps').value;
    document.getElementById('strategiesBox').innerText = document.getElementById('strategies').value;
    document.getElementById('strengthsBox').innerText = document.getElementById('strengths').value;
    document.getElementById('improveBox').innerText = document.getElementById('improve').value;
    document.getElementById('recommBox').innerText = document.getElementById('recomm').value;
}

function loadImage(input,target){
    let r = new FileReader();
    r.onload = () => document.getElementById(target).innerHTML = `<img src="${r.result}">`;
    r.readAsDataURL(input.files[0]);
}

// دالة جديدة لحفظ بيانات المعلم فقط
function saveTeacherData(){
    // البيانات التي سيتم حفظها
    const teacherData = {
        education: document.getElementById('education').value,
        school: document.getElementById('school').value,
        grade: document.getElementById('grade').value,
        subject: document.getElementById('subject').value,
        target: document.getElementById('target').value,
        place: document.getElementById('place').value
    };
    
    // حفظ البيانات في localStorage
    localStorage.setItem('teacherData', JSON.stringify(teacherData));
    
    // عرض إشعار النجاح
    showNotification('تم حفظ بيانات المعلم بنجاح!');
    
    console.log('بيانات المعلم المحفوظة:', teacherData);
}

// دالة لعرض الإشعارات
function showNotification(message) {
    const notification = document.getElementById('saveNotification');
    notification.querySelector('span').textContent = message;
    notification.classList.add('show');
    
    setTimeout(() => {
        notification.classList.remove('show');
    }, 3000);
}

// دالة لتحميل بيانات المعلم المحفوظة عند تشغيل الصفحة
function loadTeacherData() {
    const savedData = localStorage.getItem('teacherData');
    
    if (savedData) {
        const teacherData = JSON.parse(savedData);
        
        document.getElementById('education').value = teacherData.education || '';
        document.getElementById('school').value = teacherData.school || '';
        document.getElementById('grade').value = teacherData.grade || '';
        document.getElementById('subject').value = teacherData.subject || '';
        document.getElementById('target').value = teacherData.target || '';
        document.getElementById('place').value = teacherData.place || '';
        
        updateReport();
        console.log('بيانات المعلم المحملة:', teacherData);
    }
}

// وظائف الدعم الفني
function openSupportModal() {
    document.getElementById('supportModal').style.display = 'flex';
    document.body.style.overflow = 'hidden'; // منع التمرير عند فتح النافذة
}

function closeSupportModal() {
    document.getElementById('supportModal').style.display = 'none';
    document.body.style.overflow = 'auto'; // إعادة التمرير
}

// إغلاق النافذة عند النقر خارجها
document.getElementById('supportModal').addEventListener('click', function(e) {
    if (e.target === this) {
        closeSupportModal();
    }
});

// إرسال بريد إلكتروني
function sendEmailSupport() {
    const name = document.getElementById('supportName').value || 'مستخدم بدون اسم';
    const phone = document.getElementById('supportPhone').value || 'لم يتم تقديمه';
    const issue = document.getElementById('supportIssue').value || 'لا توجد تفاصيل';
    
    const subject = encodeURIComponent('طلب دعم فني - أداة إصدار التقارير');
    const body = encodeURIComponent(`الاسم: ${name}\nرقم التواصل: ${phone}\n\nتفاصيل المشكلة:\n${issue}\n\n---\nتم الإرسال من أداة إصدار التقارير`);
    
    window.location.href = `mailto:iFahadenglish@gmail.com?subject=${subject}&body=${body}`;
    
    // إغلاق النافذة بعد إرسال البريد
    setTimeout(closeSupportModal, 500);
}

// إرسال رسالة واتساب
function sendWhatsAppSupport() {
    const name = document.getElementById('supportName').value || 'مستخدم بدون اسم';
    const phone = document.getElementById('supportPhone').value || 'لم يتم تقديمه';
    const issue = document.getElementById('supportIssue').value || 'لا توجد تفاصيل';
    
    const message = encodeURIComponent(`طلب دعم فني - أداة إصدار التقارير\n\nالاسم: ${name}\nرقم التواصل: ${phone}\n\nتفاصيل المشكلة:\n${issue}\n\n---\nتم الإرسال من أداة إصدار التقارير`);
    
    window.open(`https://wa.me/966597077245?text=${message}`, '_blank');
    
    // إغلاق النافذة بعد فتح الواتساب
    setTimeout(closeSupportModal, 500);
}

function clearData(){
    if(confirm("هل أنت متأكد من مسح جميع البيانات؟")){
        localStorage.clear();
        location.reload();
    }
}

function downloadPDF(){
    document.querySelector('.control-bar').style.visibility = 'hidden';
    document.querySelector('.top-marquee').style.visibility = 'hidden';
    document.body.style.margin = "0";
    document.body.style.background = "white";

    // إظهار قسم PDF قبل التحميل
    const reportContent = document.getElementById('report-content');
    reportContent.style.display = 'block';
    reportContent.style.visibility = 'visible';
    reportContent.style.opacity = '1';
    reportContent.style.position = 'relative';
    reportContent.style.top = '0';
    reportContent.style.left = '0';

    html2pdf().set({
        filename: "report.pdf",
        html2canvas: {
            scale: 3,
            useCORS: true,
            scrollY: 0,
            backgroundColor: '#ffffff',
            onclone: function(clonedDoc) {
                clonedDoc.getElementById('report-content').style.background = '#ffffff';
                clonedDoc.querySelectorAll('*').forEach(el => {
                    el.style.color = '';
                    el.style.backgroundColor = '';
                });
            }
        },
        jsPDF: {unit: "mm", format: "a4", orientation: "portrait"}
    })
    .from(reportContent)
    .save()
    .then(() => {
        document.querySelector('.control-bar').style.visibility = 'visible';
        document.querySelector('.top-marquee').style.visibility = 'visible';
        document.body.style.margin = "";
        document.body.style.background = "#f9fcfb";
        reportContent.style.display = 'none';
        showNotification("تم تنزيل التقرير بصيغة PDF ✓");
    });
}

async function sharePDFWhatsApp(){
    document.querySelector('.control-bar').style.visibility = 'hidden';
    document.querySelector('.top-marquee').style.visibility = 'hidden';
    document.body.style.margin = "0";
    document.body.style.background = "white";

    const reportContent = document.getElementById('report-content');
    reportContent.style.display = 'block';
    reportContent.style.visibility = 'visible';
    reportContent.style.opacity = '1';
    reportContent.style.position = 'relative';
    reportContent.style.top = '0';
    reportContent.style.left = '0';

    await html2pdf().set({
        margin: 0,
        image: {type: "jpeg", quality: 1},
        html2canvas: {
            scale: 3,
            scrollY: 0,
            useCORS: true,
            backgroundColor: '#ffffff',
            onclone: function(clonedDoc) {
                clonedDoc.getElementById('report-content').style.background = '#ffffff';
            }
        },
        jsPDF: {unit: "mm", format: "a4", orientation: "portrait"}
    })
    .from(reportContent)
    .toPdf()
    .output('blob')
    .then((pdfBlob) => {
        document.querySelector('.control-bar').style.visibility = 'visible';
        document.querySelector('.top-marquee').style.visibility = 'visible';
        document.body.style.margin = "";
        document.body.style.background = "#f9fcfb";
        reportContent.style.display = 'none';

        let file = new File([pdfBlob], "report.pdf", {type: "application/pdf"});
        if(navigator.canShare && navigator.canShare({files:[file]})){
            navigator.share({files:[file], title: "تقرير جاهز", text: "تقرير مهني جاهز للتحميل"});
        } else {
            let url = URL.createObjectURL(pdfBlob);
            window.open(`https://wa.me/?text=${encodeURIComponent("تقرير مهني جاهز للتحميل\n" + url)}`, "_blank");
        }
    });
}

async function loadDates(){
    let g = new Date();
    document.getElementById('gDate').innerText = g.toLocaleDateString('ar-EG') + " م";
    try {
        let r = await fetch(`https://api.aladhan.com/v1/gToH?date=${g.getDate()}-${g.getMonth()+1}-${g.getFullYear()}`);
        let j = await r.json();
        let h = j.data.hijri;
        document.getElementById('hDate').innerText = `${h.weekday.ar} ${h.day} ${h.month.ar} ${h.year} هـ`;
    } catch {
        document.getElementById('hDate').innerText = "--";
    }
}

// منع التكبير على الأجهزة المحمولة
document.addEventListener('touchstart', function(event) {
    if (event.touches.length > 1) {
        event.preventDefault();
    }
}, { passive: false });

let lastTouchEnd = 0;
document.addEventListener('touchend', function(event) {
    const now = (new Date()).getTime();
    if (now - lastTouchEnd <= 300) {
        event.preventDefault();
    }
    lastTouchEnd = now;
}, false);

// عند تحميل الصفحة
window.onload = function() {
    loadDates();
    loadTeacherData(); // تحميل بيانات المعلم المحفوظة
    updateReport();
    
    // تحسين الأداء على الأجهزة المحمولة
    if ('ontouchstart' in window) {
        document.body.classList.add('touch-device');
    }
}
</script>

</body>
</html>