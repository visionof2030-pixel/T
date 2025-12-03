<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<title>اختبار تجريبي مع اسم الطالب وفصله</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/crypto-js/4.1.1/crypto-js.min.js"></script>
<style>
body { font-family: Arial; padding: 20px; }
button { padding: 10px 15px; font-size: 16px; }
input, select { padding: 8px; font-size: 16px; margin-bottom: 10px; width: 100%; }
</style>
</head>

<body>
<h2>اختبار تجريبي (سؤالين فقط)</h2>

<!-- بيانات الطالب -->
<div>
<label>اسم الطالب:</label>
<input type="text" id="studentName" placeholder="أدخل اسمك هنا">

<label>الفصل:</label>
<input type="text" id="studentClass" placeholder="أدخل الفصل هنا">
</div>

<!-- الأسئلة -->
<div>
<p>1. من هو مخترع المصباح الكهربائي؟</p>
<label><input type="radio" name="q1" value="wrong"> نيكولا تسلا</label><br>
<label><input type="radio" name="q1" value="correct"> توماس إديسون</label><br>
<label><input type="radio" name="q1" value="wrong"> ألبرت أينشتاين</label><br>
<label><input type="radio" name="q1" value="wrong"> نيوتن</label>
</div>

<br>

<div>
<p>2. عاصمة اليابان هي:</p>
<label><input type="radio" name="q2" value="wrong"> أوساكا</label><br>
<label><input type="radio" name="q2" value="wrong"> كيوتو</label><br>
<label><input type="radio" name="q2" value="correct"> طوكيو</label><br>
<label><input type="radio" name="q2" value="wrong"> ناغويا</label>
</div>

<br><br>

<button onclick="sendResult()">إرسال النتيجة</button>

<script>
// ------------------------------
// الإعدادات
// ------------------------------
const SECRET = "TeacherFahad1406";
const TARGET = "966533527240"; // رقمك

function sendResult() {
    const studentName = document.getElementById("studentName").value.trim();
    const studentClass = document.getElementById("studentClass").value.trim();

    if (!studentName || !studentClass) {
        alert("الرجاء إدخال اسمك والفصل قبل الإرسال.");
        return;
    }

    let score = 0;
    let weaknesses = [];

    // سؤال 1
    let q1 = document.querySelector('input[name="q1"]:checked');
    if (q1) {
        if (q1.value === "correct") score++;
        else weaknesses.push("سؤال رقم 1 (المصباح الكهربائي)");
    } else {
        weaknesses.push("سؤال رقم 1 (لم يُجب عليه)");
    }

    // سؤال 2
    let q2 = document.querySelector('input[name="q2"]:checked');
    if (q2) {
        if (q2.value === "correct") score++;
        else weaknesses.push("سؤال رقم 2 (عاصمة اليابان)");
    } else {
        weaknesses.push("سؤال رقم 2 (لم يُجب عليه)");
    }

    // الملخص
    let summary =
`اسم الطالب: ${studentName}
الفصل: ${studentClass}
الدرجة النهائية: ${score} من 2
نقاط الضعف:
${weaknesses.length === 0 ? "لا يوجد" : weaknesses.join("\n")}
`;

    // التشفير AES
    let encrypted = CryptoJS.AES.encrypt(summary, SECRET).toString();

    // إنشاء رابط واتساب
    let url =
        "https://wa.me/" +
        TARGET +
        "?text=" +
        encodeURIComponent(encrypted);

    // تحويل المستخدم لواتساب
    window.location.href = url;
}
</script>

</body>
</html>
