<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>أداة إصدار التقارير والشواهد</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap');
*{margin:0;padding:0;box-sizing:border-box;}
html,body{font-family:'Cairo',sans-serif;background:#ffffff;direction:rtl;overflow-x:hidden;}

/* نفس عرض التقرير */
.wrapper{
max-width:830px;
margin:auto;
padding:15px;
}

/* لجعل زر التنزيل مثبت بالأعلى */
.btn-container{
text-align:center;padding:12px;background:#f5f5f5;position:fixed;top:0;left:0;width:100%;z-index:20;
display:flex;gap:10px;justify-content:center;flex-wrap:wrap;box-shadow:0 3px 6px rgba(0,0,0,0.25);
}
button.main-btn{
background:#066d4d;color:#fff;border:none;padding:12px 25px;font-size:15px;border-radius:8px;cursor:pointer;
flex:1;min-width:140px;max-width:200px;
}

.input-section{
background:#f8fdfb;padding:15px;border-radius:10px;margin-top:90px;border:1px solid #e0f0ea;
width:100%;
}

label{font-size:15px;font-weight:700;margin-top:15px;display:block;color:#083024;}
input,select,textarea{
width:100%;padding:12px;margin-top:6px;border:2px solid #066d4d;border-radius:8px;font-size:15px;background:#ffffff;
}
textarea{height:85px;resize:none;font-size:15px !important;line-height:1.7;}

.auto-buttons{display:flex;gap:8px;margin-top:8px;flex-wrap:wrap;}
.auto-buttons button{
padding:7px 10px;background:#066d4d;border:none;color:#fff;cursor:pointer;border-radius:5px;font-size:12px;font-weight:bold;
flex:1;min-width:50px;
}

/********** Responsive **********/
@media (max-width:600px){
button.main-btn{min-width:100px;font-size:13px;padding:10px;}
.info-grid,.info-grid2{grid-template-columns:repeat(2,1fr);}
.report-row{grid-template-columns:1fr;}
.image-evidence-grid{grid-template-columns:1fr;}
}

/********** تقرير **********/
#report-content{width:100%;margin:20px auto;}

.header{background:#083024;padding:10px;min-height:120px;position:relative;color:#fff;text-align:center;}
.header img{width:160px;opacity:.95;}
.header-left-bottom{position:absolute;bottom:6px;left:12px;font-size:12px;font-weight:700;text-align:right;}

.info-grid{
display:grid;grid-template-columns:repeat(4,1fr);gap:4px;margin-top:10px;
}
.info-grid2{
display:grid;grid-template-columns:repeat(3,1fr);gap:4px;margin-bottom:8px;
}
.info-box{
background:#e8f2ee;border-radius:6px;height:32px;
display:flex;flex-direction:column;justify-content:center;align-items:center;
border:1px solid rgba(6,109,77,0.3);
}
.info-title{font-size:9px;font-weight:700;color:#083024;}
.info-value{font-size:10px;font-weight:700;color:#000000;}

.objective-box{
background:#f3f9f6;border:1px solid rgba(6,109,77,0.35);
padding:6px 10px;border-radius:8px;margin-bottom:10px;min-height:90px;
}
.objective-title{text-align:center;font-size:14px;font-weight:700;}
.objective-content{font-size:15px;line-height:1.7;}

.report-row{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin:10px 0;}
.report-box{
background:#ffffff;border-radius:8px;padding:6px;
border:1px solid rgba(6,109,77,0.35);min-height:95px;
}
.report-box-title{text-align:center;font-size:13px;font-weight:700;color:#083024;border-bottom:1px solid #ccd9d0;margin-bottom:4px;}
.report-box-content{font-size:14px;line-height:1.6;}

.image-evidence-grid{display:grid;grid-template-columns:1fr 1fr;gap:8px;}
.image-box{
min-height:140px;border:1px dashed #066d4d;border-radius:8px;
display:flex;align-items:center;justify-content:center;background:#fff;overflow:hidden;
}
.image-box img{max-width:100%;max-height:100%;}

.signature-section{margin-top:20px;display:grid;grid-template-columns:1fr 1fr;gap:20px;}
.signature-box{text-align:center;font-size:12px;color:#083024;font-weight:700;}
.signature-line{margin-top:8px;border-top:1px solid #083024;width:80%;margin:auto;margin-bottom:4px;}

.footer{text-align:center;font-size:10px;padding:6px;margin-top:20px;background:#083024;color:#fff;}
</style>
</head>

<body>

<div class="btn-container">
<button class="main-btn" onclick="downloadPDF()">تنزيل PDF</button>
<button class="main-btn" onclick="sharePDFWhatsApp()">مشاركة واتساب</button>
</div>

<div class="wrapper">
<div class="input-section">

<label>إدارة التعليم</label>
<select id="education" oninput="updateReport()">
<option value="">اختر الإدارة</option>
<option>الإدارة العامة للتعليم بمنطقة مكة المكرمة</option>
<option>الإدارة العامة للتعليم بمحافظة جدة</option>
</select>

<label>اسم التقرير</label>
<select id="reportType" oninput="handleReportType()">
<option value="">اختر نوع التقرير</option>
<option>تقرير نشاط إثرائي</option>
<option>أخرى</option>
</select>
<input id="reportTypeInput" oninput="updateReport()" placeholder="اكتب اسم التقرير يدوياً" style="display:none;">

<label>الصف</label>
<input id="grade" oninput="updateReport()">

<label>الفصل الدراسي</label>
<select id="term" oninput="updateReport()">
<option value="">اختر الفصل</option>
<option>الأول</option>
<option>الثاني</option>
</select>

<label>المادة</label>
<input id="subject" oninput="updateReport()">

<label>المستهدفون</label>
<input id="target" oninput="updateReport()">

<label>عدد الحضور</label>
<input id="count" oninput="updateReport()">

<label>مكان التنفيذ</label>
<input id="place" oninput="updateReport()">

<label>اسم المعلم</label>
<input id="teacher" oninput="updateReport()">

<label>اسم المدير</label>
<input id="principal" oninput="updateReport()">

<script>
const autoTexts={
goal:["تنمية مهارات الطلاب من خلال أنشطة تعليمية تفاعلية تعزز التفكير والمعرفة بشكل فعال وواضح للجميع."],
summary:["تم تنفيذ النشاط داخل الصف بمشاركة جميع الطلاب وتوظيف وسائل تعليمية محفزة عززت التعلم."],
steps:["تقديم شرح للمفهوم الرئيس ثم تقسيم الطلاب إلى مجموعات للعمل التعاوني."],
strategies:["التعلم التعاوني والعصف الذهني وتقويم المهارات بشكل منظم."],
strengths:["مشاركة فعالة من الطلاب داخل النشاط وتحسن ملحوظ في الفهم."],
improve:["زيادة وقت الأنشطة التفاعلية والاستراتيجيات الداعمة للطلاب المتأخرين."],
recomm:["تعزيز استخدام التقنية والاستمرار في تنفيذ الأنشطة الصفية الهادفة."]
};
function autoFill(x){document.getElementById(x).value=autoTexts[x].join(" ");updateReport();}
</script>

<label>الهدف التربوي</label>
<textarea id="goal" oninput="updateReport()"></textarea>
<div class="auto-buttons"><button onclick="autoFill('goal')">تعبئة</button></div>

<label>نبذة مختصرة</label>
<textarea id="summary" oninput="updateReport()"></textarea>
<div class="auto-buttons"><button onclick="autoFill('summary')">تعبئة</button></div>

<label>إجراءات التنفيذ</label>
<textarea id="steps" oninput="updateReport()"></textarea>
<div class="auto-buttons"><button onclick="autoFill('steps')">تعبئة</button></div>

<label>الاستراتيجيات</label>
<textarea id="strategies" oninput="updateReport()"></textarea>
<div class="auto-buttons"><button onclick="autoFill('strategies')">تعبئة</button></div>

<label>نقاط القوة</label>
<textarea id="strengths" oninput="updateReport()"></textarea>
<div class="auto-buttons"><button onclick="autoFill('strengths')">تعبئة</button></div>

<label>نقاط التحسين</label>
<textarea id="improve" oninput="updateReport()"></textarea>
<div class="auto-buttons"><button onclick="autoFill('improve')">تعبئة</button></div>

<label>التوصيات</label>
<textarea id="recomm" oninput="updateReport()"></textarea>
<div class="auto-buttons"><button onclick="autoFill('recomm')">تعبئة</button></div>

<label>الصورة 1</label>
<input type="file" accept="image/*" onchange="loadImage(this,'imgBox1')">

<label>الصورة 2</label>
<input type="file" accept="image/*" onchange="loadImage(this,'imgBox2')">

</div>
</div>

<div id="report-content" class="wrapper">

<div class="header">
<img src="https://i.ibb.co/1fc5gB6v/9-C92-E57-B-23-FA-479-D-A024-1-D5-F871-B4-F8-D.png">
<div class="header-left-bottom">
<span id="hDate"></span>
<br>
<span id="gDate"></span>
</div>
</div>

<div class="info-grid">
<div class="info-box"><div class="info-title">الفصل</div><div class="info-value" id="termBox"></div></div>
<div class="info-box"><div class="info-title">الصف</div><div class="info-value" id="gradeBox"></div></div>
<div class="info-box"><div class="info-title">المادة</div><div class="info-value" id="subjectBox"></div></div>
<div class="info-box"><div class="info-title">التقرير</div><div class="info-value" id="reportTypeBox"></div></div>
</div>

<div class="info-grid2">
<div class="info-box"><div class="info-title">المستهدفون</div><div class="info-value" id="targetBox"></div></div>
<div class="info-box"><div class="info-title">العدد</div><div class="info-value" id="countBox"></div></div>
<div class="info-box"><div class="info-title">المكان</div><div class="info-value" id="placeBox"></div></div>
</div>

<div class="objective-box"><div class="objective-title">الهدف التربوي</div><div class="objective-content" id="goalBox"></div></div>

<div class="report-row">
<div class="report-box"><div class="report-box-title">النبذة</div><div class="report-box-content" id="summaryBox"></div></div>
<div class="report-box"><div class="report-box-title">إجراءات التنفيذ</div><div class="report-box-content" id="stepsBox"></div></div>
</div>

<div class="report-row">
<div class="report-box"><div class="report-box-title">الاستراتيجيات</div><div class="report-box-content" id="strategiesBox"></div></div>
<div class="report-box"><div class="report-box-title">نقاط القوة</div><div class="report-box-content" id="strengthsBox"></div></div>
</div>

<div class="report-row">
<div class="report-box"><div class="report-box-title">نقاط التحسين</div><div class="report-box-content" id="improveBox"></div></div>
<div class="report-box"><div class="report-box-title">التوصيات</div><div class="report-box-content" id="recommBox"></div></div>
</div>

<div class="image-evidence-grid">
<div class="image-box" id="imgBox1">صورة توثيقية 1</div>
<div class="image-box" id="imgBox2">صورة توثيقية 2</div>
</div>

<div class="signature-section">
<div class="signature-box">
<span id="teacherBox"></span>
<div class="signature-line"></div>
المعلم
</div>
<div class="signature-box">
<span id="principalBox"></span>
<div class="signature-line"></div>
مدير المدرسة
</div>
</div>

<div class="footer">وزارة التعليم – المملكة العربية السعودية</div>
</div>

<script>
function updateReport(){
termBox.innerText=term.value;
gradeBox.innerText=grade.value;
subjectBox.innerText=subject.value;
targetBox.innerText=target.value;
countBox.innerText=count.value;
placeBox.innerText=place.value;
teacherBox.innerText=teacher.value;
principalBox.innerText=principal.value;
reportTypeBox.innerText=(reportType.value==="أخرى")?reportTypeInput.value:reportType.value;
goalBox.innerText=goal.value;
summaryBox.innerText=summary.value;
stepsBox.innerText=steps.value;
strategiesBox.innerText=strategies.value;
strengthsBox.innerText=strengths.value;
improveBox.innerText=improve.value;
recommBox.innerText=recomm.value;
}
function handleReportType(){
reportTypeInput.style.display=(reportType.value==="أخرى")?"block":"none";
updateReport();
}
function loadImage(input,target){
let reader=new FileReader();
reader.onload=()=>document.getElementById(target).innerHTML=`<img src="${reader.result}">`;
reader.readAsDataURL(input.files[0]);
}

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
let blob=await html2pdf().from(document.getElementById("report-content")).set({
margin:0,image:{type:"jpeg",quality:1},
html2canvas:{scale:3,useCORS:true},
jsPDF:{unit:"mm",format:"a4",orientation:"portrait"}
}).outputPdf("blob");
let file=new File([blob],"report.pdf",{type:"application/pdf"});
if(navigator.canShare && navigator.canShare({files:[file]})){
navigator.share({files:[file],title:"تقرير نشاط"});
}else{
let url=URL.createObjectURL(blob);
window.open(`https://wa.me/?text=${encodeURIComponent(url)}`);
}
}

/***** التاريخ الهجري + الميلادي *****/
async function loadDates(){
let g=new Date();
gDate.innerText=`${g.getDate()}-${g.getMonth()+1}-${g.getFullYear()} م`;
let r=await fetch(`https://api.aladhan.com/v1/gToH?date=${g.getFullYear()}-${g.getMonth()+1}-${g.getDate()}`);
let d=await r.json();
let h=d.data.hijri;
hDate.innerText=`${h.weekday.ar} ${h.day} ${h.month.ar} ${h.year} هـ`;
}
loadDates();
</script>

</body>
</html>