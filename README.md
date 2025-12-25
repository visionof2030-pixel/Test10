
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<title>تقرير تعليمي PDF</title>

<script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap');

* { margin: 0; padding: 0; box-sizing: border-box; }

html, body {
  font-family: 'Cairo', sans-serif;
  background: #ffffff;
  width: 100%;
  direction: rtl;
}

.btn-container {
  text-align: center;
  padding: 10px;
  background: #f5f5f5;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 10;
  display: flex;
  gap: 10px;
  justify-content: center;
}

button {
  background: #066d4d;
  color: #ffffff;
  border: none;
  padding: 10px 25px;
  font-size: 15px;
  border-radius: 6px;
  cursor: pointer;
}

button:hover { background: #05523a; }

@media print { .btn-container { display: none; } }

.top-bar {
  width: 100%;
  height: 130px;
  background-color: #0e2b22;
  display: flex;
  justify-content: center;
  align-items: center;
}

.top-bar img {
  width: 260px;
  opacity: 1;
}

.header-info {
  width: 95%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 6px 10px;
  color: #083024;
  font-size: 10px;
  margin-top: 6px;
}

.page {
  width: 100%;
  padding: 10px;
  background: #fff;
  margin: auto;
}

.info-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
  gap: 4px;
  margin-bottom: 6px;
}

.info-box {
  background-color: #eaf3ef;
  border-radius: 4px;
  padding: 6px;
  text-align: center;
  font-size: 10px;
  line-height: 1.3;
}

.info-box strong { font-size: 11px; color: #083024; display: block; }

.report-objective-box {
  background: rgba(8,48,36,0.1);
  border-radius: 6px;
  padding: 12px;
  margin-bottom: 8px;
  font-size: 12px;
  text-align: center;
  color: #083024;
}

.report-grid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 6px;
  margin-bottom: 8px;
}

.report-box {
  border-radius: 6px;
  padding: 16px;
  min-height: 120px;
}

.report-box-title {
  font-size: 12px;
  margin-bottom: 4px;
  text-align: center;
  font-weight: bold;
}

.report-box-content {
  font-size: 10px;
  white-space: pre-line;
  line-height: 1.5;
}

.box-color-1 { background: #ffecec; color: #5b1e1e; }
.box-color-2 { background: #e6f6e6; color: #245c24; }
.box-color-3 { background: #fff0e6; color: #7c4c00; }
.box-color-4 { background: #e8f1ff; color: #22386c; }
.box-color-5 { background: #fff7e8; color: #5a4a00; }
.box-color-6 { background: #f1e8ff; color: #4d339b; }

.image-evidence-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 8px;
  margin-top: 8px;
}

.image-box {
  border-radius: 6px;
  background: rgba(8,48,36,0.08);
  height: 100px;
  font-size: 11px;
  display: flex;
  align-items: center;
  justify-content: center;
}

@media (min-width: 600px) {
  .page { width: 850px; }
}
</style>
</head>

<body>

<div class="btn-container">
  <button onclick="window.print()">طباعة</button>
  <button onclick="downloadPDF()">تنزيل PDF</button>
</div>

<div id="report-content">

  <div class="top-bar">
    <img src="https://i.ibb.co/1fc5gB6v/9-C92-E57-B-23-FA-479-D-A024-1-D5-F871-B4-F8-D.png">
  </div>

  <div class="header-info">
    <div id="leader"></div>
    <div id="school"></div>
    <div id="date"></div>
  </div>

  <div class="page">

    <div class="info-grid">
      <div class="info-box"><strong>اسم المعلم</strong> <span id="teacher"></span></div>
      <div class="info-box"><strong>المادة</strong> <span id="subject"></span></div>
      <div class="info-box"><strong>الصف</strong> <span id="grade"></span></div>
      <div class="info-box"><strong>عدد الطلاب</strong> <span id="students"></span></div>
      <div class="info-box"><strong>الحضور</strong> <span id="attendance"></span></div>
      <div class="info-box"><strong>نوع التقرير</strong> <span id="type"></span></div>
    </div>

    <div class="report-objective-box" id="objective"></div>

    <div class="report-grid">
      <div class="report-box box-color-1">
        <div class="report-box-title">نبذة مختصرة</div>
        <div class="report-box-content" id="box1"></div>
      </div>

      <div class="report-box box-color-2">
        <div class="report-box-title">نقاط قوة</div>
        <div class="report-box-content" id="box2"></div>
      </div>

      <div class="report-box box-color-3">
        <div class="report-box-title">نقاط تحسين</div>
        <div class="report-box-content" id="box3"></div>
      </div>

      <div class="report-box box-color-4">
        <div class="report-box-title">استراتيجيات</div>
        <div class="report-box-content" id="box4"></div>
      </div>

      <div class="report-box box-color-5">
        <div class="report-box-title">إجراءات التنفيذ</div>
        <div class="report-box-content" id="box5"></div>
      </div>

      <div class="report-box box-color-6">
        <div class="report-box-title">توصيات</div>
        <div class="report-box-content" id="box6"></div>
      </div>
    </div>

    <div class="image-evidence-grid">
      <div class="image-box">صورة 1</div>
      <div class="image-box">صورة 2</div>
    </div>

  </div>

</div>

<script>
function downloadPDF() {
  var element = document.getElementById('report-content');
  var options = {
    margin: 0,
    filename: 'report.pdf',
    image: { type: 'jpeg', quality: 1 },
    html2canvas: { scale: 3 },
    jsPDF: { unit: 'mm', format: 'a4', orientation: 'portrait' }
  };
  html2pdf().set(options).from(element).save();
}
</script>

</body>
</html>