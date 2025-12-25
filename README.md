<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>تقرير تفعيل حصص النشاط</title>

<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap');
*{margin:0;padding:0;box-sizing:border-box;font-family:'Cairo',sans-serif;}

.page{
width:100%;
max-width:900px;
margin:auto;
padding:10px;
}

.header{
width:100%;
background:#083024;
color:white;
text-align:center;
padding:15px 0;
border-radius:4px;
position:relative;
margin-bottom:10px;
}

.header-title{
color:white;
font-size:16px;
margin-top:6px;
}

#moeLogo{
width:140px;
display:block;
margin:4px auto 0;
}

.info-grid{
display:grid;
grid-template-columns:repeat(4,1fr);
gap:6px;
margin-bottom:10px;
}

.box{
border:1px solid #083024;
border-radius:4px;
padding:4px;
font-size:10px;
background:#ffffff;
text-align:center;
}

.box strong{display:block;font-size:11px;color:#083024;margin-bottom:2px;}

.section-title{
font-size:11px;
font-weight:700;
margin-bottom:3px;
color:#083024;
}

.section{
border-radius:6px;
padding:6px;
font-size:10px;
line-height:1.4;
}

.green{background:#e9f5ee;border:1px solid #76a18a;}
.blue{background:#eef4ff;border:1px solid #8aa4d6;}
.yellow{background:#fff9df;border:1px solid #e7d98c;}
.red{background:#ffecec;border:1px solid #dca4a4;}
.orange{background:#fff1e5;border:1px solid #e7b78c;}
.gray{background:#f8f8f8;border:1px solid #c8c8c8;}

.sections-grid{
display:grid;
grid-template-columns:repeat(3,1fr);
gap:8px;
margin-bottom:8px;
}

.images{
display:grid;
grid-template-columns:1fr 1fr;
gap:8px;
margin-top:10px;
}

.img-box{
width:100%;
height:120px;
background:#eee;
border:1px dashed #083024;
border-radius:6px;
display:flex;
align-items:center;
justify-content:center;
font-size:10px;
}

.signature{
display:flex;
justify-content:space-between;
font-size:12px;
margin-top:40px;
}

@media print{
body{background:white;}
.page{page-break-after:avoid;}
}
</style>

</head>
<body>

<div class="page">

<div class="header">
<img id="moeLogo">
<div class="header-title">تقرير تفعيل حصص النشاط</div>
</div>

<div class="info-grid">
<div class="box"><strong>الإدارة</strong><span id="admin"></span></div>
<div class="box"><strong>اسم المدرسة</strong><span id="school"></span></div>
<div class="box"><strong>الفصل</strong><span id="term"></span></div>
<div class="box"><strong>الصف</strong><span id="grade"></span></div>
<div class="box"><strong>المادة</strong><span id="subject"></span></div>
<div class="box"><strong>نوع التقرير</strong><span id="type"></span></div>
<div class="box"><strong>المستهدفون</strong><span id="target"></span></div>
<div class="box"><strong>العدد</strong><span id="count"></span></div>
<div class="box"><strong>مكان التنفيذ</strong><span id="place"></span></div>
</div>

<div class="sections-grid">
<div class="section green"><div class="section-title">وصف مختصر</div><span id="desc"></span></div>
<div class="section yellow"><div class="section-title">إجراءات التنفيذ</div><span id="steps"></span></div>
<div class="section green"><div class="section-title">النتائج</div><span id="results"></span></div>
<div class="section blue"><div class="section-title">نقاط القوة</div><span id="strengths"></span></div>
<div class="section orange"><div class="section-title">ما يحتاج إلى تطوير</div><span id="develop"></span></div>
<div class="section blue"><div class="section-title">التوصيات</div><span id="recommend"></span></div>
<div class="section red"><div class="section-title">التحديات</div><span id="challenges"></span></div>
<div class="section blue"><div class="section-title">الهدف التربوي</div><span id="objective"></span></div>
</div>

<div class="images">
<div class="img-box"><img id="img1Preview" style="width:100%;height:100%;object-fit:cover;display:none;"></div>
<div class="img-box"><img id="img2Preview" style="width:100%;height:100%;object-fit:cover;display:none;"></div>
</div>

<div class="signature">
<div>المعلم: <span id="teacher"></span></div>
<div>مدير المدرسة: <span id="manager"></span></div>
</div>

</div>

<script>
// شعار الوزارة — Base64
document.getElementById("moeLogo").src =
"data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAHgAAAApCAYAAABLR3e8AAAACXBIWXMAAAsTAAALEwEAmpwYAAA..."

const data = JSON.parse(localStorage.getItem("reportData") || "{}");

for(const k in data){
const el = document.getElementById(k);
if(el) el.innerText = data[k];
}

function loadImg(key,id){
const base64 = localStorage.getItem(key);
if(base64){
const img = document.getElementById(id);
img.src = base64;
img.style.display = "block";
}
}
loadImg("img1","img1Preview");
loadImg("img2","img2Preview");
</script>

</body>
</html>