
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<title>أداة إنشاء تقرير نشاط إثرائي</title>
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap" rel="stylesheet">

<style>
*{font-family:'Cairo',sans-serif; box-sizing:border-box;}
body{background:#f2f4f5; padding:20px;}

.form-container{
  max-width:800px;
  margin:auto;
  background:#fff;
  padding:20px;
  border-radius:10px;
  border:1px solid #ddd;
}
.form-group{margin-bottom:12px;}
label{font-weight:600; font-size:15px; margin-bottom:4px; display:block;}
input,textarea,select{
  width:100%; padding:8px; border-radius:6px;
  border:1px solid #ccc; font-size:14px;
}
textarea{height:90px;}

.images-grid{display:grid; grid-template-columns:1fr 1fr; gap:10px;}

button{
  width:100%; background:#0b3d2e; color:#fff;
  padding:12px; font-size:17px;
  border:none; border-radius:6px; margin-top:10px;
  cursor:pointer; font-weight:600;
}
button:hover{background:#0e5641}
</style>
</head>

<body>

<div class="form-container">

<h2 style="text-align:center; margin-bottom:15px;">إنشاء تقرير نشاط إثرائي</h2>

<div class="form-group">
<label>اسم المدرسة</label>
<input id="school" value="مدرسة التجربة النموذجية">
</div>

<div class="form-group">
<label>المادة</label>
<input id="subject" value="أحياء">
</div>

<div class="form-group">
<label>الصف</label>
<input id="grade" value="الثالث الثانوي">
</div>

<div class="form-group">
<label>الفصل الدراسي</label>
<select id="semester">
  <option>الأول</option>
  <option>الثاني</option>
</select>
</div>

<div class="form-group">
<label>مكان التنفيذ</label>
<input id="place" value="الفصل الدراسي">
</div>

<div class="form-group">
<label>عدد الطلاب</label>
<input id="count" type="number" value="25">
</div>

<div class="form-group">
<label>المستهدفون</label>
<input id="target" value="طلاب الصف">
</div>

<div class="form-group">
<label>أسم التقرير</label>
<input id="report" value="نشاط إثرائي">
</div>

<div class="form-group">
<label>الهدف التربوي</label>
<textarea id="objective">شرح مفهوم أساسي في المنهج وتطبيقه عبر أنشطة تفاعلية تركز على التعلم النشط والعمل الجماعي وتنمية مهارات التفكير.</textarea>
</div>

<div class="form-group">
<label>وصف مختصر</label>
<textarea id="desc">تنفيذ درس نموذجي يركز على الفهم العميق والتطبيق العملي للمفاهيم باستخدام أساليب تعليمية حديثة.</textarea>
</div>

<div class="form-group">
<label>إجراءات التنفيذ</label>
<textarea id="steps">عرض المفهوم الجديد، مناقشة أمثلة توضيحية، أنشطة تطبيقية جماعية، حل تمارين فردية، تلخيص النقاط الرئيسية.</textarea>
</div>

<div class="form-group">
<label>النتائج</label>
<textarea id="results">استيعاب غالبية الطلاب للمفهوم، مشاركة فعالة في الأنشطة، إنجاز التمارين وتحقيق أهداف الدرس.</textarea>
</div>

<div class="form-group">
<label>نقاط القوة</label>
<textarea id="strengths">وضوح الشرح، تنوع الأنشطة، إدارة الوقت بفاعلية، مراعاة الفروق الفردية بين الطلاب.</textarea>
</div>

<div class="form-group">
<label>المحفزات</label>
<textarea id="motivation">تفاعل الطلاب الإيجابي، تحفيز روح التنافس بين المجموعات، استخدام وسائل تعليمية جذابة.</textarea>
</div>

<div class="form-group">
<label>مواطن القصور</label>
<textarea id="weakness">نقص بعض الوسائل التعليمية، محدودية المساحة الصفية، ضعف مشاركة عدد محدود من الطلاب.</textarea>
</div>

<div class="form-group">
<label>التحديات</label>
<textarea id="challenge">تفاوت سرعة الاستيعاب بين الطلاب، قصر وقت الحصة، صعوبة بعض المفاهيم العلمية.</textarea>
</div>

<div class="form-group">
<label>شاهد الصورة الأولى</label>
<input type="file" id="img1" accept="image/*">
</div>

<div class="form-group">
<label>شاهد الصورة الثانية</label>
<input type="file" id="img2" accept="image/*">
</div>

<button onclick="generateReport()">إنشاء وطباعة التقرير</button>

</div>

<script>
function getImage(input,cb){
  if(input.files && input.files[0]){
    const r=new FileReader();
    r.onload=e=>cb(e.target.result);
    r.readAsDataURL(input.files[0]);
  }else cb("");
}

function generateReport(){
  getImage(document.getElementById("img1"), img1=>{
  getImage(document.getElementById("img2"), img2=>{

let w=window.open("","_blank");
w.document.write(`
${document.querySelector("style").outerHTML}
<body style="padding:0;margin:0">
${htmlReport(img1,img2)}
<script>
fetch('https://api.aladhan.com/v1/gToH')
.then(r=>r.json())
.then(d=>{
 const h=d.data.hijri;
 document.getElementById('hijriDate').textContent =
 \`\${h.day} \${h.month.ar} \${h.year} هـ\`;
});
<\/script>
</body>
`);
w.document.close();

  });
 });
}

function htmlReport(img1,img2){
return `
<div class="header">
  <div class="admin-name">الإدارة العامة للتعليم بمنطقة الرياض</div>
  <div class="school-name">${school.value}</div>
  <div class="hijri-date" id="hijriDate">—</div>
</div>

<div class="container">

<div class="top-grid">
<div class="box"><strong>المادة</strong><br>${subject.value}</div>
<div class="box"><strong>الصف</strong><br>${grade.value}</div>
<div class="box"><strong>الفصل الدراسي</strong><br>${semester.value}</div>
</div>

<div class="top-grid second">
<div class="box"><strong>مكان التنفيذ</strong><br>${place.value}</div>
<div class="box"><strong>العدد</strong><br>${count.value}</div>
<div class="box"><strong>المستهدفون</strong><br>${target.value}</div>
<div class="box"><strong>التقرير</strong><br>${report.value}</div>
</div>

<div class="box objective">
<div class="box-title">الهدف التربوي</div>
${objective.value}
</div>

<div class="main-grid">

<div class="box"><div class="box-title">إجراءات التنفيذ</div>${steps.value}</div>
<div class="box"><div class="box-title">وصف مختصر</div>${desc.value}</div>
<div class="box recommend"><div class="box-title">التوصيات</div>${results.value}</div>
<div class="box result"><div class="box-title">النتائج</div>${results.value}</div>
<div class="box strength"><div class="box-title">نقاط القوة</div>${strengths.value}</div>
<div class="box motivation"><div class="box-title">المحفزات</div>${motivation.value}</div>
<div class="box weakness"><div class="box-title">مواطن القصور</div>${weakness.value}</div>
<div class="box challenge"><div class="box-title">التحديات</div>${challenge.value}</div>

</div>

<div class="evidence-section">
<div class="evidence-title">شواهد الصور</div>

<div class="evidence-grid">
<div class="evidence-box">
  ${img1?`<img src="${img1}">`:""}
  <div class="evidence-caption">الصورة الأولى</div>
</div>
<div class="evidence-box">
  ${img2?`<img src="${img2}">`:""}
  <div class="evidence-caption">الصورة الثانية</div>
</div>
</div>

</div>

</div>
`;
}
</script>

</body>
</html>