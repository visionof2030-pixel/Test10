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
  direction: rtl;
  background: #ffffff;
}

.btn-container {
  text-align: center;
  padding: 10px;
  background: #eaeaea;
  position: fixed;
  top: 0; left: 0;
  width: 100%; z-index: 10;
  gap: 10px;
  display: flex;
  justify-content: center;
}
button {
  background: #0d3b29;
  color: #ffffff;
  border: none;
  padding: 10px 25px;
  font-size: 14px;
  border-radius: 4px;
  cursor: pointer;
}
button:hover { background: #0a2d20; }

@media print { .btn-container { display: none; } }

.header {
  width: 100%;
  height: 130px;
  background: #0d3b29;
  display: flex;
  justify-content: center;
  align-items: center;
}
.header span {
  color: #fff;
  font-size: 20px;
  font-weight: 600;
}

.header-info {
  width: 95%;
  display: flex;
  justify-content: space-between;
  margin: 10px auto;
  font-size: 12px;
  color: #0d3b29;
}

.page {
  width: 100%;
  max-width: 850px;
  padding: 10px;
  margin: auto;
  background: #fff;
}

.info-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit,minmax(140px,1fr));
  gap: 6px;
  margin-bottom: 14px;
}
.info-box {
  border: 1px solid #cdd5cf;
  border-radius: 4px;
  text-align: center;
  padding: 6px;
  font-size: 11px;
  background: #f9f9f9;
}
.info-box strong {
  display: block;
  font-weight: 700;
  font-size: 12px;
  color: #0d3b29;
}

.section-title {
  background: #0d3b29;
  color: #fff;
  padding: 6px;
  font-size: 13px;
  text-align: center;
  border-radius: 4px;
  margin-top: 10px;
}

.report-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 10px;
  margin-top: 8px;
}

.report-box {
  border: 1px solid #cdd5cf;
  border-radius: 4px;
  padding: 10px;
  font-size: 11px;
  min-height: 120px;
  background: #fff;
}
.report-box-content {
  white-space: pre-line;
  line-height: 1.5;
  font-size: 11px;
  color: #333;
}

.image-evidence-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  margin-top: 15px;
  gap: 10px;
}
.image-box {
  border: 1px dashed #0d3b29;
  border-radius: 4px;
  height: 100px;
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 11px;
  color: #0d3b29;
}
</style>
</head>

<body>

<div class="btn-container">
  <button onclick="window.print()">طباعة</button>
  <button onclick="downloadPDF()">تنزيل PDF</button>
</div>

<div id="report-content">

  <div class="header">
    <span>وزارة التعليم</span>
  </div>

  <div class="header-info">
    <div id="leader">قائد المدرسة:</div>
    <div id="school">اسم المدرسة:</div>
    <div id="date">التاريخ:</div>
  </div>

  <div class="page">

    <div class="info-grid">
      <div class="info-box"><strong>مكان التنفيذ</strong><span id="place"></span></div>
      <div class="info-box"><strong>المادة</strong><span id="subject"></span></div>
      <div class="info-box"><strong>الصف</strong><span id="grade"></span></div>
      <div class="info-box"><strong>عدد الطلاب</strong><span id="students"></span></div>
      <div class="info-box"><strong>الحضور</strong><span id="attendance"></span></div>
      <div class="info-box"><strong>نوع التقرير</strong><span id="type"></span></div>
    </div>

    <div class="section-title">نبذة مختصرة وإجراءات التنفيذ</div>
    <div class="report-row">
      <div class="report-box"><div class="report-box-content" id="box1"></div></div>
      <div class="report-box"><div class="report-box-content" id="box2"></div></div>
    </div>

    <div class="section-title">استراتيجيات ونقاط القوة</div>
    <div class="report-row">
      <div class="report-box"><div class="report-box-content" id="box3"></div></div>
      <div class="report-box"><div class="report-box-content" id="box4"></div></div>
    </div>

    <div class="section-title">نقاط التحسين والتوصيات</div>
    <div class="report-row">
      <div class="report-box"><div class="report-box-content" id="box5"></div></div>
      <div class="report-box"><div class="report-box-content" id="box6"></div></div>
    </div>

    <div class="section-title">صور توثيقية</div>
    <div class="image-evidence-grid">
      <div class="image-box">صورة توثيقية 1</div>
      <div class="image-box">صورة توثيقية 2</div>
    </div>

  </div>
</div>

<script>
function downloadPDF(){
  var el = document.getElementById('report-content');
  html2pdf()
  .set({
    margin:0,
    filename:'report.pdf',
    image:{type:'jpeg', quality:1},
    html2canvas:{ scale:3, useCORS:true },
    jsPDF:{ unit:'mm', format:'a4', orientation:'portrait' }
  })
  .from(el).save();
}
</script>

</body>
</html>