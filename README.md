<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>أداة إصدار التقارير والشواهد (مُحدَّث)</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap');
        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Cairo', sans-serif; }
        body { background: #f8fdf8; color: #083024; direction: rtl; line-height: 1.6; }

        /* تذييل الأدوات الثابت */
        .toolbar {
            background: linear-gradient(135deg, #066d4d 0%, #083024 100%);
            padding: 12px 15px;
            position: fixed;
            top: 0; left: 0; width: 100%;
            z-index: 1000;
            box-shadow: 0 4px 12px rgba(6, 109, 77, 0.3);
            display: flex; justify-content: center; gap: 15px; flex-wrap: wrap;
        }
        .toolbar button {
            background: #ffffff; color: #066d4d; border: none; padding: 12px 24px;
            border-radius: 50px; font-weight: 700; font-size: 15px; cursor: pointer;
            flex: 1; min-width: 160px; max-width: 200px; transition: all 0.3s;
            box-shadow: 0 3px 6px rgba(0,0,0,0.1);
        }
        .toolbar button:hover { background: #e8f2ee; transform: translateY(-2px); }

        /* قسم الإدخال الرئيسي */
        .input-container {
            max-width: 1000px; margin: 90px auto 30px; padding: 0 15px;
        }
        .form-card {
            background: #ffffff; border-radius: 20px; padding: 25px; margin-bottom: 20px;
            box-shadow: 0 6px 18px rgba(6, 109, 77, 0.1); border: 1px solid #e0f0ea;
        }

        /* شبكة الحقول */
        .form-grid {
            display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px; margin-bottom: 25px;
        }
        .input-group { margin-bottom: 5px; }
        .input-group label {
            display: block; font-size: 15px; font-weight: 700; margin-bottom: 8px;
            color: #066d4d;
        }
        .input-group input, .input-group select, .input-group textarea {
            width: 100%; padding: 14px 16px; border: 2px solid #d0e6de;
            border-radius: 12px; font-size: 15px; background: #f8fdfb;
            transition: border 0.3s;
        }
        .input-group input:focus, .input-group select:focus, .input-group textarea:focus {
            outline: none; border-color: #066d4d; background: #ffffff;
            box-shadow: 0 0 0 3px rgba(6, 109, 77, 0.1);
        }
        .input-group textarea { resize: vertical; height: 100px; line-height: 1.7; }

        /* زرار النص التلقائي */
        .auto-fill-btn {
            background: #e8f2ee; color: #066d4d; border: 2px dashed #9bc5b5;
            padding: 10px 15px; border-radius: 10px; font-weight: 700;
            font-size: 14px; cursor: pointer; margin-top: 8px; width: 100%;
            transition: all 0.3s;
        }
        .auto-fill-btn:hover { background: #d0e6de; border-style: solid; }

        /* رأس التقرير */
        .report-header {
            background: linear-gradient(135deg, #083024 0%, #066d4d 100%);
            height: 135px; position: relative; overflow: hidden;
            display: flex; align-items: center; justify-content: center;
            margin-top: 20px; border-radius: 0 0 20px 20px;
        }
        .report-header img { width: 180px; opacity: 0.95; }
        .header-date {
            position: absolute; left: 15px; bottom: 10px;
            color: #ffffff; font-weight: 600; font-size: 13px;
            text-align: center; line-height: 1.4;
        }
        .header-date .hijri { font-size: 14px; font-weight: 700; }
        .header-date .gregorian { font-size: 12px; opacity: 0.9; }
        .header-school { position: absolute; bottom: 10px; right: 15px;
                        color: #ffffff; font-weight: 600; font-size: 14px; }
        .header-edu { position: absolute; top: 10px; right: 15px;
                     color: #ffffff; font-weight: 700; font-size: 13px; }

        /* محتوى التقرير */
        .report-content { max-width: 830px; margin: auto; padding: 20px 15px; }
        .info-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
                    gap: 8px; margin-bottom: 15px; }
        .info-box {
            background: #e8f2ee; border-radius: 10px; padding: 10px; text-align: center;
            box-shadow: 0 3px 6px rgba(6,109,77,0.1); border: 1px solid rgba(6,109,77,0.2);
        }
        .info-title { font-size: 11px; color: #083024; font-weight: 700; }
        .info-value { font-size: 13px; color: #000000; font-weight: 700; margin-top: 3px; }

        .report-row { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
                     gap: 20px; margin-bottom: 20px; }
        .report-card {
            background: #ffffff; border-radius: 12px; padding: 15px; border: 1px solid #d0e6de;
            box-shadow: 0 4px 10px rgba(6,109,77,0.1); min-height: 140px;
        }
        .report-title {
            font-size: 16px; color: #083024; font-weight: 700; text-align: center;
            border-bottom: 2px solid #9bc5b5; padding-bottom: 8px; margin-bottom: 12px;
        }
        .report-text { font-size: 15px; line-height: 1.7; }

        /* التواقيع */
        .signature-section { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
                           gap: 30px; margin-top: 30px; }
        .signature-box { text-align: center; }
        .signature-name { font-size: 16px; color: #083024; font-weight: 700; margin-bottom: 5px; }
        .signature-line {
            width: 80%; height: 2px; background: #083024; margin: 10px auto;
            border-radius: 2px;
        }
        .signature-label { font-size: 14px; color: #066d4d; font-weight: 600; }

        /* جعل التصميم متجاوباً */
        @media (max-width: 768px) {
            .form-grid { grid-template-columns: 1fr; }
            .report-row { grid-template-columns: 1fr; }
            .toolbar button { min-width: 140px; padding: 10px 15px; }
            .input-container { margin-top: 120px; }
        }
        @media (max-width: 480px) {
            .toolbar { flex-direction: column; align-items: center; }
            .toolbar button { max-width: 100%; }
        }
    </style>
</head>
<body>
    <!-- شريط الأدوات -->
    <div class="toolbar">
        <button onclick="downloadPDF()">📥 تنزيل PDF</button>
        <button onclick="sharePDFWhatsApp()">📤 مشاركة واتساب</button>
        <button onclick="window.location.reload()">🔄 صفحة جديدة</button>
    </div>

    <!-- قسم إدخال البيانات -->
    <div class="input-container">
        <div class="form-card">
            <h2 style="color:#066d4d; text-align:center; margin-bottom:25px;">🔧 أدخل بيانات التقرير</h2>

            <div class="form-grid">
                <div class="input-group">
                    <label>إدارة التعليم</label>
                    <select id="education" oninput="updateReport()">
                        <option value="">اختر الإدارة</option>
                        <option>الإدارة العامة للتعليم بمنطقة مكة المكرمة</option>
                        <option>الإدارة العامة للتعليم بمحافظة جدة</option>
                    </select>
                </div>
                <div class="input-group">
                    <label>اسم التقرير</label>
                    <select id="reportType" oninput="handleReportType()">
                        <option value="">اختر نوع التقرير</option>
                        <option>تقرير نشاط إثرائي</option>
                        <option>تقرير زيارة ميدانية</option>
                        <option>تقرير ندوة تربوية</option>
                        <option>أخرى</option>
                    </select>
                    <input id="reportTypeInput" oninput="updateReport()" placeholder="اكتب اسم التقرير يدوياً" style="display:none; margin-top:8px;">
                </div>
            </div>

            <div class="form-grid">
                <div class="input-group"><label>الصف</label><input id="grade" oninput="updateReport()" placeholder="مثال: 5/3"></div>
                <div class="input-group">
                    <label>الفصل الدراسي</label>
                    <select id="term" oninput="updateReport()">
                        <option value="">اختر الفصل</option><option>الأول</option><option>الثاني</option>
                    </select>
                </div>
                <div class="input-group"><label>المادة</label><input id="subject" oninput="updateReport()" placeholder="مثال: لغتي – علوم – رياضيات"></div>
            </div>

            <div class="form-grid">
                <div class="input-group"><label>المستهدفون</label><input id="target" oninput="updateReport()" placeholder="مثال: جميع طلاب الصف"></div>
                <div class="input-group"><label>عدد الحضور</label><input id="count" oninput="updateReport()" placeholder="مثال: 25 طالب"></div>
                <div class="input-group"><label>مكان التنفيذ</label><input id="place" oninput="updateReport()" placeholder="مثال: داخل الصف – المختبر – قاعة مصادر التعلم"></div>
            </div>

            <div class="form-grid">
                <div class="input-group"><label>اسم المعلم</label><input id="teacher" oninput="updateReport()" placeholder="مثال: فهد الخالدي"></div>
                <div class="input-group"><label>اسم المدير</label><input id="principal" oninput="updateReport()" placeholder="مثال: نايف اللحياني"></div>
            </div>
        </div>

        <!-- الحقول النصية مع أزرار النص التلقائي -->
        <div class="form-card">
            <h3 style="color:#083024; border-right:4px solid #066d4d; padding-right:10px; margin-bottom:20px;">📝 محتوى التقرير</h3>

            <div class="input-group">
                <label>الهدف التربوي</label>
                <textarea id="goal" oninput="updateReport()"></textarea>
                <button class="auto-fill-btn" onclick="autoFill('goal')">اضغط لتغيير النص</button>
            </div>

            <div class="input-group">
                <label>نبذة مختصرة</label>
                <textarea id="summary" oninput="updateReport()"></textarea>
                <button class="auto-fill-btn" onclick="autoFill('summary')">اضغط لتغيير النص</button>
            </div>

            <div class="input-group">
                <label>إجراءات التنفيذ</label>
                <textarea id="steps" oninput="updateReport()"></textarea>
                <button class="auto-fill-btn" onclick="autoFill('steps')">اضغط لتغيير النص</button>
            </div>

            <div class="input-group">
                <label>الاستراتيجيات</label>
                <textarea id="strategies" oninput="updateReport()"></textarea>
                <button class="auto-fill-btn" onclick="autoFill('strategies')">اضغط لتغيير النص</button>
            </div>

            <div class="input-group">
                <label>نقاط القوة</label>
                <textarea id="strengths" oninput="updateReport()"></textarea>
                <button class="auto-fill-btn" onclick="autoFill('strengths')">اضغط لتغيير النص</button>
            </div>

            <div class="input-group">
                <label>نقاط التحسين</label>
                <textarea id="improve" oninput="updateReport()"></textarea>
                <button class="auto-fill-btn" onclick="autoFill('improve')">اضغط لتغيير النص</button>
            </div>

            <div class="input-group">
                <label>التوصيات</label>
                <textarea id="recomm" oninput="updateReport()"></textarea>
                <button class="auto-fill-btn" onclick="autoFill('recomm')">اضغط لتغيير النص</button>
            </div>
        </div>

        <!-- رفع الصور -->
        <div class="form-card">
            <h3 style="color:#083024; border-right:4px solid #066d4d; padding-right:10px; margin-bottom:15px;">🖼️ الصور التوثيقية</h3>
            <div style="display:grid; grid-template-columns:1fr 1fr; gap:15px;">
                <div><label>الصورة 1</label><input type="file" accept="image/*" onchange="loadImage(this,'imgBox1')" style="margin-top:5px;"></div>
                <div><label>الصورة 2</label><input type="file" accept="image/*" onchange="loadImage(this,'imgBox2')" style="margin-top:5px;"></div>
            </div>
        </div>
    </div>

    <!-- معاينة التقرير -->
    <div id="report-content">
        <div class="report-header">
            <img src="https://i.ibb.co/1fc5gB6v/9-C92-E57-B-23-FA-479-D-A024-1-D5-F871-B4-F8-D.png" alt="شعار">
            <div class="header-edu" id="educationBox"></div>
            <div class="header-school">مدرسة سعيد بن العاص</div>
            <div class="header-date">
                <div class="hijri" id="hDate"></div>
                <div class="gregorian" id="gDate"></div>
            </div>
        </div>

        <div class="report-content">
            <div class="info-grid">
                <div class="info-box"><div class="info-title">الفصل</div><div class="info-value" id="termBox"></div></div>
                <div class="info-box"><div class="info-title">الصف</div><div class="info-value" id="gradeBox"></div></div>
                <div class="info-box"><div class="info-title">المادة</div><div class="info-value" id="subjectBox"></div></div>
                <div class="info-box"><div class="info-title">التقرير</div><div class="info-value" id="reportTypeBox"></div></div>
            </div>

            <div class="info-grid">
                <div class="info-box"><div class="info-title">المستهدفون</div><div class="info-value" id="targetBox"></div></div>
                <div class="info-box"><div class="info-title">العدد</div><div class="info-value" id="countBox"></div></div>
                <div class="info-box"><div class="info-title">المكان</div><div class="info-value" id="placeBox"></div></div>
            </div>

            <div class="report-card">
                <div class="report-title">الهدف التربوي</div>
                <div class="report-text" id="goalBox"></div>
            </div>

            <div class="report-row">
                <div class="report-card"><div class="report-title">النبذة</div><div class="report-text" id="summaryBox"></div></div>
                <div class="report-card"><div class="report-title">إجراءات التنفيذ</div><div class="report-text" id="stepsBox"></div></div>
            </div>

            <div class="report-row">
                <div class="report-card"><div class="report-title">الاستراتيجيات</div><div class="report-text" id="strategiesBox"></div></div>
                <div class="report-card"><div class="report-title">نقاط القوة</div><div class="report-text" id="strengthsBox"></div></div>
            </div>

            <div class="report-row">
                <div class="report-card"><div class="report-title">نقاط التحسين</div><div class="report-text" id="improveBox"></div></div>
                <div class="report-card"><div class="report-title">التوصيات</div><div class="report-text" id="recommBox"></div></div>
            </div>

            <div style="display:grid; grid-template-columns:1fr 1fr; gap:15px; margin-top:25px;">
                <div style="border:2px dashed #9bc5b5; border-radius:12px; min-height:150px; display:flex; align-items:center; justify-content:center; background:#f8fdfb; padding:10px;" id="imgBox1">صورة توثيقية 1</div>
                <div style="border:2px dashed #9bc5b5; border-radius:12px; min-height:150px; display:flex; align-items:center; justify-content:center; background:#f8fdfb; padding:10px;" id="imgBox2">صورة توثيقية 2</div>
            </div>

            <div class="signature-section">
                <div class="signature-box">
                    <div class="signature-name" id="teacherBox"></div>
                    <div class="signature-line"></div>
                    <div class="signature-label">المعلم</div>
                </div>
                <div class="signature-box">
                    <div class="signature-name" id="principalBox"></div>
                    <div class="signature-line"></div>
                    <div class="signature-label">مدير المدرسة</div>
                </div>
            </div>

            <div style="text-align:center; padding:15px; margin-top:25px; background:#083024; color:#ffffff; border-radius:10px; font-size:13px;">
                وزارة التعليم – المملكة العربية السعودية
            </div>
        </div>
    </div>

    <script>
        // البيانات التلقائية (5 نصوص لكل حقل)
        const autoTexts = {
            goal: [
                "تنمية مهارات التفكير الناقد والإبداعي لدى الطلاب من خلال أنشطة تعليمية تفاعلية تحفز الاكتشاف وحل المشكلات.",
                "تعزيز القيم الإسلامية والهوية الوطنية في نفوس الطلاب عبر برامج وأنشطة تربوية هادفة ومنظمة.",
                "تحسين مستوى التحصيل الدراسي عبر أساليب تدريس مبتكرة تراعي الفروق الفردية وتنمي القدرات الذاتية.",
                "تطوير المهارات الحياتية والتعاونية لدى الطلاب لتمكينهم من الانخراط الإيجابي في المجتمع بثقة وكفاءة.",
                "تعميق فهم الطلاب للمواد الدراسية من خلال ربطها بالتطبيقات العملية والواقع المعاش مما يجعل التعليم أكثر فاعلية."
            ],
            summary: [
                "تم تنفيذ النشاط بنجاح داخل الصف الدراسي بمشاركة جميع الطلاب الذين أظهروا تفاعلاً لافتاً واستفادة واضحة من المحتوى المقدم.",
                "شهد النشاط تفاعلاً إيجابياً من الطلاب مع استخدام وسائل تعليمية محفزة ساهمت في تحقيق الأهداف التربوية المخطط لها بشكل كامل.",
                "أظهر الطلاب حماساً ملحوظاً خلال النشاط التطبيقي مما انعكس إيجاباً على فهمهم للمفاهيم الأساسية وتحسن أدائهم في المهام الموكلة.",
                "تميز النشاط بالتنظيم الجيد والتسلسل المنطقي للخطوات مما سهل استيعاب الطلاب وساهم في إنجازه ضمن الوقت المحدد بنجاح.",
                "حقق النشاط أهدافه بشكل ممتاز من خلال بيئة تعليمية جاذبة وتفاعل بناء بين المعلم والطلاب وبين الطلاب أنفسهم."
            ],
            steps: [
                "بدأ النشاط بشرح مفصل للأهداف ثم تقسيم الطلاب إلى مجموعات عمل تعاونية لمناقشة المهام وتنفيذها بشكل منظم.",
                "شمل التنفيذ عرضاً تقديمياً للمحتوى يليه تطبيق عملي ومن ثم تقييم مباشر لفهم الطلاب وتقديم تغذية راجعة فورية.",
                "تم تقديم المادة العلمية عبر وسائط متعددة ثم مناقشة جماعية مفتوحة وأخيراً عمل فردي لتقييم مستوى الاستيعاب لدى كل طالب.",
                "مر النشاط بثلاث مراحل: الإعداد النظري، والتطبيق العملي، ثم التقويم والمناقشة الختامية لتوثيق النتائج واستخلاص الدروس.",
                "بدأ النشاط بجلسة عصف ذهني ثم انتقل إلى ورشة عمل تطبيقية وأنتهى بتقييم ذاتي وجماعي للنتائج والمخرجات المتحققة."
            ],
            strategies: [
                "اعتمد النشاط على استراتيجية التعلم التعاوني والعمل في مجموعات لتعزيز مهارات التواصل والعمل الجماعي بين الطلاب.",
                "تم استخدام استراتيجيات متنوعة شملت العصف الذهني والتعلم القائم على المشاريع والتقييم التكويني لتحقيق نواتج تعلم متنوعة.",
                "ركزت الاستراتيجية على التعلم النشط القائم على الاكتشاف والتجربة مع دمج التقنية كأداة محفزة للتعلم والإبداع.",
                "جمعت الخطة بين الاستراتيجيات التقليدية والحديثة مثل المناقشة والحوار والمحاكاة والألعاب التعليمية لتنويع مصادر التعلم.",
                "استخدمت استراتيجية التدرج من السهل إلى الصعب مع تقديم الدعم الفردي للطلاب الذين يحتاجون مساعدة إضافية لضمان مشاركة الجميع."
            ],
            strengths: [
                "من أبرز نقاط القوة التفاعل الإيجابي والحماس الكبير من الطلاب والالتزام التام بتعليمات النشاط وتنفيذ المهام بدقة.",
                "تميز النشاط بالتنظيم الجيد والتحضير المسبق الشامل مما ساهم في سير العمل بسلاسة وتحقيق الأهداف في الوقت المحدد.",
                "ظهور مبادرات إبداعية من الطلاب وتفاعل مميز مع أدوات النشاط مما يعكس جودة التخطيط وملاءمة المحتوى لمستواهم.",
                "نجاح النشاط في تحقيق التكامل بين الجانب النظري والعملي وانعكاس ذلك بشكل واضح على تحسن أداء الطلاب وتفاعلهم.",
                "توفر البيئة التعليمية المناسبة والداعمة وتكامل أدوار المعلم والطلاب مما خلق جواً من التعلم الممتع والمفيد للجميع."
            ],
            improve: [
                "يحتاج النشاط إلى زيادة الوقت المخصص للجزء التطبيقي لتعميق الفائدة وإتاحة فرصة أكبر للممارسة والتطبيق العملي.",
                "من المهم توفير المزيد من المصادر والأدوات المساعدة للطلاب المتأخرين دراسياً لضمان مشاركتهم الفعالة وتحقيق الاستفادة القصوى.",
                "يجب تنويع أساليب التقويم المستخدمة لتشمل أدوات أكثر موضوعية تقيس مدى تحقق نواتج التعلم بدقة أكبر.",
                "تحتاج الفعالية إلى دمج أكبر للتقنية الحديثة وتطبيقاتها التفاعلية لجعل المحتوى أكثر جاذبية وملاءمة لعصر التكنولوجيا.",
                "ينبغي زيادة فترات الراحة أثناء النشاط الطويل للحفاظ على تركيز الطلاب وضمان استمرارية تفاعلهم بإيجابية حتى النهاية."
            ],
            recomm: [
                "التوسع في تنفيذ مثل هذه الأنشطة التفاعلية في مختلف المواد الدراسية لدورها الفعال في رفع مستوى التحصيل والاستيعاب.",
                "توفير دورات تدريبية للمعلمين حول استراتيجيات التعلم النشط ودمج التقنية في التعليم لتحسين مخرجات العملية التعليمية.",
                "تعزيز التعاون بين المدرسة والأسرة عبر أنشطة مشتركة لتحقيق التكامل في دعم الطالب تربوياً وتعليمياً.",
                "تخصيص ميزانية لتطوير الوسائل التعليمية وتجهيز القاعات بمواد وأدوات تفاعلية تدعم أنشطة التعلم الحديثة.",
                "إنشاء بنك للأفكار والأنشطة المميزة يمكن للمعلمين الاستفادة منه وتبادل الخبرات لتحسين الأداء وتطوير الممارسات التعليمية."
            ]
        };

        // متغيرات لتتبع النص الحالي لكل حقل
        const currentIndex = {
            goal: 0, summary: 0, steps: 0, strategies: 0,
            strengths: 0, improve: 0, recomm: 0
        };

        // تعبئة النصوص تلقائياً
        function autoFill(field) {
            currentIndex[field] = (currentIndex[field] + 1) % autoTexts[field].length;
            document.getElementById(field).value = autoTexts[field][currentIndex[field]];
            updateReport();
        }

        // تحديث معاينة التقرير
        function updateReport() {
            document.getElementById('educationBox').innerText = document.getElementById('education').value;
            document.getElementById('termBox').innerText = document.getElementById('term').value;
            document.getElementById('gradeBox').innerText = document.getElementById('grade').value;
            document.getElementById('subjectBox').innerText = document.getElementById('subject').value;
            document.getElementById('targetBox').innerText = document.getElementById('target').value;
            document.getElementById('countBox').innerText = document.getElementById('count').value;
            document.getElementById('placeBox').innerText = document.getElementById('place').value;
            document.getElementById('teacherBox').innerText = document.getElementById('teacher').value;
            document.getElementById('principalBox').innerText = document.getElementById('principal').value;

            const reportType = document.getElementById('reportType');
            const reportTypeInput = document.getElementById('reportTypeInput');
            document.getElementById('reportTypeBox').innerText = 
                (reportType.value === "أخرى") ? reportTypeInput.value : reportType.value;

            document.getElementById('goalBox').innerText = document.getElementById('goal').value;
            document.getElementById('summaryBox').innerText = document.getElementById('summary').value;
            document.getElementById('stepsBox').innerText = document.getElementById('steps').value;
            document.getElementById('strategiesBox').innerText = document.getElementById('strategies').value;
            document.getElementById('strengthsBox').innerText = document.getElementById('strengths').value;
            document.getElementById('improveBox').innerText = document.getElementById('improve').value;
            document.getElementById('recommBox').innerText = document.getElementById('recomm').value;
        }

        // التعامل مع نوع التقرير
        function handleReportType() {
            const reportType = document.getElementById('reportType');
            const reportTypeInput = document.getElementById('reportTypeInput');
            reportTypeInput.style.display = (reportType.value === "أخرى") ? "block" : "none";
            updateReport();
        }

        // تحميل الصور
        function loadImage(input, target) {
            const file = input.files[0];
            if (!file) return;
            const reader = new FileReader();
            reader.onload = function(e) {
                document.getElementById(target).innerHTML = `<img src="${e.target.result}" style="max-width:100%; max-height:100%; border-radius:8px;">`;
            };
            reader.readAsDataURL(file);
        }

        // التاريخ الهجري والميلادي
        async function loadDates() {
            const now = new Date();
            const gDate = `${now.getDate()}-${now.getMonth()+1}-${now.getFullYear()}`;
            document.getElementById('gDate').innerText = `${gDate} م`;

            try {
                const response = await fetch(`https://api.aladhan.com/v1/gToH?date=${now.getDate()}-${now.getMonth()+1}-${now.getFullYear()}`);
                const data = await response.json();
                if (data.data && data.data.hijri) {
                    const hijri = data.data.hijri;
                    document.getElementById('hDate').innerText = `${hijri.day} ${hijri.month.ar} ${hijri.year} هـ`;
                }
            } catch (error) {
                document.getElementById('hDate').innerText = "التاريخ الهجري غير متوفر";
            }
        }
        loadDates();

        // تنزيل PDF
        function downloadPDF() {
            html2pdf().set({
                margin: 0,
                filename: "تقرير_نشاط_تعليمي.pdf",
                image: { type: "jpeg", quality: 0.98 },
                html2canvas: { scale: 3, scrollY: 0, useCORS: true },
                jsPDF: { unit: "mm", format: "a4", orientation: "portrait" }
            }).from(document.getElementById("report-content")).save();
        }

        // مشاركة عبر واتساب
        async function sharePDFWhatsApp() {
            try {
                const blob = await html2pdf().from(document.getElementById("report-content")).set({
                    margin: 0, image: { type: "jpeg", quality: 0.98 },
                    html2canvas: { scale: 3, scrollY: 0, useCORS: true },
                    jsPDF: { unit: "mm", format: "a4", orientation: "portrait" }
                }).outputPdf("blob");
                
                const file = new File([blob], "تقرير_نشاط.pdf", { type: "application/pdf" });
                
                if (navigator.canShare && navigator.canShare({ files: [file] })) {
                    await navigator.share({
                        files: [file],
                        title: "تقرير نشاط تعليمي",
                        text: "تقرير النشاط التعليمي - مدرسة سعيد بن العاص"
                    });
                } else {
                    const url = URL.createObjectURL(blob);
                    window.open(`https://wa.me/?text=${encodeURIComponent("تقرير النشاط التعليمي: " + url)}`, "_blank");
                }
            } catch (error) {
                alert("عذراً، حدث خطأ أثناء المشاركة. يرجى المحاولة مرة أخرى.");
            }
        }
    </script>
</body>
</html>