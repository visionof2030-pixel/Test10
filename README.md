<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>أداة إنشاء التقارير التعليمية</title>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Cairo', sans-serif;
            background: #f5f5f5;
            color: #333;
            line-height: 1.6;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: white;
            border-radius: 10px;
            box-shadow: 0 0 20px rgba(0,0,0,0.1);
            overflow: hidden;
        }

        .header {
            background: #083024;
            color: white;
            padding: 30px;
            text-align: center;
        }

        .header h1 {
            font-size: 28px;
            margin-bottom: 10px;
        }

        .header p {
            opacity: 0.9;
        }

        .form-container {
            padding: 30px;
        }

        .tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 30px;
            border-bottom: 2px solid #eee;
            padding-bottom: 10px;
        }

        .tab-btn {
            padding: 12px 25px;
            background: #f0f0f0;
            border: none;
            border-radius: 5px;
            font-family: 'Cairo', sans-serif;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
        }

        .tab-btn.active {
            background: #083024;
            color: white;
        }

        .tab-content {
            display: none;
        }

        .tab-content.active {
            display: block;
            animation: fadeIn 0.5s;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        .form-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #083024;
        }

        .form-group input,
        .form-group textarea,
        .form-group select {
            width: 100%;
            padding: 12px;
            border: 2px solid #ddd;
            border-radius: 5px;
            font-family: 'Cairo', sans-serif;
            font-size: 14px;
            transition: border-color 0.3s;
        }

        .form-group input:focus,
        .form-group textarea:focus,
        .form-group select:focus {
            border-color: #083024;
            outline: none;
        }

        .form-group textarea {
            height: 120px;
            resize: vertical;
        }

        .full-width {
            grid-column: 1 / -1;
        }

        .controls {
            display: flex;
            gap: 15px;
            justify-content: center;
            padding: 30px;
            background: #f9f9f9;
            border-top: 1px solid #eee;
        }

        .btn {
            padding: 15px 35px;
            border: none;
            border-radius: 5px;
            font-family: 'Cairo', sans-serif;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .btn-primary {
            background: #083024;
            color: white;
        }

        .btn-primary:hover {
            background: #0a3d2e;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(8, 48, 36, 0.2);
        }

        .btn-secondary {
            background: #6c757d;
            color: white;
        }

        .btn-secondary:hover {
            background: #5a6268;
        }

        .preview-section {
            margin-top: 30px;
            padding: 20px;
            background: #f8f9fa;
            border-radius: 8px;
            border: 2px dashed #083024;
        }

        .preview-section h3 {
            color: #083024;
            margin-bottom: 15px;
            text-align: center;
        }

        .hint {
            font-size: 12px;
            color: #666;
            margin-top: 5px;
        }

        .required::after {
            content: " *";
            color: #dc3545;
        }

        .image-upload {
            border: 2px dashed #ccc;
            border-radius: 8px;
            padding: 20px;
            text-align: center;
            cursor: pointer;
            transition: border-color 0.3s;
        }

        .image-upload:hover {
            border-color: #083024;
        }

        .image-upload input {
            display: none;
        }

        .image-preview {
            display: none;
            margin-top: 10px;
        }

        .image-preview img {
            max-width: 200px;
            max-height: 150px;
            border-radius: 5px;
        }

        @media (max-width: 768px) {
            .form-grid {
                grid-template-columns: 1fr;
            }
            
            .tabs {
                flex-direction: column;
            }
            
            .btn {
                padding: 12px 25px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>أداة إنشاء التقارير التعليمية</h1>
            <p>املأ النموذج التالي لإنشاء تقرير نشاط إثرائي متكامل وجاهز للطباعة</p>
        </div>

        <div class="tabs">
            <button class="tab-btn active" onclick="showTab(1)">المعلومات الأساسية</button>
            <button class="tab-btn" onclick="showTab(2)">تفاصيل النشاط</button>
            <button class="tab-btn" onclick="showTab(3)">التقييم والتحليل</button>
            <button class="tab-btn" onclick="showTab(4)">الشواهد والمرفقات</button>
        </div>

        <div class="form-container">
            <form id="reportForm">
                <!-- Tab 1: المعلومات الأساسية -->
                <div class="tab-content active" id="tab1">
                    <div class="form-grid">
                        <div class="form-group">
                            <label class="required">اسم المدرسة</label>
                            <input type="text" id="schoolName" placeholder="مثال: مدرسة التجربة النموذجية" required>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">الإدارة التعليمية</label>
                            <input type="text" id="adminName" value="الإدارة العامة للتعليم بمنطقة الرياض" required>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">المادة</label>
                            <input type="text" id="subject" placeholder="مثال: أحياء" required>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">الصف</label>
                            <input type="text" id="grade" placeholder="مثال: الثالث الثانوي" required>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">الفصل الدراسي</label>
                            <select id="semester" required>
                                <option value="الأول">الفصل الأول</option>
                                <option value="الثاني">الفصل الثاني</option>
                                <option value="الصيفي">الفصل الصيفي</option>
                            </select>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">مكان التنفيذ</label>
                            <input type="text" id="location" placeholder="مثال: الفصل الدراسي" required>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">عدد المشاركين</label>
                            <input type="number" id="number" placeholder="مثال: 25" required>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">المستهدفون</label>
                            <input type="text" id="target" placeholder="مثال: طلاب الصف" required>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">نوع التقرير</label>
                            <select id="reportType" required>
                                <option value="نشاط إثرائي">نشاط إثرائي</option>
                                <option value="نشاط صفي">نشاط صفي</option>
                                <option value="نشاط لاصفي">نشاط لا صفي</option>
                                <option value="ورشة عمل">ورشة عمل</option>
                                <option value="رحلة تعليمية">رحلة تعليمية</option>
                            </select>
                        </div>
                    </div>
                </div>

                <!-- Tab 2: تفاصيل النشاط -->
                <div class="tab-content" id="tab2">
                    <div class="form-grid">
                        <div class="form-group full-width">
                            <label class="required">الهدف التربوي</label>
                            <textarea id="objective" placeholder="اذكر الأهداف التربوية للنشاط..." required>شرح مفهوم أساسي في المنهج وتطبيقه عبر أنشطة تفاعلية تركز على التعلم النشط والعمل الجماعي وتنمية مهارات التفكير.</textarea>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">وصف مختصر</label>
                            <textarea id="description" placeholder="وصف مختصر للنشاط..." required>تنفيذ درس نموذجي يركز على الفهم العميق والتطبيق العملي للمفاهيم باستخدام أساليب تعليمية حديثة.</textarea>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">إجراءات التنفيذ</label>
                            <textarea id="procedures" placeholder="خطوات تنفيذ النشاط..." required>عرض المفهوم الجديد، مناقشة أمثلة توضيحية، أنشطة تطبيقية جماعية، حل تمارين فردية، تلخيص النقاط الرئيسية.</textarea>
                        </div>
                    </div>
                </div>

                <!-- Tab 3: التقييم والتحليل -->
                <div class="tab-content" id="tab3">
                    <div class="form-grid">
                        <div class="form-group">
                            <label class="required">النتائج</label>
                            <textarea id="results" placeholder="نتائج النشاط..." required>استيعاب غالبية الطلاب للمفهوم، مشاركة فعالة في الأنشطة، إنجاز التمارين وتحقيق أهداف الدرس.</textarea>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">نقاط القوة</label>
                            <textarea id="strengths" placeholder="نقاط القوة في النشاط..." required>وضوح الشرح، تنوع الأنشطة، إدارة الوقت بفاعلية، مراعاة الفروق الفردية بين الطلاب.</textarea>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">المحفزات</label>
                            <textarea id="motivations" placeholder="العوامل المحفزة..." required>تفاعل الطلاب الإيجابي، تحفيز روح التنافس بين المجموعات، استخدام وسائل تعليمية جذابة.</textarea>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">مواطن القصور</label>
                            <textarea id="weaknesses" placeholder="نقاط الضعف..." required>نقص بعض الوسائل التعليمية، محدودية المساحة الصفية، ضعف مشاركة عدد محدود من الطلاب.</textarea>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">التحديات</label>
                            <textarea id="challenges" placeholder="التحديات التي واجهت النشاط..." required>تفاوت سرعة الاستيعاب بين الطلاب، قصر وقت الحصة، صعوبة بعض المفاهيم العلمية.</textarea>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">التوصيات</label>
                            <textarea id="recommendations" placeholder="توصيات للتحسين..." required>تكرار استخدام الأنشطة التفاعلية، تخصيص وقت كافٍ للمراجعة، استخدام وسائل بصرية وتقنية داعمة.</textarea>
                        </div>
                    </div>
                </div>

                <!-- Tab 4: الشواهد والمرفقات -->
                <div class="tab-content" id="tab4">
                    <div class="form-grid">
                        <div class="form-group">
                            <label>رابط الصورة الأولى</label>
                            <input type="text" id="image1" placeholder="https://example.com/image1.jpg" value="https://i.ibb.co/dwKFLM99/IMG-1941.png">
                            <div class="hint">يمكنك استخدام مواقع مثل imgbb.com لرفع الصور</div>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">وصف الصورة الأولى</label>
                            <textarea id="caption1" required>تنفيذ النشاط داخل الفصل الدراسي من خلال العمل التعاوني بين الطلاب، وتطبيق استراتيجيات التعلم النشط.</textarea>
                        </div>
                        
                        <div class="form-group">
                            <label>رابط الصورة الثانية</label>
                            <input type="text" id="image2" placeholder="https://example.com/image2.jpg" value="https://i.ibb.co/fY77kdRH/IMG-1942.png">
                        </div>
                        
                        <div class="form-group">
                            <label class="required">وصف الصورة الثانية</label>
                            <textarea id="caption2" required>نماذج من أعمال الطلاب أثناء النشاط، توضح تنوع المهام بين الإبداع والتحدي وتنمية مهارات التفكير.</textarea>
                        </div>
                        
                        <div class="form-group full-width">
                            <label>ملاحظات إضافية</label>
                            <textarea id="notes" placeholder="أي ملاحظات إضافية تريد إضافتها للتقرير..."></textarea>
                        </div>
                    </div>
                    
                    <div class="preview-section">
                        <h3>معاينة سريعة للتقرير</h3>
                        <div id="quickPreview">
                            <p><strong>المادة:</strong> <span id="previewSubject">أحياء</span></p>
                            <p><strong>الصف:</strong> <span id="previewGrade">الثالث الثانوي</span></p>
                            <p><strong>الهدف التربوي:</strong> <span id="previewObjective">شرح مفهوم أساسي في المنهج...</span></p>
                        </div>
                    </div>
                </div>
            </form>
        </div>

        <div class="controls">
            <button type="button" class="btn btn-secondary" onclick="clearForm()">
                🗑️ مسح النموذج
            </button>
            <button type="button" class="btn btn-secondary" onclick="loadSampleData()">
                📋 مثال تجريبي
            </button>
            <button type="button" class="btn btn-primary" onclick="generateReport()">
                🖨️ إنشاء التقرير وطباعته
            </button>
            <button type="button" class="btn btn-primary" onclick="saveAsTemplate()">
                💾 حفظ كقالب
            </button>
        </div>
    </div>

    <script>
        // نظام التبويب
        function showTab(tabNumber) {
            // إخفاء جميع التبويبات
            document.querySelectorAll('.tab-content').forEach(tab => {
                tab.classList.remove('active');
            });
            
            // إلغاء تفعيل جميع أزرار التبويب
            document.querySelectorAll('.tab-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // إظهار التبويب المطلوب
            document.getElementById(`tab${tabNumber}`).classList.add('active');
            
            // تفعيل زر التبويب
            event.target.classList.add('active');
            
            // تحديث المعاينة السريعة
            updatePreview();
        }

        // تحديث المعاينة السريعة
        function updatePreview() {
            document.getElementById('previewSubject').textContent = document.getElementById('subject').value || 'أحياء';
            document.getElementById('previewGrade').textContent = document.getElementById('grade').value || 'الثالث الثانوي';
            document.getElementById('previewObjective').textContent = 
                (document.getElementById('objective').value || 'شرح مفهوم أساسي في المنهج...').substring(0, 100) + '...';
        }

        // تحديث المعاينة عند الكتابة
        document.querySelectorAll('input, textarea, select').forEach(element => {
            element.addEventListener('input', updatePreview);
        });

        // مسح النموذج
        function clearForm() {
            if (confirm('هل أنت متأكد من رغبتك في مسح جميع البيانات؟')) {
                document.getElementById('reportForm').reset();
                updatePreview();
            }
        }

        // تحميل بيانات تجريبية
        function loadSampleData() {
            document.getElementById('schoolName').value = 'مدرسة التجربة النموذجية';
            document.getElementById('adminName').value = 'الإدارة العامة للتعليم بمنطقة الرياض';
            document.getElementById('subject').value = 'أحياء';
            document.getElementById('grade').value = 'الثالث الثانوي';
            document.getElementById('semester').value = 'الأول';
            document.getElementById('location').value = 'الفصل الدراسي';
            document.getElementById('number').value = '25';
            document.getElementById('target').value = 'طلاب الصف';
            document.getElementById('reportType').value = 'نشاط إثرائي';
            document.getElementById('objective').value = 'شرح مفهوم أساسي في المنهج وتطبيقه عبر أنشطة تفاعلية تركز على التعلم النشط والعمل الجماعي وتنمية مهارات التفكير.';
            document.getElementById('description').value = 'تنفيذ درس نموذجي يركز على الفهم العميق والتطبيق العملي للمفاهيم باستخدام أساليب تعليمية حديثة.';
            document.getElementById('procedures').value = 'عرض المفهوم الجديد، مناقشة أمثلة توضيحية، أنشطة تطبيقية جماعية، حل تمارين فردية، تلخيص النقاط الرئيسية.';
            document.getElementById('results').value = 'استيعاب غالبية الطلاب للمفهوم، مشاركة فعالة في الأنشطة، إنجاز التمارين وتحقيق أهداف الدرس.';
            document.getElementById('strengths').value = 'وضوح الشرح، تنوع الأنشطة، إدارة الوقت بفاعلية، مراعاة الفروق الفردية بين الطلاب.';
            document.getElementById('motivations').value = 'تفاعل الطلاب الإيجابي، تحفيز روح التنافس بين المجموعات، استخدام وسائل تعليمية جذابة.';
            document.getElementById('weaknesses').value = 'نقص بعض الوسائل التعليمية، محدودية المساحة الصفية، ضعف مشاركة عدد محدود من الطلاب.';
            document.getElementById('challenges').value = 'تفاوت سرعة الاستيعاب بين الطلاب، قصر وقت الحصة، صعوبة بعض المفاهيم العلمية.';
            document.getElementById('recommendations').value = 'تكرار استخدام الأنشطة التفاعلية، تخصيص وقت كافٍ للمراجعة، استخدام وسائل بصرية وتقنية داعمة.';
            document.getElementById('image1').value = 'https://i.ibb.co/dwKFLM99/IMG-1941.png';
            document.getElementById('caption1').value = 'تنفيذ النشاط داخل الفصل الدراسي من خلال العمل التعاوني بين الطلاب، وتطبيق استراتيجيات التعلم النشط.';
            document.getElementById('image2').value = 'https://i.ibb.co/fY77kdRH/IMG-1942.png';
            document.getElementById('caption2').value = 'نماذج من أعمال الطلاب أثناء النشاط، توضح تنوع المهام بين الإبداع والتحدي وتنمية مهارات التفكير.';
            
            updatePreview();
            alert('تم تحميل البيانات التجريبية بنجاح!');
        }

        // حفظ كقالب
        function saveAsTemplate() {
            const templateData = {
                schoolName: document.getElementById('schoolName').value,
                subject: document.getElementById('subject').value,
                grade: document.getElementById('grade').value,
                // ... جمع جميع البيانات
            };
            
            const dataStr = JSON.stringify(templateData, null, 2);
            const dataUri = 'data:application/json;charset=utf-8,'+ encodeURIComponent(dataStr);
            
            const exportFileDefaultName = 'قالب_تقرير_تعليمي.json';
            
            const linkElement = document.createElement('a');
            linkElement.setAttribute('href', dataUri);
            linkElement.setAttribute('download', exportFileDefaultName);
            linkElement.click();
            
            alert('تم حفظ البيانات كقالب بنجاح!');
        }

        // الوظيفة الرئيسية: إنشاء التقرير
        function generateReport() {
            // التحقق من الحقول المطلوبة
            const requiredFields = [
                'schoolName', 'adminName', 'subject', 'grade', 
                'semester', 'location', 'number', 'target', 'reportType',
                'objective', 'description', 'procedures', 'results',
                'strengths', 'motivations', 'weaknesses', 'challenges',
                'recommendations', 'caption1', 'caption2'
            ];
            
            let isValid = true;
            requiredFields.forEach(fieldId => {
                const field = document.getElementById(fieldId);
                if (!field.value.trim()) {
                    isValid = false;
                    field.style.borderColor = '#dc3545';
                } else {
                    field.style.borderColor = '#ddd';
                }
            });
            
            if (!isValid) {
                alert('يرجى ملء جميع الحقول المطلوبة (المحددة بنجمة)');
                return;
            }
            
            // إنشاء صفحة التقرير
            const reportWindow = window.open('', '_blank');
            
            // جمع البيانات من النموذج
            const data = {
                schoolName: document.getElementById('schoolName').value,
                adminName: document.getElementById('adminName').value,
                subject: document.getElementById('subject').value,
                grade: document.getElementById('grade').value,
                semester: document.getElementById('semester').value,
                location: document.getElementById('location').value,
                number: document.getElementById('number').value,
                target: document.getElementById('target').value,
                reportType: document.getElementById('reportType').value,
                objective: document.getElementById('objective').value,
                description: document.getElementById('description').value,
                procedures: document.getElementById('procedures').value,
                results: document.getElementById('results').value,
                strengths: document.getElementById('strengths').value,
                motivations: document.getElementById('motivations').value,
                weaknesses: document.getElementById('weaknesses').value,
                challenges: document.getElementById('challenges').value,
                recommendations: document.getElementById('recommendations').value,
                image1: document.getElementById('image1').value,
                caption1: document.getElementById('caption1').value,
                image2: document.getElementById('image2').value,
                caption2: document.getElementById('caption2').value,
                notes: document.getElementById('notes').value
            };
            
            // إنشاء محتوى HTML للتقرير
            const reportHTML = `
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<title>تقرير نشاط إثرائي - ${data.subject}</title>
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap" rel="stylesheet">

<style>
@page{
  size:A4;
  margin:12mm;
}

*{margin:0;padding:0;box-sizing:border-box}

body{
  font-family:'Cairo',sans-serif;
  background:#fff;
  color:#1f2937;
  width:210mm;
  height:297mm;
  margin:0 auto;
}

/* ===== الهيدر ===== */
.header{
  width:100%;
  height:105px;
  background:#083024;
  position:relative;
  margin-bottom:10px;
}
.header::before{
  content:"";
  position:absolute;
  inset:0;
  background:url('https://i.ibb.co/kVWFFwhW/9-C92-E57-B-23-FA-479-D-A024-1-D5-F871-B4-F8-D.png') center/40% no-repeat;
  opacity:.95;
}
.admin-name,.school-name,.hijri-date{
  position:absolute;
  font-size:10.5px;
  color:#fff;
  z-index:2;
}
.admin-name{top:10px;right:16px}
.school-name{bottom:10px;right:16px}
.hijri-date{bottom:10px;left:16px}

/* ===== عام ===== */
.container{width:100%}

.box{
  border:2px solid #3f5f5a;
  border-radius:8px;
  padding:10px;
  font-size:11.5px;
  line-height:1.6;
  background:#fff;
}
.box-title{
  font-weight:700;
  margin-bottom:6px;
  font-size:12.5px;
}

/* ===== الصفوف العلوية ===== */
.top-grid{
  display:grid;
  grid-template-columns:repeat(3,1fr);
  gap:8px;
  margin-bottom:8px;
}
.top-grid.second{
  grid-template-columns:repeat(4,1fr);
}

/* ===== الهدف ===== */
.objective{
  background:#eef6ea;
  border:2px solid #6fa37a;
  text-align:center;
  font-size:13px;
  margin:8px 0;
  padding:12px;
}

/* ===== المحتوى ===== */
.main-grid{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:8px;
}

/* ===== ألوان ===== */
.result{border-color:#3f6fa5}
.recommend{border-color:#3f6fa5}
.strength{border-color:#3f6fa5}
.motivation{
  background:#fff7cc;
  border:2px dashed #e6c84f;
}
.weakness{
  background:#ffecec;
  border-color:#d16a6a;
}
.challenge{
  background:#ffecec;
  border-color:#d16a6a;
}

/* ===== شواهد الصور ===== */
.evidence-section{
  margin-top:10px;
}
.evidence-title{
  font-size:13px;
  font-weight:700;
  color:#083024;
  margin-bottom:6px;
}
.evidence-grid{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:10px;
}
.evidence-box{
  border:2px solid #083024;
  border-radius:8px;
  overflow:hidden;
}
.evidence-box img{
  width:100%;
  height:150px;
  object-fit:cover;
  display:block;
}
.evidence-caption{
  padding:6px;
  font-size:10.5px;
  line-height:1.6;
  background:#f9fafb;
  border-top:1px solid #e5e7eb;
}

/* ===== أزرار التحكم ===== */
.controls {
  position: fixed;
  top: 20px;
  left: 20px;
  display: flex;
  gap: 10px;
  z-index: 1000;
}

.print-btn {
  padding: 10px 20px;
  background: #083024;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-family: 'Cairo', sans-serif;
  font-weight: 600;
  transition: background 0.3s;
}

.print-btn:hover {
  background: #0a3d2e;
}

/* ===== ملاحظات إضافية ===== */
.notes-box {
  margin-top: 10px;
  padding: 10px;
  background: #f8f9fa;
  border: 1px dashed #6c757d;
  border-radius: 5px;
  font-size: 11px;
}

/* ===== تحسينات للطباعة ===== */
@media print {
  .controls {
    display: none;
  }
  
  body {
    width: 100%;
    height: auto;
  }
}
</style>
</head>

<body>

<div class="controls">
  <button class="print-btn" onclick="window.print()">🖨️ طباعة التقرير</button>
</div>

<div class="header">
  <div class="admin-name">${data.adminName}</div>
  <div class="school-name">${data.schoolName}</div>
  <div class="hijri-date" id="hijriDate">—</div>
</div>

<div class="container">

  <div class="top-grid">
    <div class="box"><strong>المادة</strong><br>${data.subject}</div>
    <div class="box"><strong>الصف</strong><br>${data.grade}</div>
    <div class="box"><strong>الفصل الدراسي</strong><br>${data.semester}</div>
  </div>

  <div class="top-grid second">
    <div class="box"><strong>مكان التنفيذ</strong><br>${data.location}</div>
    <div class="box"><strong>العدد</strong><br>${data.number}</div>
    <div class="box"><strong>المستهدفون</strong><br>${data.target}</div>
    <div class="box"><strong>التقرير</strong><br>${data.reportType}</div>
  </div>

  <div class="box objective">
    <div class="box-title">الهدف التربوي</div>
    ${data.objective}
  </div>

  <div class="main-grid">
    <div class="box">
      <div class="box-title">إجراءات التنفيذ</div>
      ${data.procedures}
    </div>

    <div class="box">
      <div class="box-title">وصف مختصر</div>
      ${data.description}
    </div>

    <div class="box recommend">
      <div class="box-title">التوصيات</div>
      ${data.recommendations}
    </div>

    <div class="box result">
      <div class="box-title">النتائج</div>
      ${data.results}
    </div>

    <div class="box strength">
      <div class="box-title">نقاط القوة</div>
      ${data.strengths}
    </div>

    <div class="box motivation">
      <div class="box-title">المحفزات</div>
      ${data.motivations}
    </div>

    <div class="box weakness">
      <div class="box-title">مواطن القصور</div>
      ${data.weaknesses}
    </div>

    <div class="box challenge">
      <div class="box-title">التحديات</div>
      ${data.challenges}
    </div>
  </div>

  ${data.notes ? `
  <div class="notes-box">
    <strong>ملاحظات إضافية:</strong><br>
    ${data.notes}
  </div>
  ` : ''}

  <div class="evidence-section">
    <div class="evidence-title">شواهد الصور</div>
    <div class="evidence-grid">
      <div class="evidence-box">
        <img src="${data.image1}" onerror="this.src='https://via.placeholder.com/400x300?text=صورة+غير+متاحة'">
        <div class="evidence-caption">
          ${data.caption1}
        </div>
      </div>
      <div class="evidence-box">
        <img src="${data.image2}" onerror="this.src='https://via.placeholder.com/400x300?text=صورة+غير+متاحة'">
        <div class="evidence-caption">
          ${data.caption2}
        </div>
      </div>
    </div>
  </div>
</div>

<script>
// دالة لجلب التاريخ الهجري
fetch('https://api.aladhan.com/v1/gToH')
.then(r=>r.json())
.then(d=>{
 const h=d.data.hijri;
 document.getElementById('hijriDate').textContent =
 \`\${h.day} \${h.month.ar} \${h.year} هـ\`;
}).catch(() => {
 document.getElementById('hijriDate').textContent = new Date().toLocaleDateString('ar-SA');
});

// طباعة تلقائية بعد تحميل الصفحة
window.onload = function() {
  setTimeout(() => {
    document.querySelector('.print-btn').click();
  }, 1000);
};
</script>

</body>
</html>`;
            
            // كتابة المحتوى في النافذة الجديدة
            reportWindow.document.write(reportHTML);
            reportWindow.document.close();
            
            alert('تم إنشاء التقرير بنجاح! سيتم فتح نافذة الطباعة تلقائياً.');
        }

        // تهيئة الصفحة
        document.addEventListener('DOMContentLoaded', function() {
            updatePreview();
        });
    </script>
</body>
</html>