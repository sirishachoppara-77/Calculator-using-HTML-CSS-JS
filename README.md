# Calculator-using-HTML-CSS-JS
#GeeksKeplerInternship
//HTMLCODE
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Calculator</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

    <div class="calculator">
        <input type="text" id="display" class="display" disabled />
        <div class="buttons">
            <button class="btn" onclick="appendNumber(7)">7</button>
            <button class="btn" onclick="appendNumber(8)">8</button>
            <button class="btn" onclick="appendNumber(9)">9</button>
            <button class="btn" onclick="operation('+')">+</button>
            
            <button class="btn" onclick="appendNumber(4)">4</button>
            <button class="btn" onclick="appendNumber(5)">5</button>
            <button class="btn" onclick="appendNumber(6)">6</button>
            <button class="btn" onclick="operation('-')">-</button>

            <button class="btn" onclick="appendNumber(1)">1</button>
            <button class="btn" onclick="appendNumber(2)">2</button>
            <button class="btn" onclick="appendNumber(3)">3</button>
            <button class="btn" onclick="operation('*')">*</button>

            <button class="btn" onclick="appendNumber(0)">0</button>
            <button class="btn" onclick="clearDisplay()">C</button>
            <button class="btn" onclick="calculate()">=</button>
            <button class="btn" onclick="operation('/')">/</button>
        </div>
    </div>

    <script src="script.js"></script>
</body>
</html>

//CSS CODE
/* style.css */
body {
    font-family: Arial, sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
    background-color: #f4f4f4;
}

.calculator {
    width: 250px;
    padding: 20px;
    border-radius: 10px;
    background-color: #fff;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.display {
    width: 100%;
    height: 40px;
    margin-bottom: 10px;
    text-align: right;
    font-size: 24px;
    padding: 5px;
    background-color: #f9f9f9;
    border: 1px solid #ddd;
    border-radius: 5px;
}

.buttons {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
}

button {
    padding: 15px;
    font-size: 18px;
    background-color: #f0f0f0;
    border: 1px solid #ddd;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.2s ease;
}

button:hover {
    background-color: #e0e0e0;
}

button:active {
    background-color: #ccc;
}
//JS code
// script.js
let currentInput = '';
let previousInput = '';
let operator = null;

const display = document.getElementById('display');

// Append number to current input
function appendNumber(number) {
    currentInput += number.toString();
    display.value = currentInput;
}

// Set operator for operation
function operation(op) {
    if (currentInput === '') return;  // Don't do anything if there's no number
    if (previousInput !== '') {
        calculate();  // If there's a previous operation, calculate it first
    }
    operator = op;
    previousInput = currentInput;
    currentInput = '';
}

// Calculate the result based on the operator
function calculate() {
    let result;
    const prev = parseFloat(previousInput);
    const current = parseFloat(currentInput);
    if (isNaN(prev) || isNaN(current)) return;  // Ignore if inputs are invalid

    switch (operator) {
        case '+':
            result = prev + current;
            break;
        case '-':
            result = prev - current;
            break;
        case '*':
            result = prev * current;
            break;
        case '/':
            if (current === 0) {
                alert("Cannot divide by zero!");
                result = '';
            } else {
                result = prev / current;
            }
            break;
        default:
            return;
    }

    currentInput = result.toString();
    operator = null;
    previousInput = '';
    display.value = currentInput;
}

// Clear the display and reset values
function clearDisplay() {
    currentInput = '';
    previousInput = '';
    operator = null;
    display.value = '';
}


