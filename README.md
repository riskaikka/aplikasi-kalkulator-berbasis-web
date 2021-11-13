# aplikasi-kalkulator-berbasis-web

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculator</title>
    <link rel="stylesheet" href="stylesheet.css">
</head>
<body>
    <div class="calculator">
        <input type="text" class="calculator-screen" value="0" disabled />
        <div class="calculator-keys">
            <div class="row">
                <button class="all-clear">AC</button>
                <button class="percentage">%</button>
                <button class="operator" value="/">&divide;</button>
            </div>
            <div class="row">
                <button class="number" value="7">7</button>
                <button class="number" value="8">8</button>
                <button class="number" value="9">9</button>
                <button class="operator" value="*">&times;</button>
            </div>
            <div class="row">
                <button class="number" value="4">4</button>
                <button class="number" value="5">5</button>
                <button class="number" value="6">6</button>
                <button class="operator" value="-">-</button>
            </div>
            <div class="row">
                <button class="number" value="1">1</button>
                <button class="number" value="2">2</button>
                <button class="number" value="3">3</button>
                <button class="operator" value="+">+</button>
            </div>
            <div class="row">
                <button class="number zero-btn" value="0">0</button>
                <button class="decimal" value=".">.</button>
                <button class="equal-sign">=</button>
            </div>
        </div>
    </div>
    <script type="text/javascript" src="script.js"></script>
</body>
</html>

body {
    background-repeat: no-repeat;
    background-position: center;
}
.calculator {
    text-align: center;
    margin: 0 auto;
    padding-top: 50px;
    width: 400px;
    opacity: 80%;
}

.calculator-screen {
    width: 100%;
    height: 100px;
    background-color: #252525;
    color: #fff;
    text-align: right;
    font-size: 36px;
    border: none;
    padding: 0 20px;
    box-sizing: border-box;
}

.calculator-keys {
    width: 100%;
}

.row {
    display: flex;
}

button {
    height: 80px;
    background-color: gray;
    border: 1px solid black;
    font-size: 32px;
    color: #fff;
    width: 25%;
    outline: none;
}

.all-clear, .zero-btn {
    width: 50%;
}

.operator, .equal-sign {
    background-color: orange;
}

button:hover {
    background-color: darkgray;
}

.operator:hover, .equal-sign:hover {
    background-color: darkorange;
}

let prevNumber = ''
let calculationOperator = ''
let currentNumber = ''

const calculatorScreen = document.querySelector('.calculator-screen')

const updateScreen = (number) => {
    calculatorScreen.value = number
}

const numbers = document.querySelectorAll(".number")

numbers.forEach((number) => {
    number.addEventListener("click", (event) => {
        console.log(event.target.value)
        updateScreen(currentNumber)
    })
})

const inputNumber = (number) => {
    if (currentNumber === '0') {
        currentNumber = number
    } else {
        currentNumber += number
    }
}

const operators = document.querySelectorAll(".operator")

operators.forEach((operator) => {
    operator.addEventListener("click", (event) => {
        inputOperator(event.target.value)
    })
})

const inputOperator = (operator) => {
    if (calculationOperator === ''){
        prevNumber = currentNumber
    }
    calculationOperator = operator
    currentNumber = '0'
}

const calculate = () => {
    let result = ''
    switch(calculationOperator) {
        case "+":
            result = parseFloat(prevNumber) + parseFloat(currentNumber)
            break
        case "-":
            result = parseFloat(prevNumber) - parseFloat(currentNumber)
            break
        case "*":
            result = parseFloat(prevNumber) * parseFloat(currentNumber)
            break
        case "/":
            result = parseFloat(prevNumber) / parseFloat(currentNumber)
            break
        default:
            break
    }
    currentNumber = result
    calculationOperator = ''
}

const equalSign = document.querySelector('.equal-sign')

equalSign.addEventListener('click', () => {
    calculate()
    updateScreen(currentNumber)
})

numbers.forEach((number) => {
    number.addEventListener("click", (event) => {
        inputNumber(event.target.value)
        updateScreen(currentNumber)
    })
})

const clearBtn = document.querySelector('.all-clear')

clearBtn.addEventListener('click', () => {
    clearAll()
    updateScreen(currentNumber)
})

const clearAll = () => {
    prevNumber = ''
    calculationOperator = ''
    currentNumber ='0'
}

const decimal = document.querySelector('.decimal')

inputDecimal = (dot) => {
    if(currentNumber.includes('.')) {
        return
    }
    currentNumber += dot
}

decimal.addEventListener('click', (event) => {
    inputDecimal(event.target.value)
    updateScreen(currentNumber)
})

inputPercentage = (percentage) => {
    if(currentNumber.includes('%')) {
        return
    }
    currentNumber = currentNumber / 100
}

const percentage = document.querySelector('.percentage')
percentage.addEventListener('click', (event) => {
    inputPercentage(event.target.value)
    updateScreen(currentNumber)
})
