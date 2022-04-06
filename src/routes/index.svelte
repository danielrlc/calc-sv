<script>
  let buttons = [
    "7",
    "8",
    "9",
    "DEL",
    "4",
    "5",
    "6",
    "+",
    "1",
    "2",
    "3",
    "-",
    ".",
    "0",
    "/",
    "x",
    "RESET",
    "=",
  ];

  function addInput(entry) {
    console.log(entry);
  }
</script>

<div
  class="grid grid-cols-4 gap-3 bg-blue-902 p-4 h-[667px] w-[375px]"
  style="grid-template-columns: repeat(4, 60px); grid-template-rows: repeat(5, 60px)"
>
  {#each buttons as button, i}
    <button
      class="bg-orange-500 rounded-md border-b-4 border-orange-600 pt-2 text-gray-900 {i ===
        3 || i === 16
        ? 'text-lg pt-1 bg-blue-800 text-white border-blue-801'
        : 'text-[1.5rem]'} {i === 16 && 'u-reset-btn'} {i === 17 &&
        'u-equals-btn bg-red-800 border-red-900 text-white'}"
      on:click={(_) => addInput(button)}>{button}</button
    >
  {/each}
</div>
