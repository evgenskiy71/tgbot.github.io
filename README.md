<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Кожаные изделия ручной работы</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #f5f5f5 0%, #e8e8e8 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
        }

        .header {
            text-align: center;
            margin-bottom: 40px;
            animation: fadeInDown 1s ease;
        }

        .header h1 {
            color: #8B4513;
            font-size: 2.5em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
        }

        .header p {
            color: #666;
            font-size: 1.1em;
        }

        .products-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 25px;
            margin-bottom: 40px;
        }

        .product-card {
            background: white;
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 8px 25px rgba(0,0,0,0.1);
            transition: all 0.3s ease;
            border: 2px solid transparent;
            animation: fadeInUp 0.6s ease;
            cursor: pointer;
        }

        .product-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 15px 35px rgba(0,0,0,0.15);
            border-color: #8B4513;
        }

        .product-icon {
            font-size: 2.5em;
            margin-bottom: 15px;
            text-align: center;
        }

        .product-name {
            font-size: 1.3em;
            font-weight: bold;
            color: #333;
            margin-bottom: 8px;
            text-align: center;
        }

        .product-description {
            color: #666;
            text-align: center;
            margin-bottom: 15px;
            line-height: 1.4;
        }

        .product-price {
            font-size: 1.4em;
            font-weight: bold;
            color: #8B4513;
            text-align: center;
            margin-bottom: 15px;
        }

        .buy-button {
            background: linear-gradient(135deg, #8B4513 0%, #A0522D 100%);
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 25px;
            font-size: 1em;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            display: block;
            margin: 0 auto;
            width: 80%;
        }

        .buy-button:hover {
            background: linear-gradient(135deg, #A0522D 0%, #8B4513 100%);
            transform: scale(1.05);
        }

        .footer {
            text-align: center;
            margin-top: 40px;
            color: #888;
            font-size: 0.9em;
            animation: fadeIn 1s ease;
        }

        /* Анимации */
        @keyframes fadeInDown {
            from {
                opacity: 0;
                transform: translateY(-30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
            }
            to {
                opacity: 1;
            }
        }

        /* Адаптивность */
        @media (max-width: 768px) {
            .header h1 {
                font-size: 2em;
            }
            
            .products-grid {
                grid-template-columns: 1fr;
            }
            
            .product-card {
                padding: 20px;
            }
        }

        /* Модальное окно */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            z-index: 1000;
            animation: fadeIn 0.3s ease;
        }

        .modal-content {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: white;
            padding: 30px;
            border-radius: 15px;
            text-align: center;
            max-width: 400px;
            width: 90%;
        }

        .close-button {
            position: absolute;
            top: 10px;
            right: 15px;
            font-size: 1.5em;
            cursor: pointer;
            color: #666;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>👜 Кожаные изделия</h1>
            <p>Ручная работа • Натуральная кожа • Гарантия качества</p>
        </div>

        <div class="products-grid" id="productsGrid">
            <!-- Товары будут добавлены через JavaScript -->
        </div>

        <div class="footer">
            <p>© 2024 Кожаные изделия ручной работы. Все права защищены.</p>
        </div>
    </div>

    <!-- Модальное окно -->
    <div class="modal" id="orderModal">
        <div class="modal-content">
            <span class="close-button" id="closeModal">&times;</span>
            <h2>Заказ товара</h2>
            <p id="modalProductName"></p>
            <p id="modalProductPrice"></p>
            <p style="margin: 20px 0; color: #666;">Для заказа напишите нам в Telegram:</p>
            <button class="buy-button" onclick="contactTelegram()">Написать в Telegram</button>
        </div>
    </div>

    <script>
        // Данные товаров
        const products = [
            {
                icon: "👜",
                name: "Секретарь",
                description: "Просто картхолдер",
                price: "1600₽"
            },
            {
                icon: "👜",
                name: "Цесаревич",
                description: "Компактный бумажник",
                price: "2900₽"
            },
            {
                icon: "👜",
                name: "Цесаревич",
                description: "С отделением для монет",
                price: "3200₽"
            },
            {
                icon: "👜",
                name: "Боярин",
                description: "Вместительный кошелек",
                price: "4900₽"
            },
            {
                icon: "👜",
                name: "Купец",
                description: "Портмоне для карт, документов и купюр",
                price: "4900₽"
            },
            {
                icon: "👜",
                name: "Казначей",
                description: "Зиппер для документов и карт",
                price: "6500₽"
            },
            {
                icon: "👜",
                name: "Посыльный",
                description: "Сумка через плечо",
                price: "9900₽"
            },
            {
                icon: "👜",
                name: "Посыльный",
                description: "С внешним карманом",
                price: "10900₽"
            }
        ];

        // Загрузка товаров на страницу
        function loadProducts() {
            const grid = document.getElementById('productsGrid');
            
            products.forEach((product, index) => {
                const card = document.createElement('div');
                card.className = 'product-card';
                card.style.animationDelay = `${index * 0.1}s`;
                
                card.innerHTML = `
                    <div class="product-icon">${product.icon}</div>
                    <div class="product-name">${product.name}</div>
                    <div class="product-description">${product.description}</div>
                    <div class="product-price">${product.price}</div>
                    <button class="buy-button" onclick="openOrderModal('${product.name}', '${product.description}', '${product.price}')">
                        Заказать
                    </button>
                `;
                
                grid.appendChild(card);
            });
        }

        // Открытие модального окна
        function openOrderModal(name, description, price) {
            document.getElementById('modalProductName').textContent = `${name} — ${description}`;
            document.getElementById('modalProductPrice').textContent = price;
            document.getElementById('orderModal').style.display = 'block';
        }

        // Закрытие модального окна
        document.getElementById('closeModal').onclick = function() {
            document.getElementById('orderModal').style.display = 'none';
        }

        // Закрытие модального окна при клике вне его
        window.onclick = function(event) {
            const modal = document.getElementById('orderModal');
            if (event.target === modal) {
                modal.style.display = 'none';
            }
        }

        // Контакт в Telegram
        function contactTelegram() {
            // Здесь можно указать ссылку на ваш Telegram
            // Например: window.open('https://t.me/your_username', '_blank');
            alert('Свяжитесь с нами в Telegram для заказа!');
        }

        // Загрузка при старте
        document.addEventListener('DOMContentLoaded', loadProducts);
    </script>
</body>
</html>
