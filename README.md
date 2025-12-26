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
.container{max-width:950px;margin:auto;padding:15px;}

.input-section{
background:#f8fdfb;padding:15px;border-radius:10px;margin-top:10px;border:1px solid #e0f0ea;
}
label{font-size:15px;font-weight:700;margin-top:15px;display:block;color:#083024;}
input,select,textarea{
width:100%;padding:12px;margin-top:6px;border:2px solid #066d4d;border-radius:8px;font-size:15px;background:#ffffff;
}
textarea{height:85px;resize:none;font-size:15px !important;line-height:1.7;}

.auto-buttons{text-align:center;margin-top:8px;}
.auto-buttons button{
padding:7px 10px;background:#066d4d;border:none;color:#fff;cursor:pointer;border-radius:5px;
font-size:12px;font-weight:bold;
}

.btn-container{
text-align:center;padding:12px;background:#f5f5f5;position:fixed;top:0;left:0;width:100%;z-index:20;
display:flex;gap:10px;justify-content:center;flex-wrap:wrap;box-shadow:0 3px 6px rgba(0,0,0,0.25);
}
button.main-btn{
background:#066d4d;color:#fff;border:none;padding:12px 25px;font-size:15px;border-radius:8px;cursor:pointer;
flex:1;min-width:140px;max-width:200px;
}
#report-content{margin-top:90px;width:100%;}

.header{
width:100%;height:135px;margin-top:20px;position:relative;overflow:hidden;background:#083024;
display:flex;align-items:center;justify-content:center;
}
.header img{width:180px;opacity:.95;}
.header-right-top,.header-right-bottom,.header-left-bottom{
position:absolute;color:#ffffff;font-weight:700;
}
.header-right-top{top:6px;right:12px;font-size:13px;}
.header-right-bottom{bottom:6px;right:12px;font-size:12px;font-weight:600;}
.header-left-bottom{
top:6px;left:12px;font-size:12px;font-weight:600;text-align:center;
display:flex;flex-direction:column;line-height:1.2;
}

.page{width:100%;max-width:830px;padding:10px;margin:auto;}

.info-grid{
display:grid;grid-template-columns:repeat(4,1fr);gap:4px;margin-bottom:4px;
}
.info-grid2{
display:grid;grid-template-columns:repeat(3,1fr);gap:4px;margin-bottom:8px;
}

.info-box{
background:#e8f2ee;border-radius:6px;height:32px;overflow:hidden;
box-shadow:0 2px 4px rgba(6,109,77,0.2);border:1px solid rgba(6,109,77,0.3);
display:flex;flex-direction:column;justify-content:center;align-items:center;
padding:1px;
}
.info-title{font-size:9px;font-weight:700;color:#083024;line-height:1;}
.info-value{font-size:10px;font-weight:700;color:#000000;text-align:center;white-space:nowrap;line-height:1;}

.objective-box{
background:#f3f9f6;border:1px solid rgba(6,109,77,0.35);padding:6px 10px;border-radius:8px;margin-bottom:10px;
height:110px;overflow:hidden;box-shadow:0 3px 6px rgba(6,109,77,0.28);}
.objective-title{font-size:14px;font-weight:700;color:#083024;text-align:center;border-bottom:1px solid #066d4d;margin-bottom:3px;}
.objective-content{font-size:16px;line-height:1.7;color:#000000;overflow:hidden;}

.report-row{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:10px;}
.report-box{
background:#ffffff;border-radius:8px;padding:6px;border:1px solid rgba(6,109,77,0.35);
height:115px;overflow:hidden;box-shadow:0 3px 6px rgba(6,109,77,0.28);}
.report-box-title{font-size:13px;font-weight:700;text-align:center;color:#083024;border-bottom:1px solid #ccd9d0;margin-bottom:4px;}
.report-box-content{font-size:15px;line-height:1.6;overflow:hidden;}

.image-evidence-grid{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-top:8px;}
.image-box{
min-height:140px;max-height:140px;border:1px dashed #066d4d;border-radius:8px;
display:flex;align-items:center;justify-content:center;background:#ffffff;overflow:hidden;padding:4px;
}
.image-box img{max-width:100%;max-height:100%;object-fit:contain;}

.signature-section{margin-top:20px;display:grid;grid-template-columns:1fr 1fr;gap:20px;}
.signature-box{text-align:center;font-size:12px;color:#083024;font-weight:700;}
.signature-line{margin-top:8px;border-top:1px solid #083024;width:80%;margin:auto;margin-bottom:4px;}
.footer{text-align:center;font-size:10px;padding:4px 0;margin-top:18px;background:#083024;color:#fff;}
</style>
</head>

<body>
<div class="btn-container">
<button class="main-btn" onclick="downloadPDF()">تنزيل PDF</button>
<button class="main-btn" onclick="sharePDFWhatsApp()">مشاركة واتساب</button>
</div>

<div class="container">
<div class="input-section">

<label>اسم المدرسة</label>
<input id="school" oninput="updateReport()" placeholder="اكتب اسم المدرسة">

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
<input id="grade" oninput="updateReport()" placeholder="مثال: 5/3">

<label>الفصل الدراسي</label>
<select id="term" oninput="updateReport()">
<option value="">اختر الفصل</option>
<option>الأول</option>
<option>الثاني</option>
</select>

<label>المادة</label>
<input id="subject" oninput="updateReport()" placeholder="مثال: لغتي – علوم – رياضيات">

<label>المستهدفون</label>
<input id="target" oninput="updateReport()" placeholder="مثال: جميع طلاب الصف">

<label>عدد الحضور</label>
<input id="count" oninput="updateReport()" placeholder="مثال: 25 طالب">

<label>مكان التنفيذ</label>
<input id="place" oninput="updateReport()" placeholder="مثال: داخل الصف – المختبر – مصادر التعلم">

<label>اسم المعلم</label>
<input id="teacher" oninput="updateReport()" placeholder="مثال: فهد الخالدي">

<label>اسم المدير</label>
<input id="principal" oninput="updateReport()" placeholder="مثال: نايف اللحياني">

<script>
let autoTexts={
summary:[
"تم تنفيذ النشاط وفق خطة تعليمية واضحة لتعزيز التعلم النشط وإتاحة فرص متنوعة.<br>شارك الطلاب بفاعلية وظهر اهتمامهم بالمحتوى وتحقيق نواتج التعلم المطلوبة بشكل ملحوظ.",
"ركز النشاط على رفع مستوى المشاركة وتحسين مهارات التفكير العليا عبر استراتيجيات مناسبة.<br>ساهم توظيف الوسائل التعليمية في توضيح المفاهيم وتحقيق التفاعل الإيجابي المنتظر.",
"اشتمل النشاط على ممارسات تعليمية عملية هدفت لتنمية الفهم العميق وزيادة الدافعية.<br>أظهر الطلاب تجاوباً كبيراً مع الأسئلة وأنشطة التقويم خلال التنفيذ بشكل فعال.",
"سعى النشاط لتحقيق بيئة تعليمية محفزة تعتمد على توظيف الأنشطة التشاركية المتنوعة.<br>أسهم توزيع المهام في تعزيز المسؤولية الفردية والجماعية لدى الطلاب بشكل جيد.",
"جاء النشاط وفق معايير الجودة في التعليم مع مراعاة الفروق الفردية بين الطلاب المشاركين.<br>أظهر أغلب الطلاب تقدماً واضحاً بالمهارات المستهدفة خلال فترة التنفيذ المحددة."
],
steps:[
"تقديم توجيهات أولية توضح أهداف النشاط وتعليمات الأداء بصورة تفصيلية واضحة للطلاب.<br>متابعة خطوات التنفيذ عملياً والتأكد من التزام الطلاب بالمهام الموكلة لكل مرحلة.",
"تهيئة الطلاب بطرح أسئلة تمهيدية ترتبط بالمفهوم وتحفز الاستنتاج الذاتي للمحتوى.<br>تنفيذ العمل التعاوني داخل المجموعات مع تقديم تغذية راجعة فورية ومباشرة.",
"شرح المهمة التعليمية وفق أساليب عرض مناسبة وإدارة الوقت بكفاءة عالية ومنظمة.<br>إتاحة الفرصة للطلاب لتطبيق المهارات عملياً ثم تقويم الأداء بأساليب بناءة.",
"عرض أمثلة تطبيقية ذات صلة مباشرة بموضوع الدرس وبناء تصور أوضح للطلاب.<br>تحليل إجابات الطلاب ومعالجة الأخطاء وتثبيت المعلومات الصحيحة في الختام.",
"تنظيم مراحل العمل بصورة تدريجية تضمن الفهم السليم قبل الانتقال للمستويات الأعلى.<br>تحفيز النقاش الإيجابي ومتابعة التفاعل وملاحظة تقدم الطلبة أثناء المشاركة."
],
strategies:[
"تطبيق التعلم التعاوني بأسلوب يعزز تبادل الخبرات والآراء بين الطلاب بصورة فعالة.<br>استخدام استراتيجيات التحفيز لدعم التركيز وزيادة دافعية المشاركة أثناء النشاط.",
"الاعتماد على الاستقصاء والاكتشاف لتشجيع التفكير النقدي والوصول للحلول المناسبة.<br>تعزيز التعلم الذاتي من خلال المهام الفردية الهادفة للمسؤولية الشخصية.",
"تنويع طرق العرض باستخدام الوسائط التعليمية الحديثة لتحقيق جودة في الإدراك.<br>توظيف الأسئلة المفتوحة لرفع مستوى الحوار وتطوير مهارات التواصل بين الطلاب.",
"تفعيل العصف الذهني لاستثمار الخبرات السابقة وتوليد أفكار جديدة مرتبطة بالدرس.<br>التركيز على مشاركة جميع الطلاب لضمان تعميم الفائدة دون استثناء.",
"استخدام المحاكاة والتجارب العملية لربط المعرفة النظرية بالواقع المحسوس للطلاب.<br>متابعة الأداء وتقديم إرشادات مباشرة لتحسين جودة التنفيذ أثناء النشاط."
],
strengths:[
"إقبال واضح من الطلاب على المشاركة في النشاط وتفاعل بناء يعكس فهمهم للمهمة.<br>تحسن في مهارات الاتصال والعمل الجماعي واستخدام طرق تعلم فعّالة.",
"تحقيق الأهداف التعليمية المقررة بفضل التنظيم الجيد وتوفر الوقت الكافي للنشاط.<br>الطلاب أظهروا سلوكاً إيجابياً واهتماماً ملحوظاً أثناء تنفيذ جميع المهام.",
"وضوح إرشادات المعلم وسهولة المتابعة أسهما في رفع مستوى التركيز لدى الطلاب.<br>عرض الوسائل التعليمية ساعد في استيعاب المفهوم بطريقة مبسطة ومباشرة.",
"وجود دافعية قوية لدى الطلاب شجعت على الإبداع والمبادرة في عززت نتائج التعلم.<br>العمل التعاوني كان له أثر كبير في تعزيز مهارات التواصل والثقة بالنفس.",
"توفر بيئة صفية محفزة أسهمت في تحقيق جودة الأداء والتزام الطلاب بالقواعد.<br>استخدام أدوات تقويم مناسبة ساعد في قياس تقدم الطلاب بصورة واقعية."
],
improve:[
"زيادة تخصيص الوقت للأنشطة التطبيقية لتحقيق الاستفادة القصوى داخل الصف الدراسي.<br>تقديم فرص أكبر للطلاب المتأخرين لمواكبة مستوى بقية زملائهم بنجاح.",
"مراجعة توزيع المهام لضمان عدالة المشاركة بين جميع الطلاب دون استثناء.<br>التوسع في استخدام الوسائل التعليمية الرقمية لدعم التفاعل المستمر.",
"تطوير المحتوى بإضافة أسئلة بمستويات تفكير أعلى تناسب قدرات جميع الطلاب.<br>تنويع طرائق التقويم لتحسين جودة النتائج بصورة أدق وأكثر شمولا.",
"رفع مستوى الدعم الفردي للطلاب الذين يحتاجون إرشاداً إضافياً أثناء النشاط.<br>تحسين إدارة الوقت لضمان استكمال جميع مراحل النشاط بفاعلية أكبر.",
"تعزيز التنسيق بين أفراد المجموعات لتنمية القيادة والتعاون بصورة أفضل.<br>إثراء النشاط بمصادر تعليمية مرتبطة بالواقع لزيادة الإقناع والتحفيز."
],
recomm:[
"الاستمرار في تطبيق الأنشطة التفاعلية التي تضمن مشاركة جميع الطلاب بفاعلية عالية.<br>دعم البرامج التدريبية للمعلمين لتحسين جودة التخطيط والتنفيذ التربوي.",
"التركيز على توظيف التقنية التعليمية الحديثة وإدخال وسائل رقمية مبتكرة متنوعة.<br>تعزيز التحفيز السلوكي للطلاب لتحسين مهارات التعلم الذاتي المنظم.",
"العمل على تصميم أنشطة متدرجة تراعي الفروق الفردية بين الطلاب بصورة أدق.<br>تفعيل الموارد التعليمية المتاحة بطرق تدعم تحقيق نواتج التعلم المطلوبة.",
"تطوير محتوى الدروس بإضافة تجارب عملية تزيد ارتباط المعرفة بواقع المتعلمين.<br>توسيع فرص الممارسة والتقويم البنائي خلال النشاط بصورة مستمرة.",
"تشجيع المبادرات التعليمية التي تنمي الإبداع والابتكار لدى الطلاب بكفاءة عالية.<br>تطبيق استراتيجيات تربوية تساعد على تعزيز الثقة وتحقيق الاعتماد الذاتي."
]
};

let indexes={summary:0,steps:0,strategies:0,strengths:0,improve:0,recomm:0};

function changeText(field){
indexes[field]=(indexes[field]+1)%5;
document.getElementById(field).value=autoTexts[field][indexes[field]];
updateReport();
}

function handleReportType(){
if(reportType.value==="أخرى"){
reportTypeInput.style.display="block";
document.getElementById("reportTypeBox").innerText=reportTypeInput.value;
} else {
reportTypeInput.style.display="none";
document.getElementById("reportTypeBox").innerText=reportType.value;
}
updateReport();
}

</script>

<label>الهدف التربوي</label>
<textarea id="goal" oninput="updateReport()"></textarea>

<label>نبذة مختصرة</label>
<textarea id="summary" oninput="updateReport()"></textarea>
<div class="auto-buttons"><button onclick="changeText('summary')">اضغط لتغيير النص</button></div>

<label>إجراءات التنفيذ</label>
<textarea id="steps" oninput="updateReport()"></textarea>
<div class="auto-buttons"><button onclick="changeText('steps')">اضغط لتغيير النص</button></div>

<label>الاستراتيجيات</label>
<textarea id="strategies" oninput="updateReport()"></textarea>
<div class="auto-buttons"><button onclick="changeText('strategies')">اضغط لتغيير النص</button></div>

<label>نقاط القوة</label>
<textarea id="strengths" oninput="updateReport()"></textarea>
<div class="auto-buttons"><button onclick="changeText('strengths')">اضغط لتغيير النص</button></div>

<label>نقاط التحسين</label>
<textarea id="improve" oninput="updateReport()"></textarea>
<div class="auto-buttons"><button onclick="changeText('improve')">اضغط لتغيير النص</button></div>

<label>التوصيات</label>
<textarea id="recomm" oninput="updateReport()"></textarea>
<div class="auto-buttons"><button onclick="changeText('recomm')">اضغط لتغيير النص</button></div>

<label>الصورة 1</label>
<input type="file" accept="image/*" onchange="loadImage(this,'imgBox1')">
<label>الصورة 2</label>
<input type="file" accept="image/*" onchange="loadImage(this,'imgBox2')">

</div>
</div>

<div id="report-content">
<div class="header">
<img src="https://i.ibb.co/1fc5gB6v/9-C92-E57-B-23-FA-479-D-A024-1-D5-F871-B4-F8-D.png">
<div class="header-right-top" id="educationBox"></div>
<div class="header-right-bottom" id="schoolBox"></div>
<div class="header-left-bottom">
<span id="hDate"></span>
<span id="gDate"></span>
</div>
</div>

<div class="page">

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
</div>

<script>
function updateReport(){
document.getElementById("educationBox").innerText=education.value;
document.getElementById("termBox").innerText=term.value;
document.getElementById("gradeBox").innerText=grade.value;
document.getElementById("subjectBox").innerText=subject.value;
document.getElementById("targetBox").innerText=target.value;
document.getElementById("countBox").innerText=count.value;
document.getElementById("placeBox").innerText=place.value;
document.getElementById("teacherBox").innerText=teacher.value;
document.getElementById("principalBox").innerText=principal.value;
document.getElementById("schoolBox").innerText=school.value;

if(reportType.value==="أخرى"){
document.getElementById("reportTypeBox").innerText=reportTypeInput.value;
}else{
document.getElementById("reportTypeBox").innerText=reportType.value;
}

document.getElementById("goalBox").innerHTML=goal.value.replace(/\n/g,"<br>");
document.getElementById("summaryBox").innerHTML=summary.value.replace(/\n/g,"<br>");
document.getElementById("stepsBox").innerHTML=steps.value.replace(/\n/g,"<br>");
document.getElementById("strategiesBox").innerHTML=strategies.value.replace(/\n/g,"<br>");
document.getElementById("strengthsBox").innerHTML=strengths.value.replace(/\n/g,"<br>");
document.getElementById("improveBox").innerHTML=improve.value.replace(/\n/g,"<br>");
document.getElementById("recommBox").innerHTML=recomm.value.replace(/\n/g,"<br>");
}

function loadImage(input,target){
let file=input.files[0];
let reader=new FileReader();
reader.onload=()=>document.getElementById(target).innerHTML=
`<img src="${reader.result}">`;
reader.readAsDataURL(file);
}

function downloadPDF(){
html2pdf().set({
margin:0,
filename:"report.pdf",
image:{type:"jpeg",quality:1},
html2canvas:{scale:3,scrollY:0,useCORS:true},
jsPDF:{unit:"mm",format:"a4",orientation:"portrait"}
}).from(document.getElementById("report-content")).save();
}

async function sharePDFWhatsApp(){
let blob=await html2pdf().from(document.getElementById("report-content")).set({
margin:0,image:{type:"jpeg",quality:1},
html2canvas:{scale:3,scrollY:0,useCORS:true},
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

async function loadDates(){
let g=new Date();
let gd=`${g.getFullYear()}-${g.getMonth()+1}-${g.getDate()}`;
document.getElementById("gDate").innerText=
`${g.getDate()} ${g.toLocaleString('ar-SA',{month:'long'})} ${g.getFullYear()} م`;
let r=await fetch(`https://api.aladhan.com/v1/gToH?date=${gd}`);
let d=await r.json();
let hijri=d.data.hijri;
document.getElementById("hDate").innerText=
`${hijri.day} ${hijri.month.ar} ${hijri.year} هـ`;
}
loadDates();
</script>

</body>
</html>