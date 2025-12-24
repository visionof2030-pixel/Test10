
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<title>تقرير نشاط</title>
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap" rel="stylesheet">
<style>
@page{
  size:A4;
  margin:10mm;
}
*{box-sizing:border-box;margin:0;padding:0}
body{
  font-family:'Cairo',sans-serif;
  background:#fff;
  color:#1f2937;
  width:210mm;
  height:297mm;
}

/* ===== الهيدر (ثابت بدون تغيير) ===== */
.header{
  width:100%;
  height:85px;
  background:#083024;
  position:relative;
  margin-bottom:6px
}
.header::before{
  content:"";
  position:absolute;
  inset:0;
  background:url('https://i.ibb.co/kVWFFwhW/9-C92-E57-B-23-FA-479-D-A024-1-D5-F871-B4-F8-D.png') center/35% no-repeat;
  opacity:.95
}
.admin-name,.school-name,.hijri-date{
  position:absolute;
  font-size:8px;
  color:#fff;
  z-index:2
}
.admin-name{top:6px;right:12px}
.school-name{bottom:6px;right:12px}
.hijri-date{bottom:6px;left:12px}

/* ===== عام ===== */
.container{
  width:100%;
}
.box{
  border:2px solid #3f5f5a;
  border-radius:6px;
  padding:6px;
  font-size:9.5px;
  background:#fff;
  line-height:1.4
}
.box-title{
  font-weight:700;
  margin-bottom:4px
}

/* ===== الصفوف العلوية ===== */
.top-grid{
  display:grid;
  grid-template-columns:repeat(3,1fr);
  gap:5px;
  margin-bottom:5px
}
.top-grid.second{
  grid-template-columns:repeat(4,1fr)
}

/* ===== الهدف ===== */
.objective{
  background:#eef6ea;
  border:2px solid #6fa37a;
  text-align:center;
  font-size:10.5px;
  margin:6px 0
}

/* ===== المحتوى الرئيسي ===== */
.main-grid{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:6px
}

/* ===== ألوان ===== */
.result{border-color:#3f6fa5}
.recommend{border-color:#3f6fa5}
.strength{border-color:#3f6fa5}
.motivation{
  background:#fff7cc;
  border:2px dashed #e6c84f
}
.weakness{
  background:#ffecec;
  border-color:#d16a6a
}
.challenge{
  background:#ffecec;
  border-color:#d16a6a
}
</style>
</head>
<body>

<div class="header">
  <div class="admin-name">الإدارة العامة للتعليم بمنطقة الرياض</div>
  <div class="school-name">مدرسة التجربة النموذجية</div>
  <div class="hijri-date" id="hijriDate">—</div>
</div>

<div class="container">

  <div class="top-grid">
    <div class="box"><strong>المادة</strong></div>
    <div class="box"><strong>الصف</strong></div>
    <div class="box"><strong>الفصل الدراسي</strong></div>
  </div>

  <div class="top-grid second">
    <div class="box"><strong>مكان التنفيذ</strong><br>الفصل الدراسي</div>
    <div class="box"><strong>العدد</strong><br>25</div>
    <div class="box"><strong>المستهدفون</strong><br>طلاب الصف</div>
    <div class="box"><strong>التقرير</strong></div>
  </div>

  <div class="box objective">
    <div class="box-title">الهدف التربوي</div>
    شرح مفهوم أساسي في المنهج وتطبيقه عبر أنشطة تفاعلية
  </div>

  <div class="main-grid">
    <div class="box">
      <div class="box-title">إجراءات التنفيذ</div>
      عرض المفهوم الجديد، مناقشة أمثلة توضيحية، أنشطة تطبيقية جماعية،
      حل تمارين فردية، تلخيص النقاط الرئيسية
    </div>

    <div class="box">
      <div class="box-title">وصف مختصر</div>
      تنفيذ درس نموذجي يركز على الفهم العميق والتطبيق العملي للمفاهيم
    </div>

    <div class="box recommend">
      <div class="box-title">التوصيات</div>
      تكرار استخدام الأنشطة التفاعلية، تخصيص وقت للمراجعة،
      استخدام وسائل بصرية إضافية
    </div>

    <div class="box result">
      <div class="box-title">النتائج</div>
      استيعاب غالبية الطلاب للمفهوم، مشاركة فعالة في الأنشطة،
      إنجاز التمارين بنجاح
    </div>

    <div class="box strength">
      <div class="box-title">نقاط القوة</div>
      وضوح الشرح، تنوع الأنشطة، إدارة الوقت الفعالة،
      مراعاة الفروق الفردية
    </div>

    <div class="box motivation">
      <div class="box-title">المحفزات</div>
      تفاعل الطلاب الإيجابي، حافز التنافس بين المجموعات،
      استخدام الوسائل التعليمية الجذابة
    </div>

    <div class="box weakness">
      <div class="box-title">مواطن القصور</div>
      نقص بعض الوسائل التعليمية، محدودية المساحة،
      ضعف مشاركة بعض الطلاب
    </div>

    <div class="box challenge">
      <div class="box-title">التحديات</div>
      تفاوت سرعة الاستيعاب بين الطلاب،
      وقت الحصة المحدود، صعوبة بعض المفاهيم
    </div>
  </div>

</div>

<script>
fetch('https://api.aladhan.com/v1/gToH')
.then(r=>r.json())
.then(d=>{
 const h=d.data.hijri;
 document.getElementById('hijriDate').textContent=`${h.day} ${h.month.ar} ${h.year} هـ`
});
</script>

</body>
</html>