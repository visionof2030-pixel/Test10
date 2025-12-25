<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<title>تقرير تفعيل حصص النشاط</title>
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap" rel="stylesheet">
<style>
@page {
  size: A4;
  margin: 0;
}
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Cairo', sans-serif;
  background: #fff;
  color: #1f2937;
  width: 210mm;
  min-height: 297mm;
  padding: 10mm;
  margin: 0 auto;
}

/* ===== الهيدر ===== */
.header {
  width: 100%;
  height: 90px;
  background: #083024;
  position: relative;
  margin-bottom: 8px;
  border-radius: 4px;
  overflow: hidden;
}
.header::before {
  content: "";
  position: absolute;
  inset: 0;
  background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100" width="100" height="100"><text x="50" y="60" font-family="Arial" font-size="24" fill="white" text-anchor="middle">شعار</text></svg>') center/38% no-repeat;
  opacity: .95;
}
.admin-name, .school-name, .hijri-date {
  position: absolute;
  font-size: 11px;
  color: #fff;
  z-index: 2;
  font-weight: 600;
}
.admin-name {
  top: 12px;
  right: 20px;
}
.school-name {
  bottom: 12px;
  right: 20px;
}
.hijri-date {
  bottom: 12px;
  left: 20px;
  font-size: 10px;
}

/* ===== عام ===== */
.container {
  max-width: 190mm;
  margin: auto;
}
.box {
  border: 2px solid #3f5f5a;
  border-radius: 6px;
  padding: 10px;
  font-size: 13px;
  background: #fff;
  line-height: 1.6;
  height: 100%;
}
.box-title {
  font-weight: 700;
  margin-bottom: 8px;
  color: #083024;
  font-size: 14px;
  border-bottom: 1px solid #eee;
  padding-bottom: 4px;
}

/* ===== الصف العلوي ===== */
.top-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
  margin-bottom: 10px;
}
.top-grid.second {
  grid-template-columns: repeat(4, 1fr);
  margin-bottom: 15px;
}

/* ===== الهدف ===== */
.objective {
  background: #eef6ea;
  border: 2px solid #6fa37a;
  text-align: center;
  font-size: 14px;
  margin: 12px 0;
  padding: 15px;
  border-radius: 8px;
}

/* ===== المحتوى الرئيسي ===== */
.main-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 12px;
  margin-bottom: 15px;
}

/* ===== ألوان خاصة ===== */
.result {
  border-color: #3f6fa5;
  background: #f0f7ff;
}
.recommend {
  border-color: #3f6fa5;
  background: #f0f7ff;
}
.strength {
  border-color: #3f6fa5;
  background: #f0f7ff;
}
.motivation {
  background: #fff7cc;
  border: 2px dashed #e6c84f;
}
.weakness {
  background: #ffecec;
  border-color: #d16a6a;
}
.challenge {
  background: #ffecec;
  border-color: #d16a6a;
}

/* ===== الصور ===== */
.images-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 15px;
  margin-top: 20px;
}
.image-container {
  border: 1px solid #ddd;
  border-radius: 6px;
  overflow: hidden;
  height: 150px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: #f9f9f9;
}
.image-container img {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain;
}

/* ===== التوقيعات ===== */
.signatures {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 40px;
  margin-top: 30px;
  padding-top: 20px;
  border-top: 2px solid #eee;
}
.signature-box {
  text-align: center;
}
.signature-line {
  width: 200px;
  height: 1px;
  background: #000;
  margin: 40px auto 10px;
}
.signature-name {
  font-weight: 700;
  font-size: 14px;
  color: #083024;
}
.signature-title {
  font-size: 12px;
  color: #666;
}

/* ===== طباعة ===== */
@media print {
  body {
    width: 210mm;
    height: 297mm;
    padding: 10mm;
    margin: 0;
  }
  .no-print {
    display: none;
  }
  .box {
    break-inside: avoid;
  }
}
</style>
</head>
<body>

<div class="header">
  <div class="admin-name" id="adminName">الإدارة العامة للتعليم بمنطقة مكة المكرمة – مكة المكرمة</div>
  <div class="school-name" id="schoolName">مدرسة سعيد بن العاص</div>
  <div class="hijri-date" id="hijriDate">—</div>
</div>

<div class="container">

  <div class="top-grid">
    <div class="box"><strong>المادة:</strong> <span id="subjectField">—</span></div>
    <div class="box"><strong>الصف:</strong> <span id="gradeField">—</span></div>
    <div class="box"><strong>الفصل الدراسي:</strong> <span id="termField">—</span></div>
  </div>

  <div class="top-grid second">
    <div class="box"><strong>مكان التنفيذ:</strong><br><span id="placeField">—</span></div>
    <div class="box"><strong>العدد:</strong><br><span id="countField">—</span></div>
    <div class="box"><strong>المستهدفون:</strong><br><span id="targetField">—</span></div>
    <div class="box"><strong>نوع التقرير:</strong><br><span id="typeField">تقرير تفعيل حصص النشاط</span></div>
  </div>

  <div class="box objective">
    <div class="box-title">الهدف التربوي</div>
    <div id="objectiveField">—</div>
  </div>

  <div class="main-grid">
    <div class="box">
      <div class="box-title">إجراءات التنفيذ</div>
      <div id="stepsField">—</div>
    </div>

    <div class="box">
      <div class="box-title">وصف مختصر</div>
      <div id="descField">—</div>
    </div>

    <div class="box recommend">
      <div class="box-title">التوصيات</div>
      <div id="recommendField">—</div>
    </div>

    <div class="box result">
      <div class="box-title">النتائج</div>
      <div id="resultsField">—</div>
    </div>

    <div class="box strength">
      <div class="box-title">نقاط القوة</div>
      <div id="strengthsField">—</div>
    </div>

    <div class="box motivation">
      <div class="box-title">ما يحتاج إلى تطوير</div>
      <div id="developField">—</div>
    </div>

    <div class="box weakness">
      <div class="box-title">التحديات</div>
      <div id="challengesField">—</div>
    </div>

    <div class="box challenge">
      <div class="box-title">ملاحظات إضافية</div>
      <div>—</div>
    </div>
  </div>

  <!-- قسم الصور -->
  <div class="images-grid" id="imagesSection">
    <!-- سيتم إضافة الصور هنا ديناميكيًا -->
  </div>

  <!-- التوقيعات -->
  <div class="signatures">
    <div class="signature-box">
      <div class="signature-line"></div>
      <div class="signature-name" id="teacherName">فهد الخالدي</div>
      <div class="signature-title">اسم المعلم / المشرف على النشاط</div>
    </div>
    
    <div class="signature-box">
      <div class="signature-line"></div>
      <div class="signature-name" id="managerName">نايف اللحياني</div>
      <div class="signature-title">اسم مدير المدرسة</div>
    </div>
  </div>

</div>

<script>
// دالة لتحميل البيانات من localStorage
function loadReportData() {
  const dataStr = localStorage.getItem('reportData');
  if (!dataStr) {
    alert('لا توجد بيانات للتقرير. يرجى تعبئة النموذج أولاً.');
    window.location.href = '../index.html';
    return;
  }

  const data = JSON.parse(dataStr);
  
  // تعبئة الحقول
  document.getElementById('adminName').textContent = data.admin || '—';
  document.getElementById('schoolName').textContent = data.school || '—';
  document.getElementById('subjectField').textContent = data.subject || '—';
  document.getElementById('gradeField').textContent = data.grade || '—';
  document.getElementById('termField').textContent = data.term || '—';
  document.getElementById('placeField').textContent = data.place || '—';
  document.getElementById('countField').textContent = data.count || '—';
  document.getElementById('targetField').textContent = data.target || '—';
  document.getElementById('typeField').textContent = data.type || 'تقرير تفعيل حصص النشاط';
  document.getElementById('objectiveField').textContent = data.objective || '—';
  document.getElementById('descField').textContent = data.desc || '—';
  document.getElementById('stepsField').textContent = data.steps || '—';
  document.getElementById('resultsField').textContent = data.results || '—';
  document.getElementById('strengthsField').textContent = data.strengths || '—';
  document.getElementById('challengesField').textContent = data.challenges || '—';
  document.getElementById('developField').textContent = data.develop || '—';
  document.getElementById('recommendField').textContent = data.recommend || '—';
  document.getElementById('teacherName').textContent = data.teacher || '—';
  document.getElementById('managerName').textContent = data.manager || '—';

  // عرض الصور
  const imagesSection = document.getElementById('imagesSection');
  imagesSection.innerHTML = ''; // مسح المحتوى القديم

  const img1 = localStorage.getItem('img1');
  const img2 = localStorage.getItem('img2');
  
  if (img1 || img2) {
    if (img1) {
      const imgContainer1 = document.createElement('div');
      imgContainer1.className = 'image-container';
      const img1Element = document.createElement('img');
      img1Element.src = img1;
      img1Element.alt = 'صورة النشاط 1';
      imgContainer1.appendChild(img1Element);
      imagesSection.appendChild(imgContainer1);
    }
    
    if (img2) {
      const imgContainer2 = document.createElement('div');
      imgContainer2.className = 'image-container';
      const img2Element = document.createElement('img');
      img2Element.src = img2;
      img2Element.alt = 'صورة النشاط 2';
      imgContainer2.appendChild(img2Element);
      imagesSection.appendChild(imgContainer2);
    }
  } else {
    imagesSection.innerHTML = '<p style="grid-column: span 2; text-align: center; color: #666;">لا توجد صور مرفقة</p>';
  }
}

// دالة لجلب التاريخ الهجري
function getHijriDate() {
  const today = new Date();
  const day = today.getDate();
  const month = today.getMonth() + 1;
  const year = today.getFullYear();
  
  // API للتحويل من ميلادي إلى هجري
  fetch(`https://api.aladhan.com/v1/gToH?date=${day}-${month}-${year}`)
    .then(response => response.json())
    .then(data => {
      const hijri = data.data.hijri;
      const hijriDateStr = `${hijri.day} ${hijri.month.ar} ${hijri.year} هـ`;
      document.getElementById('hijriDate').textContent = hijriDateStr;
    })
    .catch(error => {
      console.error('خطأ في جلب التاريخ الهجري:', error);
      document.getElementById('hijriDate').textContent = '—';
    });
}

// دالة للطباعة
function printReport() {
  window.print();
}

// إضافة زر الطباعة
const printButton = document.createElement('button');
printButton.textContent = '🖨️ طباعة التقرير';
printButton.style.cssText = `
  position: fixed;
  bottom: 20px;
  left: 20px;
  background: #083024;
  color: white;
  padding: 12px 24px;
  border: none;
  border-radius: 6px;
  font-family: 'Cairo', sans-serif;
  font-size: 16px;
  cursor: pointer;
  z-index: 1000;
  box-shadow: 0 2px 10px rgba(0,0,0,0.2);
`;
printButton.onclick = printReport;
document.body.appendChild(printButton);

// تحميل البيانات عند فتح الصفحة
document.addEventListener('DOMContentLoaded', () => {
  loadReportData();
  getHijriDate();
  
  // تنظيف localStorage بعد فترة (اختياري)
  setTimeout(() => {
    localStorage.removeItem('reportData');
    localStorage.removeItem('img1');
    localStorage.removeItem('img2');
  }, 5000);
});
</script>

</body>
</html>