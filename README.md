<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>إنشاء تقرير تفعيل حصص النشاط</title>
</head>

<body>

<div class="panel">

<h2>بيانات التقرير</h2>

<div class="field">
<label>الإدارة</label>
<select id="admin">
<option>الإدارة العامة للتعليم بمنطقة مكة المكرمة – مكة المكرمة</option>
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
<input id="grade">
</div>

<div class="field">
<label>المادة</label>
<input id="subject">
</div>

<div class="field">
<label>نوع التقرير</label>
<select id="type">
<option>تقرير تفعيل حصص النشاط</option>
</select>
</div>

<div class="field">
<label>المستهدفون</label>
<input id="target">
</div>

<div class="field">
<label>العدد</label>
<input id="count" type="number">
</div>

<div class="field">
<label>مكان التنفيذ</label>
<input id="place">
</div>

<div class="field">
<label>اسم المعلم</label>
<input id="teacher" value="فهد الخالدي">
</div>

<div class="field">
<label>اسم مدير المدرسة</label>
<input id="manager">
</div>

<div id="dynFields"></div>

<div class="field">
<label>صورة 1</label>
<input type="file" id="img1" accept="image/*">
</div>

<div class="field">
<label>صورة 2</label>
<input type="file" id="img2" accept="image/*">
</div>

<button onclick="createReport()">إنشاء التقرير</button>

</div>

</body>
</html>