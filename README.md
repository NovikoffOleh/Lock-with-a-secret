<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Кодовый замок</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 50px;
            background-color: #f8f8f8;
        }
        #game-container {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            display: inline-block;
        }
        input {
            width: 40px;
            font-size: 20px;
            text-align: center;
            margin: 5px;
        }
        button {
            padding: 10px;
            font-size: 18px;
            margin-top: 10px;
            cursor: pointer;
        }
        #result {
            margin-top: 20px;
            font-weight: bold;
        }
    </style>
</head>
<body>

    <div id="game-container">
        <h2>Отгадай 3-значный код</h2>
        <p>У вас есть <strong id="attempts-left">9</strong> попыток.</p>
        
        <input type="number" id="digit1" min="0" max="9">
        <input type="number" id="digit2" min="0" max="9">
        <input type="number" id="digit3" min="0" max="9">
        
        <br>
        <button onclick="checkCode()">Проверить</button>
        
        <p id="result"></p>
    </div>

    <script>
        let secretCode = generateCode(); // Генерируем случайный код
        let attempts = 9;

        function generateCode() {
            return [
                Math.floor(Math.random() * 10),
                Math.floor(Math.random() * 10),
                Math.floor(Math.random() * 10)
            ];
        }

        function checkCode() {
            if (attempts <= 0) return;

            let digit1 = parseInt(document.getElementById('digit1').value);
            let digit2 = parseInt(document.getElementById('digit2').value);
            let digit3 = parseInt(document.getElementById('digit3').value);

            if (isNaN(digit1) || isNaN(digit2) || isNaN(digit3)) {
                alert("Введите все три цифры!");
                return;
            }

            let guess = [digit1, digit2, digit3];
            let correctPositions = 0;
            let correctNumbers = 0;

            // Проверяем, сколько цифр угадано
            for (let i = 0; i < 3; i++) {
                if (guess[i] === secretCode[i]) {
                    correctPositions++;
                } else if (secretCode.includes(guess[i])) {
                    correctNumbers++;
                }
            }

            attempts--;
            document.getElementById('attempts-left').textContent = attempts;

            if (correctPositions === 3) {
                document.getElementById('result').innerHTML = "<span style='color: green;'>Поздравляем! Код угадан 🎉</span>";
                attempts = 0; // Завершаем игру
            } else if (attempts === 0) {
                document.getElementById('result').innerHTML = `<span style='color: red;'>Вы проиграли! Код был: ${secretCode.join('')}</span>`;
            } else {
                document.getElementById('result').innerHTML = `Угадано цифр: ${correctNumbers}, на своих местах: ${correctPositions}`;
            }
        }
    </script>

</body>
</html>
