<!DOCTYPE html>
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

.header{
width:100%;height:170px;background:#083024;
background-image:url('https://i.ibb.co/1fc5gB6v/9-C92-E57-B-23-FA-479-D-A024-1-D5-F871-B4-F8-D.png');
background-repeat:no-repeat;background-position:center;
background-size:38%;margin-top:60px;position:relative;
}
.header-right-top{
position:absolute;top:5px;right:10px;
font-size:13px;color:#ffffff;font-weight:700;
}
.header-right-bottom{
position:absolute;bottom:5px;right:10px;
font-size:12px;color:#ffffff;font-weight:600;
}
.header-left-bottom{
position:absolute;bottom:5px;left:10px;
font-size:12px;color:#ffffff;font-weight:600;
text-align:left;direction:ltr;
}

.page{width:100%;max-width:830px;padding:10px;margin:auto;}

.info-grid{
display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));
gap:6px;margin-bottom:14px;
}
.info-box{
background:#eaf3ef;border-radius:4px;
padding:6px;font-size:11px;font-weight:600;
color:#083024;text-align:center;
}

.section-icon{
position:absolute;top:-16px;right:50%;
transform:translateX(50%);
background:#ffffff;
padding:3px;border-radius:50%;
}
.section-icon svg{width:22px;height:22px;stroke:#066d4d;stroke-width:2;}

.objective-box{
background:#f2f9f6;border:2px solid #066d4d;
padding:25px 10px;border-radius:6px;margin-bottom:22px;
min-height:140px;position:relative;
}
.objective-title{
text-align:center;font-size:14px;font-weight:700;
margin-bottom:6px;color:#083024;
border-bottom:1px solid #066d4d;padding-bottom:4px;
}

.report-row{
display:grid;grid-template-columns:1fr 1fr;
gap:20px;margin-bottom:22px;
}
.report-box{
background:#ffffff;border-radius:6px;
padding:25px 10px;border:1px solid #cdd5cf;
min-height:150px;position:relative;
}
.report-box-title{
text-align:center;font-size:13px;color:#083024;font-weight:700;
border-bottom:1px solid #ccd9d0;margin-bottom:6px;padding-bottom:4px;
}
.report-box-content{
font-size:11px;line-height:1.5;min-height:80px;
}

.image-evidence-grid{
display:grid;grid-template-columns:1fr 1fr;
gap:10px;margin-top:10px;
}
.image-box{
height:110px;border:1px dashed #066d4d;
border-radius:6px;font-size:11px;
display:flex;align-items:center;justify-content:center;
color:#066d4d;
}

.signature-section{
margin-top:40px;
display:grid;grid-template-columns:1fr 1fr;
gap:40px;
}
.signature-box{
text-align:center;font-size:12px;color:#083024;font-weight:600;
}
.signature-line{
margin-top:25px;border-top:1px solid #083024;
width:80%;margin-inline:auto;
font-size:11px;margin-bottom:4px;
text-align:center;
}

.footer{
width:100%;background:#083024;color:#ffffff;
text-align:center;font-size:10px;padding:4px 0;
margin-top:30px;border-radius:4px;
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
<div class="header-right-top">إدارة التعليم</div>
<div class="header-right-bottom">مدرسة سعيد بن العاص</div>
<div class="header-left-bottom">
<span id="gDate"></span> | <span id="hDate"></span>
</div>
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
<div class="section-icon">
<svg fill="none" viewBox="0 0 24 24"><circle cx="12" cy="12" r="9"/><circle cx="12" cy="12" r="4"/></svg>
</div>
<div class="objective-title">الهدف التربوي</div>
</div>

<div class="report-row">
<div class="report-box">
<div class="section-icon">
<svg fill="none" viewBox="0 0 24 24"><rect x="6" y="4" width="12" height="16" rx="2"/></svg>
</div>
<div class="report-box-title">نبذة مختصرة</div>
<div class="report-box-content"></div>
</div>

<div class="report-box">
<div class="section-icon">
<svg fill="none" viewBox="0 0 24 24"><path d="M5 12h14M12 5v14"/></svg>
</div>
<div class="report-box-title">إجراءات التنفيذ</div>
<div class="report-box-content"></div>
</div>
</div>

<div class="report-row">
<div class="report-box">
<div class="section-icon">
<svg fill="none" viewBox="0 0 24 24"><path d="M9 2l6 0-2 11h-2L9 2zM12 22a2 2 0 100-4 2 2 0 000 4z"/></svg>
</div>
<div class="report-box-title">استراتيجيات</div>
<div class="report-box-content"></div>
</div>

<div class="report-box">
<div class="section-icon">
<svg fill="none" viewBox="0 0 24 24"><path d="M20 6l-11 11-5-5"/></svg>
</div>
<div class="report-box-title">نقاط القوة</div>
<div class="report-box-content"></div>
</div>
</div>

<div class="report-row">
<div class="report-box">
<div class="section-icon">
<svg fill="none" viewBox="0 0 24 24"><path d="M12 4v16M6 10l6-6 6 6"/></svg>
</div>
<div class="report-box-title">نقاط التحسين</div>
<div class="report-box-content"></div>
</div>

<div class="report-box">
<div class="section-icon">
<svg fill="none" viewBox="0 0 24 24"><path d="M6 4h12v16H6zM9 9h6M9 13h4"/></svg>
</div>
<div class="report-box-title">توصيات</div>
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
var el=document.getElementById("report-content");
html2pdf().set({
margin:0,
filename:"report.pdf",
image:{type:"jpeg",quality:1},
html2canvas:{scale:3,useCORS:true},
jsPDF:{unit:"mm",format:"a4",orientation:"portrait"}
}).from(el).save();
}

async function sharePDFWhatsApp(){
var el=document.getElementById("report-content");
const options={margin:0,filename:"report.pdf",image:{type:"jpeg",quality:1},html2canvas:{scale:3,useCORS:true},jsPDF:{unit:"mm",format:"a4",orientation:"portrait"}};
const worker=html2pdf().set(options).from(el);
const pdfBlob=await worker.outputPdf("blob");
const file=new File([pdfBlob],"report.pdf",{type:"application/pdf"});
if(navigator.share){await navigator.share({title:"تقرير إشرافي",files:[file]});}else{worker.save();}
}

async function loadDates(){
let g=new Date();let gy=g.getFullYear(),gm=g.getMonth()+1,gd=g.getDate();
document.getElementById("gDate").innerText=`${gd}-${gm}-${gy}`;
let api=`https://api.aladhan.com/v1/gToH?date=${gd}-${gm}-${gy}`;
let r=await fetch(api);let d=await r.json();let h=d.data.hijri;
document.getElementById("hDate").innerText=`${h.day}-${h.month.number}-${h.year}`;
}
loadDates();
</script>

</body>
</html>