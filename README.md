
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<title>تقرير نشاط إثرائي</title>
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap" rel="stylesheet">

<style>
@page{
  size:A4;
  margin:12mm;
}

*{margin:0;padding:0;box-sizing:border-box}

body{
  font-family:'Cairo',sans-serif;
  background:#fff;
  color:#1f2937;
  width:210mm;
  height:297mm;
}

/* ===== الهيدر (بدون تغيير) ===== */
.header{
  width:100%;
  height:95px;
  background:#083024;
  position:relative;
  margin-bottom:10px;
}
.header::before{
  content:"";
  position:absolute;
  inset:0;
  background:url('https://i.ibb.co/kVWFFwhW/9-C92-E57-B-23-FA-479-D-A024-1-D5-F871-B4-F8-D.png') center/38% no-repeat;
  opacity:.95;
}
.admin-name,.school-name,.hijri-date{
  position:absolute;
  font-size:10.5px;
  color:#fff;
  z-index:2;
}
.admin-name{top:8px;right:14px}
.school-name{bottom:8px;right:14px}
.hijri-date{bottom:8px;left:14px}

/* ===== عام ===== */
.container{width:100%}

.box{
  border:2.5px solid #3f5f5a;
  border-radius:8px;
  padding:10px;
  font-size:12.5px;
  line-height:1.6;
  background:#fff;
}
.box-title{
  font-weight:700;
  font-size:13.5px;
  margin-bottom:6px;
}

/* ===== الصفوف العلوية ===== */
.top-grid{
  display:grid;
  grid-template-columns:repeat(3,1fr);
  gap:8px;
  margin-bottom:8px;
}
.top-grid.second{
  grid-template-columns:repeat(4,1fr);
  margin-bottom:12px;
}

/* ===== الهدف ===== */
.objective{
  background:#eef6ea;
  border:2.5px solid #6fa37a;
  text-align:center;
  font-size:14px;
  margin:10px 0;
  padding:14px;
}

/* ===== المحتوى ===== */
.main-grid{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:10px;
  margin-bottom:12px;
}

/* ===== ألوان ===== */
.result{border-color:#3f6fa5}
.recommend{border-color:#3f6fa5}
.strength{border-color:#3f6fa5}
.motivation{
  background:#fff7cc;
  border:2.5px dashed #e6c84f;
}
.weakness{
  background:#ffecec;
  border-color:#d16a6a;
}
.challenge{
  background:#ffecec;
  border-color:#d16a6a;
}

/* ===== شواهد الصور ===== */
.evidence-section{
  margin-top:12px;
}
.evidence-title{
  font-size:14px;
  font-weight:700;
  color:#083024;
  margin-bottom:8px;
}
.evidence-grid{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:12px;
}
.evidence-box{
  border:2.5px solid #083024;
  border-radius:8px;
  overflow:hidden;
}
.evidence-box img{
  width:100%;
  height:170px;
  object-fit:cover;
  display:block;
}
.evidence-caption{
  padding:8px;
  font-size:11.5px;
  line-height:1.6;
  background:#f9fafb;
  border-top:1px solid #e5e7eb;
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
    <div class="box"><strong>المادة</strong><br>أحياء</div>
    <div class="box"><strong>الصف</strong><br>الثالث الثانوي</div>
    <div class="box"><strong>الفصل الدراسي</strong><br>الأول</div>
  </div>

  <div class="top-grid second">
    <div class="box"><strong>مكان التنفيذ</strong><br>الفصل الدراسي</div>
    <div class="box"><strong>العدد</strong><br>25</div>
    <div class="box"><strong>المستهدفون</strong><br>طلاب الصف</div>
    <div class="box"><strong>التقرير</strong><br>نشاط إثرائي</div>
  </div>

  <div class="box objective">
    <div class="box-title">الهدف التربوي</div>
    شرح مفهوم أساسي في المنهج وتطبيقه عبر أنشطة تفاعلية تسهم في
    تنمية مهارات التفكير والتحليل والعمل التعاوني لدى الطلاب.
  </div>

  <div class="main-grid">

    <div class="box">
      <div class="box-title">إجراءات التنفيذ</div>
      عرض المفهوم الجديد بطريقة تفاعلية، مناقشة أمثلة توضيحية،
      تنفيذ أنشطة جماعية، حل تمارين فردية،
      ثم تلخيص أهم النقاط.
    </div>

    <div class="box">
      <div class="box-title">وصف مختصر</div>
      درس تطبيقي يعتمد على التعلم النشط،
      يركز على الفهم العميق للمفاهيم العلمية
      وربطها بالتطبيق العملي.
    </div>

    <div class="box recommend">
      <div class="box-title">التوصيات</div>
      الاستمرار في تنفيذ الأنشطة الإثرائية،
      زيادة وقت التطبيق، وتوظيف وسائل تعليمية
      متنوعة لدعم الفهم.
    </div>

    <div class="box result">
      <div class="box-title">النتائج</div>
      ارتفاع مستوى التفاعل، تحسن استيعاب المفاهيم،
      ومشاركة فعالة من غالبية الطلاب.
    </div>

    <div class="box strength">
      <div class="box-title">نقاط القوة</div>
      وضوح الشرح، تنوع الاستراتيجيات،
      إدارة فعالة للوقت، ومراعاة الفروق الفردية.
    </div>

    <div class="box motivation">
      <div class="box-title">المحفزات</div>
      تعزيز التنافس الإيجابي بين المجموعات،
      استخدام أنشطة محفزة، وتقديم تغذية راجعة فورية.
    </div>

    <div class="box weakness">
      <div class="box-title">مواطن القصور</div>
      محدودية بعض الوسائل التعليمية،
      وضيق وقت الحصة لبعض الأنشطة.
    </div>

    <div class="box challenge">
      <div class="box-title">التحديات</div>
      تفاوت مستوى الاستيعاب بين الطلاب،
      وصعوبة بعض المفاهيم العلمية.
    </div>

  </div>

  <div class="evidence-section">
    <div class="evidence-title">شواهد الصور</div>

    <div class="evidence-grid">
      <div class="evidence-box">
        <img src="https://i.ibb.co/dwKFLM99/IMG-1941.png">
        <div class="evidence-caption">
          توضح الصورة تنفيذ النشاط داخل الفصل الدراسي من خلال
          العمل التعاوني بين الطلاب وتوزيعهم في مجموعات
          لإنجاز المهام التعليمية.
        </div>
      </div>

      <div class="evidence-box">
        <img src="https://i.ibb.co/fY77kdRH/IMG-1942.png">
        <div class="evidence-caption">
          تُظهر الصورة نماذج من أعمال الطلاب أثناء النشاط،
          مع تنوع المهام بين الإبداع والتحدي
          وتنمية مهارات التفكير والتعاون.
        </div>
      </div>
    </div>
  </div>

</div>

<script>
fetch('https://api.aladhan.com/v1/gToH')
.then(r=>r.json())
.then(d=>{
 const h=d.data.hijri;
 document.getElementById('hijriDate').textContent =
 `${h.day} ${h.month.ar} ${h.year} هـ`;
});
</script>

</body>
</html>