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
      direction: rtl;
    }

    .top-title {
      width: 100%;
      background-color: #066d4d;
      color: #ffffff;
      text-align: center;
      font-size: 38px;
      font-weight: bold;
      padding: 25px 0;
      position: relative;
      z-index: 5;
    }

    .title-curve {
      width: 100%;
      height: 40px;
      background: #066d4d;
      border-bottom-left-radius: 50% 100%;
      border-bottom-right-radius: 50% 100%;
      margin-top: -2px;
    }

    .header {
      width: 100%;
      height: 90px;
      background-color: #083024;
      position: relative;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    .header::before {
      content: "";
      position: absolute;
      inset: 0;
      background-image: url('https://i.ibb.co/kVWFFwhW/9-C92-E57-B-23-FA-479-D-A024-1-D5-F871-B4-F8-D.png');
      background-repeat: no-repeat;
      background-position: center;
      background-size: 45%;
      opacity: 0.90;
    }

    .header-info {
      width: calc(100% - 20mm);
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 8px 10px;
      position: relative;
      z-index: 2;
      color: #ffffff;
      font-size: 10px;
    }

    .page {
      width: 210mm;
      height: calc(297mm - 130px);
      padding: 6mm;
      background: #fff;
      margin: auto;
      overflow: hidden;
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
      background-color: #eaf3ef;
      border-radius: 4px;
      padding: 3px;
      text-align: center;
      font-size: 7px;
      line-height: 1.2;
    }

    .info-box strong {
      display: block;
      font-size: 7.3px;
      color: #083024;
    }

    .report-objective-box {
      background: rgba(8,48,36,0.1);
      border-radius: 6px;
      padding: 10px;
      margin-bottom: 6px;
      font-size: 10px;
      text-align: center;
      color: #083024;
    }

    .report-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 6px;
      margin-bottom: 6px;
    }

    .report-box {
      border-radius: 6px;
      padding: 20px;
      min-height: 100px;
    }

    .report-box-title {
      font-size: 10px;
      margin-bottom: 4px;
      text-align: center;
      font-weight: bold;
    }

    .report-box-content {
      font-size: 6.5px;
      line-height: 1.25;
      white-space: pre-line;
      text-align: justify;
    }

    .strengths { background-color: #e6f6e6; }
    .strengths .report-box-title { color: #2d7a2d; }

    .improvements { background-color: #fff0e6; }
    .improvements .report-box-title { color: #c26a00; }

    .summary { background-color: #e8f1ff; }
    .summary .report-box-title { color: #2e4a8c; }

    .execution { background-color: #fff7e8; }
    .execution .report-box-title { color: #a17d00; }

    .image-evidence-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 6px;
      margin-top: 6px;
    }

    .image-box {
      border: none;
      border-radius: 6px;
      height: 90px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 7px;
      color: #083024;
      background: rgba(8,48,36,0.05);
      overflow: hidden;
    }

    @media print {
      html, body {
        width: 210mm;
        height: 297mm;
      }
      .page {
        page-break-after: avoid;
      }
    }
  </style>
</head>

<body>

  <div class="top-title">التقارير التربوية</div>
  <div class="title-curve"></div>

  <div class="header">
    <div class="header-info">
      <div>قائد المدرسة: نايف اللحياني</div>
      <div>مدرسة المستقبل الابتدائية</div>
      <div>1447/02/15 هـ</div>
    </div>
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