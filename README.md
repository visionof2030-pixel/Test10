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
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            color: #333;
            line-height: 1.6;
            padding: 20px;
            min-height: 100vh;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: white;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #083024 0%, #0a3d2e 100%);
            color: white;
            padding: 30px;
            text-align: center;
            position: relative;
            overflow: hidden;
        }

        .header::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255,255,255,0.1) 1px, transparent 1px);
            background-size: 30px 30px;
            opacity: 0.1;
        }

        .header h1 {
            font-size: 32px;
            margin-bottom: 15px;
            position: relative;
            text-shadow: 0 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            opacity: 0.9;
            font-size: 18px;
            position: relative;
        }

        .form-container {
            padding: 30px;
            background: #fff;
        }

        .tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 30px;
            border-bottom: 3px solid #f0f0f0;
            padding-bottom: 10px;
            flex-wrap: wrap;
            justify-content: center;
        }

        .tab-btn {
            padding: 15px 30px;
            background: #f8f9fa;
            border: none;
            border-radius: 8px;
            font-family: 'Cairo', sans-serif;
            font-weight: 700;
            font-size: 16px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            min-width: 180px;
            position: relative;
            overflow: hidden;
        }

        .tab-btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, #083024 0%, #0a3d2e 100%);
            opacity: 0;
            transition: opacity 0.3s;
            z-index: 1;
        }

        .tab-btn span {
            position: relative;
            z-index: 2;
        }

        .tab-btn.active {
            background: #083024;
            color: white;
            box-shadow: 0 4px 15px rgba(8, 48, 36, 0.3);
            transform: translateY(-2px);
        }

        .tab-btn.active::before {
            opacity: 1;
        }

        .tab-btn:hover:not(.active) {
            background: #e9ecef;
            transform: translateY(-1px);
            box-shadow: 0 3px 10px rgba(0,0,0,0.15);
        }

        .tab-content {
            display: none;
            animation: fadeIn 0.5s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .tab-content.active {
            display: block;
        }

        .form-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
            gap: 25px;
            margin-bottom: 30px;
        }

        .form-group {
            margin-bottom: 25px;
        }

        .form-group label {
            display: block;
            margin-bottom: 10px;
            font-weight: 700;
            color: #083024;
            font-size: 16px;
            position: relative;
        }

        .form-group label.required::after {
            content: " *";
            color: #e74c3c;
            font-weight: bold;
        }

        .form-group input,
        .form-group textarea,
        .form-group select {
            width: 100%;
            padding: 14px 16px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-family: 'Cairo', sans-serif;
            font-size: 16px;
            transition: all 0.3s;
            background: #f8f9fa;
            color: #333;
        }

        .form-group input:focus,
        .form-group textarea:focus,
        .form-group select:focus {
            border-color: #083024;
            background: white;
            outline: none;
            box-shadow: 0 0 0 3px rgba(8, 48, 36, 0.1);
        }

        .form-group textarea {
            height: 140px;
            resize: vertical;
            line-height: 1.6;
        }

        .full-width {
            grid-column: 1 / -1;
        }

        .controls {
            display: flex;
            gap: 20px;
            justify-content: center;
            padding: 30px;
            background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
            border-top: 2px solid #dee2e6;
            flex-wrap: wrap;
        }

        .btn {
            padding: 16px 40px;
            border: none;
            border-radius: 8px;
            font-family: 'Cairo', sans-serif;
            font-size: 18px;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            min-width: 200px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            position: relative;
            overflow: hidden;
        }

        .btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(255,255,255,0.1);
            opacity: 0;
            transition: opacity 0.3s;
        }

        .btn:hover::before {
            opacity: 1;
        }

        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 20px rgba(0,0,0,0.15);
        }

        .btn:active {
            transform: translateY(-1px);
            box-shadow: 0 3px 10px rgba(0,0,0,0.1);
        }

        .btn-primary {
            background: linear-gradient(135deg, #083024 0%, #0a3d2e 100%);
            color: white;
        }

        .btn-primary:hover {
            background: linear-gradient(135deg, #0a3d2e 0%, #083024 100%);
        }

        .btn-secondary {
            background: linear-gradient(135deg, #6c757d 0%, #5a6268 100%);
            color: white;
        }

        .btn-secondary:hover {
            background: linear-gradient(135deg, #5a6268 0%, #6c757d 100%);
        }

        .btn-icon {
            font-size: 20px;
        }

        .preview-section {
            margin-top: 40px;
            padding: 25px;
            background: linear-gradient(135deg, #e3f2fd 0%, #bbdefb 100%);
            border-radius: 12px;
            border: 3px solid #083024;
            box-shadow: 0 5px 15px rgba(8, 48, 36, 0.1);
        }

        .preview-section h3 {
            color: #083024;
            margin-bottom: 20px;
            text-align: center;
            font-size: 22px;
            font-weight: 700;
            padding-bottom: 15px;
            border-bottom: 2px solid rgba(8, 48, 36, 0.2);
        }

        .preview-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
        }

        .preview-item {
            background: rgba(255,255,255,0.9);
            padding: 15px;
            border-radius: 8px;
            border-right: 4px solid #083024;
        }

        .preview-item strong {
            color: #083024;
            display: block;
            margin-bottom: 5px;
            font-size: 16px;
        }

        .preview-item span {
            color: #2c3e50;
            font-size: 15px;
            line-height: 1.5;
        }

        .hint {
            font-size: 14px;
            color: #7f8c8d;
            margin-top: 8px;
            display: block;
            font-weight: 400;
        }

        .image-preview-container {
            display: flex;
            gap: 20px;
            margin-top: 20px;
            flex-wrap: wrap;
        }

        .image-preview {
            flex: 1;
            min-width: 200px;
            background: #f8f9fa;
            border: 2px dashed #ddd;
            border-radius: 8px;
            padding: 15px;
            text-align: center;
        }

        .image-preview img {
            max-width: 100%;
            max-height: 150px;
            border-radius: 5px;
            margin-bottom: 10px;
        }

        .image-status {
            font-size: 14px;
            color: #666;
        }

        .progress-bar {
            height: 5px;
            background: #e0e0e0;
            border-radius: 3px;
            margin-top: 10px;
            overflow: hidden;
            display: none;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #083024 0%, #0a3d2e 100%);
            width: 0%;
            transition: width 0.3s ease;
        }

        .step-indicator {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin-bottom: 20px;
        }

        .step {
            width: 12px;
            height: 12px;
            border-radius: 50%;
            background: #ddd;
            transition: all 0.3s;
        }

        .step.active {
            background: #083024;
            transform: scale(1.2);
        }

        .counter {
            position: absolute;
            top: -8px;
            right: -8px;
            background: #e74c3c;
            color: white;
            font-size: 12px;
            padding: 2px 6px;
            border-radius: 10px;
            font-weight: bold;
            display: none;
        }

        .tab-btn.has-error .counter {
            display: block;
        }

        @media (max-width: 768px) {
            .container {
                margin: 10px;
            }
            
            .header {
                padding: 20px;
            }
            
            .header h1 {
                font-size: 24px;
            }
            
            .tab-btn {
                min-width: 140px;
                padding: 12px 20px;
                font-size: 14px;
            }
            
            .btn {
                min-width: 160px;
                padding: 14px 25px;
                font-size: 16px;
            }
            
            .form-grid {
                grid-template-columns: 1fr;
            }
            
            .controls {
                flex-direction: column;
                align-items: center;
            }
        }

        @media (max-width: 480px) {
            body {
                padding: 10px;
            }
            
            .header h1 {
                font-size: 20px;
            }
            
            .tab-btn {
                min-width: 100%;
            }
            
            .btn {
                width: 100%;
            }
        }

        .loading {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(255,255,255,0.9);
            z-index: 9999;
            justify-content: center;
            align-items: center;
            flex-direction: column;
        }

        .loading.active {
            display: flex;
        }

        .spinner {
            width: 50px;
            height: 50px;
            border: 5px solid #f3f3f3;
            border-top: 5px solid #083024;
            border-radius: 50%;
            animation: spin 1s linear infinite;
            margin-bottom: 20px;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .success-message {
            position: fixed;
            top: 20px;
            right: 20px;
            background: #2ecc71;
            color: white;
            padding: 15px 25px;
            border-radius: 8px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
            display: none;
            z-index: 1000;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from {
                transform: translateX(100%);
                opacity: 0;
            }
            to {
                transform: translateX(0);
                opacity: 1;
            }
        }
    </style>
</head>
<body>
    <!-- رسالة النجاح -->
    <div class="success-message" id="successMessage"></div>
    
    <!-- شاشة التحميل -->
    <div class="loading" id="loading">
        <div class="spinner"></div>
        <h3 style="color: #083024;">جاري إنشاء التقرير...</h3>
    </div>
    
    <div class="container">
        <div class="header">
            <h1>🖋️ أداة إنشاء التقارير التعليمية</h1>
            <p>أداة متكاملة لإنشاء تقارير الأنشطة الإثرائية بصورة احترافية</p>
        </div>

        <!-- مؤشر الخطوات -->
        <div class="step-indicator" id="stepIndicator">
            <div class="step active" data-step="1"></div>
            <div class="step" data-step="2"></div>
            <div class="step" data-step="3"></div>
            <div class="step" data-step="4"></div>
        </div>

        <div class="tabs">
            <button class="tab-btn active" onclick="showTab(1)" id="tabBtn1">
                <span>📋 المعلومات الأساسية</span>
                <div class="counter">0</div>
            </button>
            <button class="tab-btn" onclick="showTab(2)" id="tabBtn2">
                <span>📝 تفاصيل النشاط</span>
                <div class="counter">0</div>
            </button>
            <button class="tab-btn" onclick="showTab(3)" id="tabBtn3">
                <span>📊 التقييم والتحليل</span>
                <div class="counter">0</div>
            </button>
            <button class="tab-btn" onclick="showTab(4)" id="tabBtn4">
                <span>🖼️ الشواهد والمرفقات</span>
                <div class="counter">0</div>
            </button>
        </div>

        <div class="form-container">
            <form id="reportForm">
                <!-- Tab 1: المعلومات الأساسية -->
                <div class="tab-content active" id="tab1">
                    <div class="form-grid">
                        <div class="form-group">
                            <label class="required">اسم المدرسة</label>
                            <input type="text" id="schoolName" placeholder="أدخل اسم المدرسة" required>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">الإدارة التعليمية</label>
                            <input type="text" id="adminName" value="الإدارة العامة للتعليم بمنطقة الرياض" required>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">المادة الدراسية</label>
                            <input type="text" id="subject" placeholder="مثل: أحياء، رياضيات، فيزياء" required>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">الصف الدراسي</label>
                            <select id="grade" required>
                                <option value="">اختر الصف</option>
                                <option value="الأول الثانوي">الأول الثانوي</option>
                                <option value="الثاني الثانوي">الثاني الثانوي</option>
                                <option value="الثالث الثانوي" selected>الثالث الثانوي</option>
                                <option value="الأول المتوسط">الأول المتوسط</option>
                                <option value="الثاني المتوسط">الثاني المتوسط</option>
                                <option value="الثالث المتوسط">الثالث المتوسط</option>
                            </select>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">الفصل الدراسي</label>
                            <select id="semester" required>
                                <option value="الأول" selected>الفصل الأول</option>
                                <option value="الثاني">الفصل الثاني</option>
                                <option value="الصيفي">الفصل الصيفي</option>
                            </select>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">مكان التنفيذ</label>
                            <input type="text" id="location" placeholder="مثل: الفصل الدراسي، المعمل، المكتبة" required>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">عدد المشاركين</label>
                            <input type="number" id="number" placeholder="أدخل عدد الطلاب" min="1" max="50" required>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">المستهدفون</label>
                            <input type="text" id="target" placeholder="مثل: طلاب الصف، مجموعة مختارة" required>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">نوع التقرير</label>
                            <select id="reportType" required>
                                <option value="نشاط إثرائي" selected>نشاط إثرائي</option>
                                <option value="نشاط صفي">نشاط صفي</option>
                                <option value="نشاط لاصفي">نشاط لا صفي</option>
                                <option value="ورشة عمل">ورشة عمل</option>
                                <option value="رحلة تعليمية">رحلة تعليمية</option>
                                <option value="برنامج تدريبي">برنامج تدريبي</option>
                            </select>
                        </div>
                    </div>
                </div>

                <!-- Tab 2: تفاصيل النشاط -->
                <div class="tab-content" id="tab2">
                    <div class="form-grid">
                        <div class="form-group full-width">
                            <label class="required">الهدف التربوي</label>
                            <textarea id="objective" placeholder="اذكر الأهداف التربوية والتعليمية للنشاط..." required>شرح مفهوم أساسي في المنهج وتطبيقه عبر أنشطة تفاعلية تركز على التعلم النشط والعمل الجماعي وتنمية مهارات التفكير.</textarea>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">وصف مختصر للنشاط</label>
                            <textarea id="description" placeholder="قدم وصفاً مختصراً وشاملاً للنشاط..." required>تنفيذ درس نموذجي يركز على الفهم العميق والتطبيق العملي للمفاهيم باستخدام أساليب تعليمية حديثة.</textarea>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">إجراءات التنفيذ</label>
                            <textarea id="procedures" placeholder="صف خطوات تنفيذ النشاط بالتفصيل..." required>عرض المفهوم الجديد، مناقشة أمثلة توضيحية، أنشطة تطبيقية جماعية، حل تمارين فردية، تلخيص النقاط الرئيسية.</textarea>
                        </div>
                    </div>
                </div>

                <!-- Tab 3: التقييم والتحليل -->
                <div class="tab-content" id="tab3">
                    <div class="form-grid">
                        <div class="form-group">
                            <label class="required">النتائج المتحققة</label>
                            <textarea id="results" placeholder="ما هي النتائج التي تحققت من النشاط؟..." required>استيعاب غالبية الطلاب للمفهوم، مشاركة فعالة في الأنشطة، إنجاز التمارين وتحقيق أهداف الدرس.</textarea>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">نقاط القوة</label>
                            <textarea id="strengths" placeholder="اذكر نقاط القوة في التخطيط والتنفيذ..." required>وضوح الشرح، تنوع الأنشطة، إدارة الوقت بفاعلية، مراعاة الفروق الفردية بين الطلاب.</textarea>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">المحفزات والدافعية</label>
                            <textarea id="motivations" placeholder="ما هي العوامل التي ساهمت في تحفيز الطلاب؟..." required>تفاعل الطلاب الإيجابي، تحفيز روح التنافس بين المجموعات، استخدام وسائل تعليمية جذابة.</textarea>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">مواطن القصور</label>
                            <textarea id="weaknesses" placeholder="اذكر الجوانب التي تحتاج للتطوير..." required>نقص بعض الوسائل التعليمية، محدودية المساحة الصفية، ضعف مشاركة عدد محدود من الطلاب.</textarea>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">التحديات والصعوبات</label>
                            <textarea id="challenges" placeholder="ما هي التحديات التي واجهت التنفيذ؟..." required>تفاوت سرعة الاستيعاب بين الطلاب، قصر وقت الحصة، صعوبة بعض المفاهيم العلمية.</textarea>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">التوصيات والمقترحات</label>
                            <textarea id="recommendations" placeholder="ما هي توصياتك للتحسين والتطوير؟..." required>تكرار استخدام الأنشطة التفاعلية، تخصيص وقت كافٍ للمراجعة، استخدام وسائل بصرية وتقنية داعمة.</textarea>
                        </div>
                    </div>
                </div>

                <!-- Tab 4: الشواهد والمرفقات -->
                <div class="tab-content" id="tab4">
                    <div class="form-grid">
                        <div class="form-group">
                            <label>رابط الصورة الأولى</label>
                            <input type="text" id="image1" placeholder="https://example.com/image1.jpg" value="https://i.ibb.co/dwKFLM99/IMG-1941.png">
                            <span class="hint">انسخ رابط الصورة من أي خدمة استضافة صور</span>
                            <div class="progress-bar" id="progress1">
                                <div class="progress-fill"></div>
                            </div>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">وصف الصورة الأولى</label>
                            <textarea id="caption1" required>تنفيذ النشاط داخل الفصل الدراسي من خلال العمل التعاوني بين الطلاب، وتطبيق استراتيجيات التعلم النشط.</textarea>
                        </div>
                        
                        <div class="form-group">
                            <label>رابط الصورة الثانية</label>
                            <input type="text" id="image2" placeholder="https://example.com/image2.jpg" value="https://i.ibb.co/fY77kdRH/IMG-1942.png">
                            <span class="hint">يمكنك استخدام imgbb.com لرفع الصور مجاناً</span>
                            <div class="progress-bar" id="progress2">
                                <div class="progress-fill"></div>
                            </div>
                        </div>
                        
                        <div class="form-group">
                            <label class="required">وصف الصورة الثانية</label>
                            <textarea id="caption2" required>نماذج من أعمال الطلاب أثناء النشاط، توضح تنوع المهام بين الإبداع والتحدي وتنمية مهارات التفكير.</textarea>
                        </div>
                        
                        <div class="form-group full-width">
                            <label>ملاحظات إضافية (اختياري)</label>
                            <textarea id="notes" placeholder="أي ملاحظات أو معلومات إضافية تود إضافتها للتقرير..." rows="4"></textarea>
                        </div>
                    </div>
                    
                    <!-- معاينة الصور -->
                    <div class="image-preview-container">
                        <div class="image-preview" id="previewImage1">
                            <img src="https://i.ibb.co/dwKFLM99/IMG-1941.png" alt="معاينة الصورة الأولى" onerror="this.src='https://via.placeholder.com/400x300?text=صورة+غير+متاحة'">
                            <div class="image-status">الصورة الأولى جاهزة</div>
                        </div>
                        <div class="image-preview" id="previewImage2">
                            <img src="https://i.ibb.co/fY77kdRH/IMG-1942.png" alt="معاينة الصورة الثانية" onerror="this.src='https://via.placeholder.com/400x300?text=صورة+غير+متاحة'">
                            <div class="image-status">الصورة الثانية جاهزة</div>
                        </div>
                    </div>
                    
                    <!-- معاينة سريعة -->
                    <div class="preview-section">
                        <h3>🔍 معاينة سريعة للتقرير</h3>
                        <div class="preview-grid">
                            <div class="preview-item">
                                <strong>المدرسة:</strong>
                                <span id="previewSchool">مدرسة التجربة النموذجية</span>
                            </div>
                            <div class="preview-item">
                                <strong>المادة:</strong>
                                <span id="previewSubject">أحياء</span>
                            </div>
                            <div class="preview-item">
                                <strong>الصف:</strong>
                                <span id="previewGrade">الثالث الثانوي</span>
                            </div>
                            <div class="preview-item">
                                <strong>الهدف:</strong>
                                <span id="previewObjective">شرح مفهوم أساسي في المنهج...</span>
                            </div>
                        </div>
                    </div>
                </div>
            </form>
        </div>

        <div class="controls">
            <button type="button" class="btn btn-secondary" onclick="clearForm()">
                <span class="btn-icon">🗑️</span>
                <span>مسح النموذج</span>
            </button>
            <button type="button" class="btn btn-secondary" onclick="loadSampleData()">
                <span class="btn-icon">📋</span>
                <span>تحميل نموذج تجريبي</span>
            </button>
            <button type="button" class="btn btn-primary" onclick="generateReport()">
                <span class="btn-icon">🖨️</span>
                <span>إنشاء التقرير وطباعته</span>
            </button>
            <button type="button" class="btn btn-primary" onclick="previewReport()">
                <span class="btn-icon">👁️</span>
                <span>معاينة قبل الطباعة</span>
            </button>
        </div>
    </div>

    <script>
        // تهيئة المتغيرات
        let currentTab = 1;
        let errorCounts = [0, 0, 0, 0];
        
        // نظام التبويب
        function showTab(tabNumber) {
            // تحديث التبويب الحالي
            currentTab = tabNumber;
            
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
            document.getElementById(`tabBtn${tabNumber}`).classList.add('active');
            
            // تحديث مؤشر الخطوات
            document.querySelectorAll('.step').forEach(step => {
                step.classList.remove('active');
                if (parseInt(step.dataset.step) <= tabNumber) {
                    step.classList.add('active');
                }
            });
            
            // تحديث المعاينة السريعة
            updatePreview();
        }
        
        // الانتقال للتبويب التالي
        function nextTab() {
            if (validateTab(currentTab)) {
                if (currentTab < 4) {
                    showTab(currentTab + 1);
                }
            }
        }
        
        // الانتقال للتبويب السابق
        function prevTab() {
            if (currentTab > 1) {
                showTab(currentTab - 1);
            }
        }
        
        // التحقق من صحة بيانات التبويب
        function validateTab(tabNumber) {
            let isValid = true;
            let errorCount = 0;
            
            // الحصول على جميع الحقول المطلوبة في التبويب الحالي
            const requiredFields = document.querySelectorAll(`#tab${tabNumber} [required]`);
            
            requiredFields.forEach(field => {
                if (!field.value.trim()) {
                    field.style.borderColor = '#e74c3c';
                    field.style.boxShadow = '0 0 0 3px rgba(231, 76, 60, 0.1)';
                    isValid = false;
                    errorCount++;
                } else {
                    field.style.borderColor = '#e0e0e0';
                    field.style.boxShadow = 'none';
                }
            });
            
            // تحديث عداد الأخطاء
            errorCounts[tabNumber - 1] = errorCount;
            updateErrorCounters();
            
            return isValid;
        }
        
        // تحديث عدادات الأخطاء
        function updateErrorCounters() {
            for (let i = 0; i < 4; i++) {
                const counter = document.querySelector(`#tabBtn${i + 1} .counter`);
                if (errorCounts[i] > 0) {
                    counter.textContent = errorCounts[i];
                    counter.style.display = 'block';
                    document.querySelector(`#tabBtn${i + 1}`).classList.add('has-error');
                } else {
                    counter.style.display = 'none';
                    document.querySelector(`#tabBtn${i + 1}`).classList.remove('has-error');
                }
            }
        }
        
        // تحديث المعاينة السريعة
        function updatePreview() {
            document.getElementById('previewSchool').textContent = 
                document.getElementById('schoolName').value || 'مدرسة التجربة النموذجية';
            document.getElementById('previewSubject').textContent = 
                document.getElementById('subject').value || 'أحياء';
            document.getElementById('previewGrade').textContent = 
                document.getElementById('grade').value || 'الثالث الثانوي';
            
            const objective = document.getElementById('objective').value || 
                'شرح مفهوم أساسي في المنهج وتطبيقه عبر أنشطة تفاعلية تركز على التعلم النشط والعمل الجماعي وتنمية مهارات التفكير.';
            document.getElementById('previewObjective').textContent = 
                objective.length > 80 ? objective.substring(0, 80) + '...' : objective;
            
            // تحديث معاينة الصور
            updateImagePreviews();
            
            // التحقق من الحقول المطلوبة
            validateTab(currentTab);
        }
        
        // تحديث معاينة الصور
        function updateImagePreviews() {
            const image1 = document.getElementById('image1').value;
            const image2 = document.getElementById('image2').value;
            
            if (image1) {
                const img1 = document.querySelector('#previewImage1 img');
                img1.src = image1;
                img1.onerror = function() {
                    this.src = 'https://via.placeholder.com/400x300?text=صورة+غير+متاحة';
                };
            }
            
            if (image2) {
                const img2 = document.querySelector('#previewImage2 img');
                img2.src = image2;
                img2.onerror = function() {
                    this.src = 'https://via.placeholder.com/400x300?text=صورة+غير+متاحة';
                };
            }
        }
        
        // التحقق من صحة الروابط
        function validateImage(url) {
            return new Promise((resolve) => {
                if (!url) {
                    resolve(false);
                    return;
                }
                
                const img = new Image();
                img.onload = () => resolve(true);
                img.onerror = () => resolve(false);
                img.src = url;
            });
        }
        
        // مسح النموذج
        function clearForm() {
            if (confirm('هل أنت متأكد من رغبتك في مسح جميع البيانات؟ سيتم فقدان جميع المعلومات المدخلة.')) {
                document.getElementById('reportForm').reset();
                
                // إعادة تعيين القيم الافتراضية
                document.getElementById('adminName').value = 'الإدارة العامة للتعليم بمنطقة الرياض';
                document.getElementById('grade').value = 'الثالث الثانوي';
                document.getElementById('semester').value = 'الأول';
                document.getElementById('reportType').value = 'نشاط إثرائي';
                
                // إعادة تعيين النصوص
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
                
                // إعادة تعيين عدادات الأخطاء
                errorCounts = [0, 0, 0, 0];
                updateErrorCounters();
                
                // تحديث المعاينة
                updatePreview();
                
                // العودة للتبويب الأول
                showTab(1);
                
                showSuccess('تم مسح النموذج بنجاح');
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
            document.getElementById('notes').value = 'تم تنفيذ النشاط بنجاح وتحقيق جميع الأهداف المخطط لها.';
            
            // التحقق من جميع التبويبات
            for (let i = 1; i <= 4; i++) {
                validateTab(i);
            }
            
            updatePreview();
            showSuccess('تم تحميل النموذج التجريبي بنجاح');
        }
        
        // معاينة التقرير
        function previewReport() {
            if (!validateAllTabs()) {
                showTab(getFirstErrorTab());
                alert('يرجى تصحيح الأخطاء قبل معاينة التقرير');
                return;
            }
            
            generateReport(false);
        }
        
        // الوظيفة الرئيسية: إنشاء التقرير
        function generateReport(autoPrint = true) {
            // التحقق من جميع التبويبات
            if (!validateAllTabs()) {
                showTab(getFirstErrorTab());
                alert('يرجى ملء جميع الحقول المطلوبة (المحددة بنجمة) قبل إنشاء التقرير');
                return;
            }
            
            // عرض شاشة التحميل
            document.getElementById('loading').classList.add('active');
            
            // جمع البيانات
            const data = collectFormData();
            
            // إنشاء التقرير بعد تأخير بسيط
            setTimeout(() => {
                createReportPage(data, autoPrint);
                document.getElementById('loading').classList.remove('active');
                showSuccess('تم إنشاء التقرير بنجاح!');
            }, 1500);
        }
        
        // جمع بيانات النموذج
        function collectFormData() {
            return {
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
                notes: document.getElementById('notes').value,
                date: new Date().toLocaleDateString('ar-SA')
            };
        }
        
        // التحقق من جميع التبويبات
        function validateAllTabs() {
            let allValid = true;
            for (let i = 1; i <= 4; i++) {
                if (!validateTab(i)) {
                    allValid = false;
                }
            }
            return allValid;
        }
        
        // الحصول على أول تبويب يحتوي على أخطاء
        function getFirstErrorTab() {
            for (let i = 0; i < 4; i++) {
                if (errorCounts[i] > 0) {
                    return i + 1;
                }
            }
            return 1;
        }
        
        // إنشاء صفحة التقرير
        function createReportPage(data, autoPrint) {
            const reportWindow = window.open('', '_blank');
            
            reportWindow.document.write(`
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<title>تقرير ${data.reportType} - ${data.subject}</title>
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap" rel="stylesheet">
<style>
${getReportStyles()}
</style>
</head>
<body>

<div class="controls">
  <button class="print-btn" onclick="window.print()">🖨️ طباعة التقرير</button>
  <button class="close-btn" onclick="window.close()">✖️ إغلاق</button>
</div>

<div class="header">
  <div class="admin-name">${data.adminName}</div>
  <div class="school-name">${data.schoolName}</div>
  <div class="hijri-date" id="hijriDate">${data.date}</div>
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
    <div class="box"><strong>نوع التقرير</strong><br>${data.reportType}</div>
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
        <div class="evidence-caption">${data.caption1}</div>
      </div>
      <div class="evidence-box">
        <img src="${data.image2}" onerror="this.src='https://via.placeholder.com/400x300?text=صورة+غير+متاحة'">
        <div class="evidence-caption">${data.caption2}</div>
      </div>
    </div>
  </div>
</div>

<script>
// طباعة تلقائية
window.onload = function() {
  setTimeout(() => {
    ${autoPrint ? "document.querySelector('.print-btn').click();" : ""}
  }, 1000);
};
</script>

</body>
</html>
            `);
            
            reportWindow.document.close();
        }
        
        // الحصول على أنماط التقرير
        function getReportStyles() {
            return `
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

.top-grid{
  display:grid;
  grid-template-columns:repeat(3,1fr);
  gap:8px;
  margin-bottom:8px;
}
.top-grid.second{
  grid-template-columns:repeat(4,1fr);
}

.objective{
  background:#eef6ea;
  border:2px solid #6fa37a;
  text-align:center;
  font-size:13px;
  margin:8px 0;
  padding:12px;
}

.main-grid{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:8px;
}

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

.controls {
  position: fixed;
  top: 20px;
  left: 20px;
  display: flex;
  gap: 10px;
  z-index: 1000;
}

.print-btn, .close-btn {
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

.print-btn:hover, .close-btn:hover {
  background: #0a3d2e;
}

.notes-box {
  margin-top: 10px;
  padding: 10px;
  background: #f8f9fa;
  border: 1px dashed #6c757d;
  border-radius: 5px;
  font-size: 11px;
}

@media print {
  .controls {
    display: none;
  }
  
  body {
    width: 100%;
    height: auto;
  }
}
            `;
        }
        
        // عرض رسالة نجاح
        function showSuccess(message) {
            const successMessage = document.getElementById('successMessage');
            successMessage.textContent = message;
            successMessage.style.display = 'block';
            
            setTimeout(() => {
                successMessage.style.display = 'none';
            }, 3000);
        }
        
        // إضافة مستمعين للأحداث
        document.addEventListener('DOMContentLoaded', function() {
            // تحديث المعاينة عند تغيير الحقول
            document.querySelectorAll('input, textarea, select').forEach(element => {
                element.addEventListener('input', updatePreview);
                element.addEventListener('change', updatePreview);
            });
            
            // تحديث معاينة الصور عند تغيير الروابط
            document.getElementById('image1').addEventListener('input', updateImagePreviews);
            document.getElementById('image2').addEventListener('input', updateImagePreviews);
            
            // التحقق من الحقول عند الخروج منها
            document.querySelectorAll('[required]').forEach(field => {
                field.addEventListener('blur', function() {
                    validateTab(currentTab);
                });
            });
            
            // تهيئة المعاينة
            updatePreview();
            
            // إضافة اختصارات لوحة المفاتيح
            document.addEventListener('keydown', function(e) {
                // Ctrl + Enter لإنشاء التقرير
                if (e.ctrlKey && e.key === 'Enter') {
                    e.preventDefault();
                    generateReport();
                }
                
                // Ctrl + S لتحميل النموذج التجريبي
                if (e.ctrlKey && e.key === 's') {
                    e.preventDefault();
                    loadSampleData();
                }
                
                // Ctrl + R لمسح النموذج
                if (e.ctrlKey && e.key === 'r') {
                    e.preventDefault();
                    clearForm();
                }
                
                // مفاتيح الأسهم للتنقل بين التبويبات
                if (e.key === 'ArrowRight') {
                    e.preventDefault();
                    nextTab();
                }
                if (e.key === 'ArrowLeft') {
                    e.preventDefault();
                    prevTab();
                }
            });
            
            // تحميل النموذج التجريبي تلقائياً لأول مرة
            setTimeout(() => {
                if (!localStorage.getItem('sampleLoaded')) {
                    loadSampleData();
                    localStorage.setItem('sampleLoaded', 'true');
                }
            }, 1000);
        });
        
        // التنقل بين الحقول باستخدام Tab
        document.addEventListener('keydown', function(e) {
            if (e.key === 'Tab') {
                setTimeout(() => {
                    const activeElement = document.activeElement;
                    if (activeElement && activeElement.tagName === 'INPUT') {
                        validateTab(currentTab);
                    }
                }, 10);
            }
        });
    </script>
</body>
</html>