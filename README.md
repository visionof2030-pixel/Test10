<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<title>تقرير تفعيل حصص النشاط</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap');
*{box-sizing:border-box;font-family:'Cairo',sans-serif;}
body{margin:0;background:#f3f4f6;}
button{cursor:pointer}

/* PAGE SWITCH */
#formPage{display:block}
#reportPage{display:none}

/* PANEL */
.panel{
  background:white;padding:18px;
  max-width:380px;margin:auto;
  border-left:4px solid #083024;
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

/* REPORT ONE PAGE */
#reportPage{
  background:white;
  width:210mm;
  min-height:297mm;
  margin:auto;
  padding:0;
  overflow:hidden;
}

@page{size:A4;margin:6mm;}
@media print{
  #formPage{display:none!important}
  #printBtn,#pdfBtn,#printIcon{display:none!important}
  *{-webkit-print-color-adjust:exact;print-color-adjust:exact}
}

/* HEADER */
.header{
 height:90px;background:#083024;color:white;position:relative;
}
.header::before{
 content:"";position:absolute;inset:0;opacity:.9;
 background:url('https://i.ibb.co/kVWFFwhW/9-C92-E57-B-23-FA-479-D-A024-1-D5-F871-B4-F8-D.png')
 center/38% no-repeat;
}
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
#printIcon{
 position:absolute;top:10px;left:10px;background:#083024;
 width:36px;height:36px;border-radius:6px;
 display:flex;align-items:center;justify-content:center;color:white;font-size:20px;
}
.action-box{
 display:flex;
 justify-content:center;
 margin-top:8px;
 gap:6px;
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
"تنمية مهارات الطلاب وتعزيز مواهبهم عبر المشاركة الفعالة.",
"بناء شخصية قيادية متوازنة لدى الطلاب من خلال العمل الجماعي.",
"تحفيز الإبداع والتفكير الناقد عبر أنشطة تطبيقية.",
"تعزيز الانتماء للمدرسة وتنمية مهارات التواصل."
],desc:[
"تنفيذ نشاط يعزز العمل التعاوني ويتيح فرصًا للتطبيق العملي.",
"تصميم أنشطة محفزة تسهم في تطوير مهارات الطلاب.",
"مشاركة الطلاب في نشاط يحقق الأهداف السلوكية والتعليمية.",
"استخدام استراتيجيات تعلم حديثة لزيادة التفاعل."
],steps:[
"توضيح الأهداف وتوزيع الأدوار ثم تنفيذ المهمة بإشراف المعلم.",
"تقسيم الطلاب لمجموعات وتكليفهم بمهام محددة.",
"تهيئة أدوات النشاط ومتابعة التنفيذ ثم التقييم.",
"تنظيم أدوار المشاركة وتقديم الدعم المستمر."
],results:[
"ارتفاع التفاعل وتحسن مهارات التواصل.",
"بروز مواهب وقدرات جديدة لدى الطلاب.",
"زيادة حماس الطلاب للتعلم عبر النشاط.",
"تحقيق أهداف النشاط وتنمية الجوانب المهارية."
],motives:[
"تحفيز الطلاب بالمكافآت والإشادة بالمتميزين.",
"تعزيز المنافسة الإيجابية لزيادة المشاركة.",
"تهيئة بيئة تعليمية مشوقة.",
"استخدام أساليب تحفيزية متنوعة."
],challenges:[
"تفاوت مستويات المشاركة بين الطلاب.",
"ضيق الوقت مقارنة بخطة النشاط.",
"الحاجة لضبط بعض السلوكيات.",
"قلة الأدوات لبعض الأنشطة."
],strengths:[
"تنوع النشاط وملاءمته لقدرات الطلاب.",
"تنظيم ممتاز لعملية التنفيذ.",
"ارتفاع التفاعل والمبادرة.",
"تحسن التعاون داخل الفصل."
],develop:[
"دعم الطلاب الأقل مشاركة.",
"تخصيص وقت إضافي للنشاط.",
"زيادة تجهيزات الأنشطة.",
"رفع مستوى التشجيع."
],recommend:[
"الاستمرار في تفعيل حصص النشاط.",
"زيادة الدعم اللوجستي للأنشطة.",
"تخصيص مساحة لعرض المنجزات.",
"توسيع استخدام التقنية."
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
</div></div>

<!-- REPORT PAGE -->
<div id="reportPage">
<div id="printIcon" onclick="window.print()">🖨️</div>
<div class="action-box">
 <button id="printBtn" onclick="window.print()">طباعة</button>
 <button id="pdfBtn" onclick="downloadPDF()">PDF</button>
</div>
<div id="reportContent"></div>
</div>

<!-- PDF LIBRARY -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>

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
var element=document.getElementById("reportPage");
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