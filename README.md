<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <title>أداة إنتاج التقارير</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap');

    * { box-sizing: border-box; font-family: 'Cairo', sans-serif; }

    body {
      margin: 0;
      background: #f3f4f6;
      display: grid;
      grid-template-columns: 380px 1fr;
      height: 100vh;
    }

    /* ===== لوحة الإدخال ===== */
    .panel {
      background: #ffffff;
      padding: 16px;
      overflow-y: auto;
      border-left: 2px solid #083024;
    }

    .panel h2 {
      font-size: 16px;
      margin-bottom: 12px;
      color: #083024;
    }

    .field {
      margin-bottom: 10px;
    }

    .field label {
      font-size: 12px;
      display: block;
      margin-bottom: 4px;
    }

    .field input,
    .field textarea {
      width: 100%;
      padding: 6px;
      font-size: 12px;
      border: 1px solid #d1d5db;
      border-radius: 4px;
    }

    textarea { resize: vertical; min-height: 60px; }

    button {
      width: 100%;
      padding: 10px;
      background: #083024;
      color: #fff;
      border: none;
      border-radius: 6px;
      font-size: 14px;
      cursor: pointer;
      margin-top: 10px;
    }

    /* ===== المعاينة ===== */
    iframe {
      width: 100%;
      height: 100%;
      border: none;
      background: white;
    }
  </style>
</head>
<body>

  <!-- ===== لوحة الإدخال ===== -->
  <div class="panel">
    <h2>بيانات التقرير</h2>

    <div class="field"><label>اسم الإدارة</label><input id="admin"></div>
    <div class="field"><label>اسم المدرسة</label><input id="school"></div>
    <div class="field"><label>الفصل الدراسي</label><input id="term"></div>
    <div class="field"><label>الصف</label><input id="grade"></div>
    <div class="field"><label>المادة</label><input id="subject"></div>
    <div class="field"><label>مكان التنفيذ</label><input id="place"></div>
    <div class="field"><label>نوع التقرير</label><input id="type"></div>
    <div class="field"><label>المستهدفون</label><input id="target"></div>
    <div class="field"><label>العدد</label><input id="count"></div>
    <div class="field"><label>اسم المعلم</label><input id="teacher"></div>

    <div class="field"><label>الهدف التربوي</label><textarea id="objective"></textarea></div>
    <div class="field"><label>وصف مختصر للنشاط</label><textarea id="desc"></textarea></div>
    <div class="field"><label>إجراءات التنفيذ</label><textarea id="steps"></textarea></div>
    <div class="field"><label>النتائج</label><textarea id="results"></textarea></div>
    <div class="field"><label>نقاط القوة</label><textarea id="strengths"></textarea></div>
    <div class="field"><label>التوصيات</label><textarea id="recommendations"></textarea></div>
    <div class="field"><label>نقاط التحسين</label><textarea id="improvements"></textarea></div>

    <button onclick="generate()">إنشاء التقرير</button>
    <button onclick="printReport()">طباعة</button>
  </div>

  <!-- ===== نافذة المعاينة ===== -->
  <iframe id="preview"></iframe>

<script>
function generate() {
  const v = id => document.getElementById(id).value || '';

  const html = `
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
      grid-template-columns: repeat(4, 1fr);
      gap: 4px;
      margin-bottom: 6px;
    }

    .info-box {
      border: 1px solid #083024;
      border-radius: 4px;
      padding: 4px;
      text-align: center;
      font-size: 7px;
      background: rgba(255,255,255,0.95);
      line-height: 1.3;
    }

    .info-box strong {
      display: block;
      font-size: 7.5px;
      margin-bottom: 1px;
      color: #083024;
    }

    .page-content {
      padding: 10px;
      max-width: 210mm;
      margin: auto;
    }

    .report-objective-box {
      background: rgba(8,48,36,0.12);
      border: 1px solid rgba(8,48,36,0.4);
      border-radius: 6px;
      padding: 8px;
      margin-bottom: 8px;
      text-align: center;
      font-size: 7.5px;
      line-height: 1.5;
    }

    .report-section {
      border: 1px solid rgba(0,0,0,0.18);
      border-radius: 6px;
      padding: 8px;
      margin-bottom: 8px;
      background: #fafafa;
    }

    .report-section-title {
      font-size: 7.5px;
      font-weight: 600;
      margin-bottom: 4px;
      color: #083024;
      border-bottom: 1px solid rgba(0,0,0,0.12);
      padding-bottom: 2px;
    }

    .report-section-content {
      font-size: 6.5px;
      line-height: 1.5;
      white-space: pre-line;
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
    <div class="admin-name">${v('admin')}</div>
    <div class="school-name">${v('school')}</div>
    <div class="hijri-date" id="hijriDate">—</div>
  </div>

  <div class="info-wrapper">
    <div class="info-grid">
      <div class="info-box"><strong>الفصل الدراسي</strong>${v('term')}</div>
      <div class="info-box"><strong>الصف</strong>${v('grade')}</div>
      <div class="info-box"><strong>المادة</strong>${v('subject')}</div>
      <div class="info-box"><strong>مكان التنفيذ</strong>${v('place')}</div>
    </div>

    <div class="info-grid">
      <div class="info-box"><strong>نوع التقرير</strong>${v('type')}</div>
      <div class="info-box"><strong>المستهدفون</strong>${v('target')}</div>
      <div class="info-box"><strong>العدد</strong>${v('count')}</div>
      <div class="info-box"><strong>المعلم</strong>${v('teacher')}</div>
    </div>
  </div>

  <div class="page-content">

    <div class="report-objective-box">
      ${v('objective')}
    </div>

    <div class="report-section">
      <div class="report-section-title">وصف مختصر للنشاط</div>
      <div class="report-section-content">
${v('desc')}
      </div>
    </div>

    <div class="report-section">
      <div class="report-section-title">إجراءات التنفيذ</div>
      <div class="report-section-content">
${v('steps')}
      </div>
    </div>

    <div class="report-section">
      <div class="report-section-title">النتائج</div>
      <div class="report-section-content">
${v('results')}
      </div>
    </div>

    <div class="report-section">
      <div class="report-section-title">نقاط القوة</div>
      <div class="report-section-content">
${v('strengths')}
      </div>
    </div>

    <div class="report-section">
      <div class="report-section-title">التوصيات</div>
      <div class="report-section-content">
${v('recommendations')}
      </div>
    </div>

    <div class="report-section">
      <div class="report-section-title">نقاط التحسين</div>
      <div class="report-section-content">
${v('improvements')}
      </div>
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
          h.day + ' ' + h.month.ar + ' ' + h.year + ' هـ';
      })
      .catch(() => {
        document.getElementById('hijriDate').textContent = '—';
      });
  </script>

</body>
</html>`;

  document.getElementById('preview').srcdoc = html;
}

function printReport(){
  document.getElementById('preview').contentWindow.print();
}
</script>

</body>
</html>