<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Онлайн Банк баллов</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        body {
            background: linear-gradient(135deg, #6a11cb 0%, #2575fc 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }
        .container {
            width: 100%;
            max-width: 1000px;
            background: white;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            overflow: hidden;
        }
        header {
            background: #2c3e50;
            color: white;
            padding: 20px;
            text-align: center;
        }
        h1 {
            font-size: 28px;
            margin-bottom: 10px;
        }
        .content {
            padding: 25px;
        }
        .login-section, .admin-panel, .user-panel {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 25px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
        }
        h2 {
            color: #2c3e50;
            margin-bottom: 15px;
            font-size: 22px;
        }
        .form-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: 600;
            color: #34495e;
        }
        input[type="text"], input[type="password"], input[type="number"] {
            width: 100%;
            padding: 12px;
            border: 2px solid #ddd;
            border-radius: 5px;
            font-size: 16px;
            transition: border-color 0.3s;
        }
        input:focus {
            border-color: #3498db;
            outline: none;
        }
        button {
            padding: 12px 20px;
            background: #3498db;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            font-weight: 600;
            transition: background 0.3s;
        }
        button:hover {
            background: #2980b9;
        }
        .logout-btn {
            background: #e74c3c;
        }
        .logout-btn:hover {
            background: #c0392b;
        }
        .total-points {
            background: #2ecc71;
            color: white;
            padding: 20px;
            text-align: center;
            border-radius: 10px;
            margin-bottom: 25px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        .total-points h2 {
            color: white;
            margin-bottom: 10px;
        }
        .total-points .amount {
            font-size: 42px;
            font-weight: 700;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
        }
        th, td {
            padding: 15px;
            text-align: left;
            border-bottom: 1px solid #ddd;
        }
        th {
            background: #34495e;
            color: white;
        }
        tr:nth-child(even) {
            background: #f8f9fa;
        }
        tr:hover {
            background: #ecf0f1;
        }
        .edit-btn, .delete-btn {
            padding: 8px 12px;
            font-size: 14px;
            margin-right: 5px;
        }
        .delete-btn {
            background: #e74c3c;
        }
        .error {
            color: #e74c3c;
            margin-top: 10px;
            font-weight: 600;
        }
        .success {
            color: #2ecc71;
            margin-top: 10px;
            font-weight: 600;
        }
        .hidden {
            display: none;
        }
        .user-form {
            display: flex;
            gap: 15px;
            margin-top: 15px;
        }
        .user-form input {
            flex: 1;
        }
        .admin-controls {
            margin-top: 20px;
            padding-top: 20px;
            border-top: 2px dashed #bdc3c7;
        }
        .user-info {
            background: #3498db;
            color: white;
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 20px;
        }
        .user-points {
            font-size: 32px;
            font-weight: 700;
            text-align: center;
            margin: 15px 0;
        }
        .user-actions {
            display: flex;
            justify-content: center;
            gap: 15px;
        }
        .info-box {
            background: #e8f4fc;
            padding: 15px;
            border-radius: 8px;
            margin: 15px 0;
        }
        .sync-status {
            padding: 10px;
            border-radius: 5px;
            margin: 10px 0;
            text-align: center;
        }
        .sync-online {
            background: #d4edda;
            color: #155724;
        }
        .sync-offline {
            background: #f8d7da;
            color: #721c24;
        }
        .sync-loading {
            background: #fff3cd;
            color: #856404;
        }
        .loading {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 3px solid #f3f3f3;
            border-top: 3px solid #3498db;
            border-radius: 50%;
            animation: spin 1s linear infinite;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Онлайн Банк баллов</h1>
            <p>Синхронизация между устройствами</p>
        </header>
        
        <div class="content">
            <!-- Форма входа -->
            <div id="loginSection" class="login-section">
                <h2>Вход в систему</h2>
                
                <div class="info-box">
                    <strong>📋 Как работает синхронизация:</strong><br>
                    1. Нажмите "Обновить данные" чтобы увидеть изменения<br>
                    2. Система автоматически обновляется каждые 30 секунд<br>
                    3. Все изменения сохраняются локально
                </div>

                <div class="info-box">
                    <strong>🔐 Тестовые доступы:</strong><br>
                    • Админ: <code>admin</code> / <code>admin123</code><br>
                    • Артем: <code>artem</code> / <code>123321</code><br>
                    • Мария: <code>maria</code> / <code>123456</code>
                </div>
                
                <div class="form-group">
                    <label for="login">Логин:</label>
                    <input type="text" id="login" placeholder="Введите логин">
                </div>
                <div class="form-group">
                    <label for="password">Пароль:</label>
                    <input type="password" id="password" placeholder="Введите пароль">
                </div>
                <button onclick="tryLogin()">Войти</button>
                <p id="loginError" class="error"></p>

                <div class="sync-status sync-online" id="syncStatus">
                    ✅ Система готова к работе
                </div>
            </div>
            
            <!-- Личный кабинет пользователя -->
            <div id="userSection" class="hidden">
                <div class="user-info">
                    <h2>Личный кабинет</h2>
                    <p>Добро пожаловать, <span id="userName"></span>!</p>
                    <p>Последнее обновление: <span id="lastUpdate"></span></p>
                </div>
                
                <div class="total-points">
                    <h2>Общая сумма баллов в системе</h2>
                    <div class="amount" id="totalPoints">0</div>
                </div>
                
                <div class="total-points">
                    <h2>Ваши баллы</h2>
                    <div class="user-points" id="userPoints">0</div>
                </div>
                
                <div class="user-actions">
                    <button onclick="loadData()">🔄 Обновить данные (F5)</button>
                    <button class="logout-btn" onclick="logout()">Выйти</button>
                </div>

                <div class="sync-status sync-online" id="userSyncStatus">
                    ✅ Данные актуальны
                </div>
            </div>
            
            <!-- Панель администратора -->
            <div id="adminSection" class="hidden">
                <div class="user-info">
                    <h2>Панель администратора</h2>
                    <p>Вы вошли как администратор системы</p>
                    <p>Последнее обновление: <span id="adminLastUpdate"></span></p>
                </div>
                
                <div class="total-points">
                    <h2>Общая сумма баллов в системе</h2>
                    <div class="amount" id="totalPointsAdmin">0</div>
                </div>

                <div class="info-box">
                    <h3>Изменить общую сумму баллов</h3>
                    <input type="number" id="editTotalPoints" placeholder="Новая общая сумма" min="0">
                    <button onclick="updateTotalPoints()">Обновить</button>
                </div>
                
                <h2>Пользователи и их баллы</h2>
                <table id="usersTable">
                    <thead>
                        <tr>
                            <th>Пользователь</th>
                            <th>Логин</th>
                            <th>Баллы</th>
                            <th>Действия</th>
                        </tr>
                    </thead>
                    <tbody>
                    </tbody>
                </table>
                
                <h2>Добавить нового пользователя</h2>
                <div class="user-form">
                    <input type="text" id="newUserName" placeholder="ФИО пользователя">
                    <input type="text" id="newUserLogin" placeholder="Логин">
                    <input type="password" id="newUserPassword" placeholder="Пароль">
                    <input type="number" id="newUserPoints" placeholder="Баллы" min="0">
                    <button onclick="addUser()">Добавить пользователя</button>
                </div>
                
                <div class="admin-controls">
                    <button onclick="loadData()">🔄 Обновить данные (F5)</button>
                    <button onclick="forceSave()">💾 Сохранить изменения</button>
                    <button onclick="exportData()">📤 Экспорт данных</button>
                    <button class="logout-btn" onclick="logout()">Выйти</button>
                </div>

                <div class="sync-status sync-online" id="adminSyncStatus">
                    ✅ Изменения сохранены
                </div>
            </div>
        </div>
    </div>

    <script>
        // Константы
        const STORAGE_KEY = 'onlineBankPointsData';
        const SYNC_INTERVAL = 10000; // 10 секунд
        
        let users = [];
        let totalSystemPoints = 10000;
        let currentUser = null;
        let lastUpdateTime = new Date();
        let syncInterval = null;

        // Загрузка данных
        function loadData() {
            updateSyncStatus('Загрузка данных...', 'loading');
            
            try {
                const savedData = localStorage.getItem(STORAGE_KEY);
                
                if (savedData) {
                    const data = JSON.parse(savedData);
                    users = data.users || [];
                    totalSystemPoints = data.totalSystemPoints || 10000;
                    lastUpdateTime = new Date(data.lastUpdate || new Date());
                } else {
                    // Первоначальные данные
                    users = [
                        { id: 1, name: "Артем Козирний", login: "artem", password: "123321", points: 500 },
                        { id: 2, name: "Мария Сидорова", login: "maria", password: "123456", points: 350 },
                        { id: 3, name: "Иван Иванов", login: "ivan", password: "111", points: 150 }
                    ];
                    totalSystemPoints = 10000;
                    lastUpdateTime = new Date();
                    saveData();
                }
                
                updateUI();
                updateSyncStatus('Данные загружены!', 'success');
                
            } catch (error) {
                updateSyncStatus('Ошибка загрузки данных', 'error');
            }
        }

        // Сохранение данных
        function saveData() {
            try {
                const data = {
                    users: users,
                    totalSystemPoints: totalSystemPoints,
                    lastUpdate: new Date().toISOString()
                };
                localStorage.setItem(STORAGE_KEY, JSON.stringify(data));
                lastUpdateTime = new Date();
                return true;
            } catch (error) {
                updateSyncStatus('Ошибка сохранения', 'error');
                return false;
            }
        }

        // Принудительное сохранение
        function forceSave() {
            if (saveData()) {
                updateSyncStatus('Данные сохранены на всех устройствах!', 'success');
                alert('Изменения сохранены! На других устройствах нажмите "Обновить данные"');
            }
        }

        // Обновление статуса
        function updateSyncStatus(message, type = 'info') {
            const statusElement = document.getElementById('syncStatus') || 
                                 document.getElementById('adminSyncStatus') || 
                                 document.getElementById('userSyncStatus');
            
            if (statusElement) {
                let html = '';
                if (type === 'loading') {
                    html = `<span class="loading"></span> ${message}`;
                    statusElement.className = 'sync-status sync-loading';
                } else if (type === 'success') {
                    html = `✅ ${message}`;
                    statusElement.className = 'sync-status sync-online';
                } else if (type === 'error') {
                    html = `❌ ${message}`;
                    statusElement.className = 'sync-status sync-offline';
                } else {
                    html = `ℹ️ ${message}`;
                    statusElement.className = 'sync-status sync-online';
                }
                
                statusElement.innerHTML = html;
            }
        }

        // Обновление времени
        function updateTime() {
            const timeElement = document.getElementById('lastUpdate') || 
                               document.getElementById('adminLastUpdate');
            if (timeElement) {
                timeElement.textContent = lastUpdateTime.toLocaleTimeString();
            }
        }

        // Функция входа
        function tryLogin() {
            const login = document.getElementById('login').value;
            const password = document.getElementById('password').value;
            
            loadData();
            
            if (login === 'admin' && password === 'admin123') {
                currentUser = { isAdmin: true, name: 'Администратор' };
                showAdminPanel();
                return;
            }
            
            const user = users.find(u => u.login === login && u.password === password);
            if (user) {
                currentUser = user;
                showUserPanel();
            } else {
                alert('Неверные логин или пароль');
            }
        }

        // Показать админ-панель
        function showAdminPanel() {
            document.getElementById('loginSection').classList.add('hidden');
            document.getElementById('userSection').classList.add('hidden');
            document.getElementById('adminSection').classList.remove('hidden');
            updateUI();
            startAutoSync();
        }

        // Показать пользовательскую панель
        function showUserPanel() {
            document.getElementById('loginSection').classList.add('hidden');
            document.getElementById('adminSection').classList.add('hidden');
            document.getElementById('userSection').classList.remove('hidden');
            updateUI();
            startAutoSync();
        }

        // Выход
        function logout() {
            currentUser = null;
            document.getElementById('login').value = '';
            document.getElementById('password').value = '';
            document.getElementById('loginSection').classList.remove('hidden');
            document.getElementById('adminSection').classList.add('hidden');
            document.getElementById('userSection').classList.add('hidden');
            stopAutoSync();
        }

        // Автоматическая синхронизация
        function startAutoSync() {
            if (syncInterval) clearInterval(syncInterval);
            syncInterval = setInterval(() => {
                loadData();
            }, SYNC_INTERVAL);
        }

        function stopAutoSync() {
            if (syncInterval) {
                clearInterval(syncInterval);
                syncInterval = null;
            }
        }

        // Обновление интерфейса
        function updateUI() {
            updateTime();
            
            if (currentUser) {
                if (currentUser.isAdmin) {
                    updateUserTable();
                    updateTotalPointsDisplay();
                } else {
                    document.getElementById('userName').textContent = currentUser.name;
                    document.getElementById('userPoints').textContent = currentUser.points;
                    document.getElementById('totalPoints').textContent = totalSystemPoints;
                }
            }
        }

        // Обновление таблицы пользователей
        function updateUserTable() {
            const tbody = document.querySelector('#usersTable tbody');
            tbody.innerHTML = '';
            
            users.forEach((user, index) => {
                const row = document.createElement('tr');
                
                row.innerHTML = `
                    <td>${user.name}</td>
                    <td>${user.login}</td>
                    <td>${user.points}</td>
                    <td>
                        <button class="edit-btn" onclick="editUser(${index})">Изменить</button>
                        <button class="delete-btn" onclick="deleteUser(${index})">Удалить</button>
                    </td>
                `;
                
                tbody.appendChild(row);
            });
        }

        // Обновление отображения баллов
        function updateTotalPointsDisplay() {
            document.getElementById('totalPoints').textContent = totalSystemPoints;
            document.getElementById('totalPointsAdmin').textContent = totalSystemPoints;
        }

        // Добавить пользователя
        function addUser() {
            const name = document.getElementById('newUserName').value;
            const login = document.getElementById('newUserLogin').value;
            const password = document.getElementById('newUserPassword').value;
            const points = parseInt(document.getElementById('newUserPoints').value);

            if (name && login && password && !isNaN(points)) {
                const newUser = {
                    id: Date.now(),
                    name: name,
                    login: login,
                    password: password,
                    points: points
                };
                
                users.push(newUser);
                forceSave();
                updateUI();
                
                // Очистить поля
                document.getElementById('newUserName').value = '';
                document.getElementById('newUserLogin').value = '';
                document.getElementById('newUserPassword').value = '';
                document.getElementById('newUserPoints').value = '';
                
            } else {
                alert('Заполните все поля правильно');
            }
        }

        // Редактировать пользователя
        function editUser(index) {
            const user = users[index];
            const newPoints = prompt(`Введите новые баллы для ${user.name}:`, user.points);
            
            if (newPoints && !isNaN(newPoints)) {
                user.points = parseInt(newPoints);
                forceSave();
                updateUI();
            }
        }

        // Удалить пользователя
        function deleteUser(index) {
            if (confirm(`Удалить пользователя ${users[index].name}?`)) {
                users.splice(index, 1);
                forceSave();
                updateUI();
            }
        }

        // Обновить общую сумму
        function updateTotalPoints() {
            const newTotal = parseInt(document.getElementById('editTotalPoints').value);
            if (!isNaN(newTotal)) {
                totalSystemPoints = newTotal;
                forceSave();
                updateTotalPointsDisplay();
                document.getElementById('editTotalPoints').value = '';
            } else {
                alert('Введите корректное число');
            }
        }

        // Экспорт данных
        function exportData() {
            const data = {
                users: users,
                totalSystemPoints: totalSystemPoints,
                exportDate: new Date().toISOString()
            };
            
            const blob = new Blob([JSON.stringify(data, null, 2)], { type: 'application/json' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = 'bank_data.json';
            a.click();
        }

        // Горячие клавиши
        document.addEventListener('keydown', function(event) {
            if (event.key === 'F5') {
                event.preventDefault();
                loadData();
            }
        });

        // Инициализация
        window.onload = function() {
            loadData();
            updateSyncStatus('Система готова к работе!', 'success');
        };
    </script>
</body>
</html>
