<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>إنشاء تقرير تفعيل حصص النشاط</title>

<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap');
*{box-sizing:border-box;font-family:'Cairo',sans-serif;}
body{margin:0;background:#f3f4f6;display:flex;justify-content:center;padding:0 6px;}

.panel{
background:#ffffff;width:100%;max-width:450px;margin-top:18px;
padding:16px;border-right:5px solid #083024;border-radius:4px;
}
h2{font-size:18px;text-align:center;color:#083024;margin-bottom:16px;}
.field{margin-bottom:12px;}
label{font-size:11px;margin-bottom:4px;display:block;color:#083024;}
input, select, textarea{
width:100%;padding:8px;font-size:14px;
border:1px solid #d1d5db;border-radius:4px;
}
textarea{min-height:60px;resize:vertical;}
.auto-btn{
background:#083024;color:#fff;padding:5px 8px;border-radius:4px;
font-size:10px;margin-top:4px;border:none;cursor:pointer;width:100%;
}
button{
width:100%;padding:12px;background:#083024;color:white;border:0;
border-radius:6px;font-size:16px;cursor:pointer;margin-top:12px;
}
</style>
</head>

<body>

<div class="panel">

<h2>بيانات التقرير</h2>

<div class="field"><label>الإدارة</label>
<select id="admin"><option>الإدارة العامة للتعليم بمنطقة مكة المكرمة – مكة المكرمة</option></select></div>

<div class="field"><label>اسم المدرسة</label><input id="school" value="مدرسة سعيد بن العاص"></div>

<div class="field"><label>الفصل الدراسي</label>
<select id="term"><option>الفصل الدراسي الأول</option><option>الفصل الدراسي الثاني</option></select></div>

<div class="field"><label>الصف</label><input id="grade"></div>
<div class="field"><label>المادة</label><input id="subject"></div>
<div class="field"><label>نوع التقرير</label><select id="type"><option>تقرير تفعيل حصص النشاط</option></select></div>
<div class="field"><label>المستهدفون</label><input id="target"></div>
<div class="field"><label>العدد</label><input id="count" type="number"></div>
<div class="field"><label>مكان التنفيذ</label><input id="place"></div>

<div class="field"><label>اسم المعلم</label><input id="teacher" value="فهد الخالدي"></div>
<div class="field"><label>اسم مدير المدرسة</label><input id="manager"></div>

<script>
const autos={
objective:[
"تنمية مهارات الطلاب وتعزيز مشاركتهم عبر الأنشطة التطبيقية.",
"رفع دافعية التعلم لدى الطلاب عبر أنشطة تفاعلية محفّزة.",
"تنمية مهارات التفكير الناقد والتواصل الفعّال.",
"بناء شخصيات قيادية من خلال التعاون والعمل الجماعي."
],
desc:[
"تنفيذ نشاط طلابي تعاوني يعتمد على تبادل الأدوار وتنمية مهارات التنظيم والتفاعل الإيجابي.",
"تطبيق نشاط محفّز يعزز التعلم التعاوني ويحقق نواتج تعليمية فعّالة.",
"نشاط تفاعلي يدمج التطبيق العملي بتنمية المهارات السلوكية والمعرفية.",
"تنفيذ نشاط يسمح للطلاب بإبراز قدراتهم وتحمل المسؤولية."
],
steps:[
"توزيع المهام وشرح الأهداف ثم تنفيذ النشاط وتقييم نتائجه.",
"تقسيم الطلاب لمجموعات وتقديم التوجيه والتحفيز أثناء التنفيذ.",
"تهيئة الوسائل ثم تنفيذ النشاط ومتابعة المشاركة وفق الخطة.",
"متابعة سير العمل وتحفيز المبادرة وروح الفريق."
],
results:[
"ارتفاع مستوى التفاعل وتحسن مهارات التواصل لدى الطلاب.",
"زيادة الدافعية وتحقيق نتائج إيجابية تعزز التعلم.",
"تطور المهارات الشخصية والسلوكية للطلاب المشاركين.",
"تحقيق الأهداف المخطط لها ورفع مستوى المشاركة."
],
strengths:[
"تفاعل متميز للطلاب داخل النشاط وتعاون فعّال بينهم.",
"تنوع الأساليب والإستراتيجيات مما ساعد على تحقيق الأهداف.",
"تنظيم ممتاز للعمل وتوزيع عادل للأدوار داخل المجموعات.",
"ارتفاع مستوى الحماس والمشاركة أثناء التنفيذ."
],
challenges:[
"تفاوت مستويات المشاركة واحتياج البعض للدعم المستمر.",
"ضيق الوقت المتاح مقارنة بخطوات النشاط.",
"صعوبة تنظيم تركيز بعض الطلاب خلال النشاط.",
"الحاجة إلى تهيئة بيئة أنسب لبعض المهام العملية."
],
develop:[
"زيادة دعم الطلاب الأقل تفاعلًا داخل النشاط.",
"تخصيص وقت إضافي للأنشطة ذات الطابع العملي.",
"توفير وسائل وأدوات تعليمية إضافية.",
"تنمية روح المسؤولية لدى جميع المشاركين."
],
recommend:[
"الاستمرار في تفعيل حصص النشاط لتعزيز المهارات الطلابية.",
"التوسع في الأنشطة الإثرائية ورفع مستوى التحفيز.",
"عرض منجزات الطلاب وتشجيع الإبداع والمبادرات.",
"استخدام التقنية بطرق مبتكرة لدعم تنفيذ الأنشطة."
]
};
const idx={};for(const k in autos) idx[k]=0;
function autoFill(k){idx[k]=(idx[k]+1)%autos[k].length;document.getElementById(k).value=autos[k][idx[k]];}
function addField(title,id){
document.write(`
<div class="field">
<label>${title}</label>
<textarea id="${id}"></textarea>
<button type="button" class="auto-btn" onclick="autoFill('${id}')">اقتراح تلقائي</button>
</div>`);
}
addField("الهدف التربوي","objective");
addField("وصف مختصر","desc");
addField("إجراءات التنفيذ","steps");
addField("النتائج","results");
addField("نقاط القوة","strengths");
addField("التحديات","challenges");
addField("ما يحتاج إلى تطوير","develop");
addField("التوصيات","recommend");
</script>

<div class="field"><label>صورة 1</label><input type="file" id="img1" accept="image/*"></div>
<div class="field"><label>صورة 2</label><input type="file" id="img2" accept="image/*"></div>

<button onclick="saveData()">إنشاء التقرير</button>

<script>
function encodeImage(file, key){
const reader=new FileReader();
reader.onload=function(){localStorage.setItem(key,reader.result);};
reader.readAsDataURL(file);
}
document.getElementById("img1").addEventListener("change",e=>{
if(e.target.files[0])encodeImage(e.target.files[0],"img1");
});
document.getElementById("img2").addEventListener("change",e=>{
if(e.target.files[0])encodeImage(e.target.files[0],"img2");
});
function saveData(){
let data={};
document.querySelectorAll("input,select,textarea").forEach(el=>{
data[el.id]=el.value;
});
localStorage.setItem("reportData",JSON.stringify(data));
location.href="report/report.html";
}
</script>

</div>
</body>
</html>