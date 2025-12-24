<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<title>أداة إعداد تقرير نشاط إثرائي</title>
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap" rel="stylesheet">
<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:'Cairo',sans-serif}
body{background:#f3f4f6;padding:20px;color:#083024}
.form-container{
  max-width:900px;margin:auto;background:#fff;padding:20px;border-radius:10px;
  border:2px solid #083024
}
.form-container h2{margin-bottom:15px;text-align:center}
label{font-weight:600;margin:8px 0;display:block}
input,textarea,select{
  width:100%;padding:6px;border:1px solid #aaa;border-radius:6px;margin-top:3px
}
textarea{height:70px;resize:vertical}
.grid{display:grid;gap:10px}
.grid-3{grid-template-columns:repeat(3,1fr)}
.grid-4{grid-template-columns:repeat(4,1fr)}
button{
  width:100%;padding:12px;background:#083024;color:#fff;font-size:16px;
  border-radius:8px;border:none;cursor:pointer;margin-top:18px
}
button:hover{background:#0a4734}
</style>
</head>

<body>

<div class="form-container">
<h2>نموذج إعداد تقرير نشاط إثرائي</h2>

<form id="reportForm">

<div class="grid grid-3">
<div>
<label>المادة</label>
<input name="subject" required>
</div>
<div>
<label>الصف</label>
<input name="grade" required>
</div>
<div>
<label>الفصل الدراسي</label>
<select name="semester">
<option value="الأول">الأول</option>
<option value="الثاني">الثاني</option>
</select>
</div>
</div>

<div class="grid grid-4">
<div>
<label>مكان التنفيذ</label>
<input name="place">
</div>
<div>
<label>العدد</label>
<input name="count" type="number">
</div>
<div>
<label>المستهدفون</label>
<input name="target">
</div>
<div>
<label>نوع التقرير</label>
<input name="reportType" value="نشاط إثرائي">
</div>
</div>

<label>الهدف التربوي</label>
<textarea name="goal"></textarea>

<label>إجراءات التنفيذ</label>
<textarea name="steps"></textarea>

<label>وصف مختصر</label>
<textarea name="summary"></textarea>

<label>النتائج</label>
<textarea name="results"></textarea>

<label>نقاط القوة</label>
<textarea name="strength"></textarea>

<label>المحفزات</label>
<textarea name="motivation"></textarea>

<label>مواطن القصور</label>
<textarea name="weakness"></textarea>

<label>التحديات</label>
<textarea name="challenge"></textarea>

<label>صورة الدليل الأولى</label>
<input type="file" accept="image/*" id="img1">

<label>وصف الصورة الأولى</label>
<textarea name="cap1"></textarea>

<label>صورة الدليل الثانية</label>
<input type="file" accept="image/*" id="img2">

<label>وصف الصورة الثانية</label>
<textarea name="cap2"></textarea>

<button type="submit">إصدار التقرير</button>
</form>
</div>


<script>
document.getElementById('reportForm').addEventListener('submit', async function(e){
e.preventDefault();

const f = new FormData(this);
const readImage = (fileInput)=> new Promise(res=>{
  if(!fileInput.files[0]) return res("");
  const r=new FileReader();
  r.onload=()=>res(r.result);
  r.readAsDataURL(fileInput.files[0]);
});

const img1 = await readImage(document.getElementById('img1'));
const img2 = await readImage(document.getElementById('img2'));

const w = window.open("", "_blank");

w.document.write(`
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<title>${f.get("reportType")}</title>
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap" rel="stylesheet">
<style>
@page{size:A4;margin:12mm}
*{margin:0;padding:0;box-sizing:border-box;font-family:'Cairo',sans-serif}
body{width:210mm;min-height:297mm;color:#1f2937}
.header{
  width:100%;height:105px;background:#083024;position:relative;margin-bottom:10px;
}
.header::before{
  content:"";position:absolute;inset:0;
  background:url('https://i.ibb.co/kVWFFwhW/9-C92-E57-B-23-FA-479-D-A024-1-D5-F871-B4-F8-D.png') center/40% no-repeat;opacity:.95
}
.admin-name,.school-name,.hijri-date{
  position:absolute;font-size:10.5px;color:#fff;z-index:2
}
.admin-name{top:10px;right:16px}
.school-name{bottom:10px;right:16px}
.hijri-date{bottom:10px;left:16px}
.container{width:100%}
.box{
  border:2px solid #3f5f5a;border-radius:8px;padding:10px;font-size:11.5px;line-height:1.6;background:#fff
}
.box-title{font-weight:700;margin-bottom:6px;font-size:12.5px}
.grid{display:grid;gap:8px;margin-bottom:8px}
.grid-3{grid-template-columns:repeat(3,1fr)}
.grid-4{grid-template-columns:repeat(4,1fr)}
.objective{
  background:#eef6ea;border:2px solid #6fa37a;text-align:center;font-size:13px;margin:8px 0;padding:12px
}
.main-grid{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.motivation{background:#fff7cc;border:2px dashed #e6c84f}
.weakness,.challenge{background:#ffecec;border-color:#d16a6a}
.evidence-section{margin-top:10px}
.evidence-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.evidence-box{border:2px solid #083024;border-radius:8px;overflow:hidden}
.evidence-box img{width:100%;height:150px;object-fit:cover}
.evidence-caption{padding:6px;font-size:10.5px;background:#f9fafb;border-top:1px solid #e5e7eb}
@media print{button{display:none}}
</style>
</head>

<body>

<div class="header">
  <div class="admin-name">الإدارة العامة للتعليم بمنطقة الرياض</div>
  <div class="school-name">مدرسة التجربة النموذجية</div>
  <div class="hijri-date" id="hijriDate">—</div>
</div>

<div class="container">

<div class="grid grid-3">
<div class="box"><strong>المادة</strong><br>${f.get("subject")}</div>
<div class="box"><strong>الصف</strong><br>${f.get("grade")}</div>
<div class="box"><strong>الفصل الدراسي</strong><br>${f.get("semester")}</div>
</div>

<div class="grid grid-4">
<div class="box"><strong>مكان التنفيذ</strong><br>${f.get("place")}</div>
<div class="box"><strong>العدد</strong><br>${f.get("count")}</div>
<div class="box"><strong>المستهدفون</strong><br>${f.get("target")}</div>
<div class="box"><strong>التقرير</strong><br>${f.get("reportType")}</div>
</div>

<div class="box objective">
<div class="box-title">الهدف التربوي</div>
${f.get("goal")}
</div>

<div class="main-grid">

<div class="box"><div class="box-title">إجراءات التنفيذ</div>${f.get("steps")}</div>
<div class="box"><div class="box-title">وصف مختصر</div>${f.get("summary")}</div>
<div class="box"><div class="box-title">النتائج</div>${f.get("results")}</div>
<div class="box"><div class="box-title">نقاط القوة</div>${f.get("strength")}</div>
<div class="box motivation"><div class="box-title">المحفزات</div>${f.get("motivation")}</div>
<div class="box weakness"><div class="box-title">مواطن القصور</div>${f.get("weakness")}</div>
<div class="box challenge"><div class="box-title">التحديات</div>${f.get("challenge")}</div>

</div>

<div class="evidence-section">
<div class="box-title">شواهد الصور</div>

<div class="evidence-grid">
${img1?`
<div class="evidence-box">
<img src="${img1}">
<div class="evidence-caption">${f.get("cap1")}</div>
</div>`:""}

${img2?`
<div class="evidence-box">
<img src="${img2}">
<div class="evidence-caption">${f.get("cap2")}</div>
</div>`:""}
</div>
</div>

</div>

<script>
fetch('https://api.aladhan.com/v1/gToH')
.then(r=>r.json())
.then(d=>{
 const h=d.data.hijri;
 document.getElementById('hijriDate').textContent =
 \`\${h.day} \${h.month.ar} \${h.year} هـ\`;
 setTimeout(()=>{window.print()},1000);
});
</script>

</body>
</html>
`);

w.document.close();

});
</script>

</body>
</html>