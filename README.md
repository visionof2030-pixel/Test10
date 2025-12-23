<!DOCTYPE html>
<html dir="rtl" lang="ar">
<head>
  <meta charset="UTF-8">
  <title>تقرير نشاط إثرائي</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap');

    * { margin: 0; padding: 0; box-sizing: border-box; }

    html, body {
      width: 100%;
      height: 100%;
      font-family: 'Cairo', sans-serif;
      background: #ffffff;
      color: #1f2937;
    }

    /* ===== إعداد الصفحة للطباعة صفحة واحدة ===== */
    body {
      padding: 10mm;
    }

    .header {
      width: 100%;
      height: 80px;
      background-color: #083024;
      position: relative;
      margin-bottom: 8px;
    }

    .header::before {
      content: "";
      position: absolute;
      inset: 0;
      background-image: url('https://i.ibb.co/kVWFFwhW/9-C92-E57-B-23-FA-479-D-A024-1-D5-F871-B4-F8-D.png');
      background-repeat: no-repeat;
      background-position: center;
      background-size: 32%;
      opacity: 0.95;
    }

    .admin-name {
      position: absolute;
      top: 6px;
      right: 14px;
      font-size: 11px;
      font-weight: 600;
      color: #ffffff;
      z-index: 2;
    }

    .school-name {
      position: absolute;
      bottom: 6px;
      right: 14px;
      font-size: 11px;
      font-weight: 600;
      color: #ffffff;
      z-index: 2;
    }

    .hijri-date {
      position: absolute;
      bottom: 6px;
      left: 14px;
      font-size: 11px;
      color: #ffffff;
      z-index: 2;
    }

    .container {
      max-width: 190mm;
      margin: auto;
    }

    .info-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 6px;
      margin-bottom: 6px;
    }

    .info-grid.second {
      grid-template-columns: repeat(4, 1fr);
      margin-bottom: 10px;
    }

    .info-box {
      border: 1px solid #083024;
      border-radius: 6px;
      padding: 6px;
      text-align: center;
      font-size: 11px;
      line-height: 1.3;
    }

    .info-box strong {
      display: block;
      font-size: 11.5px;
      margin-bottom: 2px;
      color: #083024;
    }

    .report-objective-box {
      background: rgba(8,48,36,0.08);
      border: 1px solid rgba(8,48,36,0.35);
      border-radius: 8px;
      padding: 10px;
      margin-bottom: 10px;
      text-align: center;
      font-size: 13px;
      line-height: 1.6;
    }

    .report-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 10px;
      margin-bottom: 10px;
    }

    .report-box {
      border-radius: 8px;
      border: 1px solid #d1d5db;
      padding: 10px;
      background: #fafafa;
      min-height: 120px;
    }

    .report-box-title {
      font-size: 13px;
      font-weight: 700;
      margin-bottom: 6px;
      border-bottom: 1px solid #e5e7eb;
      padding-bottom: 4px;
      color: #083024;
    }

    .report-box-content {
      font-size: 11.5px;
      line-height: 1.6;
      white-space: pre-line;
    }

    .improvements-box {
      background: rgba(234,88,12,0.07);
      border: 1px solid rgba(234,88,12,0.35);
      border-radius: 8px;
      padding: 10px;
      margin-bottom: 10px;
    }

    .image-evidence-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 8px;
    }

    .image-box {
      border: 1px solid #083024;
      border-radius: 8px;
      height: 140px;
      overflow: hidden;
    }

    .image-box img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    @media print {
      body {
        padding: 8mm;
      }
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

    <div class="info-grid">
      <div class="info-box"><strong>الفصل الدراسي</strong>الأول</div>
      <div class="info-box"><strong>الصف</strong>الثالث الثانوي</div>
      <div class="info-box"><strong>المادة</strong>أحياء</div>
    </div>

    <div class="info-grid second">
      <div class="info-box"><strong>التقرير</strong>نشاط إثرائي</div>
      <div class="info-box"><strong>المستهدفون</strong>الطلاب المتميزون</div>
      <div class="info-box"><strong>العدد</strong>15 طالباً</div>
      <div class="info-box"><strong>مكان التنفيذ</strong>مختبر البحث</div>
    </div>

    <div class="report-objective-box">
      يهدف النشاط إلى تنمية مهارات البحث العلمي والتفكير الناقد لدى الطلاب
      من خلال العمل التعاوني وتحليل البيانات وتطبيق المفاهيم العلمية عملياً.
    </div>

    <div class="report-grid">
      <div class="report-box">
        <div class="report-box-title">خطوات التنفيذ</div>
        <div class="report-box-content">
تقسيم الطلاب إلى مجموعات.
توزيع أوراق العمل.
تنفيذ النشاط بإشراف المعلم.
مناقشة النتائج.
        </div>
      </div>

      <div class="report-box">
        <div class="report-box-title">النتائج</div>
        <div class="report-box-content">
ارتفاع التفاعل والمشاركة.
تحسن مهارات التحليل.
تنمية العمل الجماعي.
تحقيق أهداف النشاط.
        </div>
      </div>

      <div class="report-box">
        <div class="report-box-title">نقاط القوة</div>
        <div class="report-box-content">
وضوح التعليمات.
تنوع الأنشطة.
حماس الطلاب.
بيئة تعليمية محفزة.
        </div>
      </div>

      <div class="report-box">
        <div class="report-box-title">التوصيات</div>
        <div class="report-box-content">
الاستمرار بالأنشطة الإثرائية.
زيادة زمن النشاط.
تطبيقه بمواد أخرى.
        </div>
      </div>
    </div>

    <div class="improvements-box">
      <div class="report-box-title">نقاط التحسين</div>
      <div class="report-box-content">
توفير مصادر إضافية.
تنويع الأسئلة.
تحسين التقييم.
      </div>
    </div>

    <div class="image-evidence-grid">
      <div class="image-box">
        <img src="https://i.ibb.co/fY77kdRH/IMG-1942.png">
      </div>
      <div class="image-box">
        <img src="https://i.ibb.co/dwKFLM99/IMG-1941.png">
      </div>
    </div>

  </div>

  <script>
    fetch('https://api.aladhan.com/v1/gToH')
      .then(r => r.json())
      .then(d => {
        const h = d.data.hijri;
        document.getElementById('hijriDate').textContent =
          `${h.day} ${h.month.ar} ${h.year} هـ`;
      });
  </script>

</body>
</html>