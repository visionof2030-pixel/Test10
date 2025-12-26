
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
  direction: rtl;
}
.btn-container {
  text-align: center;
  padding: 10px;
  background: #f2f2f2;
  position: fixed;
  top: 0; left: 0;
  width: 100%; z-index: 10;
  display: flex; gap: 10px;
  justify-content: center;
}
button {
  background: #b29234;
  color: #ffffff;
  border: none;
  padding: 10px 25px;
  font-size: 15px;
  border-radius: 6px;
  cursor: pointer;
}
button:hover { background: #8b7229; }
@media print {
  .btn-container { display: none; }
}
.header {
  width: 100%;
  height: 180px;
  background: #0d241c;
  display: flex;
  justify-content: center;
  align-items: center;
}
.header img { width: 40%; }
.header-info {
  width: 95%;
  display: flex;
  justify-content: space-between;
  font-size: 12px;
  color: #0d241c;
  padding: 8px 10px;
  font-weight: 600;
}
.page {
  width: 100%;
  padding: 10px;
  background: #fff;
  margin: auto;
}
.info-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit,minmax(140px,1fr));
  gap: 6px;
  margin-bottom: 12px;
}
.info-box {
  background: #ffffff;
  border: 1px solid #d6c48e;
  border-radius: 6px;
  padding: 6px;
  text-align: center;
  font-size: 11px;
}
.info-box strong { color: #8b7229; display: block; font-size: 12px; }
.decor-line {
  width: 100%;
  height: 12px;
  background-image: url('data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMHB4IiB2aWV3Qm94PSIwIDAgMTAwIDEwIiBmaWxsPSJub25lIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciPjxwYXRoIGQ9Ik0wIDVsNSA1TDEwIDBsNSA1TDE1IDBsNSA1TDIwIDBsNSA1TDI1IDBsNSA1TDMwIDBsNSA1IiBzdHJva2U9IiNiMjkyMzQiIHN0cm9rZS13aWR0aD0iMiIgZmlsbD0ibm9uZSIvPjwvc3ZnPg==');
  background-repeat: repeat-x;
  margin: 14px 0;
}
.report-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 10px;
}
.report-box {
  background: #ffffff;
  border: 1px solid #d6c48e;
  border-radius: 10px;
  padding: 14px;
}
.report-box-title {
  font-size: 13px;
  margin-bottom: 4px;
  text-align: center;
  font-weight: bold;
  color: #0d241c;
}
.report-box-content {
  font-size: 11px;
  white-space: pre-line;
  line-height: 1.5;
  text-align: justify;
  color: #333;
}
.image-evidence-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 10px;
  margin-top: 10px;
}
.image-box {
  border-radius: 8px;
  border: 1px dashed #b29234;
  font-size: 11px;
  height: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #8b7229;
}
@media (min-width: 600px){
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
  <div class="header">
    <img crossorigin="anonymous" src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABkAAAARwCAYAAAD3lGnRAAAACXBIWXMAAAsTAAALEwEAmpwYAAAgAElEQVR4nOzde3hU5d0/8KfNmbtJm42kSUIAiQbSHIMJQ6GtVRFQ0QIeV1EbUJEB7pQWpRcBVJBdoHeiFpffoU8SqS+CBqkNUtYVbT2pBIpZpSLL+1SQIK3HOhA2/MmTmzm3MZmbvjffecb45x45yZ3zvn3PPyfOc853vtc/FzRtAgAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABA2Cgk93QxAAAAAElFTkSuQmCC">
  </div>

  <div class="header-info">
    <div id="leader"></div>
    <div id="school"></div>
    <div id="date"></div>
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

    <div class="decor-line"></div>

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

    <div class="decor-line"></div>

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
  .from(el)
  .save();
}
</script>

</body>
</html>