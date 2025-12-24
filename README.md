
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<title>أداة إنتاج التقارير</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap');

*{box-sizing:border-box;font-family:'Cairo',sans-serif;}

body{
  margin:0;
  background:#f3f4f6;
  display:grid;
  grid-template-columns:370px 1fr;
  height:100vh;
}

.panel{
  background:#fff;
  padding:16px;
  overflow-y:auto;
  border-left:3px solid #083024;
}

.panel h2{
  font-size:16px;
  margin-bottom:12px;
  color:#083024;
}

.field{margin-bottom:10px;}
.field label{font-size:12px;display:block;margin-bottom:4px;}

.field input,.field textarea{
  width:100%;
  padding:6px;
  font-size:12px;
  border:1px solid #d1d5db;
  border-radius:4px;
}
textarea{min-height:60px;resize:vertical}

button{
  width:100%;padding:10px;background:#083024;
  color:#fff;border:none;border-radius:6px;
  font-size:14px;cursor:pointer;margin-top:10px;
}

iframe{width:100%;height:100%;border:none;background:#fff}
</style>
</head>
<body>

<div class="panel">
<h2>بيانات التقرير</h2>

<div class="field"><label>اسم الإدارة</label><input id="admin"></div>
<div class="field"><label>اسم المدرسة</label><input id="school"></div>
<div class="field"><label>الفصل الدراسي</label><input id="term"></div>
<div class="field"><label>الصف</label><input id="grade"></div>
<div class="field"><label>المادة</label><input id="subject"></div>
<div class="field"><label>مكان التنفيذ</label><input id="place"></div>
<div class="field"><label>نوع التقرير</label><input id="type"></div>
<div class="field"><label>المستهدفون</label><input id="target"></div>
<div class="field"><label>العدد</label><input id="count"></div>
<div class="field"><label>اسم المعلم</label><input id="teacher"></div>

<div class="field"><label>الهدف التربوي</label><textarea id="objective"></textarea></div>
<div class="field"><label>وصف مختصر للنشاط</label><textarea id="desc"></textarea></div>
<div class="field"><label>إجراءات التنفيذ</label><textarea id="steps"></textarea></div>
<div class="field"><label>النتائج</label><textarea id="results"></textarea></div>
<div class="field"><label>نقاط القوة</label><textarea id="strengths"></textarea></div>
<div class="field"><label>التوصيات</label><textarea id="recommendations"></textarea></div>
<div class="field"><label>نقاط التحسين</label><textarea id="improvements"></textarea></div>

<div class="field"><label>صورة 1 (اختياري)</label><input type="file" id="img1" accept="image/*"></div>
<div class="field"><label>صورة 2 (اختياري)</label><input type="file" id="img2" accept="image/*"></div>

<button onclick="generate()">إنشاء التقرير</button>
<button onclick="printReport()">طباعة</button>

</div>

<iframe id="preview"></iframe>

<script>
function readImage(id){
  const f=document.getElementById(id).files[0];
  return f?new Promise(r=>{
    const rd=new FileReader();
    rd.onload=()=>r('<img src="'+rd.result+'" style="width:100%;height:100%;object-fit:cover;border-radius:6px;">');
    rd.readAsDataURL(f);
  }):Promise.resolve("شاهد صورة");
}

async function generate(){
  const v=id=>document.getElementById(id).value||'';
  const img1=await readImage('img1');
  const img2=await readImage('img2');

  const html=`<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<title>تقرير</title>

<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap');
*{margin:0;padding:0;box-sizing:border-box;}
html,body{background:white;font-family:'Cairo',sans-serif;color:#1f2937;}

@page{size:A4;margin:8mm}

@media print{
  *{-webkit-print-color-adjust:exact!important;print-color-adjust:exact!important}
  .header::before{opacity:1!important}
}

.header{
  height:90px;background:#083024;
  position:relative;width:100%;
}
.header::before{
  content:"";position:absolute;inset:0;opacity:0.95;
  background:url('https://i.ibb.co/kVWFFwhW/9-C92-E57-B-23-FA-479-D-A024-1-D5-F871-B4-F8-D.png') center/38% no-repeat;
}
.admin-name,.school-name,.hijri-date{
  position:absolute;font-size:8px;color:white;z-index:2;
}
.admin-name{top:6px;right:12px}
.school-name{bottom:6px;right:12px}
.hijri-date{bottom:6px;left:12px}

.info-wrapper{padding:6px 10px;max-width:210mm;margin:auto}
.info-grid{
  display:grid;grid-template-columns:repeat(4,1fr);
  gap:4px;margin-bottom:6px;
}
.info-box{
  background:rgba(255,255,255,0.97);
  border:1px solid #083024;
  border-radius:4px;
  padding:4px;text-align:center;
  font-size:7px;line-height:1.3;
}
.info-box strong{color:#083024;font-size:7.5px;display:block}

.page-content{padding:10px;max-width:210mm;margin:auto}

.sections-grid{
  display:grid;
  grid-template-columns:repeat(3,1fr);
  gap:8px;
}

.section{
  border-radius:6px;
  padding:6px;
}

.section-title{
  font-size:7px;
  font-weight:700;
  margin-bottom:3px;
  border-bottom:1px solid #00000010;
  padding-bottom:2px;
}

.section-content{
  font-size:6.2px;
  white-space:pre-line;
  line-height:1.4;
}

.s-green{background:#e6f0ed;border:1px solid #0d5a40}
.s-blue{background:#e7ebf4;border:1px solid #1e3a8a}
.s-gray{background:#eeeeee;border:1px solid #555}

.images{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:8px;margin-top:8px;
}
.image-box{
  height:120px;display:flex;align-items:center;justify-content:center;
  border:1px dashed #083024;border-radius:6px;
  background:#eef2ef;font-size:6.5px;
  overflow:hidden;
}
</style>

</head>
<body>

<div class="header">
  <div class="admin-name">${v('admin')}</div>
  <div class="school-name">${v('school')}</div>
  <div class="hijri-date" id="hDate">—</div>
</div>

<div class="info-wrapper">
  <div class="info-grid">
    <div class="info-box"><strong>الفصل الدراسي</strong>${v('term')}</div>
    <div class="info-box"><strong>الصف</strong>${v('grade')}</div>
    <div class="info-box"><strong>المادة</strong>${v('subject')}</div>
    <div class="info-box"><strong>مكان التنفيذ</strong>${v('place')}</div>
  </div>
  <div class="info-grid">
    <div class="info-box"><strong>نوع التقرير</strong>${v('type')}</div>
    <div class="info-box"><strong>المستهدفون</strong>${v('target')}</div>
    <div class="info-box"><strong>العدد</strong>${v('count')}</div>
    <div class="info-box"><strong>المعلم</strong>${v('teacher')}</div>
  </div>
</div>

<div class="page-content">

<div class="sections-grid">
  <div class="section s-green">
    <div class="section-title">وصف النشاط</div>
    <div class="section-content">${v('desc')}</div>
  </div>

  <div class="section s-blue">
    <div class="section-title">إجراءات التنفيذ</div>
    <div class="section-content">${v('steps')}</div>
  </div>

  <div class="section s-gray">
    <div class="section-title">النتائج</div>
    <div class="section-content">${v('results')}</div>
  </div>

  <div class="section s-green">
    <div class="section-title">نقاط القوة</div>
    <div class="section-content">${v('strengths')}</div>
  </div>

  <div class="section s-blue">
    <div class="section-title">التوصيات</div>
    <div class="section-content">${v('recommendations')}</div>
  </div>

  <div class="section s-gray">
    <div class="section-title">نقاط التحسين</div>
    <div class="section-content">${v('improvements')}</div>
  </div>
</div>

<div class="section s-green" style="margin-top:8px;">
  <div class="section-title">الهدف التربوي</div>
  <div class="section-content">${v('objective')}</div>
</div>

<div class="images">
  <div class="image-box">${img1}</div>
  <div class="image-box">${img2}</div>
</div>

</div>

<script>
fetch('https://api.aladhan.com/v1/gToH')
.then(r=>r.json()).then(d=>{
 const h=d.data.hijri;
 document.getElementById('hDate').textContent=
   h.day+' '+h.month.ar+' '+h.year+' هـ';
});
<\/script>

</body>
</html>`;

  document.getElementById('preview').srcdoc=html;
}

function printReport(){
  const f=document.getElementById('preview');
  if(f.contentWindow.document.readyState==="complete"){
    f.contentWindow.print();
  }else{
    f.onload=()=>f.contentWindow.print();
  }
}
</script>

</body>
</html>