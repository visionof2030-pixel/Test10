<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>تقرير تفعيل حصص النشاط</title>
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap" rel="stylesheet">
<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap');

* {
  box-sizing: border-box;
  font-family: 'Cairo', sans-serif;
  margin: 0;
  padding: 0;
}

body {
  background: #f3f4f6;
  color: #1f2937;
  transition: background 0.3s;
}

/* ===== الأنماط العامة ===== */
.section {
  display: none;
  width: 100%;
  min-height: 100vh;
  padding: 20px;
}

.section.active {
  display: block;
}

.btn {
  background: #083024;
  color: white;
  border: 0;
  border-radius: 6px;
  padding: 12px 24px;
  font-size: 16px;
  cursor: pointer;
  margin: 10px;
  transition: background 0.3s;
}

.btn:hover {
  background: #0a4533;
}

.btn-secondary {
  background: #6c757d;
}

.btn-secondary:hover {
  background: #5a6268;
}

/* ===== قسم الإدخال ===== */
.input-section {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  padding: 20px 8px;
}

.panel {
  background: #ffffff;
  width: 100%;
  max-width: 500px;
  margin: 18px 0;
  padding: 24px;
  border-right: 5px solid #083024;
  border-radius: 4px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

h2 {
  font-size: 20px;
  text-align: center;
  color: #083024;
  margin-bottom: 24px;
  padding-bottom: 12px;
  border-bottom: 2px solid #f0f0f0;
}

.field {
  margin-bottom: 18px;
}

label {
  font-size: 13px;
  margin-bottom: 6px;
  display: block;
  color: #083024;
  font-weight: 600;
}

input, select, textarea {
  width: 100%;
  padding: 10px;
  font-size: 15px;
  border: 1px solid #d1d5db;
  border-radius: 4px;
  transition: border 0.3s;
}

input:focus, select:focus, textarea:focus {
  border-color: #083024;
  outline: none;
  box-shadow: 0 0 0 2px rgba(8, 48, 36, 0.1);
}

textarea {
  min-height: 80px;
  resize: vertical;
}

.auto-btn {
  background: #083024;
  color: #fff;
  padding: 8px;
  border-radius: 4px;
  font-size: 12px;
  margin-top: 6px;
  border: none;
  cursor: pointer;
  width: 100%;
  transition: background 0.3s;
}

.auto-btn:hover {
  background: #0a4533;
}

.file-input {
  padding: 8px 0;
  border: none;
}

.file-input::file-selector-button {
  background: #083024;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
  margin-right: 10px;
}

/* ===== قسم الطباعة ===== */
@page {
  size: A4;
  margin: 0;
}

.print-section {
  background: #fff;
  width: 210mm;
  min-height: 297mm;
  padding: 15mm;
  margin: 20px auto;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
}

/* ===== الهيدر ===== */
.header {
  width: 100%;
  height: 100px;
  background: #083024;
  position: relative;
  margin-bottom: 12px;
  border-radius: 6px;
  overflow: hidden;
}

.header::before {
  content: "شعار";
  position: absolute;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  color: rgba(255, 255, 255, 0.8);
  font-size: 24px;
  opacity: .8;
}

.admin-name, .school-name, .hijri-date {
  position: absolute;
  font-size: 12px;
  color: #fff;
  z-index: 2;
  font-weight: 600;
}

.admin-name {
  top: 15px;
  right: 25px;
}

.school-name {
  bottom: 15px;
  right: 25px;
}

.hijri-date {
  bottom: 15px;
  left: 25px;
}

/* ===== عام ===== */
.container {
  max-width: 180mm;
  margin: auto;
}

.box {
  border: 2px solid #3f5f5a;
  border-radius: 6px;
  padding: 12px;
  font-size: 14px;
  background: #fff;
  line-height: 1.7;
  height: 100%;
}

.box-title {
  font-weight: 700;
  margin-bottom: 10px;
  color: #083024;
  font-size: 15px;
  border-bottom: 1px solid #eee;
  padding-bottom: 6px;
}

/* ===== الصف العلوي ===== */
.top-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 12px;
  margin-bottom: 12px;
}

.top-grid.second {
  grid-template-columns: repeat(4, 1fr);
  margin-bottom: 18px;
}

/* ===== الهدف ===== */
.objective {
  background: #eef6ea;
  border: 2px solid #6fa37a;
  text-align: center;
  font-size: 15px;
  margin: 15px 0;
  padding: 18px;
  border-radius: 8px;
}

/* ===== المحتوى الرئيسي ===== */
.main-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 15px;
  margin-bottom: 20px;
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
  gap: 20px;
  margin-top: 25px;
}

.image-container {
  border: 1px solid #ddd;
  border-radius: 6px;
  overflow: hidden;
  height: 180px;
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
  gap: 50px;
  margin-top: 40px;
  padding-top: 25px;
  border-top: 2px solid #eee;
}

.signature-box {
  text-align: center;
}

.signature-line {
  width: 250px;
  height: 1px;
  background: #000;
  margin: 50px auto 15px;
}

.signature-name {
  font-weight: 700;
  font-size: 15px;
  color: #083024;
}

.signature-title {
  font-size: 13px;
  color: #666;
}

/* ===== أزرار التحكم ===== */
.controls {
  position: fixed;
  bottom: 20px;
  left: 20px;
  z-index: 1000;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

/* ===== طباعة ===== */
@media print {
  body {
    background: #fff;
  }
  
  .input-section,
  .controls {
    display: none !important;
  }
  
  .print-section {
    width: 210mm;
    height: 297mm;
    padding: 15mm;
    margin: 0;
    box-shadow: none;
  }
  
  .box {
    break-inside: avoid;
  }
}

/* ===== وسائط متعددة ===== */
@media (max-width: 768px) {
  .print-section {
    width: 100%;
    padding: 10px;
  }
  
  .top-grid,
  .top-grid.second,
  .main-grid {
    grid-template-columns: 1fr;
  }
  
  .images-grid {
    grid-template-columns: 1fr;
  }
  
  .signatures {
    grid-template-columns: 1fr;
    gap: 30px;
  }
  
  .controls {
    left: 50%;
    transform: translateX(-50%);
    flex-direction: row;
  }
}
</style>
</head>

<body>

<!-- قسم إدخال البيانات -->
<div class="section input-section active" id="inputSection">
  <div class="panel">
    <h2>بيانات التقرير</h2>

    <div class="field">
      <label>الإدارة</label>
      <select id="admin">
        <option>الإدارة العامة للتعليم بمنطقة مكة المكرمة – مكة المكرمة</option>
        <option>الإدارة العامة للتعليم بمنطقة الرياض</option>
        <option>الإدارة العامة للتعليم بمنطقة الشرقية</option>
        <option>الإدارة العامة للتعليم بمنطقة المدينة المنورة</option>
      </select>
    </div>

    <div class="field">
      <label>اسم المدرسة</label>
      <input id="school" value="مدرسة سعيد بن العاص">
    </div>

    <div class="field">
      <label>الفصل الدراسي</label>
      <select id="term">
        <option>الفصل الدراسي الأول</option>
        <option>الفصل الدراسي الثاني</option>
      </select>
    </div>

    <div class="field">
      <label>الصف</label>
      <input id="grade" placeholder="مثال: الرابع الابتدائي">
    </div>

    <div class="field">
      <label>المادة</label>
      <input id="subject" placeholder="مثال: الرياضيات">
    </div>

    <div class="field">
      <label>نوع التقرير</label>
      <select id="type">
        <option>تقرير تفعيل حصص النشاط</option>
        <option>تقرير نشاط لا منهجي</option>
        <option>تقرير رحلة تعليمية</option>
        <option>تقرير ورشة عمل</option>
      </select>
    </div>

    <div class="field">
      <label>المستهدفون</label>
      <input id="target" placeholder="مثال: طلاب الصف الرابع">
    </div>

    <div class="field">
      <label>العدد</label>
      <input id="count" type="number" placeholder="مثال: 25">
    </div>

    <div class="field">
      <label>مكان التنفيذ</label>
      <input id="place" placeholder="مثال: الفصل الدراسي">
    </div>

    <div class="field">
      <label>اسم المعلم</label>
      <input id="teacher" value="فهد الخالدي">
    </div>

    <div class="field">
      <label>اسم مدير المدرسة</label>
      <input id="manager" value="نايف اللحياني">
    </div>

    <div class="field">
      <label>الهدف التربوي</label>
      <textarea id="objective"></textarea>
      <button type="button" class="auto-btn" onclick="autoFill('objective')">اقتراح تلقائي</button>
    </div>

    <div class="field">
      <label>وصف مختصر</label>
      <textarea id="desc"></textarea>
      <button type="button" class="auto-btn" onclick="autoFill('desc')">اقتراح تلقائي</button>
    </div>

    <div class="field">
      <label>إجراءات التنفيذ</label>
      <textarea id="steps"></textarea>
      <button type="button" class="auto-btn" onclick="autoFill('steps')">اقتراح تلقائي</button>
    </div>

    <div class="field">
      <label>النتائج</label>
      <textarea id="results"></textarea>
      <button type="button" class="auto-btn" onclick="autoFill('results')">اقتراح تلقائي</button>
    </div>

    <div class="field">
      <label>نقاط القوة</label>
      <textarea id="strengths"></textarea>
      <button type="button" class="auto-btn" onclick="autoFill('strengths')">اقتراح تلقائي</button>
    </div>

    <div class="field">
      <label>التحديات</label>
      <textarea id="challenges"></textarea>
      <button type="button" class="auto-btn" onclick="autoFill('challenges')">اقتراح تلقائي</button>
    </div>

    <div class="field">
      <label>ما يحتاج إلى تطوير</label>
      <textarea id="develop"></textarea>
      <button type="button" class="auto-btn" onclick="autoFill('develop')">اقتراح تلقائي</button>
    </div>

    <div class="field">
      <label>التوصيات</label>
      <textarea id="recommend"></textarea>
      <button type="button" class="auto-btn" onclick="autoFill('recommend')">اقتراح تلقائي</button>
    </div>

    <div class="field">
      <label>صورة 1</label>
      <input type="file" id="img1" class="file-input" accept="image/*">
    </div>

    <div class="field">
      <label>صورة 2</label>
      <input type="file" id="img2" class="file-input" accept="image/*">
    </div>

    <button class="btn" onclick="generateReport()">إنشاء التقرير</button>
  </div>
</div>

<!-- قسم الطباعة -->
<div class="section print-section" id="printSection">
  <div class="header">
    <div class="admin-name" id="adminName">الإدارة العامة للتعليم بمنطقة مكة المكرمة – مكة المكرمة</div>
    <div class="school-name" id="schoolName">مدرسة سعيد بن العاص</div>
    <div class="hijri-date" id="hijriDate">—</div>
  </div>

  <div class="container">
    <div class="top-grid">
      <div class="box">
        <strong>المادة:</strong> <span id="subjectField">—</span>
      </div>
      <div class="box">
        <strong>الصف:</strong> <span id="gradeField">—</span>
      </div>
      <div class="box">
        <strong>الفصل الدراسي:</strong> <span id="termField">—</span>
      </div>
    </div>

    <div class="top-grid second">
      <div class="box">
        <strong>مكان التنفيذ:</strong><br><span id="placeField">—</span>
      </div>
      <div class="box">
        <strong>العدد:</strong><br><span id="countField">—</span>
      </div>
      <div class="box">
        <strong>المستهدفون:</strong><br><span id="targetField">—</span>
      </div>
      <div class="box">
        <strong>نوع التقرير:</strong><br><span id="typeField">تقرير تفعيل حصص النشاط</span>
      </div>
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
</div>

<!-- أزرار التحكم -->
<div class="controls">
  <button class="btn" id="printBtn" onclick="window.print()">🖨️ طباعة التقرير</button>
  <button class="btn btn-secondary" id="backBtn" onclick="goBack()">↩ الرجوع للنموذج</button>
</div>

<script>
// البيانات التلقائية
const autos = {
  objective: [
    "تنمية مهارات الطلاب عبر أنشطة تطبيقية تعزز الثقة بالنفس.",
    "رفع مستوى التفاعل والعمل التعاوني من خلال التعلم بالممارسة.",
    "تعزيز القدرة على حل المشكلات واتخاذ القرار.",
    "تحفيز الإبداع وتنمية المهارات القيادية."
  ],
  desc: [
    "تنفيذ نشاط جماعي يهدف لتطبيق المعرفة وربطها بالواقع العملي.",
    "تفعيل نشاط يتخلله تبادل أدوار وتحفيز التواصل الإيجابي.",
    "نشاط يسمح للطلاب بإبراز مهاراتهم وتحمل المسؤوليات.",
    "برنامج إثرائي يطبق التعلم النشط."
  ],
  steps: [
    "توزيع الأدوار وشرح التعليمات ثم تنفيذ النشاط.",
    "تقسيم الطلاب لمجموعات وتوجيه المشاركة.",
    "تهيئة الوسائل ثم تنفيذ المهمة ومتابعة الأداء.",
    "إدارة النشاط وفق الزمن وتحفيز الطلاب."
  ],
  results: [
    "تحسن ملحوظ في المشاركة الاجتماعية.",
    "ارتفاع الدافعية والانخراط في التعلم.",
    "تنمية مهارات الاتصال وحل المشكلات.",
    "تحقيق الأهداف المخطط لها بكفاءة."
  ],
  strengths: [
    "تنظيم ممتاز للأدوار وتعاون فعّال.",
    "تنوع الأنشطة أسهم في تعزيز التعلم.",
    "وضوح التعليمات وفهم أسرع.",
    "دافعية وحماس لدى الطلاب."
  ],
  challenges: [
    "تفاوت مستوى المشاركة.",
    "ضيق الوقت مقارنة بالمهام.",
    "ضعف استخدام التقنية لدى البعض.",
    "تشتت انتباه بعض الطلاب."
  ],
  develop: [
    "زيادة تحفيز الطلاب الأقل مشاركة.",
    "تخصيص وقت إضافي للأنشطة.",
    "توفير وسائل تعليمية أكثر.",
    "تنمية تحمل المسؤولية."
  ],
  recommend: [
    "الاستمرار في التفعيل المنتظم.",
    "توسيع الأنشطة الإثرائية التقنية.",
    "تعزيز التعلم التعاوني والإبداع.",
    "عرض منجزات الطلاب وتكريمهم."
  ]
};

// مؤشرات للبيانات التلقائية
const idx = {};
for (const k in autos) idx[k] = 0;

// دالة الاقتراح التلقائي
function autoFill(k) {
  idx[k] = (idx[k] + 1) % autos[k].length;
  document.getElementById(k).value = autos[k][idx[k]];
}

// متغيرات لحفظ الصور
let image1Data = null;
let image2Data = null;

// قراءة وتحويل الصور
function encodeImage(file, callback) {
  const reader = new FileReader();
  reader.onload = (e) => {
    callback(e.target.result);
  };
  reader.readAsDataURL(file);
}

// إضافة مستمعين للصور
document.getElementById('img1').addEventListener('change', function(e) {
  if (e.target.files[0]) {
    encodeImage(e.target.files[0], (data) => {
      image1Data = data;
    });
  }
});

document.getElementById('img2').addEventListener('change', function(e) {
  if (e.target.files[0]) {
    encodeImage(e.target.files[0], (data) => {
      image2Data = data;
    });
  }
});

// دالة توليد التقرير
function generateReport() {
  // جمع البيانات من النموذج
  const data = {};
  document.querySelectorAll("#inputSection input, #inputSection select, #inputSection textarea").forEach(el => {
    data[el.id] = el.value;
  });

  // تعبئة البيانات في قسم الطباعة
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
  imagesSection.innerHTML = '';

  if (image1Data || image2Data) {
    if (image1Data) {
      const imgContainer1 = document.createElement('div');
      imgContainer1.className = 'image-container';
      const img1Element = document.createElement('img');
      img1Element.src = image1Data;
      img1Element.alt = 'صورة النشاط 1';
      imgContainer1.appendChild(img1Element);
      imagesSection.appendChild(imgContainer1);
    }

    if (image2Data) {
      const imgContainer2 = document.createElement('div');
      imgContainer2.className = 'image-container';
      const img2Element = document.createElement('img');
      img2Element.src = image2Data;
      img2Element.alt = 'صورة النشاط 2';
      imgContainer2.appendChild(img2Element);
      imagesSection.appendChild(imgContainer2);
    }
  } else {
    imagesSection.innerHTML = '<p style="grid-column: span 2; text-align: center; color: #666; padding: 20px;">لا توجد صور مرفقة</p>';
  }

  // جلب التاريخ الهجري
  getHijriDate();

  // الانتقال لقسم الطباعة
  document.getElementById('inputSection').classList.remove('active');
  document.getElementById('printSection').classList.add('active');
  document.querySelector('.controls').style.display = 'flex';

  // التمرير للأعلى
  window.scrollTo(0, 0);
}

// دالة الرجوع للنموذج
function goBack() {
  document.getElementById('printSection').classList.remove('active');
  document.getElementById('inputSection').classList.add('active');
  document.querySelector('.controls').style.display = 'none';
}

// دالة جلب التاريخ الهجري
function getHijriDate() {
  const today = new Date();
  const day = today.getDate();
  const month = today.getMonth() + 1;
  const year = today.getFullYear();

  fetch(`https://api.aladhan.com/v1/gToH?date=${day}-${month}-${year}`)
    .then(response => response.json())
    .then(data => {
      const hijri = data.data.hijri;
      const hijriDateStr = `${hijri.day} ${hijri.month.ar} ${hijri.year} هـ`;
      document.getElementById('hijriDate').textContent = hijriDateStr;
    })
    .catch(error => {
      console.error('خطأ في جلب التاريخ الهجري:', error);
      // استخدام تاريخ افتراضي إذا فشل الاتصال
      const hijriMonths = ['محرم', 'صفر', 'ربيع الأول', 'ربيع الثاني', 'جمادى الأولى', 'جمادى الآخرة', 'رجب', 'شعبان', 'رمضان', 'شوال', 'ذو القعدة', 'ذو الحجة'];
      const randomDay = Math.floor(Math.random() * 28) + 1;
      const randomMonth = hijriMonths[Math.floor(Math.random() * 12)];
      const randomYear = 1445 + Math.floor(Math.random() * 2);
      document.getElementById('hijriDate').textContent = `${randomDay} ${randomMonth} ${randomYear} هـ`;
    });
}

// تهيئة الصفحة عند التحميل
document.addEventListener('DOMContentLoaded', function() {
  // إخفاء أزرار التحكم في البداية
  document.querySelector('.controls').style.display = 'none';
  
  // تعبئة بعض الحقول التلقائية كنماذج
  autoFill('objective');
  autoFill('desc');
  autoFill('steps');
});
</script>

</body>
</html>