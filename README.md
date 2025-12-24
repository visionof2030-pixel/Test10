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
/* REPORT */
@page{size:A4;margin:8mm;}
@media print{
  #formPage{display:none!important}
  #printBtn,#printIcon{display:none!important}
  *{-webkit-print-color-adjust:exact;print-color-adjust:exact}
}
#reportPage{
  background:white;
  width:210mm;min-height:100vh;
  margin:auto;padding:0;
}
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
.info{padding:8px;}
.grid4{display:grid;grid-template-columns:repeat(4,1fr);gap:4px;margin-bottom:6px;}
.ibox{border:1px solid #083024;border-radius:4px;padding:4px;text-align:center;font-size:7px;background:white}
.ibox strong{display:block;font-size:7.5px;color:#083024;}
.page{padding:8px;}
.objective{
 background:#dcece5;border:1px solid #0b543a;border-radius:6px;
 height:70px;display:flex;align-items:center;justify-content:center;
 font-size:7.8px;font-weight:bold;text-align:center;margin-bottom:8px;line-height:1.6;
}
.sectors{display:grid;grid-template-columns:repeat(4,1fr);gap:6px;margin-top:8px;}
.sec{padding:6px;border-radius:6px;font-size:6.5px;}
.sec-title{font-size:7.2px;font-weight:bold;border-bottom:1px solid #3333;padding-bottom:2px;margin-bottom:2px;}
.sec-content{white-space:pre-line;line-height:1.4;}
.green{background:#e3ede8;border:1px solid #0c5c42;}
.blue{background:#e5e9f3;border:1px solid #1e3a8a;}
.yellow{background:#fff7d4;border:1px solid #c99b00;}
.red{background:#fde8e7;border:1px solid #a83e3e;}
.images{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-top:10px;}
.imgbox{height:130px;border:1px solid #083024;border-radius:6px;overflow:hidden;background:#eee;}
.footer{margin-top:14px;display:flex;justify-content:space-between;font-size:9px;font-weight:bold;}
#printBtn{
 background:#0b4c36;color:white;
 padding:12px;border-radius:6px;
 width:180px;margin:10px auto;display:block;font-size:14px;
}
#printIcon{
 position:absolute;top:10px;left:10px;background:#083024;
 width:36px;height:36px;border-radius:6px;
 display:flex;align-items:center;justify-content:center;color:white;font-size:20px;
}
</style>
</head>
<body>

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
const autos={
objective:[
"تنمية مهارات الطلاب وتعزيز مواهبهم عبر المشاركة الفعالة في أنشطة تربوية تطبيقية.",
"بناء شخصية قيادية متوازنة لدى الطلاب من خلال العمل الجماعي والتجارب الواقعية.",
"تحفيز الإبداع والتفكير الناقد عبر أنشطة متنوعة تربط التعلم بالحياة اليومية.",
"تعزيز الانتماء للمدرسة وتنمية مهارات التواصل الاجتماعي للطلاب."
],
desc:[
"تنفيذ نشاط داخل حصص النشاط يعزز العمل التعاوني ويتيح فرصًا للتطبيق العملي.",
"تصميم أنشطة محفزة تسهم في تطوير المهارات التعليمية والحياتية لدى الطلاب.",
"تفعيل مشاركة الطلاب في نشاط مدرسي يحقق الأهداف السلوكية والتعليمية.",
"استخدام استراتيجيات تعلم حديثة لجذب انتباه الطلاب وزيادة التفاعل."
],
steps:[
"توضيح أهداف النشاط وتوزيع الأدوار ثم تنفيذ المهمة بإشراف المعلم.",
"تقسيم الطلاب لمجموعات وتكليفهم بمهام محددة وعرض النتائج.",
"تهيئة أدوات النشاط ومتابعة التنفيذ ثم التقييم البنّاء.",
"تنظيم أدوار المشاركة وتقديم الدعم للتحسين المستمر."
],
results:[
"ارتفاع تفاعل الطلاب وتحسن في مهارات التواصل والعمل الجماعي.",
"بروز مواهب وقدرات جديدة ساهمت في تحقيق مخرجات إيجابية.",
"زيادة حماس الطلاب للتعلم عبر النشاط التربوي.",
"تحقيق أهداف النشاط وتنمية الجوانب المهارية."
],
motives:[
"تحفيز الطلاب بالمكافآت والإشادة بالمتميزين.",
"تعزيز المنافسة الإيجابية لزيادة المشاركة.",
"تهيئة بيئة تعليمية مشوقة تساعد على التفاعل.",
"استخدام أساليب تحفيزية متنوعة."
],
challenges:[
"تفاوت مستويات المشاركة بين الطلاب.",
"ضيق الوقت مقارنة بخطة النشاط.",
"الحاجة لضبط بعض السلوكيات التعاونية.",
"قلة الأدوات لبعض الأنشطة."
],
strengths:[
"تنوع النشاط وملاءمته لقدرات الطلاب.",
"تنظيم ممتاز سهل عملية التنفيذ.",
"ارتفاع التفاعل وروح المبادرة لدى الطلاب.",
"تحسن في التعاون داخل الفصل."
],
develop:[
"تطوير الدعم للطلاب الأقل مشاركة لزيادة تفاعلهم.",
"تخصيص وقت إضافي لتعزيز التطبيق العملي.",
"زيادة تجهيزات الأنشطة لضمان تنوعها.",
"رفع مستوى التشجيع لضمان استمرار الدافعية."
],
recommend:[
"الاستمرار في تفعيل حصص النشاط بطرق متميزة.",
"زيادة الدعم اللوجستي اللازم لتنوع الأنشطة.",
"تخصيص مساحة لعرض منجزات الطلاب.",
"التوسع في استخدام التقنية داخل النشاط."
]
};
const idx={};for(const k in autos) idx[k]=0;
function autoFill(k){idx[k]=(idx[k]+1)%autos[k].length;document.getElementById(k).value=autos[k][idx[k]];}
</script>

<script>
function F(t,i){
return `
<div class="field">
<label>${t}</label>
<textarea id="${i}"></textarea>
<div class="auto-box">
<div class="auto-btn" onclick="autoFill('${i}')">✦</div>
<div class="auto-text">اضغط للتبديل</div>
</div></div>`}
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

<div id="reportPage">
<div id="printIcon" onclick="window.print()">🖨️</div>
<button id="printBtn" onclick="window.print()">طباعة التقرير</button>
<div id="reportContent"></div>
</div>

<script>
function getImg(id){
return new Promise(res=>{
 const f=document.getElementById(id).files[0];
 if(!f)return res("");
 const R=new FileReader();
 R.onload=()=>res(`<img src="${R.result}" style="width:100%;height:100%;object-fit:cover;border-radius:6px;">`);
 R.readAsDataURL(f);
});
}

async function showReport(){
 const v=id=>document.getElementById(id).value||"";
 const img1=await getImg("img1");
 const img2=await getImg("img2");

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
</script>

</body>
</html>