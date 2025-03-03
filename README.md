<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculator</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f4f4f4;
            font-family: Arial, sans-serif;
            margin: 0;
        }

        .calculator {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
            max-width: 400px;
            width: 100%;
            box-sizing: border-box;
        }

        #display {
            width: 100%;
            font-size: 2rem;
            margin-bottom: 10px;
            padding: 10px;
            border: 2px solid #ddd;
            border-radius: 5px;
            text-align: right;
            box-sizing: border-box;
        }

        .buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
        }

        button {
            padding: 20px;
            font-size: 1.5rem;
            border: none;
            border-radius: 5px;
            background: #e0d3d3;
            cursor: pointer;
            transition: background 0.3s;
        }

        button:hover {
            background: #e4e1e1;
        }
    </style>
</head>
<body>
    <div class="calculator">
        <input type="text" id="display" disabled>
        <div class="buttons">
            <button onclick="clearDisplay()">C</button>
            <button onclick="deleteLast()">DEL</button>
            <button onclick="appendValue('/')">/</button>
            <button onclick="appendValue('*')">*</button>
            <button onclick="appendValue('7')">7</button>
            <button onclick="appendValue('8')">8</button>
            <button onclick="appendValue('9')">9</button>
            <button onclick="appendValue('-')">-</button>
            <button onclick="appendValue('4')">4</button>
            <button onclick="appendValue('5')">5</button>
            <button onclick="appendValue('6')">6</button>
            <button onclick="appendValue('+')">+</button>
            <button onclick="appendValue('1')">1</button>
            <button onclick="appendValue('2')">2</button>
            <button onclick="appendValue('3')">3</button>
            <button onclick="calculateResult()">=</button>
            <button onclick="appendValue('0')">0</button>
            <button onclick="appendValue('00')">00</button>
            <button onclick="appendValue('.')">.</button>
            <button onclick="appendValue('%')">%</button> 
        </div>
    </div>
    <script>
        function appendValue(value) {
            document.getElementById('display').value += value;
        }

        function clearDisplay() {
            document.getElementById('display').value = '';
        }

        function deleteLast() {
            var display = document.getElementById('display');
            display.value = display.value.slice(0, -1);
        }

        function calculateResult() {
            var display = document.getElementById('display');
            try {
                if (display.value.includes('%')) {
                    var values = display.value.split('%');
                    if (values.length === 2) {
                        display.value = (parseFloat(values[0]) * parseFloat(values[1]) / 100).toString();
                    } else {
                        display.value = 'Error';
                    }
                } else {
                    display.value = eval(display.value);
                }
            } catch (error) {
                display.value = 'Error';
            }
        }

        // Capture keypress events
        document.addEventListener('keydown', function(event) {
            var key = event.key;
            if (key >= '0' && key <= '9' || key === '.' || key === '/' || key === '*' || key === '-' || key === '+' || key === '%') {
                appendValue(key);
            } else if (key === 'Enter') {
                calculateResult();
            } else if (key === 'Backspace') {
                deleteLast();
            } else if (key === 'Escape') {
                clearDisplay();
            }
        });
    </script>  
</body>
</html>
