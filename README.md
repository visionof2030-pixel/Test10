<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<title>أداة إنتاج التقارير – تفعيل حصص النشاط</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap');
*{box-sizing:border-box;font-family:'Cairo',sans-serif;}
body{
  margin:0;
  background:#f3f4f6;
  display:grid;
  grid-template-columns:360px 1fr;
  height:100vh;
}
.panel{
  background:white;
  padding:16px;
  overflow-y:auto;
  border-left:4px solid #083024;
}
.panel h2{
  font-size:16px;
  margin-bottom:12px;
  color:#083024;
}
.field{margin-bottom:14px;}
.field label{font-size:12px;display:block;margin-bottom:4px;}
input,select,textarea{
  width:100%;padding:6px;font-size:12px;
  border:1px solid #b9b9b9;border-radius:4px;
}
textarea{min-height:60px;resize:vertical}
.auto-box{display:flex;gap:6px;align-items:center;margin-top:4px;}
.auto-btn{
  font-size:16px;cursor:pointer;background:#ececec;
  width:26px;height:26px;border-radius:4px;
  text-align:center;line-height:24px;border:1px solid #bbb;
}
.auto-text{font-size:9px;color:#555;}
button{
  width:100%;padding:10px;
  background:#083024;color:white;
  border:none;border-radius:6px;
  font-size:14px;margin-top:10px;cursor:pointer;
}
iframe{width:100%;height:100%;border:none;background:white}
</style>
</head>
<body>

<div class="panel">
<h2>بيانات التقرير</h2>

<div class="field">
<label>الإدارة العامة للتعليم</label>
<select id="admin">
<option>الإدارة العامة للتعليم بمنطقة مكة المكرمة – مكة المكرمة</option>
</select>
</div>

<div class="field"><label>اسم المدرسة</label><input id="school"></div>

<div class="field">
<label>الفصل الدراسي</label>
<select id="term">
<option>الفصل الدراسي الأول</option>
<option>الفصل الدراسي الثاني</option>
</select>
</div>

<div class="field"><label>الصف</label><input id="grade"></div>
<div class="field"><label>المادة</label><input id="subject"></div>

<div class="field">
<label>نوع التقرير</label>
<select id="type">
<option>تقرير تفعيل حصص النشاط</option>
</select>
</div>

<div class="field"><label>المستهدفون</label><input id="target"></div>
<div class="field"><label>العدد</label><input id="count"></div>
<div class="field"><label>مكان التنفيذ</label><input id="place"></div>
<div class="field"><label>اسم المعلم</label><input id="teacher"></div>
<div class="field"><label>اسم مدير المدرسة</label><input id="manager"></div>

<script>
const autos={
objective:[
"استثمار حصص النشاط لتنمية مواهب الطلاب وتعزيز مهارات التعاون والابتكار، بما يساهم في بناء شخصية إيجابية قادرة على التفاعل المنتج داخل المجتمع المدرسي."
,"تحقيق التوازن بين الجانب الأكاديمي والمهاري لدى الطلاب من خلال أنشطة تطبيقية تفتح آفاق التفكير وتعزز الثقة بالنفس."
,"تهيئة بيئة محفزة للإبداع تسمح للطلاب باكتشاف قدراتهم الشخصية وتطوير ميولهم بما يتماشى مع متطلبات العصر."
,"رفع مستوى الانتماء للمدرسة عبر تفعيل دور الطالب في التخطيط والتنفيذ للأنشطة التي تواكب اهتماماته وتطلعاته."
],
desc:[
"تنفيذ مجموعة من الأنشطة الهادفة خلال حصص النشاط تركّز على التعلم التعاوني وتحسين مهارات التواصل بين الطلاب بأساليب حديثة جاذبة."
,"تصميم برنامج نشاط مدرسي شامل يُسهم في تعزيز القيم الإيجابية لدى الطلاب واستثمار طاقاتهم بما ينعكس إيجابًا على سلوكهم وتحصيلهم."
,"إتاحة الفرصة للطلاب لخوض تجارب جديدة تعزز قدراتهم القيادية والعملية من خلال الأنشطة الجماعية."
,"تحقيق تفاعل فعّال بين الطلاب عبر أنشطة نوعية مخطط لها وفق احتياجاتهم وقدراتهم الفردية."
],
steps:[
"إعداد خطة للنشاط وتوزيع المهام على الطلاب، ثم تنفيذ الأنشطة بإشراف المعلم ومتابعة الأداء بوسائل تحفيزية تضمن مشاركة الجميع."
,"شرح أهداف النشاط قبل البدء، ثم تقسيم الطلاب إلى مجموعات تعاونية تؤدي المهام وفق جدول زمني مناسب."
,"تنظيم خطوات النشاط وفق منهجية تعلم نشط تعتمد المشاركة الفعّالة وإتاحة المجال للطلاب لاتخاذ القرار."
,"تقديم الدعم اللازم للطلاب خلال التنفيذ، ثم تقييم المخرجات ومناقشة أبرز ما تم تعلمه."
],
results:[
"ارتفاع مستوى اندماج الطلاب وتفاعلهم مع الأنشطة بما ساعد على تعزيز مهارات التواصل والعمل الجماعي."
,"إبراز إبداعات الطلاب وقدرتهم على تحمل المسؤولية وتحقيق نتائج ملموسة داخل الحصة."
,"زيادة دافعية الطلاب للتعلم من خلال النشاط وتحسن أدوارهم القيادية ومشاركتهم."
,"تحقيق أثر إيجابي على الجو المدرسي بتعزيز التعاون والانتماء."
],
motives:[
"تشجيع الطلاب عبر الجوائز الرمزية والتحفيز المستمر وإبراز المشاركات المتميزة."
,"استخدام منافسات المجموعات لتحقيق مستويات أعلى من التفاعل والحماس."
,"تهيئة مناخ داعم يبرز قدرات الطلاب ويزيد دافعيتهم للمشاركة."
,"إضافة عنصر التشويق وربط النشاط باهتمامات الطلاب اليومية."
],
challenges:[
"تفاوت مستويات تفاعل الطلاب ما يستدعي دعمًا إضافيًا للمشاركة العادلة."
,"ضيق الوقت المخصص للنشاط مقارنة بكمية المهام المخطط لها."
,"صعوبة توفير بعض المستلزمات اللازمة لتنويع الأنشطة."
,"الحاجة إلى ضبط السلوك أثناء العمل الجماعي لضمان نجاح النشاط."
],
strengths:[
"وضوح الأهداف ومناسبة الأنشطة لقدرات الطلاب مما ساهم في نجاح التنفيذ وتحقيق الفائدة."
,"تنوع الأنشطة وضمان مشاركة جميع الطلاب بطرق تفاعلية جاذبة."
,"تعزيز العلاقات الإيجابية بين الطلاب عبر العمل التعاوني."
,"فاعلية أساليب التحفيز وانعكاسها المباشر على دافعية الطلاب."
],
recommend:[
"الاستمرار في تنفيذ الأنشطة النوعية وتوسيع نطاقها لتشمل مهارات متنوعة تلبي احتياجات الطلاب."
,"زيادة زمن حصص النشاط لإتاحة فرص أكبر للإبداع والتنفيذ المثالي."
,"توفير مستلزمات إضافية لدعم جودة النشاط وتنويع التجارب التعليمية."
,"تعزيز التواصل مع أولياء الأمور لرفع فاعلية النشاط المدرسي."
]
};

const idx={objective:0,desc:0,steps:0,results:0,motives:0,challenges:0,strengths:0,recommend:0};
function autoFill(key){
 idx[key]=(idx[key]+1)%autos[key].length;
 document.getElementById(key).value=autos[key][idx[key]];
}
</script>

<!-- 8 خانات + الأيقونات -->
<div class="field">
<label>الهدف التربوي</label>
<textarea id="objective"></textarea>
<div class="auto-box"><div class="auto-btn" onclick="autoFill('objective')">✦</div><div class="auto-text">اضغط عدة مرات لخيارات أخرى</div></div>
</div>

<div class="field">
<label>وصف مختصر</label>
<textarea id="desc"></textarea>
<div class="auto-box"><div class="auto-btn" onclick="autoFill('desc')">✦</div><div class="auto-text">اضغط عدة مرات لخيارات أخرى</div></div>
</div>

<div class="field">
<label>إجراءات التنفيذ</label>
<textarea id="steps"></textarea>
<div class="auto-box"><div class="auto-btn" onclick="autoFill('steps')">✦</div><div class="auto-text">اضغط عدة مرات لخيارات أخرى</div></div>
</div>

<div class="field">
<label>النتائج</label>
<textarea id="results"></textarea>
<div class="auto-box"><div class="auto-btn" onclick="autoFill('results')">✦</div><div class="auto-text">اضغط عدة مرات لخيارات أخرى</div></div>
</div>

<div class="field">
<label>المحفزات</label>
<textarea id="motives"></textarea>
<div class="auto-box"><div class="auto-btn" onclick="autoFill('motives')">✦</div><div class="auto-text">اضغط عدة مرات لخيارات أخرى</div></div>
</div>

<div class="field">
<label>التحديات</label>
<textarea id="challenges"></textarea>
<div class="auto-box"><div class="auto-btn" onclick="autoFill('challenges')">✦</div><div class="auto-text">اضغط عدة مرات لخيارات أخرى</div></div>
</div>

<div class="field">
<label>نقاط القوة</label>
<textarea id="strengths"></textarea>
<div class="auto-box"><div class="auto-btn" onclick="autoFill('strengths')">✦</div><div class="auto-text">اضغط عدة مرات لخيارات أخرى</div></div>
</div>

<div class="field">
<label>التوصيات</label>
<textarea id="recommend"></textarea>
<div class="auto-box"><div class="auto-btn" onclick="autoFill('recommend')">✦</div><div class="auto-text">اضغط عدة مرات لخيارات أخرى</div></div>
</div>

<div class="field"><label>صورة 1</label><input type="file" id="img1" accept="image/*"></div>
<div class="field"><label>صورة 2</label><input type="file" id="img2" accept="image/*"></div>

<button onclick="generate()">إنشاء التقرير</button>
<button onclick="printReport()">طباعة</button>
</div>

<iframe id="preview"></iframe>

<script>
function getImage(id){
 const f=document.getElementById(id).files[0];
 return f?new Promise(r=>{
   const fr=new FileReader();
   fr.onload=()=>r('<img src="'+fr.result+'" style="width:100%;height:100%;object-fit:cover;border-radius:6px;">');
   fr.readAsDataURL(f);
 }):Promise.resolve(" ");
}

async function generate(){
 const v=id=>document.getElementById(id).value||'';
 const img1=await getImage('img1');
 const img2=await getImage('img2');

 const html=`
<!DOCTYPE html><html lang="ar" dir="rtl"><head>
<meta charset="UTF-8">
<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap');
*{margin:0;padding:0;box-sizing:border-box;}
body{font-family:'Cairo',sans-serif;background:#fff;color:#000;}
@page{size:A4;margin:8mm;}
@media print{
 *{-webkit-print-color-adjust:exact!important;print-color-adjust:exact!important}
 .header::before{opacity:1!important}
}
.header{height:90px;background:#083024;position:relative;}
.header::before{
content:"";position:absolute;inset:0;
background:url('https://i.ibb.co/kVWFFwhW/9-C92-E57-B-23-FA-479-D-A024-1-D5-F871-B4-F8-D.png')
center/38% no-repeat;opacity:0.95;
}
.admin-top{position:absolute;top:4px;right:12px;font-size:8px;font-weight:bold;color:#fff;}
.school{position:absolute;bottom:6px;right:12px;font-size:8px;color:#fff;}
.date{position:absolute;bottom:6px;left:12px;font-size:8px;color:#fff;}
.info{max-width:210mm;margin:auto;padding:8px;}
.grid4{display:grid;grid-template-columns:repeat(4,1fr);gap:4px;margin-bottom:6px;}
.ibox{border:1px solid #083024;text-align:center;border-radius:4px;padding:4px;font-size:7px;}
.ibox strong{display:block;font-size:7.5px;margin-bottom:1px;color:#083024;}
.page{max-width:210mm;margin:auto;padding:8px;}
.objective{
background:#dcece5;border:1px solid #0b543a;border-radius:6px;
display:flex;align-items:center;justify-content:center;
height:70px;font-size:7.8px;font-weight:bold;line-height:1.6;text-align:center;margin-bottom:8px;
}
.sectors{display:grid;grid-template-columns:repeat(4,1fr);gap:6px;}
.sec{border-radius:6px;padding:6px;font-size:6.5px;}
.sec-title{
font-size:7.2px;font-weight:bold;padding-bottom:2px;margin-bottom:2px;
border-bottom:1px solid #00000020;
}
.sec-content{white-space:pre-line;line-height:1.4;}
.green{background:#e3ede8;border:1px solid #0c5c42;}
.blue{background:#e5e9f3;border:1px solid #1e3a8a;}
.yellow{background:#fff7d4;border:1px solid #c99b00;}
.red{background:#fde8e7;border:1px solid #a83e3e;}
.gray{background:#f4f4f4;border:1px solid #6c6c6c;}
.images{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-top:12px;}
.imgbox{
height:130px;border-radius:6px;border:1px solid #083024;
overflow:hidden;background:#eee;display:flex;justify-content:center;align-items:center;
}
.footer{
max-width:210mm;margin:16px auto 0;
display:flex;justify-content:space-between;font-size:9px;font-weight:bold;
}
</style>
</head><body>

<div class="header">
<div class="admin-top">${v('admin')}</div>
<div class="school">${v('school')}</div>
<div class="date" id="hDate"></div>
</div>

<div class="info">
<div class="grid4">
<div class="ibox"><strong>الفصل الدراسي</strong>${v('term')}</div>
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
<div class="sec gray"><div class="sec-title">إجراءات التنفيذ</div><div class="sec-content">${v('steps')}</div></div>
<div class="sec green"><div class="sec-title">النتائج</div><div class="sec-content">${v('results')}</div></div>
<div class="sec yellow"><div class="sec-title">المحفزات</div><div class="sec-content">${v('motives')}</div></div>
<div class="sec blue"><div class="sec-title">نقاط القوة</div><div class="sec-content">${v('strengths')}</div></div>
<div class="sec red"><div class="sec-title">التحديات</div><div class="sec-content">${v('challenges')}</div></div>
<div class="sec red"><div class="sec-title">مواطن القصور</div><div class="sec-content">${v('weak')}</div></div>
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

</div>

<script>
fetch('https://api.aladhan.com/v1/gToH')
.then(r=>r.json()).then(d=>{
const h=d.data.hijri;
document.getElementById('hDate').textContent=h.day+' '+h.month.ar+' '+h.year+' هـ';
});
</script>

</body></html>`;

const frame=document.getElementById('preview');
frame.srcdoc=html;
}

// زر الطباعة بعد التأكد من تحميل المحتوى
function printReport(){
const frame=document.getElementById('preview');
frame.onload=()=>{frame.contentWindow.print()};
try{frame.contentWindow.print()}catch(e){}
}
</script>

</body>
</html>