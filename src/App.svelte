<!--html lang="en"/>
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head-->

<head>
	<meta charset="UTF-8">
	<title>Pog</title>
</head>

<script>
	let display = 0;
	let operation;

	let hasOperated = false;
	let num1;
	let num2;
	let result;

	function concatDisplay(number) {
		if (hasOperated) {
			clear();
		}

		display = !display ? number : display + number.toString();
	}

	function clear() {
		display = 0;
		result = 0;
		operation = "";
		hasOperated = false;
	}

	function backspace() {
		if (display) {
			display = display.toString().slice(0, -1)
			if (!display) {
				display = 0;
			}
		}
	}

	function setOperand(operand) {
		if(display || display == 0) {
			num1 = display;
			operation = operand;
			display = "";
			hasOperated = false;
		}
	}

	function equals() {
		if (operation) {
			hasOperated ? num1 = display : num2 = display;
			hasOperated = true;
			calculate();
			display = result;
		}
	}

	function calculate() {
		switch (operation) {
			case "+":
				result = Number(num1) + Number(num2);
				break;
			case "-":
				result = num1 - num2;
				break;
			case "*":
				result = num1 * num2;
				break;
			case "/":
				if (num2 != 0)
					result = num1 / num2;
				else 
					alert("Impossível dividir por 0");
				break;
			case "pwY":
				result = Math.pow(num1, num2);
				break;
			default:
				alert("Algo deu errado.");
		}
		hasOperated = true;
		display = result;
	}

	function monoOperators(operand) {
		operation = operand;
		num1 = display;

		switch (operation) {
			case "pw2":
				result = num1 * num1;
				break;
			case "1/x":
				result = 1 / num1;
				break;
			case "sqrt":
				if (num1 >= 0) {
					result = Math.sqrt(num1);
				} else {
					alert("Impossível calcular a raiz de um número negativo.");
				}
				break;
			default:
				alert("Algo deu errado.");
				break;
		}

		display = result;
		hasOperated = true;

	}

	function addComma() {
		if (!display.toString().includes('.')) {
			display = (!display) ? "0." : display + ".";
		}
		hasOperated = false;
	}
</script> 

<main>
	<h1>Calculadora:  </h1>

	<div align="center" name="calculator" width="50%">
		<input type="text" class="display" value="{display}" style="color: {hasOperated ? "yellow" : "white"};" readonly>

		<br><br>
		<button name="button_c" on:click={() => clear()}>C</button>
		<button name="button_ce" on:click={() => display = 0}>CE</button>
		<button name="button_backspace" on:click={() => backspace()}>&#9003;</button>
		<button name="button_div" on:click={() => setOperand("/")}>&divide;</button>
		<button name="button_sqrt" on:click={() => monoOperators("sqrt")}>&Sqrt;</button>
		<br>
		<button name="button_7" on:click={() => concatDisplay(7)}>7</button>
		<button name="button_8" on:click={() => concatDisplay(8)}>8</button>
		<button name="button_9" on:click={() => concatDisplay(9)}>9</button>
		<button name="button_mult" on:click={() => setOperand("*")}>*</button>
		<button name="button_pw2" on:click={() => monoOperators("pw2")}>x<sup>2</sup></button>
		<br>
		<button name="button_4" on:click={() => concatDisplay(4)}>4</button>
		<button name="button_5" on:click={() => concatDisplay(5)}>5</button>
		<button name="button_6" on:click={() => concatDisplay(6)}>6</button>
		<button name="button_minus" on:click={() => setOperand("-")}>-</button>
		<button name="button_pwY" on:click={() => setOperand("pwY")}>x<sup>y</sup></button>
		<br>
		<button name="button_1" on:click={() => concatDisplay(1)}>1</button>
		<button name="button_2" on:click={() => concatDisplay(2)}>2</button>
		<button name="button_3" on:click={() => concatDisplay(3)}>3</button>
		<button name="button_plus" on:click={() => setOperand("+")}>+</button>
		<button name="button_inverse" on:click={() => monoOperators("1/x")}>1/x</button>
		<br>
		<button name="button_0" style="min-width: 125px" on:click={() => concatDisplay(0)}>0</button>
		<button name="button_plusminus" on:click={() => display *= -1}>&PlusMinus</button>
		<button name="button_comma" on:click={() => addComma()}>,</button>
		<button name="button_equals" on:click={() => equals()}>=</button>
	</div>
</main>

<style>
	:root {
		--botao-fundo-padrao: hsl(0, 0%, 20%);
		--botao-fundo-hover: hsl(0, 10%, 80%);

		
	}

	h1 {
		color: blanchedalmond;
		font-weight: normal;
		font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
	}

	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
		font-family: Verdana, Geneva, Tahoma, sans-serif;
	}

	.display {
		text-align: center;
		width: calc(63px * 5);
		height: 50px;
		border-radius: 10px;
		border-color: grey;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
 
	button {
		transition: opacity	1.5s;
		transition: border-radius 1s;
		transition: background-color 0.5s;

		color: hsl(0, 0%, 30%);
		flood-color: hsl(0, 0%, 100%);
		background-color: var(--botao-fundo-padrao);
		size: 10px;
		width: 60px;
		height: 60px;
		font-weight: lighter;
		opacity: 50%;
		border-radius: 20px;
	}
	
	button:hover {
		animation: ease-out;
		opacity: 100%;
		font-weight: bolder;
		border-radius: 10px;
		border-color: hsl(0, 0%, 100%);
		border:  hsl(0, 0%, 20%);
		background-color: var(--botao-fundo-hover);
		transition: background-color 1 ease-in-out;
		color: white;

		transition: font-weight 1s;
		transition: opacity	1s;
		transition: border-radius 1s;
		transition: background-color 1s;
	}
</style>