<!DOCTYPE html>
<html dir="rtl" lang="ar">
<head>
  <meta charset="UTF-8">
  <title>تقرير</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap');

    * { margin: 0; padding: 0; box-sizing: border-box; }

    html, body {
      width: 100%;
      font-family: 'Cairo', sans-serif;
      background: #ffffff;
      color: #1f2937;
    }

    .header {
      width: 100%;
      height: 90px;
      background-color: #083024;
      position: relative;
    }

    .header::before {
      content: "";
      position: absolute;
      inset: 0;
      background-image: url('https://i.ibb.co/kVWFFwhW/9-C92-E57-B-23-FA-479-D-A024-1-D5-F871-B4-F8-D.png');
      background-repeat: no-repeat;
      background-position: center;
      background-size: 38%;
      opacity: 0.95;
    }

    .admin-name {
      position: absolute;
      top: 6px;
      right: 12px;
      font-size: 8px;
      color: #ffffff;
      z-index: 2;
    }

    .school-name {
      position: absolute;
      bottom: 6px;
      right: 12px;
      font-size: 8px;
      color: #ffffff;
      z-index: 2;
    }

    .hijri-date {
      position: absolute;
      bottom: 6px;
      left: 12px;
      font-size: 8px;
      color: #ffffff;
      z-index: 2;
    }

    .info-wrapper {
      padding: 6px 10px;
      max-width: 210mm;
      margin: auto;
    }

    .info-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 4px;
      margin-bottom: 4px;
    }

    .info-grid.second {
      grid-template-columns: repeat(4, 1fr);
    }

    .info-box {
      border: 1px solid #083024;
      border-radius: 4px;
      padding: 3px 4px;
      text-align: center;
      font-size: 7px;
      background: rgba(255,255,255,0.95);
      line-height: 1.2;
    }

    .info-box strong {
      display: block;
      font-size: 7.5px;
      margin-bottom: 1px;
    }

    .page-content {
      padding: 12px;
      max-width: 210mm;
      margin: auto;
    }

    .report-objective-box {
      background: rgba(8,48,36,0.15);
      border: 1px solid rgba(8,48,36,0.4);
      border-radius: 6px;
      padding: 6px;
      margin-bottom: 10px;
      text-align: center;
      font-size: 8px;
    }

    .report-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 8px;
      margin-bottom: 8px;
    }

    .report-box {
      border-radius: 6px;
      border: 1px solid rgba(0,0,0,0.2);
      padding: 6px;
      background: rgba(0,0,0,0.03);
    }

    .report-box-title {
      font-size: 7px;
      margin-bottom: 3px;
      border-bottom: 1px solid rgba(0,0,0,0.15);
      padding-bottom: 2px;
    }

    .report-box-content {
      font-size: 6px;
      line-height: 1.4;
    }

    .improvements-box {
      background: rgba(234,88,12,0.12);
      border: 1px solid rgba(234,88,12,0.4);
      border-radius: 6px;
      padding: 6px;
      margin-bottom: 10px;
    }

    .image-evidence-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 8px;
      margin-top: 8px;
    }

    .image-box {
      border: 1px dashed #083024;
      border-radius: 6px;
      height: 120px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 7px;
      color: #083024;
      background: rgba(8,48,36,0.05);
    }
  </style>
</head>
<body>

  <div class="header">
    <div class="admin-name">الإدارة العامة للتعليم بمنطقة الرياض</div>
    <div class="school-name">مدرسة التجربة النموذجية</div>
    <div class="hijri-date" id="hijriDate">جاري تحميل التاريخ...</div>
  </div>

  <div class="info-wrapper">
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
  </div>

  <div class="page-content">

    <div class="report-objective-box">الهدف التربوي يكتب هنا</div>

    <div class="report-grid">
      <div class="report-box">
        <div class="report-box-title">خطوات التنفيذ</div>
        <div class="report-box-content">المحتوى هنا</div>
      </div>
      <div class="report-box">
        <div class="report-box-title">النتائج</div>
        <div class="report-box-content">المحتوى هنا</div>
      </div>
      <div class="report-box">
        <div class="report-box-title">نقاط القوة</div>
        <div class="report-box-content">المحتوى هنا</div>
      </div>
      <div class="report-box">
        <div class="report-box-title">التوصيات</div>
        <div class="report-box-content">المحتوى هنا</div>
      </div>
    </div>

    <div class="improvements-box">
      <div class="report-box-title">نقاط التحسين</div>
      <div class="report-box-content">المحتوى هنا</div>
    </div>

    <div class="image-evidence-grid">
      <div class="image-box">شواهد الصور</div>
      <div class="image-box">شواهد الصور</div>
    </div>

  </div>

  <script>
    fetch('https://api.aladhan.com/v1/gToH')
      .then(r => r.json())
      .then(d => {
        const h = d.data.hijri;
        document.getElementById('hijriDate').textContent =
          `${h.day} ${h.month.ar} ${h.year} هـ`;
      })
      .catch(() => {
        document.getElementById('hijriDate').textContent = '—';
      });
  </script>

</body>
</html>