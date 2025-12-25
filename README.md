<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <title>تقرير تعليمي</title>

  <style>
    @page {
      size: A4;
      margin: 0;
    }

    @import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap');

    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    html, body {
      font-family: 'Cairo', sans-serif;
      background: #ffffff;
      color: #1f2937;
      width: 100%;
      height: auto;
    }

    body {
      padding: 0;
      margin: 0;
    }

    .page {
      width: 100%;
      padding: 10mm;
      background: #fff;
    }

    /* ===== Header ===== */
    .header {
      width: 100%;
      height: 100px;
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
      background-size: 50%;
      opacity: 0.95;
    }

    .admin-name,
    .school-name,
    .hijri-date {
      position: absolute;
      font-size: 8px;
      color: #ffffff;
      z-index: 2;
    }

    .admin-name { top: 6px; right: 12px; }
    .school-name { bottom: 6px; right: 12px; }
    .hijri-date { bottom: 6px; left: 12px; }

    /* ===== Info Boxes ===== */
    .info-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 4px;
      margin-bottom: 6px;
    }

    .info-grid.second {
      grid-template-columns: repeat(4, 1fr);
    }

    .info-box {
      background-color: #eaf3ef;
      border-radius: 4px;
      padding: 4px;
      text-align: center;
      font-size: 7px;
      line-height: 1.2;
    }

    .info-box strong {
      display: block;
      font-size: 7.5px;
      color: #083024;
    }

    /* ===== Objective ===== */
    .report-objective-box {
      background: rgba(8,48,36,0.1);
      border-radius: 6px;
      padding: 30px;
      margin-bottom: 8px;
      font-size: 11px;
      text-align: center;
      color: #083024;
    }

    /* ===== Two-column sections ===== */
    .report-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 8px;
      margin-bottom: 8px;
    }

    .report-box {
      border-radius: 6px;
      padding: 40px;
    }

    .report-box-title {
      font-size: 11px;
      margin-bottom: 5px;
      text-align: center;
      font-weight: bold;
    }

    .report-box-content {
      font-size: 6px;
      line-height: 1.4;
      white-space: pre-line;
      text-align: justify;
    }

    .strengths {
      background-color: #e6f6e6;
    }

    .strengths .report-box-title {
      color: #2d7a2d;
    }

    .improvements {
      background-color: #fff0e6;
    }

    .improvements .report-box-title {
      color: #c26a00;
    }

    .summary {
      background-color: #e8f1ff;
    }

    .summary .report-box-title {
      color: #2e4a8c;
    }

    .execution {
      background-color: #fff7e8;
    }

    .execution .report-box-title {
      color: #a17d00;
    }

    /* ===== Images ===== */
    .image-evidence-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 8px;
      margin-top: 8px;
    }

    .image-box {
      border: none;
      border-radius: 6px;
      height: 100px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 7px;
      color: #083024;
      background: rgba(8,48,36,0.05);
      overflow: hidden;
    }

    .image-box img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    /* منع الصفحة الفارغة عند الطباعة */
    @media print {
      .page {
        page-break-after: avoid;
      }
      body, html {
        width: auto;
        height: auto;
      }
    }
  </style>
</head>

<body>

  <div class="header">
    <div class="admin-name">قائد المدرسة: نايف اللحياني</div>
    <div class="school-name">مدرسة المستقبل الابتدائية</div>
    <div class="hijri-date">1447/02/15 هـ</div>
  </div>

  <div class="page">
    <div class="info-grid">
      <div class="info-box"><strong>اسم المعلم</strong> فهد الخالدي</div>
      <div class="info-box"><strong>المادة</strong> العلوم</div>
      <div class="info-box"><strong>الصف</strong> الخامس</div>
    </div>

    <div class="info-grid second">
      <div class="info-box"><strong>عدد الطلاب</strong> 28</div>
      <div class="info-box"><strong>نسبة الحضور</strong> 96%</div>
      <div class="info-box"><strong>نوع التقرير</strong> إشرافي</div>
      <div class="info-box"><strong>الفصل</strong> الأول</div>
    </div>

    <div class="report-objective-box">
      يهدف هذا التقرير إلى توثيق سير العملية التعليمية وتحليل مستوى التفاعل والتحصيل لدى الطلاب
    </div>

    <div class="report-grid">
      <div class="report-box summary">
        <div class="report-box-title">نبذة مختصرة</div>
        <div class="report-box-content">
          يتناول هذا التقرير وصفًا موجزًا للدرس من حيث الفكرة العامة ومستوى تفاعل الطلاب ومدى تحقق نواتج التعلم.
        </div>
      </div>

      <div class="report-box execution">
        <div class="report-box-title">إجراءات التنفيذ</div>
        <div class="report-box-content">
          • تهيئة تمهيدية للدرس
          • عرض المحتوى باستخدام وسائل تعليمية
          • تنفيذ نشاط تطبيقي
          • تقويم ختامي
        </div>
      </div>
    </div>

    <div class="report-grid">
      <div class="report-box strengths">
        <div class="report-box-title">نقاط القوة</div>
        <div class="report-box-content">
          • وضوح الأهداف
          • تنوع الاستراتيجيات
          • تفاعل إيجابي
        </div>
      </div>

      <div class="report-box improvements">
        <div class="report-box-title">نقاط التحسين</div>
        <div class="report-box-content">
          • زيادة الأنشطة التطبيقية
          • تعزيز التقويم التكويني
        </div>
      </div>
    </div>

    <div class="image-evidence-grid">
      <div class="image-box">صورة توثيقية 1</div>
      <div class="image-box">صورة توثيقية 2</div>
    </div>

  </div>

</body>
</html>
