<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<title>تقرير تعليمي PDF</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap');
* { margin: 0; padding: 0; box-sizing: border-box; }
html, body { font-family: 'Cairo', sans-serif; direction: rtl; background: #ffffff; }
.btn-container {
  text-align: center; padding: 10px; background: #f5f5f5;
  position: fixed; top: 0; left: 0; width: 100%;
  z-index: 10; display: flex; gap: 10px; justify-content: center;
}
button {
  background: #066d4d; color: #ffffff; border: none;
  padding: 10px 25px; font-size: 15px; border-radius: 6px; cursor: pointer;
}
button:hover { background: #05523a; }
@media print { .btn-container { display: none; } }

/* HEADER */
.header {
  width: 100%; height: 160px;
  background-color: #083024;
  background-image: url('https://i.ibb.co/1fc5gB6v/9-C92-E57-B-23-FA-479-D-A024-1-D5-F871-B4-F8-D.png');
  background-repeat: no-repeat; background-position: center;
  background-size: 40%; margin-top: 60px;
}

/* PAGE */
.page {
  width: 100%; max-width: 830px;
  padding: 10px; margin: auto;
}

/* INFO GRID */
.info-grid {
  display: grid; grid-template-columns: repeat(auto-fit,minmax(120px,1fr));
  gap: 6px; margin-bottom: 14px;
}
.info-box {
  background-color: #eaf3ef; border-radius: 4px;
  padding: 6px; text-align: center; font-size: 11px;
  font-weight: 600; color: #083024;
}

/* OBJECTIVE */
.objective-box {
  background: #f2f9f6; border: 2px solid #066d4d;
  padding: 10px; border-radius: 6px; margin-bottom: 10px;
  min-height: 120px;
}
.objective-title {
  text-align: center; font-size: 13px; font-weight: 700;
  margin-bottom: 6px; color: #083024;
  border-bottom: 1px solid #066d4d;
}
#goal {
  min-height: 80px;
}

/* REPORT SECTIONS */
.report-row {
  display: grid; grid-template-columns: 1fr 1fr;
  gap: 8px; margin-bottom: 8px;
}
.report-box {
  background-color: #ffffff;
  border-radius: 6px;
  padding: 10px; border: 1px solid #cdd5cf;
  min-height: 120px;
}
.report-box-title {
  text-align: center; font-size: 12px; color: #083024; font-weight: 700;
  border-bottom: 1px solid #ccd9d0; margin-bottom: 6px;
}
.report-box-content {
  font-size: 11px; line-height: 1.5;
  min-height: 70px;
}

/* IMAGES */
.image-evidence-grid {
  display: grid; grid-template-columns: 1fr 1fr;
  gap: 8px; margin-top: 10px;
}
.image-box {
  height: 100px; border: 1px dashed #066d4d;
  border-radius: 6px; font-size: 11px;
  display: flex; justify-content: center; align-items: center;
  color: #066d4d;
}

/* SIGNATURES */
.signature-section {
  margin-top: 30px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 15px;
}
.signature-box {
  border-top: 1px solid #083024;
  text-align: center;
  padding-top: 8px;
  font-size: 12px;
  color: #083024;
  position: relative;
}
.signature-icon {
  font-size: 20px;
  position: absolute;
  top: -15px;
  right: 50%;
  transform: translateX(50%);
  color: #066d4d;
}

</style>
</head>

<body>

<div class="btn-container">
  <button onclick="window.print()">طباعة</button>
  <button onclick="downloadPDF()">تنزيل PDF</button>
</div>

<div id="report-content">

  <div class="header"></div>

  <div class="page">

    <div class="info-grid">
      <div class="info-box">مكان التنفيذ</div>
      <div class="info-box">المادة</div>
      <div class="info-box">الصف</div>
      <div class="info-box">عدد الطلاب</div>
      <div class="info-box">الحضور</div>
      <div class="info-box">نوع التقرير</div>
    </div>

    <div class="objective-box">
      <div class="objective-title">الهدف التربوي</div>
      <div id="goal"></div>
    </div>

    <div class="report-row">
      <div class="report-box">
        <div class="report-box-title">نبذة مختصرة</div>
        <div class="report-box-content" id="box1"></div>
      </div>

      <div class="report-box">
        <div class="report-box-title">إجراءات التنفيذ</div>
        <div class="report-box-content" id="box2"></div>
      </div>
    </div>

    <div class="report-row">
      <div class="report-box">
        <div class="report-box-title">استراتيجيات</div>
        <div class="report-box-content" id="box3"></div>
      </div>

      <div class="report-box">
        <div class="report-box-title">نقاط القوة</div>
        <div class="report-box-content" id="box4"></div>
      </div>
    </div>

    <div class="report-row">
      <div class="report-box">
        <div class="report-box-title">نقاط التحسين</div>
        <div class="report-box-content" id="box5"></div>
      </div>

      <div class="report-box">
        <div class="report-box-title">توصيات</div>
        <div class="report-box-content" id="box6"></div>
      </div>
    </div>

    <div class="image-evidence-grid">
      <div class="image-box">صورة توثيقية 1</div>
      <div class="image-box">صورة توثيقية 2</div>
    </div>

    <div class="signature-section">
      <div class="signature-box">
        <span class="signature-icon">✒️</span>
        اسم المعلم / التوقيع
      </div>
      <div class="signature-box">
        <span class="signature-icon">✒️</span>
        مدير المدرسة / التوقيع
      </div>
    </div>

  </div>
</div>

<script>
function downloadPDF(){
  var el = document.getElementById('report-content');
  html2pdf().set({
    margin: 0,
    filename: 'report.pdf',
    image: { type: 'jpeg', quality: 1 },
    html2canvas: { scale: 3, useCORS: true },
    jsPDF: { unit: 'mm', format: 'a4', orientation: 'portrait' }
  }).from(el).save();
}
</script>

</body>
</html>