# Vua-decor
Chuyên các sản phẩm về decor:  Led Neon, Chữ nổi, Bảng Led, Hộp đèn, Nội thất CNC....
<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>VUA DECOR</title>
    <!-- Thêm Manifest và Theme Color cho PWA -->
    <link rel="manifest" href="manifest.json">
    <meta name="theme-color" content="#ff4757">
    <link rel="apple-touch-icon" href="https://placehold.co/192x192/ff4757/ffffff?text=VUA">

    <!-- Thư viện icon -->
    <script src="https://unpkg.com/@phosphor-icons/web"></script>
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-color: #ff4757; /* Màu đỏ thương hiệu */
            --background-color: #f0f2f5;
            --card-background: #ffffff;
            --text-color: #2f3542;
            --secondary-text-color: #57606f;
            --border-color: #dee2e6;
            --success-color: #2ed573;
            --pending-color: #ffa502;
        }

        body {
            font-family: 'Inter', sans-serif;
            margin: 0;
            background-color: var(--background-color);
            color: var(--text-color);
            padding-bottom: 80px; 
        }

        .app-container {
            max-width: 600px;
            margin: 0 auto;
            background-color: var(--card-background);
            min-height: 100vh;
        }
        
        .page {
            display: none;
        }
        .page.active {
            display: block;
        }

        /* --- Header --- */
        .app-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 20px;
            background-color: var(--card-background);
            border-bottom: 1px solid var(--border-color);
            position: sticky;
            top: 0;
            z-index: 100;
        }
        .app-header h1 { margin: 0; font-size: 1.5rem; color: var(--primary-color); font-weight: 700; }
        .header-icons { display: flex; gap: 15px; font-size: 1.5rem; }

        /* --- Trang Chủ --- */
        .search-bar { padding: 15px 20px; }
        .search-bar input { width: 100%; padding: 12px 15px; border: 1px solid var(--border-color); border-radius: 25px; font-size: 1rem; box-sizing: border-box; }
        .category-tabs { display: flex; overflow-x: auto; padding: 0 20px 15px; gap: 10px; border-bottom: 1px solid var(--border-color); -ms-overflow-style: none; scrollbar-width: none; }
        .category-tabs::-webkit-scrollbar { display: none; }
        .category-tab { padding: 8px 15px; border: 1px solid var(--border-color); border-radius: 20px; white-space: nowrap; cursor: pointer; transition: all 0.3s ease; }
        .category-tab.active { background-color: var(--primary-color); color: white; border-color: var(--primary-color); }
        .product-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 15px; padding: 20px; }
        .product-card { background: var(--card-background); border-radius: 12px; overflow: hidden; box-shadow: 0 4px 12px rgba(0,0,0,0.08); display: flex; flex-direction: column; }
        .product-card img { width: 100%; height: 150px; object-fit: cover; }
        .product-info { padding: 12px; display: flex; flex-direction: column; flex-grow: 1; }
        .product-info h3 { font-size: 0.95rem; margin: 0 0 5px 0; font-weight: 600; flex-grow: 1; }
        .product-price { font-size: 1.1rem; font-weight: 700; color: var(--primary-color); margin-bottom: 10px; }
        .buy-btn { background-color: var(--primary-color); color: white; border: none; padding: 8px 12px; border-radius: 8px; cursor: pointer; width: 100%; font-size: 0.9rem; font-weight: 500; transition: background-color 0.2s; }
        .buy-btn:hover { background-color: #d63031; }

        /* --- Trang Tài Khoản --- */
        .account-page { padding: 20px; }
        .card { background-color: white; padding: 25px; border-radius: 12px; box-shadow: 0 4px 12px rgba(0,0,0,0.08); text-align: center; margin-bottom: 20px; }
        .card h2 { margin-top: 0; }
        .card p { color: var(--secondary-text-color); }
        .login-form input { width: 100%; padding: 12px; margin: 15px 0; border: 1px solid var(--border-color); border-radius: 8px; box-sizing: border-box; }
        .btn { display: block; width: 100%; padding: 12px; border: none; border-radius: 8px; font-size: 1rem; font-weight: 600; color: white; cursor: pointer; text-align: center; text-decoration: none; }
        .btn-primary { background-color: var(--primary-color); }
        .balance-amount { font-size: 2.5rem; font-weight: 700; color: var(--primary-color); margin: 5px 0 10px 0; }
        .pending-text { font-size: 1rem; color: var(--secondary-text-color); margin-top: 0; }
        .pending-text strong { color: var(--pending-color); font-weight: 700; }
        .btn-success { background-color: var(--success-color); }
        .logout-btn { background: none; border: none; color: var(--secondary-text-color); text-decoration: underline; cursor: pointer; margin-top: 20px; }
        .referral-card i { font-size: 2rem; color: var(--primary-color); margin-bottom: 10px; }

        /* --- Thanh điều hướng dưới cùng --- */
        .bottom-nav { position: fixed; bottom: 0; left: 0; right: 0; max-width: 600px; margin: 0 auto; display: flex; justify-content: space-around; background-color: var(--card-background); border-top: 1px solid var(--border-color); box-shadow: 0 -2px 10px rgba(0,0,0,0.05); padding: 5px 0; z-index: 199; }
        .nav-item { display: flex; flex-direction: column; align-items: center; padding: 5px 10px; color: var(--secondary-text-color); text-decoration: none; font-size: 0.75rem; cursor: pointer; }
        .nav-item i { font-size: 1.6rem; margin-bottom: 2px; }
        .nav-item.active { color: var(--primary-color); }

        /* --- Cửa sổ Modal --- */
        .modal-backdrop { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5); z-index: 200; opacity: 0; visibility: hidden; transition: opacity 0.3s, visibility 0.3s; }
        .modal-backdrop.show { opacity: 1; visibility: visible; }
        .modal { position: fixed; top: 50%; left: 50%; transform: translate(-50%, -50%); background: white; padding: 25px; border-radius: 15px; z-index: 201; width: 90%; max-width: 400px; box-shadow: 0 5px 20px rgba(0,0,0,0.2); opacity: 0; visibility: hidden; transition: opacity 0.3s, visibility 0.3s; }
        .modal.show { opacity: 1; visibility: visible; }
        .modal-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px; }
        .modal-header h2 { margin: 0; font-size: 1.4rem; }
        .close-btn { font-size: 2rem; cursor: pointer; border: none; background: none; }

        /* Modal Liên hệ */
        .contact-info-item { margin-bottom: 15px; }
        .contact-info-item h4 { margin: 0 0 5px 0; color: var(--secondary-text-color); }
        .contact-info-item p, .contact-info-item a { margin: 0; font-size: 1.1rem; text-decoration: none; color: var(--text-color); }
        .qr-code { text-align: center; }
        .qr-code img { max-width: 200px; width: 100%; border: 1px solid var(--border-color); border-radius: 8px; }
        .zalo-button { display: inline-block; background-color: #0068ff; color: white; padding: 10px 15px; border-radius: 8px; font-weight: bold; }

        /* Modal Nạp tiền */
        .deposit-modal input { width: 100%; padding: 12px; margin-bottom: 15px; border: 1px solid var(--border-color); border-radius: 8px; box-sizing: border-box; text-align: right; font-size: 1.2rem; }
        .bonus-info { background-color: #f8f9fa; padding: 15px; border-radius: 8px; font-size: 0.9rem; }
        .deposit-suggestion { display: flex; justify-content: space-between; align-items: center; padding: 12px 0; border-bottom: 1px solid #e9ecef; }
        .deposit-suggestion:last-child { border-bottom: none; }
        .deposit-suggestion p { margin: 0; font-size: 1rem; }
        .deposit-suggestion strong { color: var(--primary-color); }
        .btn-quick-deposit { padding: 6px 14px; font-size: 0.8rem; border-radius: 6px; background-color: var(--secondary-text-color); flex-shrink: 0; margin-left: 15px; border: none; color: white; cursor: pointer;}
        .total-receive { margin-top: 15px; font-size: 1.1rem; font-weight: 600; text-align: center; height: 20px; }
        #qr-display-area { text-align: center; }
        #qr-display-area img { max-width: 250px; width: 100%; margin: 15px 0; }
        #qr-display-area p { font-size: 0.9rem; color: var(--secondary-text-color); }

        /* --- Thông báo --- */
        .toast-notification { position: fixed; bottom: 90px; left: 50%; transform: translateX(-50%); background-color: rgba(0,0,0,0.75); color: white; padding: 12px 25px; border-radius: 25px; opacity: 0; visibility: hidden; transition: opacity 0.5s, visibility 0.5s; z-index: 300; }
        .toast-notification.show { opacity: 1; visibility: visible; }
    </style>
</head>
<body>

    <div class="app-container">

        <!-- ===== TRANG CHỦ ===== -->
        <div id="home-page" class="page active">
            <header class="app-header">
                <h1>VUA DECOR</h1>
                <div class="header-icons"><i class="ph ph-bell"></i><i class="ph ph-heart"></i></div>
            </header>
            <main>
                <div class="search-bar"><input type="text" placeholder="Tìm kiếm tranh, chữ nổi..."></div>
                <div class="category-tabs" id="category-container"></div>
                <div class="product-grid" id="product-grid"></div>
            </main>
        </div>

        <!-- ===== TRANG TÀI KHOẢN ===== -->
        <div id="account-page" class="page">
            <header class="app-header"><h1>Tài Khoản</h1></header>
            <div class="account-page">
                <!-- Giao diện chưa đăng nhập -->
                <div id="login-view" class="card login-form">
                    <h2>Đăng ký / Đăng nhập</h2>
                    <p>Sử dụng số điện thoại để nhận nhiều ưu đãi thành viên!</p>
                    <input type="tel" id="phone-input" placeholder="Nhập số điện thoại của bạn">
                    <button id="login-btn" class="btn btn-primary">Tiếp tục</button>
                </div>
                <!-- Giao diện đã đăng nhập -->
                <div id="account-view" style="display: none;">
                    <div class="card account-info">
                        <h2 id="welcome-message">Chào mừng quay trở lại!</h2>
                        <p>Số điện thoại: <strong id="user-phone"></strong></p>
                        <div class="balance-card">
                            <p>SỐ DƯ TÀI SẢN</p>
                            <div id="balance-amount" class="balance-amount">0₫</div>
                            <div id="pending-balance-area" style="display: none;">
                                <p class="pending-text">Số dư chờ duyệt: <strong id="pending-balance-amount">0₫</strong></p>
                            </div>
                            <button id="deposit-btn" class="btn btn-success">NẠP TIỀN</button>
                        </div>
                    </div>
                    <div class="card referral-card">
                        <i class="ph-fill ph-gift"></i>
                        <h2>Chia sẻ bạn bè</h2>
                        <p>Nhận ngay <strong>300.000₫</strong> khi bạn bè đăng ký và nạp tối thiểu 1.000.000₫.</p>
                        <button id="share-btn" class="btn btn-primary">Chia sẻ ngay</button>
                    </div>
                     <button id="logout-btn" class="logout-btn">Đăng xuất</button>
                </div>
            </div>
        </div>

    </div>

    <!-- ===== THANH ĐIỀU HƯỚNG ===== -->
    <nav class="bottom-nav">
        <a class="nav-item active" data-page="home-page"><i class="ph-fill ph-house"></i><span>Trang chủ</span></a>
        <a class="nav-item" id="contact-nav-btn"><i class="ph ph-phone"></i><span>Liên hệ</span></a>
        <a class="nav-item" data-page="account-page"><i class="ph ph-user"></i><span>Tài khoản</span></a>
    </nav>
    
    <!-- ===== MODAL & THÔNG BÁO ===== -->
    <div id="toast" class="toast-notification"></div>
    <div class="modal-backdrop" id="modal-backdrop"></div>
    
    <!-- Modal Liên hệ -->
    <div class="modal" id="contact-modal">
        <div class="modal-header">
            <h2>Thông Tin Liên Hệ</h2>
            <button class="close-btn" data-modal="contact-modal">&times;</button>
        </div>
        <div class="modal-body">
            <div class="contact-info-item"><h4>Kết nối Zalo</h4><a href="https://zalo.me/0333334795" class="zalo-button" target="_blank">Chat với VUA DECOR</a></div>
            <div class="contact-info-item"><h4>Địa chỉ cửa hàng</h4><p>123 Đường ABC, Phường XYZ, Quận 1, TP. Hồ Chí Minh</p></div>
            <div class="contact-info-item"><h4>Thông tin thanh toán</h4><p>Ngân hàng: MB BANK</p><p>Số tài khoản: 789999999789</p><p>Chủ tài khoản: BUI XUAN LONG</p></div>
            <div class="qr-code"><p><strong>Quét mã để thanh toán</strong></p><img id="static-qr-code" src="" alt="Mã QR thanh toán"></div>
        </div>
    </div>
    
    <!-- Modal Nạp tiền -->
    <div class="modal deposit-modal" id="deposit-modal">
        <div class="modal-header"><h2>Nạp tiền vào tài sản</h2><button class="close-btn" data-modal="deposit-modal">&times;</button></div>
        <div class="modal-body">
            <div id="deposit-input-area">
                <input type="number" id="deposit-amount-input" placeholder="Hoặc nhập số tiền khác">
                <div class="bonus-info">
                    <div class="deposit-suggestion">
                        <p>Nạp <strong>1.000.000₫</strong> - Tặng <strong>5%</strong></p>
                        <button class="btn-quick-deposit" data-amount="1000000">Nạp ngay</button>
                    </div>
                     <div class="deposit-suggestion">
                        <p>Nạp <strong>3.000.000₫</strong> - Tặng <strong>10%</strong></p>
                        <button class="btn-quick-deposit" data-amount="3000000">Nạp ngay</button>
                    </div>
                     <div class="deposit-suggestion">
                        <p>Nạp <strong>5.000.000₫</strong> - Tặng <strong>15%</strong></p>
                        <button class="btn-quick-deposit" data-amount="5000000">Nạp ngay</button>
                    </div>
                    <div class="deposit-suggestion">
                        <p>Nạp <strong>10.000.000₫</strong> - Tặng <strong>20%</strong></p>
                        <button class="btn-quick-deposit" data-amount="10000000">Nạp ngay</button>
                    </div>
                </div>
                <div id="total-receive" class="total-receive"></div>
                <button id="generate-qr-btn" class="btn btn-primary" style="margin-top: 20px;">Tạo mã QR cho số tiền đã nhập</button>
            </div>
            <div id="qr-display-area" style="display: none;">
                <img id="qr-code-img" src="" alt="QR Code Thanh toán">
                <p>Vui lòng quét mã QR bằng ứng dụng ngân hàng của bạn. <br>Sau khi chuyển khoản, VUA DECOR sẽ xác nhận và cộng tiền vào tài khoản của bạn trong ít phút.</p>
                <a id="download-qr-btn" href="#" class="btn" style="background-color: var(--secondary-text-color); margin-top: 10px; display: inline-block; width: auto; padding: 10px 20px;">Tải mã QR</a>
            </div>
        </div>
    </div>


    <script>
        // --- JAVASCRIPT ---

        // Đăng ký Service Worker
        if ('serviceWorker' in navigator) {
            window.addEventListener('load', () => {
                navigator.serviceWorker.register('./sw.js')
                .then(registration => {
                    console.log('ServiceWorker registration successful with scope: ', registration.scope);
                })
                .catch(err => {
                    console.log('ServiceWorker registration failed: ', err);
                });
            });
        }

        const VUA_DECOR_CONFIG = {
            BANK_ID: "970422", // MB Bank
            ACCOUNT_NO: "789999999789", // STK của bạn
            ACCOUNT_NAME: "BUI XUAN LONG" // Tên của bạn
        };

        const products = [
             { id: 1, name: "Tranh Neon 'Live Your Dream'", price: 1250000, image: 'https://placehold.co/300x300/FFC0CB/000?text=Tranh+Neon', category: 'Tranh Neon' },
            { id: 2, name: 'Bộ Chữ Nổi Mica "VUA DECOR"', price: 2500000, image: 'https://placehold.co/300x300/ADD8E6/000?text=Chữ+Nổi', category: 'Chữ Nổi' },
            { id: 3, name: 'Đèn Decor Hình Đám Mây', price: 750000, image: 'https://placehold.co/300x300/FFFFE0/000?text=Đèn+Decor', category: 'Đèn Decor' },
            { id: 4, name: 'Gương Soi Toàn Thân LED', price: 1990000, image: 'https://placehold.co/300x300/E6E6FA/000?text=Gương+LED', category: 'Gương LED' },
            { id: 5, name: 'Kệ Gỗ Treo Tường 3 Tầng', price: 450000, image: 'https://placehold.co/300x300/F5DEB3/000?text=Kệ+Trang+Trí', category: 'Kệ Trang Trí' },
            { id: 6, name: 'Giảm giá bộ chữ nổi "HOME"', price: 999000, image: 'https://placehold.co/300x300/FFE4E1/000?text=Chữ+Nổi', category: 'Khuyến Mãi' }
        ];

        let user = { isLoggedIn: false, phone: null, balance: 0, pendingBalance: 0 };

        const productGrid = document.getElementById('product-grid');
        const categoryContainer = document.getElementById('category-container');
        const toast = document.getElementById('toast');
        const modalBackdrop = document.getElementById('modal-backdrop');

        const formatCurrency = (amount) => new Intl.NumberFormat('vi-VN', { style: 'currency', currency: 'VND' }).format(amount);

        function displayProducts(filteredProducts) {
            productGrid.innerHTML = filteredProducts.map(product => `
                <div class="product-card">
                    <img src="${product.image}" alt="${product.name}">
                    <div class="product-info">
                        <h3>${product.name}</h3>
                        <p class="product-price">${formatCurrency(product.price)}</p>
                        <button class="buy-btn" onclick="buyProduct(${product.id})">Mua ngay</button>
                    </div>
                </div>
            `).join('');
        }
        
        function displayCategories() {
            const categories = ['Tất cả', ...new Set(products.map(p => p.category))];
            categoryContainer.innerHTML = categories.map(category => 
                `<div class="category-tab ${category === 'Tất cả' ? 'active' : ''}" data-category="${category}">${category}</div>`
            ).join('');

            categoryContainer.querySelectorAll('.category-tab').forEach(tab => {
                tab.addEventListener('click', () => {
                    categoryContainer.querySelector('.category-tab.active').classList.remove('active');
                    tab.classList.add('active');
                    const selectedCategory = tab.dataset.category;
                    const filtered = selectedCategory === 'Tất cả' ? products : products.filter(p => p.category === selectedCategory);
                    displayProducts(filtered);
                });
            });
        }
        
        function showToast(message, duration = 3000) {
            toast.textContent = message;
            toast.classList.add('show');
            setTimeout(() => toast.classList.remove('show'), duration);
        }

        function buyProduct(productId) {
            if (!user.isLoggedIn) {
                showToast("Vui lòng đăng nhập để mua hàng!");
                switchPage('account-page');
                return;
            }
            const product = products.find(p => p.id === productId);
            if (user.balance >= product.price) {
                 if (confirm(`Bạn có chắc chắn muốn mua "${product.name}" với giá ${formatCurrency(product.price)}?`)) {
                    user.balance -= product.price;
                    updateUserUI();
                    showToast("Mua hàng thành công!");
                }
            } else {
                showToast("Số dư không đủ. Vui lòng nạp thêm tiền.");
            }
        }

        // === LOGIC TÀI KHOẢN & ĐĂNG NHẬP ===
        const loginView = document.getElementById('login-view');
        const accountView = document.getElementById('account-view');
        
        function updateUserUI() {
            const pendingBalanceArea = document.getElementById('pending-balance-area');
            const pendingBalanceAmount = document.getElementById('pending-balance-amount');

            if (user.isLoggedIn) {
                loginView.style.display = 'none';
                accountView.style.display = 'block';
                document.getElementById('user-phone').textContent = user.phone;
                document.getElementById('balance-amount').textContent = formatCurrency(user.balance);
                
                if (user.pendingBalance > 0) {
                    pendingBalanceAmount.textContent = formatCurrency(user.pendingBalance);
                    pendingBalanceArea.style.display = 'block';
                } else {
                    pendingBalanceArea.style.display = 'none';
                }

            } else {
                loginView.style.display = 'block';
                accountView.style.display = 'none';
            }
        }
        
        document.getElementById('login-btn').addEventListener('click', () => {
            const phoneInput = document.getElementById('phone-input');
            if (phoneInput.value.trim().length >= 9) {
                user.isLoggedIn = true;
                user.phone = phoneInput.value;
                user.balance = 0;
                user.pendingBalance = 0;
                updateUserUI();
                showToast(`Đăng nhập thành công với SĐT: ${user.phone}`);
            } else {
                showToast("Số điện thoại không hợp lệ.");
            }
        });

        document.getElementById('logout-btn').addEventListener('click', () => {
            user.isLoggedIn = false;
            user.phone = null;
            user.balance = 0;
            user.pendingBalance = 0;
            updateUserUI();
            showToast("Bạn đã đăng xuất.");
        });

        function switchPage(pageId) {
            document.querySelectorAll('.page').forEach(page => page.classList.remove('active'));
            document.getElementById(pageId).classList.add('active');
            
            document.querySelectorAll('.nav-item').forEach(item => {
                item.classList.remove('active');
                if(item.dataset.page === pageId) item.classList.add('active');
            });
            document.getElementById('contact-nav-btn').classList.remove('active');
        }

        document.querySelectorAll('.nav-item[data-page]').forEach(item => {
            item.addEventListener('click', () => switchPage(item.dataset.page));
        });

        // === LOGIC MODAL ===
        function toggleModal(modalId, show) {
            const modal = document.getElementById(modalId);
            if (show) {
                modalBackdrop.classList.add('show');
                modal.classList.add('show');
            } else {
                modalBackdrop.classList.remove('show');
                modal.classList.remove('show');
            }
        }

        document.getElementById('contact-nav-btn').addEventListener('click', (e) => {
            e.preventDefault();
            // Tạo mã QR tĩnh cho mục liên hệ khi được mở
            const staticQrUrl = `https://img.vietqr.io/image/${VUA_DECOR_CONFIG.BANK_ID}-${VUA_DECOR_CONFIG.ACCOUNT_NO}-compact.png?accountName=${encodeURIComponent(VUA_DECOR_CONFIG.ACCOUNT_NAME)}`;
            document.getElementById('static-qr-code').src = staticQrUrl;
            toggleModal('contact-modal', true);
        });

        document.querySelectorAll('.close-btn').forEach(btn => {
            btn.addEventListener('click', () => toggleModal(btn.dataset.modal, false));
        });
        modalBackdrop.addEventListener('click', () => {
            document.querySelectorAll('.modal.show').forEach(modal => toggleModal(modal.id, false));
        });

        // === LOGIC NẠP TIỀN & QR ===
        const depositAmountInput = document.getElementById('deposit-amount-input');
        const totalReceiveDiv = document.getElementById('total-receive');
        const depositInputArea = document.getElementById('deposit-input-area');
        const qrDisplayArea = document.getElementById('qr-display-area');

        document.getElementById('deposit-btn').addEventListener('click', () => {
            depositAmountInput.value = '';
            totalReceiveDiv.textContent = '';
            depositInputArea.style.display = 'block';
            qrDisplayArea.style.display = 'none';
            toggleModal('deposit-modal', true);
        });
        
        function calculateBonus(amount) {
            let bonus = 0;
            if (amount >= 10000000) bonus = 0.20;
            else if (amount >= 5000000) bonus = 0.15;
            else if (amount >= 3000000) bonus = 0.10;
            else if (amount >= 1000000) bonus = 0.05;
            return amount * bonus;
        }

        depositAmountInput.addEventListener('input', () => {
            const amount = parseFloat(depositAmountInput.value) || 0;
            const bonusAmount = calculateBonus(amount);
            const total = amount + bonusAmount;
            
            if (amount > 0) {
                totalReceiveDiv.innerHTML = `Thực nhận: <strong>${formatCurrency(total)}</strong> (gồm ${formatCurrency(bonusAmount)} tiền thưởng)`;
            } else {
                totalReceiveDiv.innerHTML = '';
            }
        });
        
        function simulateAdminApproval() {
            const amountToApprove = user.pendingBalance;
            // Mô phỏng admin nhận được thông báo và duyệt sau 3 giây
            setTimeout(() => {
                if (confirm(`[ADMIN] Duyệt khoản nạp ${formatCurrency(amountToApprove)} cho SĐT ${user.phone}?`)) {
                    user.balance += user.pendingBalance;
                    user.pendingBalance = 0;
                    updateUserUI();
                    showToast("Khoản nạp của bạn đã được duyệt thành công!");
                } else {
                    // Xử lý trường hợp admin từ chối (trong thực tế)
                    user.pendingBalance = 0;
                    updateUserUI();
                    showToast("Admin đã từ chối giao dịch nạp tiền của bạn.");
                }
            }, 3000);
        }

        function generateQr(amount) {
             if (amount < 1000) {
                showToast("Vui lòng nhập số tiền hợp lệ (tối thiểu 1.000đ).");
                return;
            }
             if (user.pendingBalance > 0) {
                showToast("Bạn đang có một giao dịch chờ duyệt, vui lòng đợi.");
                return;
            }
            const bonusAmount = calculateBonus(amount);
            const totalToReceive = amount + bonusAmount;
            user.pendingBalance = totalToReceive;

            const qrInfo = `Nap tien VUA DECOR cho SĐT ${user.phone}`;
            const qrImgUrl = `https://img.vietqr.io/image/${VUA_DECOR_CONFIG.BANK_ID}-${VUA_DECOR_CONFIG.ACCOUNT_NO}-compact.png?amount=${amount}&addInfo=${encodeURIComponent(qrInfo)}`;
            
            document.getElementById('qr-code-img').src = qrImgUrl;
            
            // Add download functionality
            const downloadBtn = document.getElementById('download-qr-btn');
            downloadBtn.href = qrImgUrl;
            downloadBtn.download = `VUA-DECOR-Thanh-Toan-${amount}d.png`;

            depositInputArea.style.display = 'none';
            qrDisplayArea.style.display = 'block';

            // Cập nhật UI ngay lập tức để hiển thị số dư chờ duyệt
            updateUserUI(); 
            // Bắt đầu quy trình nền sau khi QR được hiển thị
            setTimeout(() => {
                // ĐÃ SỬA LỖI: Không tự động đóng modal
                showToast("Giao dịch đang chờ xử lý. Vui lòng chờ xác nhận.");
                // Bắt đầu quá trình mô phỏng admin duyệt
                simulateAdminApproval();
            }, 2000); 
        }

        document.getElementById('generate-qr-btn').addEventListener('click', () => {
            const amount = parseFloat(depositAmountInput.value) || 0;
            generateQr(amount);
        });

        document.querySelectorAll('.btn-quick-deposit').forEach(btn => {
            btn.addEventListener('click', () => {
                const amount = parseFloat(btn.dataset.amount);
                generateQr(amount);
            });
        });

        // === LOGIC CHIA SẺ ===
        document.getElementById('share-btn').addEventListener('click', () => {
            if (navigator.share) {
                navigator.share({
                    title: 'VUA DECOR - Trang trí nhà cửa',
                    text: `Hãy dùng thử ứng dụng VUA DECOR! Đăng ký với mã giới thiệu của tôi để nhận ưu đãi: ${user.phone.slice(-6)}`,
                    url: window.location.href,
                })
                .then(() => showToast('Cảm ơn bạn đã chia sẻ!'))
                .catch((err) => console.log('Error sharing', err));
            } else {
                const referralLink = `https://vuadecor.example.com/register?ref=${user.phone.slice(-6)}`;
                 navigator.clipboard.writeText(referralLink).then(() => {
                    showToast('Đã sao chép link giới thiệu của bạn!');
                 });
            }
        });

        window.onload = () => {
            displayCategories();
            displayProducts(products);
            updateUserUI();
        };
    </script>
</body>
</html>

