<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>اختبار + ملخص مشفّر</title>

<!-- مكتبة التشفير AES -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/crypto-js/4.1.1/crypto-js.min.js"></script>

<style>
body { font-family: Arial; direction: rtl; padding: 20px; }
button { padding: 10px 20px; font-size: 18px; margin-top: 20px; }
#summaryBox { display:none; margin-top:20px; background:#f7f7f7; padding:15px; }
</style>
</head>
<body>

<h3>اختبار تجريبي</h3>

<form id="quizForm">
  <!-- سؤال 1 -->
  <p><b>1- ما عاصمة السعودية؟</b></p>
  <label><input type="radio" name="q1" value="1"> الرياض</label><br>
  <label><input type="radio" name="q1" value="0"> جدة</label><br>
  <label><input type="radio" name="q1" value="0"> الدمام</label><br><br>

  <!-- سؤال 2 -->
  <p><b>2- كم ناتج 3 × 4 ؟</b></p>
  <label><input type="radio" name="q2" value="1"> 12</label><br>
  <label><input type="radio" name="q2" value="0"> 10</label><br>
  <label><input type="radio" name="q2" value="0"> 15</label><br><br>

  <button type="button" onclick="finishExam()">إظهار الملخص</button>
</form>

<div id="summaryBox">
  <h3>الملخص النهائي</h3>
  <pre id="summaryText"></pre>
  <button onclick="sendWhatsApp()">إرسال النتيجة المشفّرة للواتساب</button>
</div>

<script>
let encryptedMessage = "";

function finishExam() {

  let correct = 0;
  let wrongPoints = [];

  const form = document.forms["quizForm"];

  // السؤال الأول
  if (form.q1.value === "1") correct++;
  else wrongPoints.push("س1: الإجابة الصحيحة هي (الرياض)");

  // السؤال الثاني
  if (form.q2.value === "1") correct++;
  else wrongPoints.push("س2: الإجابة الصحيحة هي (12)");

  // ====== الملخص الحقيقي ======
  const realSummary = 
`الدرجة النهائية: ${correct} من 2

نقاط الضعف:
${wrongPoints.length === 0 ? "لا يوجد أخطاء" : wrongPoints.join("\n")}
`;

  // عرض الملخص للطالب
  document.getElementById("summaryText").innerText = realSummary;
  document.getElementById("summaryBox").style.display = "block";

  // ====== تشفير AES ======
  const secretKey = "FAHAD-2025"; // ← غيّرها إذا تبي
  encryptedMessage = CryptoJS.AES.encrypt(realSummary, secretKey).toString();
}

function sendWhatsApp() {
  const teacher = "966533527240"; // ← رقمك جاهز
  const url = "https://wa.me/" + teacher + "?text=" + encodeURIComponent(encryptedMessage);
  window.location.href = url;
}
</script>

</body>
</html>
