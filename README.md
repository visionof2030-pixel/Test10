<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <title>أداة إنتاج التقارير</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap');

    * { box-sizing: border-box; font-family: 'Cairo', sans-serif; }

    body {
      margin: 0;
      background: #f3f4f6;
      display: grid;
      grid-template-columns: 380px 1fr;
      height: 100vh;
    }

    /* ===== لوحة الإدخال ===== */
    .panel {
      background: #ffffff;
      padding: 16px;
      overflow-y: auto;
      border-left: 2px solid #083024;
    }

    .panel h2 {
      font-size: 16px;
      margin-bottom: 12px;
      color: #083024;
    }

    .field {
      margin-bottom: 10px;
    }

    .field label {
      font-size: 12px;
      display: block;
      margin-bottom: 4px;
    }

    .field input,
    .field textarea {
      width: 100%;
      padding: 6px;
      font-size: 12px;
      border: 1px solid #d1d5db;
      border-radius: 4px;
    }

    textarea { resize: vertical; min-height: 60px; }

    button {
      width: 100%;
      padding: 10px;
      background: #083024;
      color: #fff;
      border: none;
      border-radius: 6px;
      font-size: 14px;
      cursor: pointer;
      margin-top: 10px;
    }

    /* ===== المعاينة ===== */
    iframe {
      width: 100%;
      height: 100%;
      border: none;
      background: white;
    }
  </style>
</head>
<body>

  <!-- ===== لوحة الإدخال ===== -->
  <div class="panel">
    <h2>بيانات التقرير</h2>

    <div class="field"><label>اسم الإدارة</label><input id="admin"></div>
    <div class="field"><label>اسم المدرسة</label><input id="school"></div>
    <div class="field"><label>الفصل الدراسي</label><input id="term"></div>
    <div class="field"><label>الصف</label><input id="grade"></div>
    <div class="field"><label>المادة</label><input id="subject"></div>
    <div class="field"><label>نوع التقرير</label><input id="type"></div>
    <div class="field"><label>المستهدفون</label><input id="target"></div>
    <div class="field"><label>العدد</label><input id="count"></div>
    <div class="field"><label>مكان التنفيذ</label><input id="place"></div>

    <div class="field"><label>الهدف التربوي</label><textarea id="objective"></textarea></div>
    <div class="field"><label>خطوات التنفيذ</label><textarea id="steps"></textarea></div>
    <div class="field"><label>النتائج</label><textarea id="results"></textarea></div>
    <div class="field"><label>نقاط القوة</label><textarea id="strengths"></textarea></div>
    <div class="field"><label>التوصيات</label><textarea id="recommendations"></textarea></div>
    <div class="field"><label>نقاط التحسين</label><textarea id="improvements"></textarea></div>

    <button onclick="generate()">إنشاء التقرير</button>
    <button onclick="printReport()">طباعة</button>
  </div>

  <!-- ===== نافذة المعاينة ===== -->
  <iframe id="preview"></iframe>

<script>
function generate() {
  const v = id => document.getElementById(id).value || '';

  const html = `
<!DOCTYPE html>
<html dir="rtl" lang="ar">
<head>
<meta charset="UTF-8">
<style>
body{font-family:Cairo,sans-serif;margin:0}
.header{height:90px;background:#083024;color:#fff;position:relative}
.admin{position:absolute;top:6px;right:12px;font-size:8px}
.school{position:absolute;bottom:6px;right:12px;font-size:8px}
.date{position:absolute;bottom:6px;left:12px;font-size:8px}
.wrap{max-width:210mm;margin:auto;padding:10px}
.grid{display:grid;grid-template-columns:repeat(3,1fr);gap:4px}
.box{border:1px solid #083024;border-radius:4px;padding:4px;font-size:7px;text-align:center}
.section{border:1px solid #ccc;border-radius:6px;padding:6px;margin-bottom:8px}
.title{font-size:7px;font-weight:600;border-bottom:1px solid #ccc;margin-bottom:3px}
.content{font-size:6px;line-height:1.4}
.images{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.img{height:120px;border:1px dashed #083024;display:flex;align-items:center;justify-content:center;font-size:7px}
</style>
</head>
<body>
<div class="header">
  <div class="admin">${v('admin')}</div>
  <div class="school">${v('school')}</div>
  <div class="date" id="d"></div>
</div>

<div class="wrap">
  <div class="grid">
    <div class="box"><strong>الفصل</strong>${v('term')}</div>
    <div class="box"><strong>الصف</strong>${v('grade')}</div>
    <div class="box"><strong>المادة</strong>${v('subject')}</div>
  </div>

  <div class="grid" style="margin-top:4px">
    <div class="box"><strong>التقرير</strong>${v('type')}</div>
    <div class="box"><strong>المستهدفون</strong>${v('target')}</div>
    <div class="box"><strong>العدد</strong>${v('count')}</div>
    <div class="box"><strong>المكان</strong>${v('place')}</div>
  </div>

  <div class="section"><div class="content">${v('objective')}</div></div>

  <div class="grid" style="grid-template-columns:1fr 1fr">
    <div class="section"><div class="title">خطوات التنفيذ</div><div class="content">${v('steps')}</div></div>
    <div class="section"><div class="title">النتائج</div><div class="content">${v('results')}</div></div>
    <div class="section"><div class="title">نقاط القوة</div><div class="content">${v('strengths')}</div></div>
    <div class="section"><div class="title">التوصيات</div><div class="content">${v('recommendations')}</div></div>
  </div>

  <div class="section">
    <div class="title">نقاط التحسين</div>
    <div class="content">${v('improvements')}</div>
  </div>

  <div class="images">
    <div class="img">شواهد الصور</div>
    <div class="img">شواهد الصور</div>
  </div>
</div>

<script>
fetch('https://api.aladhan.com/v1/gToH')
.then(r=>r.json())
.then(d=>{
 const h=d.data.hijri;
 document.getElementById('d').textContent=h.day+' '+h.month.ar+' '+h.year+' هـ';
});
<\/script>

</body>
</html>`;
  document.getElementById('preview').srcdoc = html;
}

function printReport(){
  document.getElementById('preview').contentWindow.print();
}
</script>

</body>
</html>