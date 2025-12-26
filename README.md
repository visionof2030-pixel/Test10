<!DOCTYPE html>
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

.header-info {
  width: 95%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 6px 10px;
  color: #083024;
  font-size: 10px;
  margin-top: 60px;
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
  margin-bottom: 12px;
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

.decor-line {
  width: 100%;
  height: 4px;
  background: repeating-linear-gradient(90deg, #083024, #083024 10px, transparent 10px, transparent 20px);
  margin: 10px 0;
}

.report-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 6px;
  margin-bottom: 6px;
}

.report-box {
  border-radius: 6px;
  padding: 14px;
  min-height: 110px;
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

.box1 { background: #e8f1ff; color: #2e4a8c; }
.box2 { background: #fff7e8; color: #a17d00; }
.box3 { background: #e6f6e6; color: #2d7a2d; }
.box4 { background: #ffecec; color: #b02222; }
.box5 { background: #fff0e6; color: #c26a00; }
.box6 { background: #f1e8ff; color: #5d3da3; }

.image-evidence-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 8px;
  margin-top: 10px;
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

@media (min-width: 600px) { .page { width: 850px; } }
</style>
</head>

<body>

<div class="btn-container">
  <button onclick="window.print()">طباعة</button>
  <button onclick="downloadPDF()">تنزيل PDF</button>
</div>

<div id="report-content">

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

    <div class="report-row">
      <div class="report-box box1">
        <div class="report-box-title">نبذة مختصرة</div>
        <div class="report-box-content" id="box1"></div>
      </div>

      <div class="report-box box2">
        <div class="report-box-title">إجراءات التنفيذ</div>
        <div class="report-box-content" id="box2"></div>
      </div>
    </div>

    <div class="decor-line"></div>

    <div class="report-row">
      <div class="report-box box3">
        <div class="report-box-title">استراتيجيات</div>
        <div class="report-box-content" id="box3"></div>
      </div>

      <div class="report-box box4">
        <div class="report-box-title">نقاط القوة</div>
        <div class="report-box-content" id="box4"></div>
      </div>
    </div>

    <div class="decor-line"></div>

    <div class="report-row">
      <div class="report-box box5">
        <div class="report-box-title">نقاط التحسين</div>
        <div class="report-box-content" id="box5"></div>
      </div>

      <div class="report-box box6">
        <div class="report-box-title">توصيات</div>
        <div class="report-box-content" id="box6"></div>
      </div>
    </div>

    <div class="image-evidence-grid">
      <div class="image-box">صورة توثيقية 1</div>
      <div class="image-box">صورة توثيقية 2</div>
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