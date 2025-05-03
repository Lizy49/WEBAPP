```
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>OlimpShop49</title>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap" rel="stylesheet">
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body {
      font-family: 'Montserrat', sans-serif;
      background-color: #0e0e1f;
      background-image: url('https://img.freepik.com/free-photo/view-ancient-greek-architecture-with-temple-structure_23-2151664764.jpg?semt=ais_hybrid&w=740');
      background-size: cover;
      background-position: center;
      background-attachment: fixed;
      color: #f0f0f0;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 20px;
      animation: fadeIn 1s ease-in-out;
    }
    .hero { text-align: center; margin-bottom: 30px; animation: thunderFlash 2s ease-in-out infinite; }
    .logo { font-size: 3rem; font-weight: 900; color: #ffd700; text-shadow: 0 0 15px #ffd700, 0 0 30px #fffb00; }
    .welcome { margin-top: 10px; font-size: 1.2rem; color: #ccc; }
    .container { width: 100%; max-width: 1000px; }
    .category-tabs { display: flex; justify-content: center; flex-wrap: wrap; gap: 10px; margin-bottom: 20px; }
    .category-tabs button {
      background: #ffd700; color: #000; padding: 10px 15px; border: none;
      border-radius: 6px; cursor: pointer; font-weight: bold; transition: background 0.3s;
    }
    .category-tabs button:hover { background: #fff700; }
    .products { display: grid; grid-template-columns: repeat(auto-fill, minmax(240px, 1fr)); gap: 20px; }
    .product-card {
      background: rgba(0, 0, 0, 0.6); border: 1px solid rgba(255, 255, 255, 0.1);
      border-radius: 12px; padding: 15px; text-align: center; backdrop-filter: blur(6px);
      transition: transform 0.3s ease, box-shadow 0.3s ease;
      box-shadow: 0 0 25px rgba(255, 215, 0, 0.2);
    }
    .product-card:hover { transform: scale(1.03); box-shadow: 0 0 35px rgba(255, 215, 0, 0.4); }
    .product-card img { width: 100%; height: 180px; object-fit: cover; border-radius: 8px; }
    .product-card h3 { margin-top: 10px; font-size: 1.2rem; color: #ffd700; }
    .product-card p { font-size: 0.9rem; color: #bbb; margin: 10px 0; }
    .price { color: #fff; font-weight: bold; margin-bottom: 10px; }
    .flavor-select { margin: 10px 0; width: 100%; padding: 6px; border-radius: 5px; border: none; }
    .cart {
      margin-top: 40px; background: rgba(0, 0, 0, 0.6); padding: 20px;
      border-radius: 10px; backdrop-filter: blur(8px); width: 100%; max-width: 1000px;
    }
    #delivery, #address {
      width: 100%; padding: 12px; margin: 10px 0;
      border-radius: 6px; border: none;
    }
    #delivery { background: rgba(255, 255, 255, 0.9); color: #000; font-weight: bold; }
    .delivery-info { color: #ffd700; margin: 5px 0; font-size: 0.9rem; }
    #confirmOrder {
      margin-top: 15px; width: 100%; padding: 12px;
      background: #ffd700; border: none; font-weight: bold;
      border-radius: 6px; cursor: pointer; transition: all 0.3s;
    }
    #confirmOrder:hover { background: #fff700; box-shadow: 0 0 15px rgba(255, 215, 0, 0.6); }
    footer { margin-top: 60px; text-align: center; color: #aaa; font-size: 0.9rem; }
    footer a { color: #ffd700; text-decoration: none; }
    @keyframes fadeIn { 0% { opacity: 0; transform: translateY(-20px); } 100% { opacity: 1; transform: translateY(0); } }
    @keyframes thunderFlash {
      0%, 100% { text-shadow: 0 0 15px #ffd700, 0 0 30px #fffb00; }
      50% { text-shadow: 0 0 25px #fffb00, 0 0 45px #fff200; }
    }
    #total-summary { margin: 10px 0; font-weight: bold; }
    #total-summary p { margin: 5px 0; }
    .stock-info { color: #ffd700; font-size: 0.8rem; margin-top: 5px; }
  </style>
</head>
<body>
  <div class="hero">
    <h1 class="logo">⚡️ OlimpShop49 ⚡️</h1>
    <p class="welcome">Добро пожаловать! Почувствуй гнев Зевса — выбери свой товар и будь молниеносным.</p>
  </div>

  <div class="container">
    <div class="category-tabs">
      <button onclick="filterCategory('pod')">Подики</button>
      <button onclick="filterCategory('juice')">Жижи</button>
      <button onclick="filterCategory('disposable')">Одноразки</button>
      <button onclick="filterCategory('vaporizer')">Испарители</button>
      <button onclick="filterCategory()">Все товары</button>
    </div>
    <div class="products" id="product-list">
      <!-- JS добавит товары сюда -->
    </div>
  </div>

  <div class="cart" id="cart">
    <h2>🛒 Корзина</h2>
    <div id="cart-items"></div>
    <select id="delivery">
      <option value="">-- Выбери район, смертный --</option>
      <option value="200">3-й микрорайон и Яма (200₽)</option>
      <option value="200">5-й микрорайон (200₽)</option>
      <option value="225">Пригородный (225₽)</option>
      <option value="225">Звезда / Автотэк (225₽)</option>
      <option value="325">Солнечный / Пионерный (325₽)</option>
      <option value="180">Центр (180₽)</option>
    </select>
    <p class="delivery-info">⚡ Выбери район и получи молнию Зевса прямо в руки!</p>
    <input type="text" id="address" placeholder="Точный адрес, смертный" />
    <div id="total-summary"></div>
    <button id="confirmOrder" onclick="submitOrder()">⚡ Подтвердить заказ ⚡</button>
  </div>

  <footer>
    <hr style="border-color: rgba(255, 255, 255, 0.2); margin-bottom: 15px;">
    <p>© 2025 OlimpShop49. Все права защищены.</p>
    <p>
      <a href="https://t.me/olimpmagadan" target="_blank">Мы в Telegram</a> |
      <a href="#">Политика конфиденциальности</a> |
      <a href="#">Контакты</a>
    </p>
  </footer>

  <script src="https://telegram.org/js/telegram-web-app.js"></script>
  <script>
    // СЕРВЕРНАЯ ЧАСТЬ (ЭМУЛЯЦИЯ)
    let serverStock = {
      "4": { "Апельсиновая газировка": 1, "Лимонад": 1, "Пиноколада груша": 1, "Ежевичный лимонад": 1 },
      "5": { "Киви банан": 1, "Киви помела": 1, "Хвоя грейпфрут": 1, "Ананас лайм земляника": 1, "Манго банан ментол": 3 },
      "7": { "Яблоко малина": 1, "Апельсин лемон виноград грейпфрут роза": 1, "Энергетик цитрус": 1, "Клубника арбуз": 1, "Персик ананас клюква малина": 1 }
    };

    // Функция для обновления остатков на сервере (в реальности это будет API-запрос)
    function updateServerStock(productId, flavor, newStock) {
      if (serverStock[productId] && serverStock[productId][flavor] !== undefined) {
        serverStock[productId][flavor] = newStock;
        console.log(`Обновлено на сервере: ${productId} - ${flavor} = ${newStock}`);
      }
    }

    // Функция для получения остатков с сервера (в реальности это будет API-запрос)
    function getServerStock(productId) {
      return serverStock[productId] || {};
    }

    const products = [
      { id: 1, name: "Испаритель Geekvape Aegis B Series coil", category: "vaporizer", price: 300, image: 'Evapo/1.jpg', description: "Испаритель для Aegis, 0.6 Ом 15-25W." },
      { id: 2, name: "Жидкость Skala", category: "juice", price: 450, image: 'Li/1.jpg', description: "Крепкость: 20мг, Объем: 30мл", flavors: {} },
      { id: 3, name: "Одноразка Waka", category: "disposable", price: 2000, image: 'od/1.jpg', description: "На 10000 тяг, чтобы вставило" },
      { id: 4, name: "Жидкость Podonki Vintage", category: "juice", price: 500, image: 'Li/2.jpg', description: "Крепкость: 50мг, Объем: 30мл", flavors: getServerStock("4") },
      { id: 5, name: "Жидкость HOTSPOT", category: "juice", price: 500, image: 'Li/3.jpg', description: "Крепкость: 50мг, Объем: 30мл", flavors: getServerStock("5") },
      { id: 6, name: "Картридж для XROS", category: "vaporizer", price: 200, image: 'Evapo/2.jpg', description: "Картридж для XROS 0.6 Ом" },
      { id: 7, name: "Жидкость XYLINET x3 1шт.", category: "juice", price: 500, image: 'Li/4.jpg', description: "Крепкость: 50мг, Объем: 30мл", flavors: getServerStock("7") }
    ];

    let cart = [];

    function renderProducts(filter = null) {
      const list = document.getElementById('product-list');
      list.innerHTML = '';
      const filtered = filter ? products.filter(p => p.category === filter) : products;
      if (filtered.length === 0) {
        list.innerHTML = '<p style="grid-column: 1/-1; text-align: center;">Товаров нет, смертный! Проверь позже.</p>';
        return;
      }
      for (const product of filtered) {
        const card = document.createElement('div');
        card.className = 'product-card';
        const flavorOptions = product.flavors ? Object.entries(product.flavors).map(
          ([flavor, stock]) => `<option value="${flavor}" ${stock === 0 ? 'disabled' : ''}>
                                  ${flavor}${stock === 0 ? ' (нет в наличии)' : ''} 
                                </option>`
        ).join('') : '';
        card.innerHTML = `
          <img src="${product.image}" alt="${product.name}" />
          <h3>${product.name}</h3>
          <p>${product.description}</p>
          <p class="price">${product.price} ₽</p>
          ${product.flavors ? `
            <select class="flavor-select" id="flavor-${product.id}" onchange="addToCart(${product.id})">
              <option value="">-- Выбери вкус --</option>
              ${flavorOptions}
            </select>
            <div class="stock-info" id="stock-${product.id}">
              ${Object.entries(product.flavors).map(([flavor, stock]) => `${flavor}: ${stock} шт.`).join('<br>')}
            </div>
          ` : ''}
        `;
        list.appendChild(card);
      }
    }

    function addToCart(productId) {
      const flavorSelect = document.getElementById(`flavor-${productId}`);
      const selectedFlavor = flavorSelect.value;
      if (!selectedFlavor) return;

      const product = products.find(p => p.id === productId);
      if (!product.flavors[selectedFlavor] || product.flavors[selectedFlavor] <= 0) {
        alert("Этот вкус закончился, дебил!");
        flavorSelect.value = "";
        return;
      }

      // Уменьшаем остаток локально и на сервере
      product.flavors[selectedFlavor]--;
      updateServerStock(productId.toString(), selectedFlavor, product.flavors[selectedFlavor]);

      // Обновляем отображение остатков
      document.getElementById(`stock-${productId}`).innerHTML = 
        Object.entries(product.flavors).map(([flavor, stock]) => `${flavor}: ${stock} шт.`).join('<br>');

      // Добавляем в корзину
      const existingItem = cart.find(item => item.id === productId && item.flavor === selectedFlavor);
      if (existingItem) {
        existingItem.qty++;
      } else {
        cart.push({
          id: productId,
          name: product.name,
          flavor: selectedFlavor,
          price: product.price,
          qty: 1
        });
      }

      // Обновляем селектор вкусов
      updateFlavorSelect(productId);

      // Обновляем корзину
      updateCartDisplay();
    }

    function updateFlavorSelect(productId) {
      const product = products.find(p => p.id === productId);
      const flavorSelect = document.getElementById(`flavor-${productId}`);
      if (!flavorSelect) return;

      const selectedFlavor = flavorSelect.value;
      flavorSelect.innerHTML = `<option value="">-- Выбери вкус --</option>` + 
        Object.entries(product.flavors).map(
          ([flavor, stock]) => `<option value="${flavor}" ${stock === 0 ? 'disabled' : ''}>
                                  ${flavor}${stock === 0 ? ' (нет в наличии)' : ''} 
                                </option>`
        ).join('');

      if (selectedFlavor && product.flavors[selectedFlavor] > 0) {
        flavorSelect.value = selectedFlavor;
      } else {
        flavorSelect.value = "";
      }
    }

    function filterCategory(cat) { renderProducts(cat); }

    function updateCartDisplay() {
      const cartItems = document.getElementById("cart-items");
      cartItems.innerHTML = '';
      let subtotal = 0;

      for (const item of cart) {
        const cost = item.price * item.qty;
        const p = document.createElement('p');
        p.textContent = `${item.name} (${item.flavor}) x${item.qty} — ${cost}₽`;
        cartItems.appendChild(p);
        subtotal += cost;
      }

      const deliverySelect = document.getElementById("delivery");
      const deliveryPrice = deliverySelect.value ? parseInt(deliverySelect.value) : 0;
      const deliveryName = deliverySelect.selectedOptions[0]?.text || "";

      document.getElementById("total-summary").innerHTML = `
        <p>Товары: ${subtotal}₽</p>
        ${deliveryName ? `<p>Доставка: ${deliveryName}</p>` : ''}
        <p style="color: #ffd700;">Итого: ${subtotal + deliveryPrice}₽</p>
      `;
    }

    function submitOrder() {
      const address = document.getElementById('address').value.trim();
      const deliverySelect = document.getElementById("delivery");
      const district = deliverySelect.selectedOptions[0]?.text;
      const deliveryPrice = parseInt(deliverySelect.value);

      if (!address) {
        alert("Где адрес, смертный? Зевс не всевидящий!");
        return;
      }
      if (!deliveryPrice) {
        alert("Выбери район, иначе Гермес не найдет дорогу!");
        return;
      }
      if (cart.length === 0) {
        alert("Корзина пуста! Ты что, не хочешь гнева Зевса?");
        return;
      }

      const subtotal = cart.reduce((sum, item) => sum + item.price * item.qty, 0);
      const total = subtotal + deliveryPrice;

      const summary = {
        address,
        district,
        items: cart,
        subtotal,
        deliveryPrice,
        total,
        timestamp: new Date().toISOString()
      };

      // Очищаем корзину и обновляем список товаров
      cart = [];
      renderProducts();
      updateCartDisplay();

      // Отправка в Telegram (если подключен)
      if (typeof Telegram !== 'undefined' && Telegram.WebApp) {
        Telegram.WebApp.sendData(JSON.stringify(summary));
        Telegram.WebApp.close();
      } else {
        console.log("Заказ оформлен:", summary);
        alert("Заказ отправлен! Жди молнию Зевса.");
      }
    }

    renderProducts();
    document.getElementById("delivery").addEventListener("change", updateCartDisplay);
  </script>
</body>
</html>
```
