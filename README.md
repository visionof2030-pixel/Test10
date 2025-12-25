<!DOCTYPE html>
<html dir="rtl" lang="ar">
<head>
  <meta charset="UTF-8">
  <title>تقرير نشاط إثرائي</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;500;600;700&display=swap');

    * { 
      margin: 0; 
      padding: 0; 
      box-sizing: border-box; 
    }

    html, body {
      width: 100%;
      min-height: 100%;
      font-family: 'Cairo', sans-serif;
      background: #ffffff;
      color: #1f2937;
      line-height: 1.5;
    }

    /* إعدادات الطباعة */
    @page {
      size: A4;
      margin: 15mm 10mm 15mm 10mm;
    }

    body {
      padding: 0;
      margin: 0 auto;
      max-width: 210mm; /* عرض A4 */
      min-height: 297mm; /* طول A4 */
    }

    .header {
      width: 100%;
      height: 25mm;
      background-color: #083024;
      position: relative;
      margin-bottom: 8px;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .header::before {
      content: "";
      position: absolute;
      inset: 0;
      background-image: url('https://i.ibb.co/kVWFFwhW/9-C92-E57-B-23-FA-479-D-A024-1-D5-F871-B4-F8-D.png');
      background-repeat: no-repeat;
      background-position: center;
      background-size: contain;
      max-width: 60%;
      opacity: 0.95;
    }

    .admin-name {
      position: absolute;
      top: 8px;
      right: 15px;
      font-size: 11pt;
      color: #ffffff;
      font-weight: 600;
    }

    .school-name {
      position: absolute;
      bottom: 8px;
      right: 15px;
      font-size: 11pt;
      color: #ffffff;
      font-weight: 600;
    }

    .hijri-date {
      position: absolute;
      bottom: 8px;
      left: 15px;
      font-size: 11pt;
      color: #ffffff;
      font-weight: 600;
    }

    .container {
      width: 100%;
      padding: 10px 15px;
      margin: 0 auto;
    }

    .info-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 8px;
      margin-bottom: 12px;
    }

    .info-grid.second {
      grid-template-columns: repeat(4, 1fr);
      margin-bottom: 15px;
    }

    .info-box {
      border: 1.5px solid #083024;
      border-radius: 6px;
      padding: 8px 6px;
      text-align: center;
      font-size: 11pt;
      line-height: 1.4;
      background: white;
      box-shadow: 0 2px 4px rgba(0,0,0,0.05);
    }

    .info-box strong {
      display: block;
      font-size: 11.5pt;
      margin-bottom: 4px;
      color: #083024;
      font-weight: 700;
    }

    .report-objective-box {
      background: rgba(8,48,36,0.07);
      border: 1.5px solid rgba(8,48,36,0.35);
      border-radius: 8px;
      padding: 12px 15px;
      margin-bottom: 15px;
      text-align: center;
      font-size: 12.5pt;
      line-height: 1.6;
      font-weight: 500;
      box-shadow: 0 3px 6px rgba(0,0,0,0.05);
    }

    .report-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 12px;
      margin-bottom: 15px;
    }

    .report-box {
      border-radius: 8px;
      border: 1.5px solid #d1d5db;
      padding: 12px 10px;
      background: #fafafa;
      min-height: 130px;
      display: flex;
      flex-direction: column;
      box-shadow: 0 3px 6px rgba(0,0,0,0.03);
    }

    .report-box-title {
      font-size: 12pt;
      font-weight: 700;
      margin-bottom: 8px;
      border-bottom: 2px solid #e5e7eb;
      padding-bottom: 6px;
      color: #083024;
      text-align: right;
    }

    .report-box-content {
      font-size: 11pt;
      line-height: 1.5;
      white-space: pre-line;
      flex-grow: 1;
      text-align: right;
      padding: 0 2px;
    }

    .improvements-box {
      background: rgba(234,88,12,0.08);
      border: 1.5px solid rgba(234,88,12,0.4);
      border-radius: 8px;
      padding: 12px 15px;
      margin-bottom: 15px;
      box-shadow: 0 3px 6px rgba(0,0,0,0.05);
    }

    .image-evidence-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 15px;
      margin-top: 5px;
    }

    .image-box {
      border: 2px solid #083024;
      border-radius: 8px;
      height: 150px;
      overflow: hidden;
      background: #f8f9fa;
      display: flex;
      align-items: center;
      justify-content: center;
      box-shadow: 0 4px 8px rgba(0,0,0,0.08);
    }

    .image-box img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      display: block;
    }

    /* تحسينات للطباعة */
    @media print {
      body {
        padding: 0;
        margin: 0;
        max-width: 100%;
        min-height: auto;
        -webkit-print-color-adjust: exact !important;
        print-color-adjust: exact !important;
      }
      
      .container {
        padding: 5mm;
      }
      
      .header {
        height: 22mm;
        -webkit-print-color-adjust: exact;
      }
      
      .header::before {
        -webkit-print-color-adjust: exact;
      }
      
      .admin-name,
      .school-name,
      .hijri-date {
        font-size: 10pt;
      }
      
      .info-box {
        font-size: 10pt;
        break-inside: avoid;
      }
      
      .info-box strong {
        font-size: 10.5pt;
      }
      
      .report-objective-box {
        font-size: 11.5pt;
        break-inside: avoid;
      }
      
      .report-box {
        min-height: 120px;
        break-inside: avoid;
      }
      
      .report-box-title {
        font-size: 11pt;
      }
      
      .report-box-content {
        font-size: 10pt;
      }
      
      .image-box {
        height: 130px;
        break-inside: avoid;
      }
      
      /* منع تقسيم العناصر المهمة بين صفحات */
      .report-grid,
      .info-grid,
      .improvements-box {
        break-inside: avoid;
      }
      
      /* إزالة الظلال للطباعة */
      .info-box,
      .report-box,
      .report-objective-box,
      .improvements-box,
      .image-box {
        box-shadow: none;
      }
    }

    /* تحسينات للشاشات الصغيرة */
    @media screen and (max-width: 768px) {
      .container {
        padding: 10px;
      }
      
      .info-grid,
      .info-grid.second {
        grid-template-columns: 1fr;
        gap: 10px;
      }
      
      .report-grid {
        grid-template-columns: 1fr;
        gap: 15px;
      }
      
      .image-evidence-grid {
        grid-template-columns: 1fr;
        gap: 10px;
      }
      
      .image-box {
        height: 180px;
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
        <img src="https://i.ibb.co/fY77kdRH/IMG-1942.png" alt="صورة النشاط 1">
      </div>
      <div class="image-box">
        <img src="https://i.ibb.co/dwKFLM99/IMG-1941.png" alt="صورة النشاط 2">
      </div>
    </div>

  </div>

  <script>
    // تحميل التاريخ الهجري
    fetch('https://api.aladhan.com/v1/gToH')
      .then(response => {
        if (!response.ok) throw new Error('Network error');
        return response.json();
      })
      .then(data => {
        const hijri = data.data.hijri;
        document.getElementById('hijriDate').textContent =
          `${hijri.day} ${hijri.month.ar} ${hijri.year} هـ`;
      })
      .catch(error => {
        console.error('Error loading Hijri date:', error);
        // التاريخ الاحتياطي
        const date = new Date();
        const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
        document.getElementById('hijriDate').textContent = 
          date.toLocaleDateString('ar-SA', options);
      });
  </script>

</body>
</html>