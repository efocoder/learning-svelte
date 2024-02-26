<script lang="ts">
    const numbers : string[] = ["1", "2", "3", "4", "5", "6", "7", "8", "9", "0", "."];
    const operators : string[] = ["/", "x", "+", "-","="];

    let selecterdOperator: string = "";
    let display: string = "";
    let firstNumber: string = "";
    let secondNumber: string = "";
    let isResults = false;


    const handleOperationClick  = (operator: string) =>  {
      if (!firstNumber) return;
      if (operator === '=') {
        if (!secondNumber) return;
        const firstNum = parseInt(firstNumber);
        const secondNum = parseInt(secondNumber);

        let results = "";

        switch (selecterdOperator) {
          case "/":
            results = (firstNum / secondNum).toFixed(2)
            break;
          case "+":
            results = (firstNum + secondNum).toFixed(2)
            break;
          case "*":
            results = (firstNum * secondNum).toFixed(2)
            break;
          case "-":
            results = (firstNum - secondNum).toFixed(2)
            break;
          default:
            break;
        }
        display = results;
        isResults = true ;
      }
      selecterdOperator = operator;
      
    }

    const clearData = () => {
      firstNumber = "";
      secondNumber ="";
      selecterdOperator = "";
      display = "";
      isResults = false;
    }

    const handleNumberClick = (number: string) => {
      if(isResults) {
        clearData();
      }

      if(display == "" && number === "0") return;
      if(number === '.' && display.includes('.')) return;
      

      if (!selecterdOperator) {
        if (display === "" && number === ".") {
          firstNumber = "0."
          return display = firstNumber
        } 
         firstNumber = `${firstNumber}${number}`
         return display = firstNumber;
      }else {
         if (display === "" && number === ".") {
          secondNumber = "0."
          return display = secondNumber
        } 
        secondNumber = `${secondNumber}${number}`
         return display = secondNumber;
      }
  
      // display = `${display}${number}`
    }

</script>

<main>
    <div class="calculator">
        <div class="results">
          {display}
        </div>
        <div class="digits"> 
            <div class="numbers">
                <button class="btn btn-xlg" on:click={clearData}>C</button>
                {#each  numbers as number (number)}
                    <button class={`btn ${number === '0' ? 'btn-lg' : ''}`}
                    on:click={() => handleNumberClick(number)}
                    >
                    {number}
                  </button>
                {/each}            
            </div> 
            <div class="operations">
              {#each operators as operator (operator)}
                <button class={`btn ${selecterdOperator === operator ? 'btn-silver' : 'btn-orange'}`} on:click={() => handleOperationClick(operator) }>{operator}</button>
              {/each}
            </div>
        </div>
    </div> 
</main>


<style>
  main {
    width: 100vw;
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .calculator {
    background-color: rgb(28, 28, 28);
    width: 240px;
    padding: 15px;
    border-radius: 7px;
  }
  .digits {
    display: flex;
  }
  .operations {
    display: flex;
    flex-direction: column;
  }
  .numbers {
    display: flex;
    flex-wrap: wrap;
    width: 200px;
  }
  .btn {
    width: 50px;
    height: 50px;
    border-radius: 100px;
    background-color: rgb(114, 113, 113);
    font-size: 20px;
    font-weight: bold;
    color: white;
    margin: 5px;
    border: none;
  }
  .btn-lg {
    width: 110px;
  }
  .btn-orange {
    background-color: orange;
  }
  .btn-silver {
    background-color: silver;
  }
  .btn-xlg {
    width: 170px;
  }
  .results {
    height: 60px;
    color: white;
    font-size: 50px;
    display: flex;
    flex-direction: row-reverse;
    margin-right: 10px;
  }
</style>
