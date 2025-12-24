<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<title>تقرير تفعيل حصص النشاط</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap');
*{box-sizing:border-box;font-family:'Cairo',sans-serif;}
body{
  margin:0;background:#f3f4f6;
  display:grid;grid-template-columns:360px 1fr;
  height:100vh;
}
.panel{
  background:white;padding:16px;
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
.auto-box{display:flex;align-items:center;gap:6px;margin-top:4px;}
.auto-btn{
  width:26px;height:26px;border-radius:4px;
  background:#ddd;border:1px solid #aaa;
  text-align:center;line-height:24px;cursor:pointer;
}
.auto-text{font-size:9px;color:#555;}
button{
  width:100%;padding:10px;
  background:#083024;color:white;
  border:none;border-radius:6px;
  font-size:14px;margin-top:10px;
}
</style>
</head>
<body>

<div class="panel">
<h2 style="color:#083024">بيانات التقرير</h2>

<div class="field">
<label>الإدارة العامة للتعليم</label>
<select id="admin">
<option>الإدارة العامة للتعليم بمنطقة مكة المكرمة – مكة المكرمة</option>
</select>
</div>

<div class="field"><label>اسم المدرسة</label><input id="school"></div>

<div class="field"><label>الفصل الدراسي</label>
<select id="term">
<option>الفصل الدراسي الأول</option>
<option>الفصل الدراسي الثاني</option>
</select></div>

<div class="field"><label>الصف</label><input id="grade"></div>
<div class="field"><label>المادة</label><input id="subject"></div>

<div class="field"><label>نوع التقرير</label>
<select id="type">
<option>تقرير تفعيل حصص النشاط</option>
</select></div>

<div class="field"><label>المستهدفون</label><input id="target"></div>
<div class="field"><label>العدد</label><input id="count"></div>
<div class="field"><label>مكان التنفيذ</label><input id="place"></div>
<div class="field"><label>اسم المعلم</label><input id="teacher"></div>
<div class="field"><label>اسم مدير المدرسة</label><input id="manager"></div>

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
const idx={};
for(const k in autos) idx[k]=0;
function autoFill(k){
 idx[k]=(idx[k]+1)%autos[k].length;
 document.getElementById(k).value=autos[k][idx[k]];
}
</script>

<!-- خانات النصوص -->
<script>
function field(title,id){
 return `
<div class="field"><label>${title}</label>
<textarea id="${id}"></textarea>
<div class="auto-box">
<div class="auto-btn" onclick="autoFill('${id}')">✦</div>
<div class="auto-text">اضغط للتبديل</div>
</div></div>
`;
}
document.write(
 field("الهدف التربوي","objective")+
 field("وصف مختصر","desc")+
 field("إجراءات التنفيذ","steps")+
 field("النتائج","results")+
 field("المحفزات","motives")+
 field("التحديات","challenges")+
 field("نقاط القوة","strengths")+
 field("ما يحتاج إلى تطوير","develop")+
 field("التوصيات","recommend")
);
</script>

<div class="field"><label>صورة 1</label><input type="file" id="img1" accept="image/*"></div>
<div class="field"><label>صورة 2</label><input type="file" id="img2" accept="image/*"></div>

<button onclick="generate()">إنشاء التقرير</button>
<button onclick="generate()">طباعة</button>

</div>

<script>
function getImg(id){
 return new Promise(res=>{
   const f=document.getElementById(id).files[0];
   if(!f) return res("");
   const r=new FileReader();
   r.onload=()=>res(`<img src="${r.result}" style="width:100%;height:100%;object-fit:cover;border-radius:6px;">`);
   r.readAsDataURL(f);
 });
}
async function generate(){
 const v=id=>document.getElementById(id).value||"";
 const img1=await getImg('img1');
 const img2=await getImg('img2');

 const html=`<!DOCTYPE html><html dir="rtl" lang="ar"><head><meta charset="UTF-8">
<style>@page{size:A4;margin:8mm;}</style></head><body>
<table border="1" width="100%" style="font-family:Cairo;font-size:10px;border-collapse:collapse">
<tr><td colspan="4">${v('admin')}</td></tr>
<tr><td>${v('term')}</td><td>${v('grade')}</td><td>${v('subject')}</td><td>${v('type')}</td></tr>
<tr><td>${v('target')}</td><td>${v('count')}</td><td>${v('place')}</td><td>${v('teacher')}</td></tr>
</table><br>
<div>${v('objective')}</div><br>
<div>${v('desc')}</div><br>
<div>${v('steps')}</div><br>
<div>${v('results')}</div><br>
<div>${v('motives')}</div><br>
<div>${v('challenges')}</div><br>
<div>${v('strengths')}</div><br>
<div>${v('develop')}</div><br>
<div>${v('recommend')}</div><br>
<div style="display:flex;gap:10px;">${img1}${img2}</div>
<script>window.print();<\/script>
</body></html>`;

const w=window.open("","_blank");
w.document.write(html);
w.document.close();
}
</script>

</body>
</html>