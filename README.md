<!DOCTYPE html>
<html dir="rtl" lang="ar">
<head>
  <meta charset="UTF-8">
  <title>تقرير نشاط إثرائي</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;600&display=swap');

    * { margin: 0; padding: 0; box-sizing: border-box; }

    html, body {
      width: 100%;
      height: 100%;
      font-family: 'Cairo', sans-serif;
      background: #ffffff;
      color: #1f2937;
    }

    body { padding: 8mm; }

    .header {
      width: 100%;
      height: 70px;
      background-color: #083024;
      position: relative;
      margin-bottom: 6px;
    }

    .header::before {
      content: "";
      position: absolute;
      inset: 0;
      background-image: url('https://i.ibb.co/kVWFFwhW/9-C92-E57-B-23-FA-479-D-A024-1-D5-F871-B4-F8-D.png');
      background-repeat: no-repeat;
      background-position: center;
      background-size: 30%;
      opacity: 0.95;
    }

    .admin-name {
      position: absolute;
      top: 4px;
      right: 10px;
      font-size: 9px;
      color: #ffffff;
    }

    .school-name {
      position: absolute;
      bottom: 4px;
      right: 10px;
      font-size: 9px;
      color: #ffffff;
    }

    .hijri-date {
      position: absolute;
      bottom: 4px;
      left: 10px;
      font-size: 9px;
      color: #ffffff;
    }

    .container {
      max-width: 190mm;
      margin: auto;
    }

    .info-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 5px;
      margin-bottom: 5px;
    }

    .info-grid.second {
      grid-template-columns: repeat(4, 1fr);
      margin-bottom: 8px;
    }

    .info-box {
      border: 1px solid #083024;
      border-radius: 5px;
      padding: 4px;
      text-align: center;
      font-size: 9px;
      line-height: 1.3;
    }

    .info-box strong {
      display: block;
      font-size: 9.5px;
      margin-bottom: 1px;
      color: #083024;
    }

    .report-objective-box {
      background: rgba(8,48,36,0.07);
      border: 1px solid rgba(8,48,36,0.35);
      border-radius: 6px;
      padding: 8px;
      margin-bottom: 8px;
      text-align: center;
      font-size: 10.5px;
      line-height: 1.5;
    }

    .report-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 8px;
      margin-bottom: 8px;
    }

    .report-box {
      border-radius: 6px;
      border: 1px solid #d1d5db;
      padding: 8px;
      background: #fafafa;
      min-height: 105px;
    }

    .report-box-title {
      font-size: 10.5px;
      font-weight: 600;
      margin-bottom: 4px;
      border-bottom: 1px solid #e5e7eb;
      padding-bottom: 3px;
      color: #083024;
    }

    .report-box-content {
      font-size: 9.5px;
      line-height: 1.45;
      white-space: pre-line;
    }

    .improvements-box {
      background: rgba(234,88,12,0.06);
      border: 1px solid rgba(234,88,12,0.35);
      border-radius: 6px;
      padding: 8px;
      margin-bottom: 8px;
    }

    .image-evidence-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 6px;
    }

    .image-box {
      border: 1px solid #083024;
      border-radius: 6px;
      height: 120px;
      overflow: hidden;
    }

    .image-box img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    @media print {
      body { padding: 6mm; }
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
      <div class="info-box"><strong>العدد</strong>15</div>
      <div class="info-box"><strong>مكان التنفيذ</strong>مختبر البحث</div>
    </div>

    <div class="report-objective-box">
      تنمية مهارات البحث العلمي والتفكير الناقد لدى الطلاب
      من خلال أنشطة تطبيقية تعتمد على العمل التعاوني
      وتحليل المعلومات العلمية.
    </div>

    <div class="report-grid">
      <div class="report-box">
        <div class="report-box-title">خطوات التنفيذ</div>
        <div class="report-box-content">
تقسيم الطلاب إلى مجموعات.
توزيع أوراق العمل.
تنفيذ النشاط بإشراف المعلم.
        </div>
      </div>

      <div class="report-box">
        <div class="report-box-title">النتائج</div>
        <div class="report-box-content">
زيادة التفاعل والمشاركة.
تحسن مهارات التحليل.
تحقيق أهداف النشاط.
        </div>
      </div>

      <div class="report-box">
        <div class="report-box-title">نقاط القوة</div>
        <div class="report-box-content">
وضوح التعليمات.
تنوع الأنشطة.
حماس الطلاب.
        </div>
      </div>

      <div class="report-box">
        <div class="report-box-title">التوصيات</div>
        <div class="report-box-content">
تكرار الأنشطة الإثرائية.
زيادة زمن النشاط.
توظيف التقنية.
        </div>
      </div>
    </div>

    <div class="improvements-box">
      <div class="report-box-title">نقاط التحسين</div>
      <div class="report-box-content">
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