<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>نظام إنشاء PDF باللغة العربية</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Amiri:wght@400;700&family=Noto+Naskh+Arabic:wght@400;700&display=swap" rel="stylesheet">
    <style>
        /* التنسيقات الأساسية */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Amiri', serif;
            background-color: #f5f7fa;
            color: #333;
            line-height: 1.6;
            direction: rtl;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        /* الترويسة */
        .header {
            text-align: center;
            margin-bottom: 30px;
            padding: 20px;
            background: linear-gradient(135deg, #2c3e50, #4a6491);
            color: white;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }

        .header h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
            font-weight: 700;
        }

        .subtitle {
            font-size: 1.2rem;
            opacity: 0.9;
        }

        /* الأزرار */
        .controls {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 15px;
            margin-bottom: 30px;
        }

        .btn {
            padding: 12px 24px;
            border: none;
            border-radius: 8px;
            font-size: 1rem;
            font-weight: bold;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            transition: all 0.3s ease;
            font-family: inherit;
        }

        .btn-primary {
            background-color: #3498db;
            color: white;
        }

        .btn-primary:hover {
            background-color: #2980b9;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(52, 152, 219, 0.4);
        }

        .btn-secondary {
            background-color: #2ecc71;
            color: white;
        }

        .btn-secondary:hover {
            background-color: #27ae60;
            transform: translateY(-2px);
        }

        .btn-danger {
            background-color: #e74c3c;
            color: white;
        }

        .btn-danger:hover {
            background-color: #c0392b;
            transform: translateY(-2px);
        }

        .icon {
            font-size: 1.2rem;
        }

        /* قسم الإعدادات */
        .editor-section {
            background-color: white;
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 30px;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.08);
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
        }

        .form-group {
            flex: 1;
            min-width: 250px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #2c3e50;
        }

        .form-control {
            width: 100%;
            padding: 12px;
            border: 1px solid #ddd;
            border-radius: 6px;
            font-size: 1rem;
            font-family: inherit;
            transition: border 0.3s ease;
        }

        .form-control:focus {
            outline: none;
            border-color: #3498db;
            box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.2);
        }

        /* المحتوى القابل للطباعة */
        .printable-content {
            background-color: white;
            padding: 40px;
            border-radius: 10px;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
            margin-bottom: 30px;
            min-height: 1200px;
            position: relative;
        }

        /* رأس المستند */
        .document-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 40px;
            padding-bottom: 20px;
            border-bottom: 2px solid #eee;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .logo-placeholder {
            font-size: 3rem;
            background-color: #f8f9fa;
            width: 80px;
            height: 80px;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 50%;
            border: 2px dashed #ddd;
        }

        .logo-text h2 {
            font-size: 1.8rem;
            margin-bottom: 5px;
            color: #2c3e50;
        }

        .logo-text p {
            color: #7f8c8d;
            font-size: 1rem;
        }

        .document-info p {
            margin-bottom: 8px;
            text-align: left;
        }

        /* عنوان المستند */
        .document-title {
            text-align: center;
            margin-bottom: 40px;
        }

        .document-title h1 {
            font-size: 2.5rem;
            color: #2c3e50;
            margin-bottom: 15px;
        }

        .title-decoration {
            height: 4px;
            width: 150px;
            background: linear-gradient(90deg, #3498db, #2ecc71);
            margin: 0 auto;
            border-radius: 2px;
        }

        /* محتوى المستند */
        .document-body {
            margin-bottom: 40px;
        }

        .section {
            margin-bottom: 40px;
        }

        .section h2 {
            font-size: 1.8rem;
            color: #2c3e50;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 2px solid #f1f1f1;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .section p {
            margin-bottom: 15px;
            font-size: 1.2rem;
            line-height: 1.8;
            text-align: justify;
        }

        /* الجداول */
        .table-container {
            overflow-x: auto;
            margin: 20px 0;
        }

        .arabic-table {
            width: 100%;
            border-collapse: collapse;
            font-size: 1.1rem;
        }

        .arabic-table thead {
            background-color: #2c3e50;
            color: white;
        }

        .arabic-table th {
            padding: 15px;
            text-align: right;
            font-weight: bold;
        }

        .arabic-table tbody tr {
            border-bottom: 1px solid #eee;
            transition: background-color 0.2s ease;
        }

        .arabic-table tbody tr:hover {
            background-color: #f9f9f9;
        }

        .arabic-table td {
            padding: 15px;
            text-align: right;
        }

        .arabic-table tbody tr:nth-child(even) {
            background-color: #f8f9fa;
        }

        /* القوائم */
        .arabic-list {
            padding-right: 25px;
            margin: 20px 0;
        }

        .arabic-list li {
            margin-bottom: 12px;
            font-size: 1.2rem;
            position: relative;
            padding-right: 10px;
        }

        .arabic-list li:before {
            content: "•";
            color: #3498db;
            font-size: 1.5rem;
            position: absolute;
            right: -20px;
            top: 0;
        }

        /* مربع متميز */
        .highlight-box {
            background-color: #f8f9fa;
            border-right: 4px solid #3498db;
            padding: 20px;
            border-radius: 8px;
            margin: 25px 0;
        }

        .highlight-box h3 {
            color: #2c3e50;
            margin-bottom: 15px;
            font-size: 1.5rem;
        }

        /* التوقيعات */
        .signatures {
            display: flex;
            justify-content: space-between;
            flex-wrap: wrap;
            gap: 20px;
            margin-top: 60px;
            padding-top: 30px;
            border-top: 2px solid #eee;
        }

        .signature-block {
            flex: 1;
            min-width: 200px;
            text-align: center;
        }

        .signature-label {
            font-weight: bold;
            margin-bottom: 15px;
            font-size: 1.2rem;
        }

        .signature-line {
            height: 1px;
            background-color: #333;
            margin: 20px auto;
            width: 80%;
        }

        .signature-block p {
            margin-bottom: 8px;
        }

        .stamp {
            font-size: 2.5rem;
            margin: 15px 0;
        }

        /* تذييل المستند */
        .document-footer {
            text-align: center;
            padding-top: 20px;
            border-top: 1px solid #eee;
            color: #7f8c8d;
            font-size: 0.9rem;
        }

        /* التعليمات */
        .instructions {
            background-color: #f8f9fa;
            padding: 25px;
            border-radius: 10px;
            margin-bottom: 30px;
            border-right: 5px solid #3498db;
        }

        .instructions h3 {
            color: #2c3e50;
            margin-bottom: 15px;
            font-size: 1.5rem;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .instructions ol {
            padding-right: 25px;
        }

        .instructions li {
            margin-bottom: 12px;
            font-size: 1.1rem;
        }

        /* التذييل */
        .footer {
            text-align: center;
            padding: 20px;
            color: #7f8c8d;
            font-size: 0.9rem;
            border-top: 1px solid #eee;
            margin-top: 20px;
        }

        /* الطباعة */
        @media print {
            .controls, .editor-section, .instructions, .footer {
                display: none;
            }
            
            .printable-content {
                box-shadow: none;
                padding: 0;
                min-height: auto;
            }
        }

        /* التجاوب مع الشاشات المختلفة */
        @media (max-width: 768px) {
            .header h1 {
                font-size: 2rem;
            }
            
            .document-header {
                flex-direction: column;
                align-items: flex-start;
                gap: 20px;
            }
            
            .signatures {
                flex-direction: column;
                align-items: center;
            }
            
            .controls {
                flex-direction: column;
                align-items: stretch;
            }
            
            .btn {
                width: 100%;
            }
        }

        /* تنسيقات إضافية للرسائل */
        .message-content {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }
        
        .spinner {
            border: 3px solid rgba(255, 255, 255, 0.3);
            border-radius: 50%;
            border-top: 3px solid white;
            width: 20px;
            height: 20px;
            animation: spin 1s linear infinite;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body>
    <div class="container">
        <header class="header">
            <h1>نظام إنشاء ملفات PDF بالعربية</h1>
            <p class="subtitle">أداة متكاملة لإنشاء وتصدير ملفات PDF تحتوي على نص عربي</p>
        </header>

        <main class="main-content">
            <div class="controls">
                <button id="generatePdf" class="btn btn-primary">
                    <span class="icon">📄</span> إنشاء PDF
                </button>
                <button id="previewPdf" class="btn btn-secondary">
                    <span class="icon">👁️</span> معاينة PDF
                </button>
                <button id="printContent" class="btn btn-secondary">
                    <span class="icon">🖨️</span> طباعة
                </button>
                <button id="resetContent" class="btn btn-danger">
                    <span class="icon">🗑️</span> مسح المحتوى
                </button>
            </div>

            <div class="editor-section">
                <div class="form-group">
                    <label for="documentTitle">عنوان المستند:</label>
                    <input type="text" id="documentTitle" class="form-control" value="مستند عربي رسمي">
                </div>

                <div class="form-group">
                    <label for="fontSelector">اختر الخط:</label>
                    <select id="fontSelector" class="form-control">
                        <option value="Amiri, serif">Amiri (افتراضي)</option>
                        <option value="'Noto Naskh Arabic', serif">Noto Naskh Arabic</option>
                        <option value="Arial, sans-serif">Arial</option>
                        <option value="'Times New Roman', serif">Times New Roman</option>
                    </select>
                </div>
            </div>

            <div id="contentToPrint" class="printable-content">
                <div class="document-header">
                    <div class="logo">
                        <div class="logo-placeholder">🌙</div>
                        <div class="logo-text">
                            <h2>شركة التقنية العربية</h2>
                            <p>مقر الشركة: الرياض - المملكة العربية السعودية</p>
                        </div>
                    </div>
                    <div class="document-info">
                        <p><strong>رقم المستند:</strong> AR-2024-001</p>
                        <p><strong>التاريخ:</strong> <span id="currentDate"></span></p>
                    </div>
                </div>

                <div class="document-title">
                    <h1 id="dynamicTitle">مستند عربي رسمي</h1>
                    <div class="title-decoration"></div>
                </div>

                <div class="document-body">
                    <div class="section">
                        <h2><span class="section-icon">📌</span> المقدمة</h2>
                        <p>هذا مستند تجريبي يوضح قدرة النظام على معالجة النصوص العربية بشكل كامل. يتم استخدام خطوط عربية مدعومة بشكل كامل في ملفات PDF. النص العربي يكتب من اليمين إلى اليسار وهذا ما يدعمه النظام بشكل تلقائي.</p>
                        <p>يمكنك تعديل هذا النص كما تريد، وإضافة أي محتوى عربي وسيتم الحفاظ على تنسيقه في ملف PDF الناتج. يدعم النظام جميع أحرف اللغة العربية بما في ذلك الحروف الخاصة.</p>
                    </div>

                    <div class="section">
                        <h2><span class="section-icon">📊</span> جدول بيانات عربي</h2>
                        <div class="table-container">
                            <table class="arabic-table">
                                <thead>
                                    <tr>
                                        <th>الرقم</th>
                                        <th>الاسم الكامل</th>
                                        <th>القسم</th>
                                        <th>الراتب</th>
                                        <th>تاريخ التعيين</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td>1</td>
                                        <td>أحمد محمد السعيد</td>
                                        <td>تطوير البرمجيات</td>
                                        <td>15,000 ر.س</td>
                                        <td>2023-01-15</td>
                                    </tr>
                                    <tr>
                                        <td>2</td>
                                        <td>فاطمة عبدالله العتيبي</td>
                                        <td>التصميم الجرافيكي</td>
                                        <td>12,500 ر.س</td>
                                        <td>2023-03-22</td>
                                    </tr>
                                    <tr>
                                        <td>3</td>
                                        <td>خالد سعيد الحربي</td>
                                        <td>إدارة المشاريع</td>
                                        <td>18,000 ر.س</td>
                                        <td>2022-11-10</td>
                                    </tr>
                                    <tr>
                                        <td>4</td>
                                        <td>نورة راشد القحطاني</td>
                                        <td>التسويق الرقمي</td>
                                        <td>11,000 ر.س</td>
                                        <td>2024-02-05</td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>

                    <div class="section">
                        <h2><span class="section-icon">📝</span> قائمة نقاط عربية</h2>
                        <ul class="arabic-list">
                            <li>دعم كامل للغة العربية في إنشاء ملفات PDF</li>
                            <li>القدرة على إضافة جداول بنص عربي</li>
                            <li>دعم الأحرف العربية الخاصة (ء، ى، ة، إلخ)</li>
                            <li>تنسيق النص (عريض، مائل، تحته خط)</li>
                            <li>إضافة صور وتنسيقات متقدمة</li>
                        </ul>
                    </div>

                    <div class="section">
                        <h2><span class="section-icon">📋</span> معلومات إضافية</h2>
                        <p>هذا النص يحتوي على <strong>كلمات عريضة</strong> و <em>كلمات مائلة</em> و <u>نص تحته خط</u>.</p>
                        <p>كما يمكن كتابة النص باللغة الإنجليزية مع النص العربي في نفس السطر مثل: Hello World! مرحباً بالعالم!</p>
                        
                        <div class="highlight-box">
                            <h3>ملاحظة هامة:</h3>
                            <p>جميع محتويات هذا المستند ستظهر في ملف PDF بنفس التنسيق والشكل الذي تراه الآن. يمكنك إضافة أي عناصر HTML وسيتم تحويلها إلى PDF.</p>
                        </div>
                    </div>

                    <div class="signatures">
                        <div class="signature-block">
                            <p class="signature-label">التوقيع:</p>
                            <div class="signature-line"></div>
                            <p>مدير قسم التقنية</p>
                            <p>م. عبدالرحمن العلي</p>
                        </div>
                        <div class="signature-block">
                            <p class="signature-label">التوقيع:</p>
                            <div class="signature-line"></div>
                            <p>مدير الموارد البشرية</p>
                            <p>أ. فهد السعد</p>
                        </div>
                        <div class="signature-block">
                            <p class="signature-label">ختم المؤسسة:</p>
                            <div class="stamp">📍</div>
                            <p>شركة التقنية العربية</p>
                        </div>
                    </div>
                </div>

                <div class="document-footer">
                    <p>صفحة 1 من 1 | تم إنشاء هذا المستند بواسطة نظام إنشاء PDF العربي</p>
                    <p>جميع الحقوق محفوظة © 2024 شركة التقنية العربية</p>
                </div>
            </div>

            <div class="instructions">
                <h3><span class="icon">💡</span> تعليمات الاستخدام:</h3>
                <ol>
                    <li>قم بتعديل المحتوى كما تريد (العنوان، الجدول، النصوص)</li>
                    <li>اختر الخط المناسب من القائمة المنسدلة</li>
                    <li>اضغط على زر "إنشاء PDF" لتحميل الملف</li>
                    <li>استخدم زر "معاينة PDF" لرؤية كيف سيبدو الملف</li>
                    <li>يمكنك طباعة المحتوى مباشرة باستخدام زر "طباعة"</li>
                </ol>
            </div>
        </main>

        <footer class="footer">
            <p>تم التطوير باستخدام مكتبة html2pdf.js - يدعم اللغة العربية بشكل كامل</p>
        </footer>
    </div>

    <!-- مكتبة html2pdf -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
    
    <script>
        // تهيئة التاريخ الحالي
        function initializeCurrentDate() {
            const now = new Date();
            const options = { 
                weekday: 'long', 
                year: 'numeric', 
                month: 'long', 
                day: 'numeric' 
            };
            const arabicDate = now.toLocaleDateString('ar-SA', options);
            document.getElementById('currentDate').textContent = arabicDate;
        }

        // تحديث عنوان المستند
        function updateDocumentTitle() {
            const titleInput = document.getElementById('documentTitle');
            const dynamicTitle = document.getElementById('dynamicTitle');
            
            titleInput.addEventListener('input', function() {
                dynamicTitle.textContent = this.value || 'مستند عربي رسمي';
            });
        }

        // تغيير الخط
        function setupFontSelector() {
            const fontSelector = document.getElementById('fontSelector');
            const printableContent = document.getElementById('contentToPrint');
            
            fontSelector.addEventListener('change', function() {
                printableContent.style.fontFamily = this.value;
            });
        }

        // إنشاء PDF
        function setupPdfGeneration() {
            const generateBtn = document.getElementById('generatePdf');
            const previewBtn = document.getElementById('previewPdf');
            const printBtn = document.getElementById('printContent');
            const resetBtn = document.getElementById('resetContent');
            
            // خيارات PDF
            const pdfOptions = {
                margin: [15, 15, 15, 15],
                filename: 'المستند_العربي.pdf',
                image: { 
                    type: 'jpeg', 
                    quality: 0.98 
                },
                html2canvas: { 
                    scale: 2,
                    useCORS: true,
                    logging: false,
                    backgroundColor: '#FFFFFF'
                },
                jsPDF: { 
                    unit: 'mm', 
                    format: 'a4', 
                    orientation: 'portrait',
                    compress: true
                },
                pagebreak: { 
                    mode: ['avoid-all', 'css', 'legacy'] 
                }
            };
            
            // إنشاء PDF مع تحميله
            generateBtn.addEventListener('click', function() {
                const element = document.getElementById('contentToPrint');
                const title = document.getElementById('documentTitle').value || 'المستند_العربي';
                pdfOptions.filename = `${title}.pdf`;
                
                // إظهار رسالة تحميل
                showLoadingMessage('جاري إنشاء PDF...');
                
                // إنشاء PDF
                html2pdf()
                    .set(pdfOptions)
                    .from(element)
                    .save()
                    .then(() => {
                        showSuccessMessage('تم إنشاء PDF بنجاح!');
                    })
                    .catch(error => {
                        console.error('خطأ في إنشاء PDF:', error);
                        showErrorMessage('حدث خطأ أثناء إنشاء PDF. الرجاء المحاولة مرة أخرى.');
                    });
            });
            
            // معاينة PDF في نافذة جديدة
            previewBtn.addEventListener('click', function() {
                const element = document.getElementById('contentToPrint');
                
                // إظهار رسالة تحميل
                showLoadingMessage('جاري إنشاء معاينة PDF...');
                
                // إنشاء PDF للمعاينة
                html2pdf()
                    .set(pdfOptions)
                    .from(element)
                    .toPdf()
                    .get('pdf')
                    .then(function(pdf) {
                        const pdfBlob = pdf.output('blob');
                        const pdfUrl = URL.createObjectURL(pdfBlob);
                        
                        // فتح PDF في نافذة جديدة
                        window.open(pdfUrl, '_blank');
                        
                        // إظهار رسالة نجاح
                        setTimeout(() => {
                            showSuccessMessage('تم فتح معاينة PDF في نافذة جديدة');
                        }, 500);
                    })
                    .catch(error => {
                        console.error('خطأ في معاينة PDF:', error);
                        showErrorMessage('حدث خطأ أثناء إنشاء معاينة PDF.');
                    });
            });
            
            // طباعة المحتوى مباشرة
            printBtn.addEventListener('click', function() {
                const originalContent = document.body.innerHTML;
                const printContent = document.getElementById('contentToPrint').innerHTML;
                
                // استبدال محتوى الصفحة بالمحتوى القابل للطباعة فقط
                document.body.innerHTML = `
                    <div style="direction: rtl; font-family: 'Amiri', serif; padding: 20px;">
                        ${printContent}
                    </div>
                    <script>
                        window.onload = function() {
                            window.print();
                            setTimeout(function() {
                                window.location.reload();
                            }, 100);
                        }
                    <\/script>
                `;
            });
            
            // إعادة تعيين المحتوى
            resetBtn.addEventListener('click', function() {
                if (confirm('هل أنت متأكد من مسح جميع التعديلات؟')) {
                    // إعادة تعيين العنوان
                    document.getElementById('documentTitle').value = 'مستند عربي رسمي';
                    document.getElementById('dynamicTitle').textContent = 'مستند عربي رسمي';
                    
                    // إعادة تعيين الخط
                    document.getElementById('fontSelector').value = 'Amiri, serif';
                    document.getElementById('contentToPrint').style.fontFamily = 'Amiri, serif';
                    
                    showSuccessMessage('تم إعادة تعيين المحتوى بنجاح');
                }
            });
        }

        // عرض رسائل التحميل والنتائج
        function showLoadingMessage(message) {
            // إزالة أي رسائل سابقة
            const existingMessage = document.querySelector('.status-message');
            if (existingMessage) existingMessage.remove();
            
            // إنشاء رسالة جديدة
            const messageDiv = document.createElement('div');
            messageDiv.className = 'status-message loading';
            messageDiv.innerHTML = `
                <div class="message-content">
                    <div class="spinner"></div>
                    <p>${message}</p>
                </div>
            `;
            
            // إضافة التنسيقات
            messageDiv.style.cssText = `
                position: fixed;
                top: 20px;
                left: 50%;
                transform: translateX(-50%);
                background-color: #3498db;
                color: white;
                padding: 15px 25px;
                border-radius: 8px;
                box-shadow: 0 5px 15px rgba(0,0,0,0.2);
                z-index: 10000;
                min-width: 250px;
                text-align: center;
            `;
            
            document.body.appendChild(messageDiv);
        }

        function showSuccessMessage(message) {
            // إزالة أي رسائل سابقة
            const existingMessage = document.querySelector('.status-message');
            if (existingMessage) existingMessage.remove();
            
            // إنشاء رسالة جديدة
            const messageDiv = document.createElement('div');
            messageDiv.className = 'status-message success';
            messageDiv.innerHTML = `
                <div class="message-content">
                    <span style="font-size: 1.5rem; margin-left: 10px;">✅</span>
                    <p>${message}</p>
                </div>
            `;
            
            // إضافة التنسيقات
            messageDiv.style.cssText = `
                position: fixed;
                top: 20px;
                left: 50%;
                transform: translateX(-50%);
                background-color: #2ecc71;
                color: white;
                padding: 15px 25px;
                border-radius: 8px;
                box-shadow: 0 5px 15px rgba(0,0,0,0.2);
                z-index: 10000;
                min-width: 250px;
                text-align: center;
            `;
            
            document.body.appendChild(messageDiv);
            
            // إزالة الرسالة بعد 3 ثواني
            setTimeout(() => {
                messageDiv.style.transition = 'opacity 0.5s ease';
                messageDiv.style.opacity = '0';
                setTimeout(() => {
                    if (messageDiv.parentNode) {
                        messageDiv.parentNode.removeChild(messageDiv);
                    }
                }, 500);
            }, 3000);
        }

        function showErrorMessage(message) {
            // إزالة أي رسائل سابقة
            const existingMessage = document.querySelector('.status-message');
            if (existingMessage) existingMessage.remove();
            
            // إنشاء رسالة جديدة
            const messageDiv = document.createElement('div');
            messageDiv.className = 'status-message error';
            messageDiv.innerHTML = `
                <div class="message-content">
                    <span style="font-size: 1.5rem; margin-left: 10px;">❌</span>
                    <p>${message}</p>
                </div>
            `;
            
            // إضافة التنسيقات
            messageDiv.style.cssText = `
                position: fixed;
                top: 20px;
                left: 50%;
                transform: translateX(-50%);
                background-color: #e74c3c;
                color: white;
                padding: 15px 25px;
                border-radius: 8px;
                box-shadow: 0 5px 15px rgba(0,0,0,0.2);
                z-index: 10000;
                min-width: 250px;
                text-align: center;
            `;
            
            document.body.appendChild(messageDiv);
            
            // إزالة الرسالة بعد 4 ثواني
            setTimeout(() => {
                messageDiv.style.transition = 'opacity 0.5s ease';
                messageDiv.style.opacity = '0';
                setTimeout(() => {
                    if (messageDiv.parentNode) {
                        messageDiv.parentNode.removeChild(messageDiv);
                    }
                }, 500);
            }, 4000);
        }

        // تهيئة التطبيق عند تحميل الصفحة
        document.addEventListener('DOMContentLoaded', function() {
            initializeCurrentDate();
            updateDocumentTitle();
            setupFontSelector();
            setupPdfGeneration();
            
            // رسالة ترحيب
            setTimeout(() => {
                showSuccessMessage('مرحباً! يمكنك الآن إنشاء ملف PDF باللغة العربية');
            }, 1000);
        });
    </script>
</body>
</html>