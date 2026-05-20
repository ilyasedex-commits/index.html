# index.html<!DOCTYPE html><!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>khalifa 29M - منصة الصباغة والديكور الحديث</title>
    <style>
        /* إعدادات الخطوط والألوان العامة */
        :root {
            --primary-gold: #f39c12;
            --dark-bg: #111116;
            --card-glass: rgba(255, 255, 255, 0.06);
            --border-glass: rgba(255, 255, 255, 0.1);
        }

        body {
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
            background-size: 400% 400%;
            animation: gradientBG 15s ease infinite;
            color: #fff;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow-x: hidden;
        }

        /* أنيميشن متحرك للخلفية يعطي إيحاء ثلاثي الأبعاد */
        @keyframes gradientBG {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        .main-wrapper {
            width: 100%;
            max-width: 500px;
            padding: 20px;
            box-sizing: border-box;
        }

        /* أسلوب التصميم الزجاجي (Glassmorphism) */
        .glass-panel {
            background: var(--card-glass);
            backdrop-filter: blur(15px);
            -webkit-backdrop-filter: blur(15px);
            border: 1px solid var(--border-glass);
            border-radius: 24px;
            padding: 35px;
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.4);
            display: none; /* إخفاء الصفحات افتراضياً والتحكم بها عبر JS */
        }

        .glass-panel.active {
            display: block;
            animation: fadeIn 0.5s ease-in-out;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* الهيدر والشعار */
        .app-header {
            text-align: center;
            margin-bottom: 30px;
        }

        .app-header h1 {
            color: var(--primary-gold);
            font-size: 2.2rem;
            margin: 0 0 5px 0;
            text-shadow: 0 0 15px rgba(243, 156, 18, 0.3);
            letter-spacing: 1px;
        }

        .app-header p {
            color: #ccc;
            margin: 0;
            font-size: 0.95rem;
        }

        /* حقول الإدخال */
        .form-group {
            margin-bottom: 20px;
            text-align: right;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            color: #ddd;
            font-size: 0.9rem;
        }

        .form-group input {
            width: 100%;
            padding: 14px;
            background: rgba(0, 0, 0, 0.3);
            border: 1px solid var(--border-glass);
            border-radius: 12px;
            color: #fff;
            box-sizing: border-box;
            font-size: 1rem;
            transition: 0.3s;
            text-align: right;
        }

        .form-group input:focus {
            border-color: var(--primary-gold);
            outline: none;
            box-shadow: 0 0 10px rgba(243, 156, 18, 0.2);
        }

        /* الأزرار */
        .btn-prime {
            width: 100%;
            padding: 14px;
            background: linear-gradient(90deg, #f39c12, #d35400);
            border: none;
            border-radius: 12px;
            color: #fff;
            font-size: 1.1rem;
            font-weight: bold;
            cursor: pointer;
            transition: 0.3s;
            box-shadow: 0 5px 15px rgba(211, 84, 0, 0.3);
            text-decoration: none;
            display: block;
            text-align: center;
        }

        .btn-prime:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 20px rgba(211, 84, 0, 0.5);
        }

        /* شبكة عرض الخدمات */
        .services-grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 15px;
            margin-bottom: 25px;
        }

        .service-card {
            background: rgba(255, 255, 255, 0.03);
            border: 1px solid var(--border-glass);
            border-radius: 15px;
            padding: 15px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            cursor: pointer;
            transition: 0.3s;
        }

        .service-card:hover {
            background: rgba(255, 255, 255, 0.08);
            border-color: rgba(243, 156, 18, 0.5);
        }

        .service-card.selected {
            background: rgba(243, 156, 18, 0.15);
            border-color: var(--primary-gold);
            box-shadow: 0 0 15px rgba(243, 156, 18, 0.2);
        }

        .service-info h3 {
            margin: 0 0 5px 0;
            font-size: 1.1rem;
        }

        .service-info p {
            margin: 0;
            color: #aaa;
            font-size: 0.85rem;
        }

        .price-tag {
            color: var(--primary-gold);
            font-weight: bold;
            font-size: 1.05rem;
        }

        /* شاشة الفاتورة الإجمالية */
        .invoice-box {
            background: rgba(0, 0, 0, 0.2);
            border-radius: 12px;
            padding: 15px;
            margin-top: 20px;
            border-right: 4px solid var(--primary-gold);
        }

        .invoice-row {
            display: flex;
            justify-content: space-between;
            margin-bottom: 8px;
            font-size: 0.95rem;
        }

        .invoice-row.total {
            border-top: 1px solid var(--border-glass);
            padding-top: 10px;
            margin-top: 10px;
            font-weight: bold;
            font-size: 1.2rem;
            color: var(--primary-gold);
        }

        /* كارت معلومات الاتصال المستبدل بالبطاقة الذهبية */
        .contact-card {
            background: linear-gradient(135deg, #1d1d24, #2c3e50);
            border: 1px solid #f39c12;
            border-radius: 15px;
            padding: 25px;
            margin-bottom: 25px;
            text-align: center;
            box-shadow: 0 10px 25px rgba(0,0,0,0.3);
        }

        .phone-display {
            font-size: 1.8rem;
            color: var(--primary-gold);
            letter-spacing: 2px;
            margin: 15px 0;
            font-weight: bold;
        }
    </style>
</head>
<body>

    <div class="main-wrapper">

        <!-- 1. واجهة الدخول -->
        <div id="loginPage" class="glass-panel active">
            <div class="app-header">
                <h1>khalifa 29M</h1>
                <p>عالم الصباغة والديكور الحديث ثلاثي الأبعاد</p>
            </div>
            <form id="loginForm" onsubmit="handleLogin(event)">
                <div class="form-group">
                    <label>البريد الإلكتروني أو رقم الهاتف</label>
                    <input type="text" required placeholder="أدخل بياناتك هنا...">
                </div>
                <button type="submit" class="btn-prime">دخول إلى المنصة</button>
            </form>
        </div>

        <!-- 2. واجهة اختيار الخدمات والحجز -->
        <div id="servicesPage" class="glass-panel">
            <div class="app-header">
                <h1>خدماتنا الإبداعية</h1>
                <p>اختر الديكور المناسب وفضاء العمل</p>
            </div>
            
            <div class="services-grid">
                <div class="service-card" id="srv-sabli" onclick="selectService('srv-sabli', 'ديكور صابلي', 300)">
                    <div class="service-info">
                        <h3>ديكور صابلي (Sabli)</h3>
                        <p>مظهر رملي عصري جذاب</p>
                    </div>
                    <div class="price-tag">300 دج/م²</div>
                </div>

                <div class="service-card" id="srv-galaxy" onclick="selectService('srv-galaxy', 'ديكور ڨلاكسي', 250)">
                    <div class="service-info">
                        <h3>ديكور ڨلاكسي (Galaxy)</h3>
                        <p>لمعان وبريق النجوم الساحر</p>
                    </div>
                    <div class="price-tag">250 دج/م²</div>
                </div>

                <div class="service-card" id="srv-stucco" onclick="selectService('srv-stucco', 'ديكور ستيكو', 450)">
                    <div class="service-info">
                        <h3>ديكور ستيكو (Stucco)</h3>
                        <p>تأثير رخامي ملكي براق</p>
                    </div>
                    <div class="price-tag">450 دج/م²</div>
                </div>
            </div>

            <div class="form-group">
                <label>المساحة المراد صباغتها (بالمتر المربع م²)</label>
                <input type="number" id="surfaceInput" min="1" placeholder="مثال: 20" oninput="calculateInvoice()">
            </div>

            <div class="invoice-box">
                <div class="invoice-row">
                    <span>الخدمة المحددة:</span>
                    <span id="inv-service">لم يتم الاختيار</span>
                </div>
                <div class="invoice-row">
                    <span>المساحة الإجمالية:</span>
                    <span id="inv-area">0 م²</span>
                </div>
                <div class="invoice-row total">
                    <span>المبلغ الإجمالي:</span>
                    <span id="inv-total">0 دج</span>
                </div>
            </div>

            <button class="btn-prime" style="margin-top: 20px;" onclick="goToBooking()">تأكيد واختيار وسيلة الحجز</button>
        </div>

        <!-- 3. واجهة الحجز عبر الهاتف المستحدثة -->
        <div id="bookingPage" class="glass-panel">
            <div class="app-header">
                <h1>تأكيد الحجز المباشر</h1>
                <p>تواصل معنا لإتمام الاتفاق وتحديد الموعد</p>
            </div>

            <div class="contact-card">
                <div style="font-size: 1.1rem; color: #eee;">رقم هاتف صباغ الديكور التابع لنا:</div>
                <div class="phone-display">0797953827</div>
                <div style="font-size: 0.9rem; color: #aaa;">يمكنك الاتصال مباشرة أو إرسال تفاصيل المساحة لتأكيد انطلاق الورشة.</div>
            </div>

            <div class="form-group">
                <label>اسمك الكامل</label>
                <input type="text" id="clientName" placeholder="أدخل اسمك لتسجيل الحجز">
            </div>

            <div class="form-group">
                <label>رقم هاتفك الشخصي</label>
                <input type="tel" id="clientPhone" placeholder="0XXXXXXXXX">
            </div>

            <button class="btn-prime" onclick="processBooking()">إرسال الطلب وتأكيد الحجز</button>
            <a href="tel:0797953827" class="btn-prime" style="background: linear-gradient(90deg, #27ae60, #2ecc71); margin-top: 10px; box-shadow: 0 5px 15px rgba(46, 204, 113, 0.3);">إتصال هاتفي مباشر الآن</a>
        </div>

    </div>

    <script>
        // متغيرات تتبع حالة الحجز
        let selectedServiceId = '';
        let serviceName = '';
        let pricePerMeter = 0;
        let totalAmount = 0;

        // الانتقال بين الصفحات
        function switchPage(fromId, toId) {
            document.getElementById(fromId).classList.remove('active');
            document.getElementById(toId).classList.add('active');
        }

        // معالجة الدخول
        function handleLogin(event) {
            event.preventDefault();
            switchPage('loginPage', 'servicesPage');
        }

        // اختيار نوع الديكور
        function selectService(elementId, name, price) {
            if(selectedServiceId) {
                document.getElementById(selectedServiceId).classList.remove('selected');
            }
            
            selectedServiceId = elementId;
            document.getElementById(elementId).classList.add('selected');
            
            serviceName = name;
            pricePerMeter = price;
            
            calculateInvoice();
        }

        // حساب الفاتورة تلقائياً
        function calculateInvoice() {
            const area = document.getElementById('surfaceInput').value || 0;
            totalAmount = area * pricePerMeter;
            
            document.getElementById('inv-service').innerText = serviceName ? serviceName : 'لم يتم الاختيار';
            document.getElementById('inv-area').innerText = area + ' م²';
            document.getElementById('inv-total').innerText = totalAmount.toLocaleString() + ' دج';
        }

        // التوجيه لصفحة معلومات الحجز والهاتف
        function goToBooking() {
            if (!selectedServiceId) {
                alert('من فضلك، اختر نوع الديكور أولاً (صابلي، ڨلاكسي، أو ستيكو).');
                return;
            }
            if (totalAmount <= 0) {
                alert('من فضلك، أدخل مساحة صالحة بالمتر المربع لحساب السعر.');
                return;
            }
            switchPage('servicesPage', 'bookingPage');
        }

        // معالجة طلب الحجز وإظهار رسالة النجاح للمستخدم
        function processBooking() {
            const name = document.getElementById('clientName').value;
            const phone = document.getElementById('clientPhone').value;

            if(!name || !phone) {
                alert('الرجاء إدخال اسمك ورقم هاتفك لتسجيل الحجز في النظام بنجاح.');
                return;
            }

            alert(`شكراً لك ${name}!\nتم تسجيل طلب الحجز بنجاح لخدمة: ${serviceName}.\nالتكلفة التقديرية: ${totalAmount.toLocaleString()} دج.\n\nيرجى الاتصال بنا على الرقم 0797953827 أو سنقوم بالتواصل معك على رقمك (${phone}) خلال الساعات القادمة.`);
            
            // إعادة تصفير الحقول والتوجيه للرئيسية
            document.getElementById('clientName').value = '';
            document.getElementById('clientPhone').value = '';
            switchPage('bookingPage', 'servicesPage');
        }
    </script>
</body>
</html>

<html>

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title></title>
</head>

<body>
  
</body>

</html>
