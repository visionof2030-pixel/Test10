
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

/* 1) تقليل ارتفاع الهيدر */
.header{
width:100%;height:128px;
background:#083024;
background-image:url('https://i.ibb.co/1fc5gB6v/9-C92-E57-B-23-FA-479-D-A024-1-D5-F871-B4-F8-D.png');
background-repeat:no-repeat;background-position:center;
background-size:34%;margin-top:60px;position:relative;
}
.header-right-top{position:absolute;top:5px;right:10px;font-size:13px;color:#ffffff;font-weight:700;}
.header-right-bottom{position:absolute;bottom:5px;right:10px;font-size:12px;color:#ffffff;font-weight:600;}
.header-left-bottom{position:absolute;bottom:5px;left:10px;font-size:12px;color:#ffffff;font-weight:600;text-align:left;direction:ltr;}

.page{width:100%;max-width:830px;padding:10px;margin:auto;}

.info-grid{
display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));
gap:6px;margin-bottom:14px;
}
.info-box{
background:#eaf3ef;border-radius:4px;
font-size:11px;font-weight:600;
color:#083024;text-align:center;
height:40px;display:flex;align-items:center;justify-content:center;
}

/* 2) تقليل ارتفاع الهدف التربوي وتفعيل Scroll */
.objective-box{
background:#f2f9f6;border:2px solid #066d4d;
padding:8px 10px;border-radius:6px;margin-bottom:12px;
height:115px;overflow:auto;
}
.objective-box::-webkit-scrollbar{width:5px;}
.objective-box::-webkit-scrollbar-thumb{background:#066d4d;border-radius:4px;}

.icon-title{display:flex;align-items:center;gap:6px;justify-content:center;font-size:13px;font-weight:700;color:#083024;}
.icon-title svg{width:14px;height:14px;stroke:#066d4d;stroke-width:2;fill:none;}
.objective-box .icon-title{border-bottom:1px solid #066d4d;margin-bottom:4px;padding-bottom:3px;}

/* 3) تثبيت ارتفاع صناديق التقرير + Scroll */
.report-row{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:10px;}
.report-box{
background:#ffffff;border-radius:6px;
padding:8px;border:1px solid #cdd5cf;
height:120px;overflow:auto;
}
.report-box::-webkit-scrollbar{width:5px;}
.report-box::-webkit-scrollbar-thumb{background:#066d4d;border-radius:4px;}
.report-box-title{
font-size:12px;font-weight:700;
border-bottom:1px solid #ccd9d0;margin-bottom:4px;padding-bottom:3px;
}
.report-box-content{font-size:10px;line-height:1.3;}

.image-evidence-grid{
display:grid;grid-template-columns:1fr 1fr;
gap:8px;margin-top:8px;
}
.image-box{
height:120px;border:1px dashed #066d4d;border-radius:6px;
display:flex;align-items:center;justify-content:center;
color:#066d4d;font-size:10px;overflow:hidden;
}

.signature-section{
margin-top:20px;display:grid;grid-template-columns:1fr 1fr;gap:20px;
}
.signature-box{text-align:center;font-size:11px;color:#083024;font-weight:600;}
.signature-line{
margin-top:10px;border-top:1px solid #083024;
width:80%;margin-inline:auto;font-size:10px;margin-bottom:4px;
}

.footer{
width:100%;background:#083024;color:#ffffff;
text-align:center;font-size:10px;padding:3px 0;margin-top:18px;
border-radius:4px;
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
<div class="icon-title">
<svg viewBox="0 0 24 24">
  <circle cx="12" cy="12" r="10" stroke-width="1.5" fill="none"/>
  <path d="M9 12l2 2 4-4" stroke-width="1.5" fill="none"/>
</svg>
الهدف التربوي
</div>
</div>

<div class="report-row">
<div class="report-box">
<div class="icon-title">
<svg viewBox="0 0 24 24">
  <rect x="3" y="3" width="18" height="18" rx="2" ry="2" stroke-width="1.5" fill="none"/>
  <line x1="8" y1="8" x2="16" y2="8" stroke-width="1.5"/>
  <line x1="8" y1="12" x2="16" y2="12" stroke-width="1.5"/>
  <line x1="8" y1="16" x2="12" y2="16" stroke-width="1.5"/>
</svg>
نبذة مختصرة
</div>
<div class="report-box-content"></div>
</div>

<div class="report-box">
<div class="icon-title">
<svg viewBox="0 0 24 24">
  <path d="M12 3v18M3 12h18" stroke-width="1.5" fill="none"/>
  <circle cx="12" cy="12" r="8" stroke-width="1.5" fill="none"/>
</svg>
إجراءات التنفيذ
</div>
<div class="report-box-content"></div>
</div>
</div>

<div class="report-row">
<div class="report-box">
<div class="icon-title">
<svg viewBox="0 0 24 24">
  <path d="M12 2L2 7l10 5 10-5-10-5z" stroke-width="1.5" fill="none"/>
  <path d="M2 17l10 5 10-5" stroke-width="1.5" fill="none"/>
  <path d="M2 12l10 5 10-5" stroke-width="1.5" fill="none"/>
</svg>
استراتيجيات
</div>
<div class="report-box-content"></div>
</div>

<div class="report-box">
<div class="icon-title">
<svg viewBox="0 0 24 24">
  <polyline points="20 6 9 17 4 12" stroke-width="1.5" fill="none"/>
  <circle cx="12" cy="12" r="10" stroke-width="1.5" fill="none"/>
</svg>
نقاط القوة
</div>
<div class="report-box-content"></div>
</div>
</div>

<div class="report-row">
<div class="report-box">
<div class="icon-title">
<svg viewBox="0 0 24 24">
  <path d="M17 8l-5 5-5-5" stroke-width="1.5" fill="none"/>
  <line x1="12" y1="4" x2="12" y2="20" stroke-width="1.5"/>
</svg>
نقاط التحسين
</div>
<div class="report-box-content"></div>
</div>

<div class="report-box">
<div class="icon-title">
<svg viewBox="0 0 24 24">
  <rect x="3" y="3" width="18" height="18" rx="2" ry="2" stroke-width="1.5" fill="none"/>
  <line x1="8" y1="8" x2="16" y2="8" stroke-width="1.5"/>
  <line x1="8" y1="12" x2="16" y2="12" stroke-width="1.5"/>
  <line x1="8" y1="16" x2="12" y2="16" stroke-width="1.5"/>
  <circle cx="18" cy="6" r="2" stroke-width="1.5" fill="none"/>
</svg>
توصيات
</div>
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
margin:0,filename:"report.pdf",
image:{type:"jpeg",quality:1},
html2canvas:{scale:3,useCORS:true},
jsPDF:{unit:"mm",format:"a4",orientation:"portrait"}
}).from(document.getElementById("report-content")).save();
}

async function sharePDFWhatsApp(){
const el=document.getElementById("report-content");
const pdf=html2pdf().set({
margin:0,filename:"report.pdf",
image:{type:"jpeg",quality:1},
html2canvas:{scale:3,useCORS:true},
jsPDF:{unit:"mm",format:"a4",orientation:"portrait"}
}).from(el);
const blob=await pdf.outputPdf("blob");
const file=new File([blob],"report.pdf",{type:"application/pdf"});
if(navigator.share){navigator.share({title:"تقرير إشرافي",files:[file]});}
else{pdf.save();}
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