<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<title>تقرير تفعيل حصص النشاط</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap');
*{box-sizing:border-box;font-family:'Cairo',sans-serif;}

/* منع انزلاق الصفحة وبدء صفحة ثانية */
html, body {
margin:0; padding:0;
background:#fff;
overflow:hidden;
}

/* حاوية صفحة التقرير */
.page {
width:210mm;
height:297mm;
position:relative;
margin:0 auto;
background:white;
overflow:hidden;
}

/* أزرار PDF وطباعة */
.action-box {
position:fixed;top:8px;left:0;right:0;
text-align:center;z-index:1000;
}
.action-box button{
background:#083024;color:white;border:0;
padding:10px 16px;font-size:14px;border-radius:6px;
cursor:pointer;margin:4px;
}

/* HEADER */
.header {
height:105px; background:#083024; color:white;
position:relative;
}
.school-name {
position:absolute; bottom:6px; right:12px;
font-size:9px; font-weight:bold;
}
.admin-name {
position:absolute; top:6px; right:12px;
font-size:9px;
}
.date {
position:absolute; bottom:6px; left:12px;
font-size:9px;
}

/* شعار الوزارة يمين */
.moe-logo {
position:absolute; top:18px; right:12px;
height:40px;
}

/* عنوان التقرير في المنتصف */
.report-title {
position:absolute; top:35px; left:50%;
transform:translateX(-50%);
color:white;font-size:12px;
font-weight:bold;text-align:center;
}

/* المعلومات */
.info {
padding:6px 8px;
}
.grid4 {
display:grid;
grid-template-columns:repeat(4,1fr);
gap:3px;
margin-bottom:4px;
}
.ibox {
border:1px solid #083024;border-radius:3px;
padding:3px;text-align:center;font-size:7px;
}
.ibox strong {
display:block;font-size:8px;margin-bottom:1px;color:#083024;
}

/* الأقسام */
.page-content {
padding:4px 8px;
}
.objective-box {
background:#dfece6;border:1px solid #0d5640;
border-radius:5px;margin-bottom:5px;text-align:center;
font-size:8px;padding:4px;
font-weight:bold;
}

.sectors {
display:grid;
grid-template-columns:repeat(4,1fr);
gap:3px;
}
.sec {
border-radius:5px;font-size:6.5px;
min-height:65px;padding:3px;
}
.sec-title {
font-size:7.2px;font-weight:bold;
color:#083024;margin-bottom:1px;
border-bottom:1px solid #999;
}
.sec-content {
white-space:pre-line;line-height:1.4;
font-size:6.2px;
}

/* ألوان */
.green {background:#e3ede8;border:1px solid #0c5c42;}
.blue {background:#e5e9f3;border:1px solid #1e3a8a;}
.red {background:#fde8e7;border:1px solid #a83e3e;}
.yellow {background:#fff7d4;border:1px solid #c99b00;}
.gray {background:#f4f4f4;border:1px solid #6c6c6c;}

/* الصور */
.images {
display:grid;grid-template-columns:1fr 1fr;
gap:4px;margin-top:4px;
}
.imgbox {
height:85px;border:1px solid #083024;border-radius:5px;
overflow:hidden;background:#eee;
}
.imgbox img {
width:100%;height:100%;object-fit:cover;
}

/* التواقيع */
.footer {
margin-top:5px;
display:flex;justify-content:space-between;
font-size:8px;font-weight:bold;
}

/* فقط للطباعة */
@media print {
.action-box {display:none!important;}
* {-webkit-print-color-adjust:exact;print-color-adjust:exact;}
}
</style>

</head>
<body>

<div class="action-box">
<button onclick="downloadPDF()">PDF</button>
<button onclick="window.print()">طباعة</button>
</div>

<div class="page" id="reportPage">
<div class="header">
<img src="https://i.ibb.co/j6QD2sS/moe.png" class="moe-logo">
<div class="report-title">تقرير تفعيل حصص النشاط</div>
<div class="admin-name" id="admin"></div>
<div class="school-name" id="school"></div>
<div class="date" id="hDate"></div>
</div>

<div class="info">
<div class="grid4">
<div class="ibox"><strong>الفصل</strong><span id="term"></span></div>
<div class="ibox"><strong>الصف</strong><span id="grade"></span></div>
<div class="ibox"><strong>المادة</strong><span id="subject"></span></div>
<div class="ibox"><strong>نوع التقرير</strong><span id="type"></span></div>
</div>

<div class="grid4">
<div class="ibox"><strong>المستهدفون</strong><span id="target"></span></div>
<div class="ibox"><strong>العدد</strong><span id="count"></span></div>
<div class="ibox"><strong>مكان التنفيذ</strong><span id="place"></span></div>
<div class="ibox"><strong>المعلم</strong><span id="teacher"></span></div>
</div>
</div>

<div class="page-content">
<div class="objective-box" id="objective"></div>

<div class="sectors">
<div class="sec green"><div class="sec-title">وصف مختصر</div><div id="desc" class="sec-content"></div></div>
<div class="sec yellow"><div class="sec-title">إجراءات التنفيذ</div><div id="steps" class="sec-content"></div></div>
<div class="sec blue"><div class="sec-title">نقاط القوة</div><div id="strengths" class="sec-content"></div></div>
<div class="sec red"><div class="sec-title">التحديات</div><div id="challenges" class="sec-content"></div></div>
<div class="sec green"><div class="sec-title">النتائج</div><div id="results" class="sec-content"></div></div>
<div class="sec gray"><div class="sec-title">ما يحتاج إلى تطوير</div><div id="develop" class="sec-content"></div></div>
<div class="sec blue"><div class="sec-title">التوصيات</div><div id="recommend" class="sec-content"></div></div>
<div class="sec" style="background:#fff;border:1px solid transparent;"></div>
</div>

<div class="images">
<div class="imgbox" id="imgbox1"></div>
<div class="imgbox" id="imgbox2"></div>
</div>

<div class="footer">
<div>مدير المدرسة:<br><span id="manager"></span></div>
<div>المعلم:<br><span id="teacher2"></span></div>
</div>

</div>
</div>

<script>
function loadData(){
const data=JSON.parse(localStorage.getItem("reportData"));
if(!data) return;

for(const k in data){
if(document.getElementById(k)) document.getElementById(k).textContent=data[k];
}
document.getElementById("teacher2").textContent=data.teacher;

loadImg("img1","imgbox1");
loadImg("img2","imgbox2");
}

/* تحميل الصور */
function loadImg(key,boxID){
const file=localStorage.getItem(key);
if(!file) return;
document.getElementById(boxID).innerHTML=
`<img src="${file}" />`;
}

/* تاريخ هجري */
fetch('https://api.aladhan.com/v1/gToH')
.then(r=>r.json()).then(d=>{
const h=d.data.hijri;
document.getElementById('hDate').textContent=
`${h.day} ${h.month.ar} ${h.year} هـ`;
});

/* PDF */
function downloadPDF(){
html2pdf().set({
margin:0,
filename:'تقرير-حصص-النشاط.pdf',
image:{type:'jpeg',quality:1},
html2canvas:{scale:3},
jsPDF:{unit:'mm',format:'a4',orientation:'portrait'}
}).from(document.getElementById("reportPage")).save();
}

/* استرجاع المدخلات المخزنة */
window.onload=loadData;
</script>

</body>
</html>