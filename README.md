
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <title>تقرير تعليمي PDF</title>

  <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>

  <style>
    @import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap');

    * { margin: 0; padding: 0; box-sizing: border-box; }

    html, body {
      font-family: 'Cairo', sans-serif;
      background: #ffffff;
      color: #1f2937;
      width: 100%;
      direction: rtl;
    }

    body { padding: 0; margin: 0; }

    .btn-container {
      text-align: center;
      padding: 10px;
      background: #f5f5f5;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      z-index: 10;
      display: flex;
      gap: 10px;
      justify-content: center;
    }

    button {
      background: #066d4d;
      color: #ffffff;
      border: none;
      padding: 10px 25px;
      font-size: 15px;
      border-radius: 6px;
      cursor: pointer;
    }

    button:hover { background: #05523a; }

    @media print { .btn-container { display: none; } }

    .header {
      width: 100%;
      height: 100px;
      background-color: #083024;
      position: relative;
      display: flex;
      justify-content: center;
      align-items: center;
      margin-top: 60px;
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

    .header-info {
      width: 95%;
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
      width: 100%;
      padding: 10px;
      background: #fff;
      margin: auto;
    }

    .info-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
      gap: 4px;
      margin-bottom: 6px;
    }

    .info-box {
      background-color: #eaf3ef;
      border-radius: 4px;
      padding: 6px;
      text-align: center;
      font-size: 10px;
      line-height: 1.3;
    }

    .info-box strong {
      display: block;
      font-size: 11px;
      color: #083024;
    }

    .report-objective-box {
      background: rgba(8,48,36,0.1);
      border-radius: 6px;
      padding: 12px;
      margin-bottom: 8px;
      font-size: 13px;
      text-align: center;
      color: #083024;
    }

    .report-grid {
      display: grid;
      grid-template-columns: 1fr 1fr 1fr;
      gap: 6px;
      margin-bottom: 8px;
    }

    .report-box {
      border-radius: 6px;
      padding: 16px;
      min-height: 120px;
    }

    .report-box-title {
      font-size: 12px;
      margin-bottom: 6px;
      text-align: center;
      font-weight: bold;
    }

    .report-box-content {
      font-size: 10px;
      line-height: 1.4;
      white-space: pre-line;
      text-align: justify;
    }

    .box-color-1 { background-color: #ffecec; }
    .box-color-1 .report-box-title { color: #b02222; }

    .box-color-2 { background-color: #e6f6e6; }
    .box-color-2 .report-box-title { color: #2d7a2d; }

    .box-color-3 { background-color: #fff0e6; }
    .box-color-3 .report-box-title { color: #c26a00; }

    .box-color-4 { background-color: #e8f1ff; }
    .box-color-4 .report-box-title { color: #2e4a8c; }

    .box-color-5 { background-color: #fff7e8; }
    .box-color-5 .report-box-title { color: #a17d00; }

    .box-color-6 { background-color: #f1e8ff; }
    .box-color-6 .report-box-title { color: #5d3da3; }

    .image-evidence-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 8px;
      margin-top: 8px;
    }

    .image-box {
      border-radius: 6px;
      height: 100px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 11px;
      color: #083024;
      background: rgba(8,48,36,0.05);
    }

    @media (min-width: 600px) {
      .page { width: 850px; }
    }

    .lang-switch {
      margin-bottom: 10px;
      text-align: center;
    }

    .lang-switch button {
      background: #1f3b57;
      padding: 6px 15px;
      font-size: 12px;
    }
  </style>
</head>

<body>

  <div class="btn-container">
    <button onclick="window.print()">Print / طباعة</button>
    <button onclick="downloadPDF()">Download PDF / تنزيل PDF</button>
  </div>

  <div class="lang-switch">
    <button onclick="switchLanguage('ar')">عربي</button>
    <button onclick="switchLanguage('en')">English</button>
  </div>

  <div id="report-content">

    <div class="header">
      <div class="header-info">
        <div id="leader"></div>
        <div id="school"></div>
        <div id="date"></div>
      </div>
    </div>

    <div class="page">

      <div class="info-grid">
        <div class="info-box"><strong>اسم المعلم / Teacher Name</strong> <span id="teacher"></span></div>
        <div class="info-box"><strong>المادة / Subject</strong> <span id="subject"></span></div>
        <div class="info-box"><strong>الصف / Grade</strong> <span id="grade"></span></div>
        <div class="info-box"><strong>عدد الطلاب / Students</strong> <span id="students"></span></div>
        <div class="info-box"><strong>نسبة الحضور / Attendance</strong> <span id="attendance"></span></div>
        <div class="info-box"><strong>نوع التقرير / Type</strong> <span id="type"></span></div>
      </div>

      <div class="report-objective-box" id="objective"></div>

      <div class="report-grid">
        <div class="report-box box-color-1">
          <div class="report-box-title">وصف مختصر / Summary</div>
          <div class="report-box-content" id="box1"></div>
        </div>

        <div class="report-box box-color-2">
          <div class="report-box-title">نقاط قوة / Strengths</div>
          <div class="report-box-content" id="box2"></div>
        </div>

        <div class="report-box box-color-3">
          <div class="report-box-title">نقاط تحسين / Improvements</div>
          <div class="report-box-content" id="box3"></div>
        </div>

        <div class="report-box box-color-4">
          <div class="report-box-title">استراتيجيات / Strategies</div>
          <div class="report-box-content" id="box4"></div>
        </div>

        <div class="report-box box-color-5">
          <div class="report-box-title">إجراءات التنفيذ / Execution</div>
          <div class="report-box-content" id="box5"></div>
        </div>

        <div class="report-box box-color-6">
          <div class="report-box-title">التوصيات / Recommendations</div>
          <div class="report-box-content" id="box6"></div>
        </div>
      </div>

      <div class="image-evidence-grid">
        <div class="image-box">صورة توثيقية / Image 1</div>
        <div class="image-box">صورة توثيقية / Image 2</div>
      </div>

    </div>
  </div>

  <script>
    function downloadPDF() {
      var element = document.getElementById('report-content');
      var options = {
        margin: 0,
        filename: 'report.pdf',
        image: { type: 'jpeg', quality: 1 },
        html2canvas: { scale: 3 },
        jsPDF: { unit: 'mm', format: 'a4', orientation: 'portrait' }
      };
      html2pdf().set(options).from(element).save();
    }

    function switchLanguage(lang) {
      if (lang === 'ar') {
        document.documentElement.dir = "rtl";
        document.documentElement.lang = "ar";
      } else {
        document.documentElement.dir = "ltr";
        document.documentElement.lang = "en";
      }
    }
  </script>

</body>
</html>