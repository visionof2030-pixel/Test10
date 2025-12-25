<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>إنشاء تقرير تفعيل حصص النشاط</title>

<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap');
*{box-sizing:border-box;font-family:'Cairo',sans-serif;}
body{margin:0;background:#f3f4f6;display:flex;justify-content:center;padding:0 8px;}
.panel{
background:#ffffff;width:100%;max-width:480px;margin:18px 0;
padding:18px;border-right:5px solid #083024;border-radius:4px;
}
h2{font-size:18px;text-align:center;color:#083024;margin-bottom:18px;}
.field{margin-bottom:14px;}
label{font-size:12px;margin-bottom:4px;display:block;color:#083024;}
input, select, textarea{
width:100%;padding:8px;font-size:14px;
border:1px solid #d1d5db;border-radius:4px;
}
textarea{min-height:60px;resize:vertical;}

.auto-btn{
background:#083024;color:#fff;padding:6px;border-radius:4px;
font-size:11px;margin-top:4px;border:none;cursor:pointer;width:100%;
}

button{
width:100%;padding:14px;background:#083024;color:white;border:0;
border-radius:6px;font-size:17px;cursor:pointer;margin-top:14px;
}
</style>
</head>

<body>

<div class="panel">

<h2>بيانات التقرير</h2>

<div class="field"><label>الإدارة</label>
<select id="admin">
<option>الإدارة العامة للتعليم بمنطقة مكة المكرمة – مكة المكرمة</option>
</select>
</div>

<div class="field"><label>اسم المدرسة</label>
<input id="school" value="مدرسة سعيد بن العاص">
</div>

<div class="field"><label>الفصل الدراسي</label>
<select id="term">
<option>الفصل الدراسي الأول</option>
<option>الفصل الدراسي الثاني</option>
</select></div>

<div class="field"><label>الصف</label><input id="grade"></div>
<div class="field"><label>المادة</label><input id="subject"></div>
<div class="field"><label>نوع التقرير</label>
<select id="type"><option>تقرير تفعيل حصص النشاط</option></select></div>
<div class="field"><label>المستهدفون</label><input id="target"></div>
<div class="field"><label>العدد</label><input id="count" type="number"></div>
<div class="field"><label>مكان التنفيذ</label><input id="place"></div>

<div class="field"><label>اسم المعلّم</label>
<input id="teacher" value="فهد الخالدي"></div>

<div class="field"><label>اسم مدير المدرسة</label>
<input id="manager"></div>

<!-- حقول النصوص -->
<script>
const autos={
objective:[
"تنمية مهارات الطلاب عبر أنشطة تطبيقية تعزز الثقة بالنفس.",
"رفع مستوى التفاعل والعمل التعاوني من خلال التعلم بالممارسة.",
"تعزيز القدرة على حل المشكلات واتخاذ القرار في مواقف تعليمية.",
"تشجيع المبادرات الإبداعية وتنمية المهارات القيادية لدى الطلاب."
],
desc:[
"تنفيذ نشاط جماعي يهدف إلى تطبيق المعرفة وربطها بالواقع العملي داخل المدرسة.",
"تفعيل نشاط منهجي يتخلله تبادل أدوار وتحفيز مهارات التواصل الإيجابي.",
"نشاط تعليمي تفاعلي يسمح للطلاب بإبراز مهاراتهم وتحمل مسؤولياتهم.",
"برنامج إثرائي يطبق التعلم النشط ويعزز دور الطالب كشريك في التعلم."
],
steps:[
"توزيع الأدوار وشرح التعليمات، ثم تنفيذ النشاط وتقييم المخرجات.",
"تقسيم الطلاب لمجموعات، وتوجيه التفاعل أثناء أداء المهام.",
"تهيئة الوسائل، وتنفيذ المهمة، ثم متابعة مستوى المشاركة.",
"إدارة النشاط وفق الزمن المخصص وتحفيز الطلاب على الابتكار."
],
results:[
"تحسن ملحوظ في المشاركة الجماعية وتطور المهارات الاجتماعية.",
"ارتفاع الدافعية والانخراط في عملية التعلم بصورة إيجابية.",
"تنمية مهارات الاتصال وحل المشكلات لدى الطلاب المشاركين.",
"تحقيق معظم أهداف النشاط المخطط لها بكفاءة عالية."
],
strengths:[
"تنظيم ممتاز للأدوار ووجود تفاعل فعّال داخل المجموعات.",
"تنوع الأنشطة مما أسهم في تعزيز التعلم لدى جميع الطلاب.",
"وضوح التعليمات مما أدى لفهم أسرع وتنفيذ أدق.",
"وجود دافعية وحماس لدى الطلاب طوال النشاط."
],
challenges:[
"تفاوت مستوى المشاركة لدى بعض الطلاب.",
"ضيق الوقت مقارنة بمتطلبات تنفيذ النشاط.",
"ضعف استخدام التقنية لدى بعض الطلاب.",
"صعوبة المحافظة على التركيز لدى فئة من الطلاب."
],
develop:[
"زيادة تحفيز الطلاب الأقل مشاركة داخل النشاط.",
"تخصيص وقت إضافي للأنشطة التطبيقية.",
"توفير وسائل تعليمية أكثر دعماً للتنفيذ.",
"تنمية مهارات التفكير وتحمل المسؤولية."
],
recommend:[
"الاستمرار في تفعيل الأنشطة التطبيقية.",
"توسيع نطاق الأنشطة الإثرائية المدعومة بالتقنية.",
"تعزيز التعلم التعاوني وتحفيز الإبداع.",
"عرض منجزات الطلاب وتكريم المشاركين."
]
};

const idx={};for(const k in autos) idx[k]=0;
function autoFill(k){
idx[k]=(idx[k]+1)%autos[k].length;
document.getElementById(k).value = autos[k][idx[k]];
}

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
function encodeImage(file,key){
const reader=new FileReader();
reader.onload=()=>localStorage.setItem(key,reader.result);
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