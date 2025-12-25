<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<title>تقرير تفعيل حصص النشاط</title>

<script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap');
*{box-sizing:border-box;font-family:'Cairo',sans-serif;}
body{margin:0;background:#f3f4f6;}
button{cursor:pointer}

/* إخفاء عناصر GitHub Pages مثل Test10 و DOCTYPE */
body > *:first-child:not(#formPage):not(#reportPage) {
  display: none !important;
}

/* PAGE SWITCH */
#formPage{display:block}
#reportPage{display:none}

/* PANEL (FORM) */
.panel{
  background:white;padding:18px;
  max-width:380px;margin:auto;
  border-right:4px solid #083024;
}
.field{margin-bottom:12px;}
.field label{font-size:12px;display:block;margin-bottom:4px;}
input,select,textarea{
  width:100%;padding:6px;font-size:12px;
  border:1px solid #ccc;border-radius:4px;
}
textarea{min-height:60px;resize:vertical}
.auto-box{display:flex;gap:6px;align-items:center;margin-top:4px}
.auto-btn{
  width:26px;height:26px;border-radius:4px;background:#ddd;border:1px solid #aaa;
  text-align:center;line-height:24px;font-size:15px;
}
button{
  width:100%;padding:10px;
  background:#083024;color:white;
  border:none;border-radius:6px;font-size:14px;
  margin-top:10px;
}

/* REPORT */
#reportPage{
  background:white;
  width:210mm;
  min-height:297mm;
  margin:auto;
  padding:0;
  overflow:hidden;
  position:relative;
}

@page{size:A4;margin:6mm;}
@media print{
  #formPage{display:none!important}
  #printBtn,#pdfBtn,#printIcon{display:none!important}
  *{-webkit-print-color-adjust:exact;print-color-adjust:exact}
}

/* HEADER */
.header{
 height:110px;background:#083024;color:white;position:relative;
}
.header::before{
 content:"";position:absolute;inset:0;opacity:.9;
 background:url('https://i.ibb.co/kVWFFwhW/9-C92-E57-B-23-FA-479-D-A024-1-D5-F871-B4-F8-D.png')
 center/40% no-repeat;
}
.ministry {
  position:absolute;top:25px;left:50%;transform:translateX(-50%);
  font-size:8px;text-align:center;color:white;
}
.ministry img {height:26px;margin-bottom:4px;}
.admin{position:absolute;top:6px;right:12px;font-size:8px;font-weight:bold;}
.school{position:absolute;bottom:6px;right:12px;font-size:8px;}
.date{position:absolute;bottom:6px;left:12px;font-size:8px;}

/* TOP INFO */
.info{padding:6px 8px;}
.grid4{
 display:grid;
 grid-template-columns:repeat(4,1fr);
 gap:3px;
 margin-bottom:4px;
}
.ibox{
 border:1px solid #083024;border-radius:3px;
 padding:3px;text-align:center;font-size:6.4px;background:white;
}
.ibox strong{display:block;font-size:7px;color:#083024;margin-bottom:1px;}

/* SECTIONS */
.page{padding:6px 8px;}
.objective{
 background:#dcece5;border:1px solid #0b543a;border-radius:5px;
 height:55px;display:flex;align-items:center;justify-content:center;
 font-size:7px;font-weight:bold;text-align:center;margin-bottom:6px;line-height:1.4;
}

.sectors{
 display:grid;
 grid-template-columns:repeat(4,1fr);
 gap:4px;
 margin-top:4px;
}
.sec{
 padding:4px;border-radius:4px;font-size:5.8px;
 min-height:72px;
}
.sec-title{font-size:6.4px;font-weight:bold;border-bottom:1px solid #3333;padding-bottom:1px;margin-bottom:1px;}
.sec-content{white-space:pre-line;line-height:1.3;}

.green{background:#e3ede8;border:1px solid #0c5c42;}
.blue{background:#e5e9f3;border:1px solid #1e3a8a;}
.yellow{background:#fff7d4;border:1px solid #c99b00;}
.red{background:#fde8e7;border:1px solid #a83e3e;}
.gray{background:#f4f4f4;border:1px solid #6c6c6c;}

/* IMAGES */
.images{
 display:grid;
 grid-template-columns:1fr 1fr;
 gap:6px;margin-top:6px;
}
.imgbox{
 height:95px;border:1px solid #083024;border-radius:5px;
 overflow:hidden;background:#eee;
}

/* FOOTER */
.footer{
 margin-top:6px;display:flex;justify-content:space-between;
 font-size:8px;font-weight:bold;
}

/* ACTION BUTTONS */
#printBtn,#pdfBtn{
 background:#0b4c36;color:white;
 padding:10px;border-radius:6px;
 width:48%;font-size:14px;margin:6px 1%;
}
.action-box{
 display:flex;
 justify-content:center;
 gap:8px;
 margin-top:8px;
}

/*====== دعم كامل للجوال ======*/
@media(max-width: 768px){

  body {
    display: block !important;
  }

  .panel {
    width: 100% !important;
    max-width: 95% !important;
    margin: 0 auto !important;
    border-right: 5px solid #083024 !important;
  }

  input, select, textarea {
    font-size: 14px !important;
  }

  #reportPage {
    width: 100% !important;
    min-height: auto !important;
    padding-bottom: 20px;
  }

  .action-box {
    position: static !important;
    transform: none !important;
    margin: 10px auto !important;
  }

  #printBtn, #pdfBtn {
    width: 45% !important;
    font-size: 13px !important;
  }

  .header {
    height: 120px !important;
  }

  .sectors {
    grid-template-columns: 1fr 1fr !important;
  }

  .grid4 {
    grid-template-columns: 1fr 1fr !important;
  }

  .ministry img {
    height: 20px !important;
  }

  .objective {
    height: auto !important;
    padding: 6px !important;
    font-size: 7.5px !important;
  }

  .sec {
    min-height: auto !important;
    font-size: 7px !important;
  }

  .sec-title {
    font-size: 7.4px !important;
  }

  .images {
    grid-template-columns: 1fr !important;
  }

  .footer {
    font-size: 10px !important;
    flex-direction: column !important;
    gap: 10px;
    text-align: center;
  }
}
</style>
</head>
<body>

<!-- FORM PAGE -->
<div id="formPage">
<div class="panel">
<h2 style="color:#083024;font-size:16px;">بيانات التقرير</h2>

<select id="admin" class="field"><option>الإدارة العامة للتعليم بمنطقة مكة المكرمة – مكة المكرمة</option></select>
<input class="field" id="school" placeholder="اسم المدرسة">
<select class="field" id="term"><option>الفصل الدراسي الأول</option><option>الفصل الدراسي الثاني</option></select>
<input class="field" id="grade" placeholder="الصف">
<input class="field" id="subject" placeholder="المادة">
<select class="field" id="type"><option>تقرير تفعيل حصص النشاط</option></select>
<input class="field" id="target" placeholder="المستهدفون">
<input class="field" id="count" placeholder="العدد">
<input class="field" id="place" placeholder="مكان التنفيذ">
<input class="field" id="teacher" placeholder="اسم المعلم">
<input class="field" id="manager" placeholder="اسم مدير المدرسة">

<script>
const autos={objective:[
"تنمية مهارات الطلاب وتعزيز مشاركتهم الفاعلة وتطوير قدراتهم.", 
"بناء شخصية قيادية لدى الطلاب من خلال تفعيل الأنشطة التربوية.",
"تعزيز التفكير الناقد وتنمية مهارات التواصل الاجتماعي لديهم.",
"رفع مستوى الدافعية للتعلم عبر أنشطة تطبيقية متنوعة."
],desc:[
"تنفيذ نشاط تعليمي تفاعلي يعتمد على العمل الجماعي وتنمية المهارات.",
"تطبيق استراتيجية تعليمية محفزة تسهم في تطوير مهارات الطلاب.",
"مشاركة الطلاب في نشاط يحقق الأهداف السلوكية والمعرفية.",
"إشراك الطلاب في مهام تعزز التعاون والتطبيق العملي."
],steps:[
"توزيع الأدوار وشرح المطلوب ثم التنفيذ والمتابعة المباشرة.", 
"تقسيم الطلاب لمجموعات وإدارة النقاش وتقديم التغذية الراجعة.", 
"تهيئة الوسائل التعليمية ثم تنفيذ النشاط وتقييم الأداء.", 
"التوجيه والتحفيز المستمر لتحقيق الأهداف الموضوعة."
],results:[
"تحسن مستوى تفاعل الطلاب وتطور مهارات التواصل.", 
"بروز قدرات جديدة لدى الطلاب أثناء النشاط.", 
"زيادة الدافعية والحماس لدى الطلاب.", 
"تحقيق نتائج إيجابية انعكست على مستوى التعلم."
],motives:[
"تشجيع الطلاب بالإشادة والمكافآت المناسبة.", 
"تعزيز المنافسة الإيجابية داخل المجموعات.", 
"تهيئة بيئة محفزة وجاذبة للطلاب.", 
"تنويع أساليب التحفيز لزيادة المشاركة."
],challenges:[
"تفاوت مستويات الطلاب في الفهم والمشاركة.", 
"ضيق الوقت مقارنة بمتطلبات النشاط.", 
"الحاجة إلى ضبط بعض السلوكيات.", 
"نقص أدوات معينة أثناء التنفيذ."
],strengths:[
"تنظيم متميز وتفاعل عالٍ داخل النشاط.", 
"تنوع الوسائل التعليمية داخل النشاط.", 
"ارتفاع روح التعاون بين الطلاب.", 
"وضوح التعليمات وسهولة التطبيق."
],develop:[
"زيادة دعم الطلاب الأقل مشاركة بالنشاط.", 
"تخصيص وقت إضافي لبعض الأنشطة.", 
"توفير تجهيزات إضافية داعمة.", 
"رفع مستوى التشجيع الفردي."
],recommend:[
"الاستمرار في تفعيل حصص النشاط.", 
"زيادة الإمكانات الداعمة للأنشطة.", 
"عرض منجزات الطلاب وتحفيزهم عليها.", 
"التوسع باستخدام الوسائل التقنية."
]};
const idx={};for(const k in autos) idx[k]=0;
function autoFill(k){idx[k]=(idx[k]+1)%autos[k].length;document.getElementById(k).value=autos[k][idx[k]];}
</script>

<script>
function F(t,i){
return `<div class="field"><label>${t}</label>
<textarea id="${i}"></textarea>
<div class="auto-box"><div class="auto-btn" onclick="autoFill('${i}')">✦</div>
<div class="auto-text">اضغط للتبديل</div></div></div>`}
document.write(
F("الهدف التربوي","objective")+
F("وصف مختصر","desc")+
F("إجراءات التنفيذ","steps")+
F("النتائج","results")+
F("المحفزات","motives")+
F("التحديات","challenges")+
F("نقاط القوة","strengths")+
F("ما يحتاج إلى تطوير","develop")+
F("التوصيات","recommend")
);
</script>

<input class="field" type="file" id="img1" accept="image/*">
<input class="field" type="file" id="img2" accept="image/*">

<button onclick="showReport()">إنشاء التقرير</button>

</div>
</div>

<!-- REPORT PAGE -->
<div id="reportPage">
<div class="action-box">
 <button id="printBtn" onclick="window.print()">طباعة</button>
 <button id="pdfBtn" onclick="downloadPDF()">PDF</button>
</div>
<div id="reportContent"></div>
</div>

<script>
function getImg(id){
return new Promise(res=>{
const f=document.getElementById(id).files[0];
if(!f)return res("");
const R=new FileReader();
R.onload=()=>res(`<img src="${R.result}" style="width:100%;height:100%;object-fit:cover;border-radius:5px;">`);
R.readAsDataURL(f);
});
}

async function showReport(){
const v=id=>document.getElementById(id).value||"";
const img1=await getImg("img1"),img2=await getImg("img2");

document.getElementById("reportContent").innerHTML=`
<div class="header">
<div class="ministry">
<img src="https://i.ibb.co/j6QD2sS/moe.png">
وزارة التعليم<br>Ministry of Education
</div>
<div class="admin">${v('admin')}</div>
<div class="school">${v('school')}</div>
<div class="date" id="hDate"></div>
</div>

<div class="info">
<div class="grid4">
 <div class="ibox"><strong>الفصل</strong>${v('term')}</div>
 <div class="ibox"><strong>الصف</strong>${v('grade')}</div>
 <div class="ibox"><strong>المادة</strong>${v('subject')}</div>
 <div class="ibox"><strong>التقرير</strong>${v('type')}</div>
</div>
<div class="grid4">
 <div class="ibox"><strong>المستهدفون</strong>${v('target')}</div>
 <div class="ibox"><strong>العدد</strong>${v('count')}</div>
 <div class="ibox"><strong>مكان التنفيذ</strong>${v('place')}</div>
 <div class="ibox"><strong>المعلم</strong>${v('teacher')}</div>
</div>
</div>

<div class="page">
<div class="objective">${v('objective')}</div>

<div class="sectors">
<div class="sec green"><div class="sec-title">وصف مختصر</div><div class="sec-content">${v('desc')}</div></div>
<div class="sec green"><div class="sec-title">النتائج</div><div class="sec-content">${v('results')}</div></div>
<div class="sec blue"><div class="sec-title">نقاط القوة</div><div class="sec-content">${v('strengths')}</div></div>
<div class="sec red"><div class="sec-title">التحديات</div><div class="sec-content">${v('challenges')}</div></div>
<div class="sec gray"><div class="sec-title">إجراءات التنفيذ</div><div class="sec-content">${v('steps')}</div></div>
<div class="sec yellow"><div class="sec-title">المحفزات</div><div class="sec-content">${v('motives')}</div></div>
<div class="sec red"><div class="sec-title">ما يحتاج إلى تطوير</div><div class="sec-content">${v('develop')}</div></div>
<div class="sec blue"><div class="sec-title">التوصيات</div><div class="sec-content">${v('recommend')}</div></div>
</div>

<div class="images">
 <div class="imgbox">${img1}</div>
 <div class="imgbox">${img2}</div>
</div>

<div class="footer">
<div>مدير المدرسة:<br>${v('manager')}</div>
<div>المعلم:<br>${v('teacher')}</div>
</div>
</div>`;

fetch('https://api.aladhan.com/v1/gToH')
.then(r=>r.json()).then(d=>{
const h=d.data.hijri;
document.getElementById('hDate').textContent=h.day+' '+h.month.ar+' '+h.year+' هـ';
});

document.getElementById("formPage").style.display="none";
document.getElementById("reportPage").style.display="block";
}

function downloadPDF(){
var element=document.getElementById("reportContent");
var opt={
 margin:0,
 filename:'تقرير-حصص-النشاط.pdf',
 image:{type:'jpeg',quality:1},
 html2canvas:{scale:3},
 jsPDF:{unit:'mm',format:'a4',orientation:'portrait'}
};
html2pdf().set(opt).from(element).save();
}
</script>

</body>
</html>