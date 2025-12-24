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
.field{margin-bottom:14px;}
.field label{font-size:12px;display:block;margin-bottom:4px;}
input,select,textarea{
  width:100%;padding:6px;font-size:12px;
  border:1px solid #ccc;border-radius:4px;
}
textarea{min-height:60px;resize:vertical}

.auto-box{display:flex;gap:6px;align-items:center;margin-top:4px;}
.auto-btn{
  width:26px;height:26px;border-radius:4px;
  text-align:center;line-height:24px;
  cursor:pointer;background:#ddd;
  font-size:16px;border:1px solid #aaa;
}
.auto-text{font-size:9px;color:#555;}

button{
  width:100%;padding:10px;
  background:#083024;color:white;
  border:none;border-radius:6px;
  font-size:14px;margin-top:10px;cursor:pointer;
}

.preview-msg{
  font-size:13px;color:#333;padding:20px;text-align:center;
}
</style>
</head>
<body>

<div class="panel">
<h2 style="color:#083024;">بيانات التقرير</h2>

<!--------- الحقول الرئيسية --------->

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


<!--------- النصوص التلقائية --------->
<script>
const autos={
objective:[
"استثمار حصص النشاط في تعزيز مهارات الطلاب وتنمية مواهبهم بما يحقق مشاركة فعّالة ويزيد من ارتباطهم بالمدرسة.",
"تنمية شخصية الطالب من خلال أنشطة جماعية ترفع الثقة بالنفس والعمل بروح الفريق.",
"توفير بيئة محفزة للإبداع تسهم في تنمية الجوانب المعرفية والمهارية لدى الطلاب.",
"تحقيق تفاعل إيجابي داخل المدرسة عبر تنفيذ أنشطة تعزز الانتماء والقدرات الاجتماعية."
],
desc:[
"تنفيذ نشاط خلال حصة النشاط يركز على مشاركة جميع الطلاب وتحفيزهم على تطبيق المهارات بشكل عملي تفاعلي.",
"تصميم وتنفيذ أنشطة متنوعة بهدف تطوير مهارات الطلاب وربط التعلم بالواقع.",
"إشراك الطلاب في أنشطة تحاكي اهتماماتهم وتساهم في اكتشاف مواهب جديدة.",
"الاعتماد على التعلم التعاوني في إنجاز مهام النشاط وتعزيز روح الفريق."
],
steps:[
"توضيح أهداف النشاط وتوزيع الأدوار ثم تنفيذ المهام بإشراف المعلم ومتابعة التفاعل.",
"تقسيم الطلاب لمجموعات والعمل على خطة نشاط محددة وعرض المخرجات.",
"تهيئة وسائل النشاط ومتابعة التنفيذ ثم تقييم النتائج ومناقشة الفوائد.",
"تنظيم العمل التعاوني وتقديم التغذية الراجعة لتحسين الأداء داخل النشاط."
],
results:[
"زيادة تفاعل الطلاب ومشاركتهم الفاعلة في تنفيذ المهام.",
"تحسن ملحوظ في مهارات التواصل والعمل الجماعي.",
"إبراز مواهب الطلاب وقدرتهم على الابتكار.",
"تعزيز دافعية الطلاب وتحقيق أهداف النشاط."
],
motives:[
"استخدام التشجيع والتحفيز المستمر لزيادة التفاعل بين الطلاب.",
"عرض مشاركات الطلاب المتميزة وإبراز منجزاتهم.",
"خلق روح تنافس إيجابي بين المجموعات.",
"توفير بيئة مشجعة ومحفزة للطلاب."
],
challenges:[
"تفاوت مستويات المشاركة بين الطلاب داخل المجموعات.",
"عدم توفر الوقت الكافي لتنفيذ جميع مهام النشاط.",
"الحاجة إلى ضبط سلوك بعض الطلاب أثناء التنفيذ.",
"قلة توفر الأدوات المناسبة لبعض الأنشطة."
],
strengths:[
"تنوع الأنشطة جذبت اهتمام الطلاب وحققت تفاعلهم.",
"مناسبة النشاط لقدرات الطلاب وميولهم.",
"تنفيذ منظم ساهم في تحقيق أهداف النشاط.",
"تحسن ملحوظ في روح التعاون داخل الفصل."
],
develop:[
"زيادة دعم الطلاب الأقل تفاعلًا لضمان مشاركة عادلة للجميع.",
"تخصيص وقت إضافي لبعض الأنشطة لتحقيق نتائج أفضل.",
"توفير أدوات وموارد أكثر لتنوع الأنشطة.",
"تحسين الأساليب التحفيزية لضمان استمرارية الحماس أثناء النشاط."
],
recommend:[
"الاستمرار في تفعيل حصص النشاط بطرق جذابة ومحفزة.",
"زيادة زمن النشاط عند الحاجة لضمان تنفيذ أفضل.",
"توفير أدوات ومواد إضافية تدعم جودة النشاط.",
"إتاحة مزيد من الفرص لعرض منجزات الطلاب."
]
};

const idx={objective:0,desc:0,steps:0,results:0,motives:0,challenges:0,strengths:0,develop:0,recommend:0};
function autoFill(k){
 idx[k]=(idx[k]+1)%autos[k].length;
 document.getElementById(k).value=autos[k][idx[k]];
}
</script>


<!--------- خانات النصوص --------->

<div class="field"><label>الهدف التربوي</label><textarea id="objective"></textarea><div class="auto-box"><div class="auto-btn" onclick="autoFill('objective')">✦</div><div class="auto-text">اضغط للتبديل</div></div></div>

<div class="field"><label>وصف مختصر</label><textarea id="desc"></textarea><div class="auto-box"><div class="auto-btn" onclick="autoFill('desc')">✦</div><div class="auto-text">اضغط للتبديل</div></div></div>

<div class="field"><label>إجراءات التنفيذ</label><textarea id="steps"></textarea><div class="auto-box"><div class="auto-btn" onclick="autoFill('steps')">✦</div><div class="auto-text">اضغط للتبديل</div></div></div>

<div class="field"><label>النتائج</label><textarea id="results"></textarea><div class="auto-box"><div class="auto-btn" onclick="autoFill('results')">✦</div><div class="auto-text">اضغط للتبديل</div></div></div>

<div class="field"><label>المحفزات</label><textarea id="motives"></textarea><div class="auto-box"><div class="auto-btn" onclick="autoFill('motives')">✦</div><div class="auto-text">اضغط للتبديل</div></div></div>

<div class="field"><label>التحديات</label><textarea id="challenges"></textarea><div class="auto-box"><div class="auto-btn" onclick="autoFill('challenges')">✦</div><div class="auto-text">اضغط للتبديل</div></div></div>

<div class="field"><label>نقاط القوة</label><textarea id="strengths"></textarea><div class="auto-box"><div class="auto-btn" onclick="autoFill('strengths')">✦</div><div class="auto-text">اضغط للتبديل</div></div></div>

<div class="field"><label>ما يحتاج إلى تطوير</label><textarea id="develop"></textarea><div class="auto-box"><div class="auto-btn" onclick="autoFill('develop')">✦</div><div class="auto-text">اضغط للتبديل</div></div></div>

<div class="field"><label>التوصيات</label><textarea id="recommend"></textarea><div class="auto-box"><div class="auto-btn" onclick="autoFill('recommend')">✦</div><div class="auto-text">اضغط للتبديل</div></div></div>


<!--------- الصور --------->

<div class="field"><label>صورة 1</label><input type="file" id="img1" accept="image/*"></div>
<div class="field"><label>صورة 2</label><input type="file" id="img2" accept="image/*"></div>


<!--------- الأزرار --------->

<button onclick="generate()">إنشاء التقرير</button>
<button onclick="generate()">طباعة</button>

</div><!-- panel -->

<div class="preview-msg">
تم تفعيل الطباعة المباشرة كما كانت سابقًا
</div>


<!--------- سكربت إنشاء التقرير والطباعة --------->

<script>
function getImg(id){
 const f=document.getElementById(id).files[0];
 return new Promise(res=>{
   if(!f)return res("");
   const R=new FileReader();
   R.onload=()=>res(`<img src="${R.result}" style="width:100%;height:100%;object-fit:cover;border-radius:6px;">`);
   R.readAsDataURL(f);
 });
}

async function generate(){
 const v=id=>document.getElementById(id).value||"";
 const img1=await getImg('img1');
 const img2=await getImg('img2');

 const html=`<!DOCTYPE html><html lang="ar" dir="rtl"><head><meta charset="UTF-8">
<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap');
*{margin:0;padding:0;box-sizing:border-box;}
body{font-family:'Cairo',sans-serif;}
@page{size:A4;margin:8mm;}
@media print{*{-webkit-print-color-adjust:exact!important;print-color-adjust:exact!important}}
.header{
 height:90px;background:#083024;color:white;position:relative;
}
.header::before{
 content:"";position:absolute;inset:0;opacity:.9;
 background:url('https://i.ibb.co/kVWFFwhW/9-C92-E57-B-23-FA-479-D-A024-1-D5-F871-B4-F8-D.png')
 center/38% no-repeat;
}
.admin{position:absolute;top:5px;right:10px;font-size:8px;font-weight:bold;}
.school{position:absolute;bottom:5px;right:10px;font-size:8px;}
.date{position:absolute;bottom:5px;left:10px;font-size:8px;}

.info{max-width:210mm;margin:auto;padding:8px;}
.grid4{display:grid;grid-template-columns:repeat(4,1fr);gap:4px;margin-bottom:6px;}
.ibox{border:1px solid #083024;border-radius:4px;padding:4px;text-align:center;font-size:7px;}
.ibox strong{display:block;font-size:7.5px;color:#083024;}

.page{max-width:210mm;margin:auto;padding:8px;}
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
.gray{background:#f4f4f4;border:1px solid #6c6c6c;}

.images{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-top:10px;}
.imgbox{height:130px;border:1px solid #083024;border-radius:6px;overflow:hidden;background:#eee;display:flex;align-items:center;justify-content:center;}

.footer{max-width:210mm;margin:16px auto 0;display:flex;justify-content:space-between;font-size:9px;font-weight:bold;}
</style>
</head><body>

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
<div class="sec gray"><div class="sec-title">إجراءات التنفيذ</div><div class="sec-content">${v('steps')}</div></div>
<div class="sec green"><div class="sec-title">النتائج</div><div class="sec-content">${v('results')}</div></div>
<div class="sec yellow"><div class="sec-title">المحفزات</div><div class="sec-content">${v('motives')}</div></div>
<div class="sec blue"><div class="sec-title">نقاط القوة</div><div class="sec-content">${v('strengths')}</div></div>
<div class="sec red"><div class="sec-title">التحديات</div><div class="sec-content">${v('challenges')}</div></div>
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

</div>

<script>
fetch('https://api.aladhan.com/v1/gToH')
.then(r=>r.json()).then(d=>{
 const h=d.data.hijri;
 document.getElementById('hDate').textContent=h.day+' '+h.month.ar+' '+h.year+' هـ';
 window.print();
});
</script>

</body></html>`;

const w=window.open("","_blank");
w.document.write(html);
w.document.close();
}
</script>

</body>
</html>