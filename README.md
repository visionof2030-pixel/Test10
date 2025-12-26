
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<title>تقرير إشرافي</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap');
*{margin:0;padding:0;box-sizing:border-box;}
html,body{font-family:'Cairo',sans-serif;background:#ffffff;direction:rtl;}

.btn-container{
text-align:center;padding:10px;background:#f5f5f5;
position:fixed;top:0;left:0;width:100%;z-index:10;
display:flex;gap:10px;justify-content:center;
}
button{
background:#066d4d;color:#fff;border:none;
padding:10px 25px;font-size:15px;border-radius:6px;cursor:pointer;
}
button:hover{background:#05523a;}
@media print{.btn-container{display:none;}}

/* HEADER */
.header{
width:100%;height:135px;margin-top:60px;
position:relative;overflow:hidden;
background:#083024;
display:flex;align-items:center;justify-content:center;
}
.header img{
position:relative;z-index:2;width:180px;opacity:.95;
}
.header-right-top,.header-right-bottom,.header-left-bottom{
position:absolute;color:#ffffff;font-weight:700;
}
.header-right-top{top:6px;right:12px;font-size:13px;}
.header-right-bottom{bottom:6px;right:12px;font-size:12px;font-weight:600;}
.header-left-bottom{bottom:6px;left:12px;font-size:12px;font-weight:600;direction:ltr;text-align:left;}

.page{width:100%;max-width:830px;padding:10px;margin:auto;}

.info-grid{
display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));
gap:6px;margin-bottom:12px;
}
.info-box{
background:#e8f2ee;border-radius:8px;
font-size:11px;font-weight:600;
color:#083024;text-align:center;
height:42px;
display:flex;align-items:center;justify-content:center;
box-shadow:0 3px 6px rgba(6,109,77,0.28);
border:1px solid rgba(6,109,77,0.35);
}

/* OBJECTIVE */
.objective-box{
background:#f3f9f6;
border:1px solid rgba(6,109,77,0.35);
padding:6px 10px;border-radius:8px;margin-bottom:10px;
height:110px;overflow:auto;
box-shadow:0 3px 6px rgba(6,109,77,0.28);
}
.objective-title{
text-align:center;font-size:13px;font-weight:700;color:#083024;
border-bottom:1px solid #066d4d;padding-bottom:3px;margin-bottom:3px;
}

/* REPORT BOXES */
.report-row{
display:grid;grid-template-columns:1fr 1fr;
gap:10px;margin-bottom:10px;
}
.report-box{
background:#ffffff;border-radius:8px;
padding:6px;
border:1px solid rgba(6,109,77,0.35);
height:115px;overflow:auto;
box-shadow:0 3px 6px rgba(6,109,77,0.28);
}
.report-box-title{
font-size:12px;font-weight:700;text-align:center;color:#083024;
border-bottom:1px solid #ccd9d0;margin-bottom:4px;padding-bottom:3px;
}
.report-box-content{font-size:10px;line-height:1.3;}

.report-box::-webkit-scrollbar,
.objective-box::-webkit-scrollbar{width:5px;}
.report-box::-webkit-scrollbar-thumb,
.objective-box::-webkit-scrollbar-thumb{background:#066d4d;border-radius:4px;}

/* IMAGES */
.image-evidence-grid{
display:grid;grid-template-columns:1fr 1fr;
gap:8px;margin-top:8px;
}
.image-box{
height:150px;border:1px dashed #066d4d;border-radius:8px;
display:flex;align-items:center;justify-content:center;
color:#066d4d;font-size:10px;overflow:hidden;
box-shadow:0 3px 6px rgba(6,109,77,0.28);
}

/* SIGNATURE */
.signature-section{
margin-top:20px;display:grid;grid-template-columns:1fr 1fr;gap:20px;
}
.signature-box{
text-align:center;font-size:11px;color:#083024;font-weight:600;
}
.signature-line{
margin-top:8px;border-top:1px solid #083024;
width:80%;margin-inline:auto;margin-bottom:4px;
}

/* FOOTER */
.footer{
width:100%;background:#083024;color:#ffffff;
text-align:center;font-size:10px;padding:4px 0;margin-top:18px;
}
</style>
</head>

<body>

<div class="btn-container">
<button onclick="downloadPDF()">تنزيل ملف PDF</button>
<button onclick="sharePDFWhatsApp()">مشاركة عبر واتساب</button>
</div>

<div id="report-content">

<div class="header">
<img src="https://i.ibb.co/1fc5gB6v/9-C92-E57-B-23-FA-479-D-A024-1-D5-F871-B4-F8-D.png">
<div class="header-right-top">إدارة التعليم</div>
<div class="header-right-bottom">مدرسة سعيد بن العاص</div>
<div class="header-left-bottom"><span id="gDate"></span> | <span id="hDate"></span></div>
</div>

<div class="page">

<div class="info-grid">
<div class="info-box">الفصل الدراسي</div>
<div class="info-box">الصف</div>
<div class="info-box">المادة</div>
<div class="info-box">عنوان التقرير</div>
<div class="info-box">المستهدفون</div>
<div class="info-box">عدد الحضور</div>
<div class="info-box">مكان التنفيذ</div>
</div>

<div class="objective-box">
<div class="objective-title">الهدف التربوي</div>
<div class="report-box-content"></div>
</div>

<div class="report-row">
<div class="report-box">
<div class="report-box-title">نبذة مختصرة</div>
<div class="report-box-content"></div>
</div>
<div class="report-box">
<div class="report-box-title">إجراءات التنفيذ</div>
<div class="report-box-content"></div>
</div>
</div>

<div class="report-row">
<div class="report-box">
<div class="report-box-title">الاستراتيجيات</div>
<div class="report-box-content"></div>
</div>
<div class="report-box">
<div class="report-box-title">نقاط القوة</div>
<div class="report-box-content"></div>
</div>
</div>

<div class="report-row">
<div class="report-box">
<div class="report-box-title">نقاط التحسين</div>
<div class="report-box-content"></div>
</div>
<div class="report-box">
<div class="report-box-title">التوصيات</div>
<div class="report-box-content"></div>
</div>
</div>

<div class="image-evidence-grid">
<div class="image-box">صورة توثيقية 1</div>
<div class="image-box">صورة توثيقية 2</div>
</div>

<div class="signature-section">
<div class="signature-box">
اسم المعلم: فهد الخالدي
<div class="signature-line"></div>
توقيع المعلم
</div>
<div class="signature-box">
مدير المدرسة: نايف اللحياني
<div class="signature-line"></div>
توقيع المدير
</div>
</div>

<div class="footer">وزارة التعليم – المملكة العربية السعودية</div>

</div>
</div>

<script>
function downloadPDF(){
html2pdf().set({
margin:0,
filename:"report.pdf",
image:{type:"jpeg",quality:1},
html2canvas:{scale:3,useCORS:true},
jsPDF:{unit:"mm",format:"a4",orientation:"portrait"}
}).from(document.getElementById("report-content")).save();
}

async function sharePDFWhatsApp(){
const el=document.getElementById("report-content");
const worker=html2pdf().set({
margin:0,filename:"report.pdf",
image:{type:"jpeg",quality:1},
html2canvas:{scale:3,useCORS:true},
jsPDF:{unit:"mm",format:"a4",orientation:"portrait"}
}).from(el);
const blob=await worker.outputPdf("blob");
const file=new File([blob],"report.pdf",{type:"application/pdf"});
if(navigator.share){
navigator.share({title:"تقرير إشرافي",files:[file]});
}else{
worker.save();
}
}

async function loadDates(){
let g=new Date(),gy=g.getFullYear(),gm=g.getMonth()+1,gd=g.getDate();
document.getElementById("gDate").innerText=`${gd}-${gm}-${gy}`;
let r=await fetch(`https://api.aladhan.com/v1/gToH?date=${gd}-${gm}-${gy}`);
let d=await r.json(),h=d.data.hijri;
document.getElementById("hDate").innerText=`${h.day}-${h.month.number}-${h.year}`;
}
loadDates();
</script>

</body>
</html>