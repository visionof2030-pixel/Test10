<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>أداة إصدار التقارير والشواهد</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;500;600;700&display=swap');
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

html, body {
    font-family: 'Cairo', sans-serif;
    background: linear-gradient(135deg, #f8fdfb 0%, #e8f2ee 100%);
    direction: rtl;
    color: #083024;
    line-height: 1.6;
}

/* الأزرار العلوية */
.btn-container {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    background: #066d4d;
    padding: 15px 20px;
    display: flex;
    justify-content: center;
    gap: 15px;
    z-index: 1000;
    box-shadow: 0 4px 12px rgba(6, 109, 77, 0.2);
}

.btn-container button {
    background: white;
    color: #066d4d;
    border: none;
    padding: 12px 25px;
    font-size: 16px;
    font-weight: 700;
    border-radius: 8px;
    cursor: pointer;
    transition: all 0.3s ease;
    min-width: 160px;
    box-shadow: 0 3px 8px rgba(0, 0, 0, 0.15);
}

.btn-container button:hover {
    background: #f0f9f5;
    transform: translateY(-2px);
    box-shadow: 0 5px 12px rgba(0, 0, 0, 0.2);
}

/* الحاوية الرئيسية */
.container {
    max-width: 1000px;
    margin: 100px auto 40px;
    padding: 0 20px;
}

/* قسم الإدخال */
.input-section {
    background: white;
    border-radius: 16px;
    padding: 30px;
    margin-bottom: 30px;
    box-shadow: 0 8px 30px rgba(6, 109, 77, 0.1);
    border: 1px solid rgba(6, 109, 77, 0.1);
}

.input-section h2 {
    color: #066d4d;
    margin-bottom: 25px;
    text-align: center;
    font-size: 24px;
    border-bottom: 2px solid #e8f2ee;
    padding-bottom: 15px;
}

/* تنسيق مجموعة الإدخال */
.input-group {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 20px;
    margin-bottom: 25px;
}

.input-group:last-child {
    margin-bottom: 0;
}

.input-field {
    display: flex;
    flex-direction: column;
}

.input-field label {
    font-weight: 700;
    color: #083024;
    margin-bottom: 8px;
    font-size: 15px;
    display: flex;
    align-items: center;
    gap: 5px;
}

.input-field label:before {
    content: "•";
    color: #066d4d;
    font-size: 18px;
}

.input-field input,
.input-field select,
.input-field textarea {
    padding: 14px 16px;
    border: 2px solid #e0f0ea;
    border-radius: 10px;
    font-size: 16px;
    font-family: 'Cairo', sans-serif;
    transition: all 0.3s ease;
    background: #f8fdfb;
}

.input-field input:focus,
.input-field select:focus,
.input-field textarea:focus {
    outline: none;
    border-color: #066d4d;
    box-shadow: 0 0 0 3px rgba(6, 109, 77, 0.1);
    background: white;
}

.input-field textarea {
    resize: vertical;
    min-height: 120px;
    line-height: 1.7;
}

/* أزرار النصوص التلقائية المحسنة */
.auto-buttons {
    margin-top: 10px;
    display: flex;
    justify-content: center;
}

.auto-btn {
    background: linear-gradient(135deg, #066d4d 0%, #083024 100%);
    color: white;
    border: none;
    padding: 10px 20px;
    border-radius: 8px;
    cursor: pointer;
    font-size: 14px;
    font-weight: 600;
    transition: all 0.3s ease;
    width: 100%;
    max-width: 200px;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    box-shadow: 0 3px 8px rgba(6, 109, 77, 0.3);
}

.auto-btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 5px 12px rgba(6, 109, 77, 0.4);
}

.auto-btn:active {
    transform: translateY(0);
}

/* قسم المعاينة */
#report-content {
    background: white;
    border-radius: 16px;
    overflow: hidden;
    box-shadow: 0 8px 30px rgba(6, 109, 77, 0.1);
    margin-bottom: 40px;
}

/* الرأس المحسن */
.header {
    background: linear-gradient(135deg, #083024 0%, #066d4d 100%);
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
    color: white;
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
    color: white;
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

/* المحتوى الرئيسي */
.page {
    padding: 30px;
}

/* شبكة المعلومات */
.info-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
    gap: 15px;
    margin-bottom: 20px;
}

.info-box {
    background: #f8fdfb;
    border: 1px solid #e0f0ea;
    border-radius: 10px;
    padding: 15px;
    text-align: center;
    box-shadow: 0 3px 10px rgba(6, 109, 77, 0.08);
}

.info-title {
    font-size: 12px;
    font-weight: 700;
    color: #066d4d;
    margin-bottom: 5px;
}

.info-value {
    font-size: 14px;
    font-weight: 600;
    color: #083024;
}

/* مربع الهدف */
.objective-box {
    background: #f0f9f5;
    border: 2px solid #066d4d;
    border-radius: 12px;
    padding: 20px;
    margin: 25px 0;
}

.objective-title {
    font-size: 18px;
    font-weight: 700;
    color: #083024;
    text-align: center;
    margin-bottom: 15px;
    padding-bottom: 10px;
    border-bottom: 2px solid #066d4d;
}

.objective-content {
    font-size: 17px;
    line-height: 1.8;
    color: #083024;
    text-align: center;
}

/* شبكة التقارير */
.report-row {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 20px;
    margin-bottom: 20px;
}

.report-box {
    background: white;
    border: 1px solid #e0f0ea;
    border-radius: 12px;
    padding: 20px;
    box-shadow: 0 4px 15px rgba(6, 109, 77, 0.08);
    transition: transform 0.3s ease;
}

.report-box:hover {
    transform: translateY(-5px);
}

.report-box-title {
    font-size: 16px;
    font-weight: 700;
    color: #066d4d;
    text-align: center;
    margin-bottom: 15px;
    padding-bottom: 10px;
    border-bottom: 1px solid #e0f0ea;
}

.report-box-content {
    font-size: 15px;
    line-height: 1.7;
    color: #083024;
    min-height: 100px;
}

/* شبكة الصور */
.image-evidence-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
    margin: 30px 0;
}

.image-box {
    border: 2px dashed #066d4d;
    border-radius: 12px;
    min-height: 180px;
    display: flex;
    align-items: center;
    justify-content: center;
    background: #f8fdfb;
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
    color: #066d4d;
    font-weight: 600;
    text-align: center;
    padding: 20px;
}

/* التوقيعات */
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
    color: #083024;
    margin-bottom: 10px;
    min-height: 24px;
}

.signature-line {
    width: 80%;
    height: 1px;
    background: #083024;
    margin: 0 auto 10px;
}

.signature-label {
    font-size: 14px;
    font-weight: 600;
    color: #066d4d;
}

/* التذييل */
.footer {
    background: #083024;
    color: white;
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
    }
    
    .input-section {
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
    
    .input-group {
        grid-template-columns: 1fr;
    }
}

@media (max-width: 480px) {
    .input-section {
        padding: 15px;
    }
    
    .page {
        padding: 20px 15px;
    }
    
    .report-box {
        padding: 15px;
    }
    
    .auto-btn {
        padding: 10px 15px;
        font-size: 13px;
    }
}

/* تخصيص شريط التمرير */
::-webkit-scrollbar {
    width: 10px;
}

::-webkit-scrollbar-track {
    background: #f1f1f1;
    border-radius: 5px;
}

::-webkit-scrollbar-thumb {
    background: #066d4d;
    border-radius: 5px;
}

::-webkit-scrollbar-thumb:hover {
    background: #083024;
}
</style>
</head>

<body>
<div class="btn-container">
    <button class="main-btn" onclick="downloadPDF()">📥 تنزيل PDF</button>
    <button class="main-btn" onclick="sharePDFWhatsApp()">📱 مشاركة واتساب</button>
</div>

<div class="container">
    <div class="input-section">
        <h2>📝 أدخل بيانات التقرير</h2>
        
        <div class="input-group">
            <div class="input-field">
                <label>إدارة التعليم</label>
                <select id="education" oninput="updateReport()">
                    <option value="">اختر الإدارة</option>
                    <option>الإدارة العامة للتعليم بمنطقة مكة المكرمة</option>
                    <option>الإدارة العامة للتعليم بمحافظة جدة</option>
                    <option>الإدارة العامة للتعليم بمنطقة الرياض</option>
                    <option>الإدارة العامة للتعليم بالمنطقة الشرقية</option>
                </select>
            </div>
            
            <div class="input-field">
                <label>نوع التقرير</label>
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
        
        <div class="input-group">
            <div class="input-field">
                <label>الصف</label>
                <input id="grade" oninput="updateReport()" placeholder="مثال: 5/3">
            </div>
            
            <div class="input-field">
                <label>الفصل الدراسي</label>
                <select id="term" oninput="updateReport()">
                    <option value="">اختر الفصل</option>
                    <option>الأول</option>
                    <option>الثاني</option>
                    <option>الثالث</option>
                </select>
            </div>
        </div>
        
        <div class="input-group">
            <div class="input-field">
                <label>المادة</label>
                <input id="subject" oninput="updateReport()" placeholder="مثال: لغتي – علوم – رياضيات">
            </div>
            
            <div class="input-field">
                <label>المستهدفون</label>
                <input id="target" oninput="updateReport()" placeholder="مثال: جميع طلاب الصف">
            </div>
        </div>
        
        <div class="input-group">
            <div class="input-field">
                <label>عدد الحضور</label>
                <input id="count" oninput="updateReport()" placeholder="مثال: 25 طالب">
            </div>
            
            <div class="input-field">
                <label>مكان التنفيذ</label>
                <input id="place" oninput="updateReport()" placeholder="مثال: داخل الصف – المختبر – قاعة مصادر التعلم">
            </div>
        </div>
        
        <div class="input-group">
            <div class="input-field">
                <label>اسم المعلم</label>
                <input id="teacher" oninput="updateReport()" placeholder="مثال: فهد الخالدي">
            </div>
            
            <div class="input-field">
                <label>اسم المدير</label>
                <input id="principal" oninput="updateReport()" placeholder="مثال: نايف اللحياني">
            </div>
        </div>
        
        <div class="input-field">
            <label>الهدف التربوي</label>
            <textarea id="goal" oninput="updateReport()" placeholder="اكتب الهدف التربوي من النشاط..."></textarea>
        </div>
        
        <div class="input-field">
            <label>نبذة مختصرة</label>
            <textarea id="summary" oninput="updateReport()" placeholder="اكتب نبذة مختصرة عن النشاط..."></textarea>
            <div class="auto-buttons">
                <button class="auto-btn" onclick="cycleAutoText('summary')">🔄 اضغط لتغيير النص</button>
            </div>
        </div>
        
        <div class="input-field">
            <label>إجراءات التنفيذ</label>
            <textarea id="steps" oninput="updateReport()" placeholder="صف إجراءات تنفيذ النشاط..."></textarea>
            <div class="auto-buttons">
                <button class="auto-btn" onclick="cycleAutoText('steps')">🔄 اضغط لتغيير النص</button>
            </div>
        </div>
        
        <div class="input-field">
            <label>الاستراتيجيات</label>
            <textarea id="strategies" oninput="updateReport()" placeholder="اذكر الاستراتيجيات المستخدمة..."></textarea>
            <div class="auto-buttons">
                <button class="auto-btn" onclick="cycleAutoText('strategies')">🔄 اضغط لتغيير النص</button>
            </div>
        </div>
        
        <div class="input-field">
            <label>نقاط القوة</label>
            <textarea id="strengths" oninput="updateReport()" placeholder="اذكر نقاط القوة في النشاط..."></textarea>
            <div class="auto-buttons">
                <button class="auto-btn" onclick="cycleAutoText('strengths')">🔄 اضغط لتغيير النص</button>
            </div>
        </div>
        
        <div class="input-field">
            <label>نقاط التحسين</label>
            <textarea id="improve" oninput="updateReport()" placeholder="اذكر نقاط التحسين الممكنة..."></textarea>
            <div class="auto-buttons">
                <button class="auto-btn" onclick="cycleAutoText('improve')">🔄 اضغط لتغيير النص</button>
            </div>
        </div>
        
        <div class="input-field">
            <label>التوصيات</label>
            <textarea id="recomm" oninput="updateReport()" placeholder="اكتب توصياتك المستقبلية..."></textarea>
            <div class="auto-buttons">
                <button class="auto-btn" onclick="cycleAutoText('recomm')">🔄 اضغط لتغيير النص</button>
            </div>
        </div>
        
        <div class="input-group">
            <div class="input-field">
                <label>الصورة 1</label>
                <input type="file" accept="image/*" onchange="loadImage(this,'imgBox1')">
            </div>
            
            <div class="input-field">
                <label>الصورة 2</label>
                <input type="file" accept="image/*" onchange="loadImage(this,'imgBox2')">
            </div>
        </div>
    </div>
    
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
// النصوص التلقائية - 5 نصوص لكل حقل
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
        const message = `تقرير ${reportTitle} - ${subject}\n\nرابط التقرير: ${pdfUrl}`;
        
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
    cycleAutoText('summary');
    cycleAutoText('steps');
    cycleAutoText('strategies');
    cycleAutoText('strengths');
    cycleAutoText('improve');
    cycleAutoText('recomm');
};
</script>
</body>
</html>