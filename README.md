<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>أحسب عمرك لكأس العالم لعام 2034</title>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600&display=swap" rel="stylesheet">
    <style>
        body {
            text-align: center;
            font-family: 'Cairo', Arial, sans-serif;
            direction: rtl;
            background: linear-gradient(to bottom right, #0f2027, #203a43, #2c5364);
            margin: 0;
            padding: 0;
            color: white;
        }

        h1 {
            font-size: 32px;
            color: black;
            font-weight: 600;
            margin-top: 40px;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        p {
            font-size: 16px;
            margin-top: 10px;
            color: black;
        }

        select, button {
            padding: 12px;
            margin: 10px 0;
            font-size: 16px;
            border-radius: 10px;
            border: 1px solid #ddd;
            width: 100%;
            max-width: 300px;
            background-color: #ffffff;
            transition: transform 0.3s ease-in-out;
            font-weight: bold;
        }

        select:focus, button:focus {
            outline: none;
            border-color: #3498db;
            box-shadow: 0 0 8px rgba(52, 152, 219, 0.8);
        }

        button {
            background-color: #3498db;
            color: white;
            border: none;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }

        button:hover {
            background-color: #2980b9;
            transform: scale(1.05);
        }

        .container {
            background: rgba(255, 255, 255, 0.9);
            padding: 30px;
            margin: 50px auto;
            width: 90%;
            max-width: 400px;
            box-shadow: 0 6px 30px rgba(0, 0, 0, 0.2);
            border-radius: 15px;
            text-align: center;
        }

        #introText {
            font-size: 22px;
            font-weight: bold;
            color: #333;
            margin-top: 20px;
            letter-spacing: 1px;
            margin-bottom: 30px;
        }

        #result, #ageInWorldCup {
            margin-top: 20px;
            font-size: 20px;
            font-weight: 600;
            color: #333;
            white-space: pre-wrap;
            line-height: 1.6;
        }

        select:hover, button:hover {
            background-color: #ecf0f1;
        }

        @media (max-width: 600px) {
            h1 {
                font-size: 28px;
            }
            select, button {
                width: 100%;
                font-size: 16px;
                padding: 12px;
                max-width: 100%;
            }
            #introText {
                font-size: 18px;
                margin-bottom: 20px;
            }
            #result, #ageInWorldCup {
                font-size: 18px;
            }
        }

        @media (max-width: 400px) {
            .container {
                padding: 20px;
                margin: 30px auto;
            }
        }

        /* رسالة تنبيه للأجهزة غير الهاتفية */
        @media (min-width: 601px) {
            #mobileWarning {
                display: block;
                position: fixed;
                bottom: 0;
                left: 0;
                width: 100%;
                background-color: #e74c3c;
                color: white;
                font-size: 18px;
                padding: 10px;
                text-align: center;
                font-weight: bold;
            }
        }

        /* إخفاء الرسالة على الأجهزة المحمولة */
        @media (max-width: 600px) {
            #mobileWarning {
                display: none;
            }
        }
    </style>
</head>
<body>

    <div class="container">
        <div id="introText">
            عمرك في كأس العالم لعام 2034
        </div>

        <h1>حساب العمر</h1>
        <p>اختر تاريخ ميلادك:</p>

        <select id="year" onchange="updateDays()">
            <option value="">السنة</option>
        </select>
        <select id="month" onchange="updateDays()">
            <option value="">الشهر</option>
        </select>
        <select id="day">
            <option value="">اليوم</option>
        </select>

        <br>
        <button onclick="calculateAge()">احسب العمر</button>

        <h2 id="result"></h2>
        <h3 id="ageInWorldCup"></h3>
    </div>

    <!-- رسالة التنبيه لغير الهواتف -->
    <div id="mobileWarning">
        هذا الموقع يعمل فقط على الهواتف المحمولة.
    </div>

    <script>
        // الحصول على العناصر
        const daySelect = document.getElementById("day");
        const monthSelect = document.getElementById("month");
        const yearSelect = document.getElementById("year");
        const ageInWorldCupElement = document.getElementById("ageInWorldCup");

        // تعبئة قائمة الأشهر
        function populateMonths() {
            const months = ["يناير", "فبراير", "مارس", "أبريل", "مايو", "يونيو", "يوليو", "أغسطس", "سبتمبر", "أكتوبر", "نوفمبر", "ديسمبر"];
            for (let i = 0; i < months.length; i++) {
                const option = document.createElement("option");
                option.value = i + 1;
                option.textContent = months[i];
                monthSelect.appendChild(option);
            }
        }

        // تعبئة قائمة السنوات
        function populateYears() {
            const currentYear = new Date().getFullYear();
            for (let i = 1900; i <= currentYear; i++) {
                const option = document.createElement("option");
                option.value = i;
                option.textContent = i;
                yearSelect.appendChild(option);
            }
        }

        // تحديث الأيام بناءً على الشهر والسنة المختارين
        function updateDays() {
            const month = parseInt(monthSelect.value);
            const year = parseInt(yearSelect.value);

            // التأكد من اختيار شهر وسنة
            if (!month || !year) return;

            // حساب عدد الأيام في الشهر
            const daysInMonth = new Date(year, month, 0).getDate();

            // إعادة تعيين قائمة الأيام
            daySelect.innerHTML = '<option value="">اليوم</option>';
            for (let i = 1; i <= daysInMonth; i++) {
                const option = document.createElement("option");
                option.value = i;
                option.textContent = i;
                daySelect.appendChild(option);
            }
        }

        // تعبئة القوائم عند تحميل الصفحة
        window.onload = function() {
            populateMonths();
            populateYears();
            updateDays();  // إضافة هذا السطر لتحديث الأيام عند تحميل الصفحة
        };

        // حساب العمر
        function calculateAge() {
            const day = parseInt(daySelect.value);
            const month = parseInt(monthSelect.value);
            const year = parseInt(yearSelect.value);

            // التحقق من صحة الإدخال
            if (!day || !month || !year) {
                document.getElementById("result").innerText = "يرجى اختيار تاريخ الميلاد بالكامل.";
                return;
            }

            const birthdate = new Date(year, month - 1, day); // الشهر يبدأ من 0 في JavaScript
            const currentYear = new Date().getFullYear();
            const worldCupYear = 2034;

            // حساب العمر الحالي
            const currentAge = currentYear - birthdate.getFullYear();

            // حساب العمر في كأس العالم
            const ageInWorldCup = worldCupYear - birthdate.getFullYear();

            // عرض النتيجة بشكل مرتب في سطر واحد
            document.getElementById("result").innerText = `عمرك الآن: ${currentAge} سنة`;

            // عرض العمر في كأس العالم 2034
            ageInWorldCupElement.innerText = `عمرك في كأس العالم لعام ${worldCupYear}: ${ageInWorldCup} سنة`;
        }
    </script>

</body>
</html>
