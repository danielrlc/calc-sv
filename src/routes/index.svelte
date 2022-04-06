<script>
  $: outputNum = 0;
  $: decimalPending = false;
  $: outputStr = decimalPending
    ? outputNum.toString() + "."
    : outputNum.toString();
  $: savedNum = null;
  $: newNumPending = false;
  $: nextOperation = null;

  function handleInput(input) {
    if (typeof input === "number" && (outputNum === 0 || newNumPending)) {
      outputNum = input;
      newNumPending = false;
    } else if (typeof input === "number" && !decimalPending) {
      outputNum = Number(outputNum.toString() + input.toString());
      newNumPending = false;
    } else if (typeof input === "number" && decimalPending) {
      outputNum = Number(outputNum.toString() + "." + input.toString());
      newNumPending = false;
      decimalPending = false;
    } else if (input === ".") {
      decimalPending = true;
    } else if (input === "+") {
      savedNum = outputNum;
      newNumPending = true;
      nextOperation = "+";
    } else if (input === "-") {
      savedNum = outputNum;
      newNumPending = true;
      nextOperation = "-";
    } else if (input === "x") {
      savedNum = outputNum;
      newNumPending = true;
      nextOperation = "x";
    } else if (input === "/") {
      savedNum = outputNum;
      newNumPending = true;
      nextOperation = "/";
    } else if (input === "reset") {
      savedNum = null;
      outputNum = 0;
      newNumPending = false;
      nextOperation = null;
    } else if (input === "del") {
      outputNum = Number(
        outputNum.toString().slice(0, outputNum.toString().length - 1)
      );
      newNumPending = false;
    } else if (input === "=") {
      if (nextOperation === "+") {
        outputNum = savedNum + outputNum;
      } else if (nextOperation === "-") {
        outputNum = savedNum - outputNum;
      } else if (nextOperation === "x") {
        outputNum = Number((savedNum * outputNum).toFixed(6));
      } else if (nextOperation === "/") {
        outputNum = Number((savedNum / outputNum).toFixed(6));
      }
    }
  }
</script>

<div class="bg-blue-801 flex flex-col items-center">
  <div
    class="bg-blue-902 mt-6 px-6 pt-5 pb-3 min-w-[324px] rounded-lg text-white text-3xl text-right"
  >
    {outputStr}
  </div>
  <div
    class="grid grid-cols-4 gap-3 bg-blue-902 p-6 rounded-lg m-6"
    style="grid-template-columns: repeat(4, 60px); grid-template-rows: repeat(5, 60px)"
  >
    <button on:click={(_) => handleInput(7)} class="c-key-regular">7</button>
    <button on:click={(_) => handleInput(8)} class="c-key-regular">8</button>
    <button on:click={(_) => handleInput(9)} class="c-key-regular">9</button>
    <button on:click={(_) => handleInput("del")} class="c-key-blue">DEL</button>
    <button on:click={(_) => handleInput(4)} class="c-key-regular">4</button>
    <button on:click={(_) => handleInput(5)} class="c-key-regular">5</button>
    <button on:click={(_) => handleInput(6)} class="c-key-regular">6</button>
    <button on:click={(_) => handleInput("+")} class="c-key-regular">+</button>
    <button on:click={(_) => handleInput(1)} class="c-key-regular">1</button>
    <button on:click={(_) => handleInput(2)} class="c-key-regular">2</button>
    <button on:click={(_) => handleInput(3)} class="c-key-regular">3</button>
    <button on:click={(_) => handleInput("-")} class="c-key-regular">-</button>
    <button on:click={(_) => handleInput(".")} class="c-key-regular">.</button>
    <button on:click={(_) => handleInput(0)} class="c-key-regular">0</button>
    <button on:click={(_) => handleInput("/")} class="c-key-regular">/</button>
    <button on:click={(_) => handleInput("x")} class="c-key-regular">x</button>
    <button
      on:click={(_) => handleInput("reset")}
      class="c-key-blue u-reset-btn">RESET</button
    >
    <button on:click={(_) => handleInput("=")} class="c-key-red u-equals-btn"
      >=</button
    >
  </div>
</div>
