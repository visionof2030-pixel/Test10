<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>أداة إصدار التقارير والشواهد</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;500;600;700&display=swap');

:root {
    --primary-color: #066d4d;
    --primary-dark: #083024;
    --primary-light: #e8f2ee;
    --secondary-color: #f8fdfb;
    --accent-color: #10b981;
    --text-dark: #083024;
    --text-light: #64748b;
    --white: #ffffff;
    --shadow: 0 4px 20px rgba(6, 109, 77, 0.1);
    --radius: 12px;
}

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

html, body {
    font-family: 'Cairo', sans-serif;
    background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
    direction: rtl;
    color: var(--text-dark);
    min-height: 100vh;
}

/* تصميم الأزرار العلوية */
.btn-container {
    position: sticky;
    top: 0;
    left: 0;
    width: 100%;
    background: var(--white);
    padding: 15px 20px;
    display: flex;
    justify-content: center;
    gap: 15px;
    z-index: 1000;
    box-shadow: var(--shadow);
    border-bottom: 2px solid var(--primary-light);
}

.btn-container button {
    background: linear-gradient(135deg, var(--primary-color) 0%, var(--primary-dark) 100%);
    color: var(--white);
    border: none;
    padding: 14px 28px;
    font-size: 16px;
    font-weight: 700;
    border-radius: var(--radius);
    cursor: pointer;
    transition: all 0.3s ease;
    min-width: 180px;
    box-shadow: 0 4px 12px rgba(6, 109, 77, 0.3);
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
}

.btn-container button:hover {
    transform: translateY(-2px);
    box-shadow: 0 6px 16px rgba(6, 109, 77, 0.4);
}

.btn-container button:active {
    transform: translateY(0);
}

/* تصميم الحاوية الرئيسية */
.container {
    max-width: 1200px;
    margin: 100px auto 40px;
    padding: 0 20px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 30px;
}

@media (max-width: 992px) {
    .container {
        grid-template-columns: 1fr;
    }
}

/* تصميم قسم الإدخال الجديد */
.input-section {
    background: var(--white);
    border-radius: var(--radius);
    padding: 30px;
    box-shadow: var(--shadow);
    border: 1px solid var(--primary-light);
    height: fit-content;
    position: sticky;
    top: 90px;
}

.input-section h2 {
    color: var(--primary-dark);
    margin-bottom: 25px;
    text-align: center;
    font-size: 24px;
    position: relative;
    padding-bottom: 15px;
}

.input-section h2::after {
    content: '';
    position: absolute;
    bottom: 0;
    right: 0;
    width: 60px;
    height: 3px;
    background: linear-gradient(to left, var(--primary-color), var(--accent-color));
    border-radius: 2px;
}

.input-section h2::before {
    content: '📝';
    margin-left: 10px;
}

/* تصميم المجموعات */
.section-group {
    margin-bottom: 30px;
    padding-bottom: 20px;
    border-bottom: 1px solid var(--primary-light);
}

.section-group:last-child {
    border-bottom: none;
    margin-bottom: 0;
}

.section-group h3 {
    color: var(--primary-color);
    margin-bottom: 20px;
    font-size: 18px;
    display: flex;
    align-items: center;
    gap: 10px;
}

/* تصميم شبكة الحقول */
.field-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
}

@media (max-width: 768px) {
    .field-grid {
        grid-template-columns: 1fr;
    }
}

/* تصميم الحقول */
.field {
    display: flex;
    flex-direction: column;
}

.field label {
    font-weight: 700;
    color: var(--text-dark);
    margin-bottom: 8px;
    font-size: 15px;
    display: flex;
    align-items: center;
    gap: 8px;
}

.field label::before {
    content: '';
    display: block;
    width: 6px;
    height: 6px;
    background: var(--primary-color);
    border-radius: 50%;
}

.field input,
.field select,
.field textarea {
    padding: 14px 16px;
    border: 2px solid var(--primary-light);
    border-radius: 10px;
    font-size: 16px;
    font-family: 'Cairo', sans-serif;
    transition: all 0.3s ease;
    background: var(--secondary-color);
    color: var(--text-dark);
}

.field input:focus,
.field select:focus,
.field textarea:focus {
    outline: none;
    border-color: var(--primary-color);
    box-shadow: 0 0 0 3px rgba(6, 109, 77, 0.1);
    background: var(--white);
}

.field textarea {
    resize: vertical;
    min-height: 120px;
    line-height: 1.7;
}

/* تصميم أزرار النصوص التلقائية المحسنة */
.auto-btn-container {
    margin-top: 15px;
    display: flex;
    justify-content: center;
}

.auto-btn {
    background: linear-gradient(135deg, var(--primary-color) 0%, var(--accent-color) 100%);
    color: var(--white);
    border: none;
    padding: 12px 24px;
    border-radius: 10px;
    cursor: pointer;
    font-size: 15px;
    font-weight: 600;
    transition: all 0.3s ease;
    width: 100%;
    max-width: 220px;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
    box-shadow: 0 4px 12px rgba(16, 185, 129, 0.3);
}

.auto-btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 6px 16px rgba(16, 185, 129, 0.4);
}

.auto-btn:active {
    transform: translateY(0);
}

/* تصميم زر رفع الصور */
.file-upload {
    position: relative;
    margin-top: 8px;
}

.file-upload input[type="file"] {
    position: absolute;
    width: 100%;
    height: 100%;
    opacity: 0;
    cursor: pointer;
}

.file-upload label {
    display: block;
    padding: 14px;
    background: var(--secondary-color);
    border: 2px dashed var(--primary-color);
    border-radius: 10px;
    text-align: center;
    cursor: pointer;
    transition: all 0.3s ease;
    color: var(--primary-color);
    font-weight: 600;
}

.file-upload label:hover {
    background: var(--primary-light);
    border-color: var(--accent-color);
}

/* قسم المعاينة - المحفوظ كما هو */
#report-content {
    background: var(--white);
    border-radius: var(--radius);
    overflow: hidden;
    box-shadow: var(--shadow);
    margin-bottom: 40px;
}

/* تصميم الرأس المحفوظ */
.header {
    background: linear-gradient(135deg, var(--primary-dark) 0%, var(--primary-color) 100%);
    padding: 25px 30px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    position: relative;
    min-height: 150px;
}

.header img {
    width: 160px;
    height: auto;
    filter: brightness(0) invert(1);
}

.header-info {
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    gap: 10px;
}

.header-right-top {
    color: var(--white);
    font-weight: 700;
    font-size: 16px;
    text-align: right;
}

.header-right-bottom {
    color: rgba(255, 255, 255, 0.9);
    font-weight: 600;
    font-size: 14px;
}

.header-left-bottom {
    position: absolute;
    left: 30px;
    bottom: 25px;
    color: var(--white);
    display: flex;
    flex-direction: column;
    gap: 8px;
    align-items: flex-start;
}

.date-hijri {
    font-size: 14px;
    font-weight: 600;
    color: rgba(255, 255, 255, 0.95);
}

.date-gregorian {
    font-size: 14px;
    font-weight: 600;
    color: rgba(255, 255, 255, 0.85);
}

/* باقي تنسيقات PDF - محفوظة كما هي */
.page {
    padding: 30px;
}

.info-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
    gap: 15px;
    margin-bottom: 20px;
}

.info-box {
    background: var(--primary-light);
    border: 1px solid var(--primary-light);
    border-radius: 10px;
    padding: 15px;
    text-align: center;
    box-shadow: 0 3px 10px rgba(6, 109, 77, 0.08);
}

.info-title {
    font-size: 12px;
    font-weight: 700;
    color: var(--primary-color);
    margin-bottom: 5px;
}

.info-value {
    font-size: 14px;
    font-weight: 600;
    color: var(--primary-dark);
}

.objective-box {
    background: var(--secondary-color);
    border: 2px solid var(--primary-color);
    border-radius: 12px;
    padding: 20px;
    margin: 25px 0;
}

.objective-title {
    font-size: 18px;
    font-weight: 700;
    color: var(--primary-dark);
    text-align: center;
    margin-bottom: 15px;
    padding-bottom: 10px;
    border-bottom: 2px solid var(--primary-color);
}

.objective-content {
    font-size: 17px;
    line-height: 1.8;
    color: var(--primary-dark);
    text-align: center;
}

.report-row {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 20px;
    margin-bottom: 20px;
}

.report-box {
    background: var(--white);
    border: 1px solid var(--primary-light);
    border-radius: 12px;
    padding: 20px;
    box-shadow: 0 4px 15px rgba(6, 109, 77, 0.08);
}

.report-box-title {
    font-size: 16px;
    font-weight: 700;
    color: var(--primary-color);
    text-align: center;
    margin-bottom: 15px;
    padding-bottom: 10px;
    border-bottom: 1px solid var(--primary-light);
}

.report-box-content {
    font-size: 15px;
    line-height: 1.7;
    color: var(--primary-dark);
    min-height: 100px;
}

.image-evidence-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
    margin: 30px 0;
}

.image-box {
    border: 2px dashed var(--primary-color);
    border-radius: 12px;
    min-height: 180px;
    display: flex;
    align-items: center;
    justify-content: center;
    background: var(--secondary-color);
    overflow: hidden;
    padding: 15px;
}

.image-box img {
    max-width: 100%;
    max-height: 100%;
    object-fit: contain;
    border-radius: 8px;
}

.image-placeholder {
    color: var(--primary-color);
    font-weight: 600;
    text-align: center;
    padding: 20px;
}

.signature-section {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 30px;
    margin: 30px 0;
}

.signature-box {
    text-align: center;
}

.signature-name {
    font-size: 16px;
    font-weight: 700;
    color: var(--primary-dark);
    margin-bottom: 10px;
    min-height: 24px;
}

.signature-line {
    width: 80%;
    height: 1px;
    background: var(--primary-dark);
    margin: 0 auto 10px;
}

.signature-label {
    font-size: 14px;
    font-weight: 600;
    color: var(--primary-color);
}

.footer {
    background: var(--primary-dark);
    color: var(--white);
    text-align: center;
    padding: 15px;
    font-size: 14px;
    font-weight: 600;
}

/* تحسينات للجوال */
@media (max-width: 768px) {
    .btn-container {
        flex-direction: column;
        align-items: center;
        padding: 12px 15px;
    }
    
    .btn-container button {
        width: 100%;
        max-width: 300px;
        margin-bottom: 8px;
    }
    
    .container {
        margin-top: 140px;
        padding: 0 15px;
        grid-template-columns: 1fr;
    }
    
    .input-section {
        position: static;
        padding: 20px;
    }
    
    .header {
        flex-direction: column;
        text-align: center;
        padding: 20px;
        gap: 15px;
    }
    
    .header-info {
        align-items: center;
    }
    
    .header-left-bottom {
        position: relative;
        left: 0;
        bottom: 0;
        align-items: center;
        margin-top: 15px;
    }
    
    .info-grid,
    .report-row,
    .signature-section {
        grid-template-columns: 1fr;
    }
}

/* تأثيرات إضافية */
.field input:invalid,
.field select:invalid,
.field textarea:invalid {
    border-color: #ef4444;
}

.field input:valid:not(:placeholder-shown),
.field select:valid,
.field textarea:valid:not(:placeholder-shown) {
    border-color: #10b981;
}

/* تخصيص شريط التمرير */
::-webkit-scrollbar {
    width: 10px;
}

::-webkit-scrollbar-track {
    background: var(--primary-light);
    border-radius: 5px;
}

::-webkit-scrollbar-thumb {
    background: linear-gradient(var(--primary-color), var(--primary-dark));
    border-radius: 5px;
}

::-webkit-scrollbar-thumb:hover {
    background: linear-gradient(var(--primary-dark), var(--primary-color));
}

/* تأثيرات للتفعيل */
@keyframes pulse {
    0% { box-shadow: 0 0 0 0 rgba(6, 109, 77, 0.4); }
    70% { box-shadow: 0 0 0 10px rgba(6, 109, 77, 0); }
    100% { box-shadow: 0 0 0 0 rgba(6, 109, 77, 0); }
}

.auto-btn.pulsing {
    animation: pulse 2s infinite;
}

/* تحسين العناوين */
.section-group h3::before {
    font-size: 20px;
    margin-left: 5px;
}

.section-group:nth-child(1) h3::before { content: "🏫"; }
.section-group:nth-child(2) h3::before { content: "📚"; }
.section-group:nth-child(3) h3::before { content: "🎯"; }
.section-group:nth-child(4) h3::before { content: "📊"; }
.section-group:nth-child(5) h3::before { content: "📸"; }
</style>
</head>

<body>
<div class="btn-container">
    <button onclick="downloadPDF()">
        <span>📥</span>
        تنزيل PDF
    </button>
    <button onclick="sharePDFWhatsApp()">
        <span>📱</span>
        مشاركة واتساب
    </button>
</div>

<div class="container">
    <!-- قسم الإدخال الجديد -->
    <div class="input-section">
        <h2>بيانات التقرير</h2>
        
        <!-- المجموعة الأولى: المعلومات الأساسية -->
        <div class="section-group">
            <h3>المعلومات الأساسية</h3>
            <div class="field-grid">
                <div class="field">
                    <label for="education">إدارة التعليم</label>
                    <select id="education" oninput="updateReport()">
                        <option value="">اختر الإدارة</option>
                        <option>الإدارة العامة للتعليم بمنطقة مكة المكرمة</option>
                        <option>الإدارة العامة للتعليم بمحافظة جدة</option>
                        <option>الإدارة العامة للتعليم بمنطقة الرياض</option>
                        <option>الإدارة العامة للتعليم بالمنطقة الشرقية</option>
                    </select>
                </div>
                
                <div class="field">
                    <label for="reportType">نوع التقرير</label>
                    <select id="reportType" oninput="handleReportType()">
                        <option value="">اختر نوع التقرير</option>
                        <option>تقرير نشاط إثرائي</option>
                        <option>تقرير زيارة ميدانية</option>
                        <option>تقرير ورشة عمل</option>
                        <option>تقرير ندوة</option>
                        <option>أخرى</option>
                    </select>
                    <input id="reportTypeInput" oninput="updateReport()" placeholder="اكتب اسم التقرير يدوياً" style="display:none; margin-top: 10px;">
                </div>
            </div>
        </div>
        
        <!-- المجموعة الثانية: المعلومات الأكاديمية -->
        <div class="section-group">
            <h3>المعلومات الأكاديمية</h3>
            <div class="field-grid">
                <div class="field">
                    <label for="grade">الصف</label>
                    <input id="grade" oninput="updateReport()" placeholder="مثال: 5/3">
                </div>
                
                <div class="field">
                    <label for="term">الفصل الدراسي</label>
                    <select id="term" oninput="updateReport()">
                        <option value="">اختر الفصل</option>
                        <option>الأول</option>
                        <option>الثاني</option>
                        <option>الثالث</option>
                    </select>
                </div>
                
                <div class="field">
                    <label for="subject">المادة</label>
                    <input id="subject" oninput="updateReport()" placeholder="مثال: لغتي – علوم – رياضيات">
                </div>
            </div>
        </div>
        
        <!-- المجموعة الثالثة: تفاصيل النشاط -->
        <div class="section-group">
            <h3>تفاصيل النشاط</h3>
            <div class="field-grid">
                <div class="field">
                    <label for="target">المستهدفون</label>
                    <input id="target" oninput="updateReport()" placeholder="مثال: جميع طلاب الصف">
                </div>
                
                <div class="field">
                    <label for="count">عدد الحضور</label>
                    <input id="count" oninput="updateReport()" placeholder="مثال: 25 طالب">
                </div>
                
                <div class="field">
                    <label for="place">مكان التنفيذ</label>
                    <input id="place" oninput="updateReport()" placeholder="مثال: داخل الصف – المختبر – قاعة مصادر التعلم">
                </div>
            </div>
        </div>
        
        <!-- المجموعة الرابعة: محتوى التقرير -->
        <div class="section-group">
            <h3>محتوى التقرير</h3>
            <div class="field-grid">
                <div class="field">
                    <label for="teacher">اسم المعلم</label>
                    <input id="teacher" oninput="updateReport()" placeholder="مثال: فهد الخالدي">
                </div>
                
                <div class="field">
                    <label for="principal">اسم المدير</label>
                    <input id="principal" oninput="updateReport()" placeholder="مثال: نايف اللحياني">
                </div>
            </div>
            
            <div class="field" style="grid-column: 1/-1;">
                <label for="goal">الهدف التربوي</label>
                <textarea id="goal" oninput="updateReport()" placeholder="اكتب الهدف التربوي من النشاط..."></textarea>
            </div>
            
            <div class="field" style="grid-column: 1/-1;">
                <label for="summary">نبذة مختصرة</label>
                <textarea id="summary" oninput="updateReport()" placeholder="اكتب نبذة مختصرة عن النشاط..."></textarea>
                <div class="auto-btn-container">
                    <button class="auto-btn" onclick="cycleAutoText('summary')">
                        <span>🔄</span>
                        اضغط لتغيير النص
                    </button>
                </div>
            </div>
            
            <div class="field" style="grid-column: 1/-1;">
                <label for="steps">إجراءات التنفيذ</label>
                <textarea id="steps" oninput="updateReport()" placeholder="صف إجراءات تنفيذ النشاط..."></textarea>
                <div class="auto-btn-container">
                    <button class="auto-btn" onclick="cycleAutoText('steps')">
                        <span>🔄</span>
                        اضغط لتغيير النص
                    </button>
                </div>
            </div>
            
            <div class="field" style="grid-column: 1/-1;">
                <label for="strategies">الاستراتيجيات</label>
                <textarea id="strategies" oninput="updateReport()" placeholder="اذكر الاستراتيجيات المستخدمة..."></textarea>
                <div class="auto-btn-container">
                    <button class="auto-btn" onclick="cycleAutoText('strategies')">
                        <span>🔄</span>
                        اضغط لتغيير النص
                    </button>
                </div>
            </div>
            
            <div class="field" style="grid-column: 1/-1;">
                <label for="strengths">نقاط القوة</label>
                <textarea id="strengths" oninput="updateReport()" placeholder="اذكر نقاط القوة في النشاط..."></textarea>
                <div class="auto-btn-container">
                    <button class="auto-btn" onclick="cycleAutoText('strengths')">
                        <span>🔄</span>
                        اضغط لتغيير النص
                    </button>
                </div>
            </div>
            
            <div class="field" style="grid-column: 1/-1;">
                <label for="improve">نقاط التحسين</label>
                <textarea id="improve" oninput="updateReport()" placeholder="اذكر نقاط التحسين الممكنة..."></textarea>
                <div class="auto-btn-container">
                    <button class="auto-btn" onclick="cycleAutoText('improve')">
                        <span>🔄</span>
                        اضغط لتغيير النص
                    </button>
                </div>
            </div>
            
            <div class="field" style="grid-column: 1/-1;">
                <label for="recomm">التوصيات</label>
                <textarea id="recomm" oninput="updateReport()" placeholder="اكتب توصياتك المستقبلية..."></textarea>
                <div class="auto-btn-container">
                    <button class="auto-btn" onclick="cycleAutoText('recomm')">
                        <span>🔄</span>
                        اضغط لتغيير النص
                    </button>
                </div>
            </div>
        </div>
        
        <!-- المجموعة الخامسة: الوسائط -->
        <div class="section-group">
            <h3>الوسائط التوثيقية</h3>
            <div class="field-grid">
                <div class="field">
                    <label>الصورة 1</label>
                    <div class="file-upload">
                        <input type="file" accept="image/*" onchange="loadImage(this,'imgBox1')">
                        <label>📷 اختر صورة 1</label>
                    </div>
                </div>
                
                <div class="field">
                    <label>الصورة 2</label>
                    <div class="file-upload">
                        <input type="file" accept="image/*" onchange="loadImage(this,'imgBox2')">
                        <label>📷 اختر صورة 2</label>
                    </div>
                </div>
            </div>
        </div>
    </div>
    
    <!-- قسم المعاينة - لم يتم تغييره -->
    <div id="report-content">
        <div class="header">
            <img src="https://i.ibb.co/1fc5gB6v/9-C92-E57-B-23-FA-479-D-A024-1-D5-F871-B4-F8-D.png" alt="شعار">
            <div class="header-info">
                <div class="header-right-top" id="educationBox"></div>
                <div class="header-right-bottom">مدرسة سعيد بن العاص</div>
            </div>
            <div class="header-left-bottom">
                <div class="date-hijri" id="hDate"></div>
                <div class="date-gregorian" id="gDate"></div>
            </div>
        </div>
        
        <div class="page">
            <div class="info-grid">
                <div class="info-box">
                    <div class="info-title">الفصل الدراسي</div>
                    <div class="info-value" id="termBox"></div>
                </div>
                <div class="info-box">
                    <div class="info-title">الصف</div>
                    <div class="info-value" id="gradeBox"></div>
                </div>
                <div class="info-box">
                    <div class="info-title">المادة</div>
                    <div class="info-value" id="subjectBox"></div>
                </div>
                <div class="info-box">
                    <div class="info-title">نوع التقرير</div>
                    <div class="info-value" id="reportTypeBox"></div>
                </div>
            </div>
            
            <div class="info-grid">
                <div class="info-box">
                    <div class="info-title">المستهدفون</div>
                    <div class="info-value" id="targetBox"></div>
                </div>
                <div class="info-box">
                    <div class="info-title">عدد الحضور</div>
                    <div class="info-value" id="countBox"></div>
                </div>
                <div class="info-box">
                    <div class="info-title">مكان التنفيذ</div>
                    <div class="info-value" id="placeBox"></div>
                </div>
            </div>
            
            <div class="objective-box">
                <div class="objective-title">الهدف التربوي</div>
                <div class="objective-content" id="goalBox"></div>
            </div>
            
            <div class="report-row">
                <div class="report-box">
                    <div class="report-box-title">نبذة مختصرة</div>
                    <div class="report-box-content" id="summaryBox"></div>
                </div>
                <div class="report-box">
                    <div class="report-box-title">إجراءات التنفيذ</div>
                    <div class="report-box-content" id="stepsBox"></div>
                </div>
            </div>
            
            <div class="report-row">
                <div class="report-box">
                    <div class="report-box-title">الاستراتيجيات المستخدمة</div>
                    <div class="report-box-content" id="strategiesBox"></div>
                </div>
                <div class="report-box">
                    <div class="report-box-title">نقاط القوة</div>
                    <div class="report-box-content" id="strengthsBox"></div>
                </div>
            </div>
            
            <div class="report-row">
                <div class="report-box">
                    <div class="report-box-title">نقاط التحسين</div>
                    <div class="report-box-content" id="improveBox"></div>
                </div>
                <div class="report-box">
                    <div class="report-box-title">التوصيات</div>
                    <div class="report-box-content" id="recommBox"></div>
                </div>
            </div>
            
            <div class="image-evidence-grid">
                <div class="image-box" id="imgBox1">
                    <div class="image-placeholder">صورة توثيقية 1</div>
                </div>
                <div class="image-box" id="imgBox2">
                    <div class="image-placeholder">صورة توثيقية 2</div>
                </div>
            </div>
            
            <div class="signature-section">
                <div class="signature-box">
                    <div class="signature-name" id="teacherBox"></div>
                    <div class="signature-line"></div>
                    <div class="signature-label">المعلم</div>
                </div>
                <div class="signature-box">
                    <div class="signature-name" id="principalBox"></div>
                    <div class="signature-line"></div>
                    <div class="signature-label">مدير المدرسة</div>
                </div>
            </div>
            
            <div class="footer">وزارة التعليم – المملكة العربية السعودية</div>
        </div>
    </div>
</div>

<script>
// النصوص التلقائية - 5 نصوص لكل حقل (16 كلمة لكل نص)
const autoTexts = {
    summary: [
        "تم تنفيذ النشاط بنجاح داخل الصف الدراسي بمشاركة جميع الطلاب بشكل إيجابي وفعال مما ساهم في تحقيق الأهداف التعليمية المخطط لها بكل دقة واحترافية.",
        "تفاعل الطلاب بشكل ملحوظ خلال النشاط التعليمي مما أظهر تحسناً كبيراً في استيعاب المفاهيم المطروحة وتطبيقها بشكل عملي متميز وجدير بالثناء.",
        "شهد النشاط مشاركة واسعة من الطلاب الذين أظهروا حماساً وتفاعلاً إيجابياً مع المحتوى المقدم مما أدى إلى تحقيق النتائج المرجوة بكل كفاءة واحترافية.",
        "تميز النشاط بتنوع الأساليب التعليمية المستخدمة والتي ساهمت في جذب انتباه الطلاب وزيادة دافعيتهم للتعلم وتحقيق أفضل النتائج التعليمية الممكنة.",
        "أظهر النشاط نتائج إيجابية على تحصيل الطلاب التعليمي مع تحسن ملحوظ في مهارات التفكير النقدي لديهم مما يعكس نجاح التخطيط والتنفيذ الدقيق."
    ],
    steps: [
        "بدأ النشاط بشرح مفصل للأهداف ثم تقسيم الطلاب إلى مجموعات عمل تعاونية نفذت المهام المطلوبة بدقة متناهية وإشراف مباشر من المعلم.",
        "تضمن التنفيذ عرضاً تقديمياً للمحتوى ثم تدريبات عملية وتفاعلية شارك فيها جميع الطلاب بشكل إيجابي ومثمر لتحقيق الأهداف المطلوبة.",
        "تم تقديم شرح نظري للمفاهيم الأساسية ثم تطبيق عملي من قبل الطلاب مع مناقشة النتائج وتقويم الأداء بشكل مستمر ومنهجي ودقيق.",
        "بدأ النشاط بتحديد الأهداف ثم تقسيم الطلاب إلى فرق عمل نفذت أنشطة متنوعة تحت إشراف المعلم الذي قدم التوجيهات اللازمة بدقة.",
        "شمل التنفيذ جلسة شرح تفاعلية ثم أنشطة جماعية وتقييم مستمر للأداء مع توفير تغذية راجعة فورية للطلاب لتحسين تعلمهم."
    ],
    strategies: [
        "استخدام التعلم التعاوني والعمل الجماعي لتعزيز مهارات التواصل والتفكير النقدي لدى الطلاب مع دعم استقلاليتهم في البحث والتعلم.",
        "توظيف استراتيجيات التعلم النشط والعصف الذهني لتحفيز التفكير الإبداعي وتنمية مهارات حل المشكلات بطرق مبتكرة وفعالة.",
        "تطبيق التمايز التعليمي لمواكبة الفروق الفردية مع استخدام التقويم التكويني المستمر لتتبع التقدم وتوجيه التعلم بشكل فعال.",
        "اعتماد استراتيجية المحاكاة والتمثيل لتعزيز الفهم العميق مع استخدام التقنيات الحديثة لدعم عملية التعليم والتعلم بشكل متكامل.",
        "استخدام خرائط المفاهيم والتعلم القائم على المشاريع لتعزيز الربط بين الأفكار وتطبيق المعرفة في مواقف حياتية واقعية ومفيدة."
    ],
    strengths: [
        "مشاركة فعالة من جميع الطلاب مع تفاعل إيجابي وملاحظة تحسن واضح في مستوى الفهم والاستيعاب للمفاهيم المطروحة بشكل منهجي.",
        "تنوع الأنشطة وملاءمتها لمستويات الطلاب المختلفة مع وجود بيئة تعليمية محفزة وداعمة للإبداع والتميز الأكاديمي الواضح.",
        "التزام الطلاب بتعليمات النشاط مع إظهار روح التعاون والعمل الجماعي والمبادرة في تقديم الأفكار والحلول المبتكرة والمفيدة.",
        "تحقيق الأهداف التعليمية بكفاءة عالية مع ملاحظة تطور مهارات التفكير العليا لدى الطلاب وزيادة ثقتهم بأنفسهم وقدراتهم.",
        "تفعيل دور الطالب كمحور للعملية التعليمية مع تنمية مهارات البحث والاستكشاف والتحليل لديهم بشكل منهجي ومتميز وفعال."
    ],
    improve: [
        "زيادة وقت الأنشطة التطبيقية لتوفير فرص أكثر للطلاب لممارسة المهارات وتطبيق المفاهيم بشكل أوسع وأكثر فعالية وواقعية.",
        "توفير مصادر تعليمية إضافية ومتنوعة لدعم الفروق الفردية وتلبية احتياجات جميع الطلاب بكل فئاتهم وقدراتهم المختلفة.",
        "تنويع أساليب التقويم لتشمل أدوات أكثر موضوعية مع زيادة التركيز على الجوانب التطبيقية والمهارات العملية للطلاب.",
        "تطوير بيئة الصف لتكون أكثر تحفيزاً للإبداع مع توفير تقنيات تعليمية متطورة تواكب التطورات الحديثة في مجال التعليم.",
        "تعزيز الشراكة مع أولياء الأمور لدعم تعلم الطلاب خارج المدرسة مع تنظيم زيارات ميدانية لربط التعليم بالواقع العملي."
    ],
    recomm: [
        "الاستمرار في تطبيق الأنشطة التفاعلية التي تنمي مهارات التفكير مع تحديث المحتوى ليكون أكثر ارتباطاً بواقع حياة الطلاب اليومية.",
        "توسيع نطاق استخدام التقنيات التعليمية الحديثة وتدريب المعلمين على أفضل الممارسات العالمية في مجال التعليم والتعلم الفعال.",
        "تعزيز الشراكة المجتمعية مع المؤسسات التعليمية الأخرى لتبادل الخبرات وتطوير البرامج التعليمية بشكل مستمر ومتجددة.",
        "تطوير بنك من الأنشطة الإثرائية المتنوعة التي تلبي احتياجات جميع الطلاب مع التركيز على الجوانب التطبيقية والعملية.",
        "تنظيم ورش عمل للمعلمين لتبادل الخبرات حول أفضل استراتيجيات التعلم مع متابعة تطبيقها داخل الصفوف الدراسية المختلفة."
    ]
};

// تتبع النص الحالي لكل حقل
let currentTextIndex = {
    summary: 0,
    steps: 0,
    strategies: 0,
    strengths: 0,
    improve: 0,
    recomm: 0
};

// دورة النصوص التلقائية
function cycleAutoText(field) {
    const textArray = autoTexts[field];
    currentTextIndex[field] = (currentTextIndex[field] + 1) % textArray.length;
    document.getElementById(field).value = textArray[currentTextIndex[field]];
    updateReport();
    
    // تأثير بسيط للزر
    const btn = event.target.closest('.auto-btn');
    btn.classList.add('pulsing');
    setTimeout(() => btn.classList.remove('pulsing'), 2000);
}

// تحديث التقرير
function updateReport() {
    // تحديث المعلومات الأساسية
    document.getElementById('educationBox').textContent = document.getElementById('education').value;
    document.getElementById('termBox').textContent = document.getElementById('term').value;
    document.getElementById('gradeBox').textContent = document.getElementById('grade').value;
    document.getElementById('subjectBox').textContent = document.getElementById('subject').value;
    document.getElementById('targetBox').textContent = document.getElementById('target').value;
    document.getElementById('countBox').textContent = document.getElementById('count').value;
    document.getElementById('placeBox').textContent = document.getElementById('place').value;
    document.getElementById('teacherBox').textContent = document.getElementById('teacher').value;
    document.getElementById('principalBox').textContent = document.getElementById('principal').value;
    
    // تحديث نوع التقرير
    const reportType = document.getElementById('reportType').value;
    const reportTypeInput = document.getElementById('reportTypeInput');
    
    if (reportType === "أخرى") {
        document.getElementById('reportTypeBox').textContent = reportTypeInput.value || "تقرير";
    } else {
        document.getElementById('reportTypeBox').textContent = reportType;
    }
    
    // تحديث المحتوى
    document.getElementById('goalBox').textContent = document.getElementById('goal').value;
    document.getElementById('summaryBox').textContent = document.getElementById('summary').value;
    document.getElementById('stepsBox').textContent = document.getElementById('steps').value;
    document.getElementById('strategiesBox').textContent = document.getElementById('strategies').value;
    document.getElementById('strengthsBox').textContent = document.getElementById('strengths').value;
    document.getElementById('improveBox').textContent = document.getElementById('improve').value;
    document.getElementById('recommBox').textContent = document.getElementById('recomm').value;
}

// التعامل مع نوع التقرير
function handleReportType() {
    const reportType = document.getElementById('reportType');
    const reportTypeInput = document.getElementById('reportTypeInput');
    
    if (reportType.value === "أخرى") {
        reportTypeInput.style.display = "block";
    } else {
        reportTypeInput.style.display = "none";
    }
    updateReport();
}

// تحميل الصور
function loadImage(input, target) {
    const file = input.files[0];
    if (file) {
        const reader = new FileReader();
        reader.onload = function(e) {
            const imgBox = document.getElementById(target);
            imgBox.innerHTML = `<img src="${e.target.result}" alt="صورة توثيقية">`;
        };
        reader.readAsDataURL(file);
    }
}

// تنزيل PDF
function downloadPDF() {
    const element = document.getElementById('report-content');
    
    // إضافة تأثير للزر
    const btn = event.target;
    btn.style.transform = 'scale(0.95)';
    setTimeout(() => btn.style.transform = '', 200);
    
    html2pdf().set({
        margin: [10, 10, 10, 10],
        filename: 'تقرير_نشاط.pdf',
        image: { type: 'jpeg', quality: 1 },
        html2canvas: { 
            scale: 2,
            useCORS: true,
            scrollY: 0
        },
        jsPDF: { 
            unit: 'mm', 
            format: 'a4', 
            orientation: 'portrait' 
        }
    }).from(element).save();
}

// مشاركة عبر واتساب
async function sharePDFWhatsApp() {
    try {
        // إضافة تأثير للزر
        const btn = event.target;
        btn.style.transform = 'scale(0.95)';
        setTimeout(() => btn.style.transform = '', 200);
        
        const element = document.getElementById('report-content');
        
        const pdfBlob = await html2pdf().from(element).set({
            margin: [10, 10, 10, 10],
            image: { type: 'jpeg', quality: 1 },
            html2canvas: { 
                scale: 2,
                useCORS: true,
                scrollY: 0
            },
            jsPDF: { 
                unit: 'mm', 
                format: 'a4', 
                orientation: 'portrait' 
            }
        }).outputPdf('blob');
        
        // إنشاء رابط للملف
        const pdfUrl = URL.createObjectURL(pdfBlob);
        
        // إنشاء نص للمشاركة
        const reportTitle = document.getElementById('reportTypeBox').textContent || 'تقرير';
        const subject = document.getElementById('subjectBox').textContent || '';
        const message = `📋 تقرير ${reportTitle}\n📚 المادة: ${subject}\n📅 التاريخ: ${document.getElementById('gDate').textContent}\n\nتم إنشاء التقرير باستخدام أداة إصدار التقارير`;
        
        // فتح واتساب مع الرسالة
        window.open(`https://wa.me/?text=${encodeURIComponent(message)}`, '_blank');
        
    } catch (error) {
        alert('حدث خطأ أثناء تحضير الملف للمشاركة: ' + error.message);
    }
}

// تحميل التواريخ الهجرية والميلادية
async function loadDates() {
    const today = new Date();
    
    // التاريخ الميلادي
    const gregorianDate = today.toLocaleDateString('ar-SA', {
        year: 'numeric',
        month: 'long',
        day: 'numeric'
    });
    
    document.getElementById('gDate').textContent = gregorianDate;
    
    // التاريخ الهجري
    try {
        const response = await fetch(`https://api.aladhan.com/v1/gToH/${today.getDate()}-${today.getMonth() + 1}-${today.getFullYear()}`);
        const data = await response.json();
        
        if (data.code === 200) {
            const hijriDate = data.data.hijri;
            const hijriDateString = `${hijriDate.day} ${hijriDate.month.ar} ${hijriDate.year} هـ`;
            document.getElementById('hDate').textContent = hijriDateString;
        } else {
            document.getElementById('hDate').textContent = "تاريخ هجري غير متوفر";
        }
    } catch (error) {
        console.error('Error fetching Hijri date:', error);
        document.getElementById('hDate').textContent = "تاريخ هجري غير متوفر";
    }
}

// تهيئة الصفحة
window.onload = function() {
    loadDates();
    
    // تعبئة النصوص التلقائية عند التحميل
    setTimeout(() => {
        cycleAutoText('summary');
        cycleAutoText('steps');
        cycleAutoText('strategies');
        cycleAutoText('strengths');
        cycleAutoText('improve');
        cycleAutoText('recomm');
    }, 500);
    
    // إضافة بعض البيانات الافتراضية للمساعدة في الاختبار
    document.getElementById('education').value = "الإدارة العامة للتعليم بمنطقة مكة المكرمة";
    document.getElementById('reportType').value = "تقرير نشاط إثرائي";
    document.getElementById('grade').value = "5/3";
    document.getElementById('term').value = "الأول";
    document.getElementById('subject').value = "لغتي";
    document.getElementById('target').value = "جميع طلاب الصف";
    document.getElementById('count').value = "25 طالب";
    document.getElementById('place').value = "داخل الصف";
    document.getElementById('teacher').value = "فهد الخالدي";
    document.getElementById('principal').value = "نايف اللحياني";
    document.getElementById('goal').value = "تنمية مهارات الطلاب من خلال أنشطة تعليمية تفاعلية تعزز التفكير والمعرفة بشكل فعال وواضح للجميع.";
    
    updateReport();
};
</script>
</body>
</html>