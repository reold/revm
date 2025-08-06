<script lang="ts">
  import EVMAnimated from "./assets/evmtrans.webp";

  let machine = $state({
    id: "23232",
    maxContestants: 4,
  });

  let sessionConfig = $state({
    contestants: [] as { name: string; id: number }[],
  });

  const canAppendContestant = $derived(
    machine.maxContestants > sessionConfig.contestants.length
  );

  const handleAppendContestant = () => {
    if (!canAppendContestant) {
      alert(
        `Machine doesn't support more than ${machine.maxContestants} contestants!`
      );
      return;
    }

    sessionConfig.contestants = [
      ...sessionConfig.contestants,
      { name: "", id: 0 },
    ];
  };
</script>

<main class="overflow-hidden">
  <div
    class="bg-blue-200 text-black px-2 min-h-[40dvh] relative flex flex-col items-center justify-center"
  >
    <h1 class="text-6xl">Reold's <b>Electronic Voting Machine</b></h1>
    <div
      class="absolute h-[45dvh] w-[110dvw] flex flex-col items-end justify-end overflow-hidden"
    >
      <img
        src={EVMAnimated}
        alt="animation of an EVM"
        class="max-h-[35dvh] max-w-[75dvw] opacity-95"
      />
    </div>
  </div>
  <div
    class="w-screen bg-emerald-600 font-light flex flex-row items-center justify-end p-2"
  >
    <p>connected to <b class="font-bold">EVM {machine.id}</b> via WiFi</p>
  </div>
  <div class="flex flex-row items-center justify-around px-1 pt-1">
    <button
      type="button"
      class="inline-flex items-center px-5 py-2.5 text-sm font-medium text-center text-white bg-blue-700 rounded-lg hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
      onclick={handleAppendContestant}
      disabled={!canAppendContestant}
    >
      Add Contestant
      <span
        class="inline-flex items-center justify-center w-4 h-4 ms-2 text-xs font-semibold text-blue-800 bg-blue-200 rounded-full"
      >
        {machine.maxContestants - sessionConfig.contestants.length}
      </span>
    </button>

    <button
      type="button"
      class="focus:outline-none text-white bg-green-700 hover:bg-green-800 focus:ring-4 focus:ring-green-300 font-medium rounded-lg text-sm px-5 py-2.5 dark:bg-green-600 dark:hover:bg-green-700 dark:focus:ring-green-800"
      disabled={sessionConfig.contestants.length <= 1}>Continue</button
    >
  </div>
  <form class="mt-2 space-y-2">
    {#each sessionConfig.contestants as contestant}
      <div class="px-1 flex flex-row justify-center items-center space-x-1">
        <div class="relative min-w-[75%]">
          <input
            type="text"
            id="floating_outlined"
            class="block px-2.5 pb-2.5 pt-4 w-full text-sm text-gray-900 bg-transparent rounded-lg border-1 border-gray-300 appearance-none dark:text-white dark:border-gray-600 dark:focus:border-blue-500 focus:outline-none focus:ring-0 focus:border-blue-600 peer"
            placeholder=" "
            bind:value={contestant.name}
          />
          <label
            for="floating_outlined"
            class="absolute text-sm text-gray-500 dark:text-gray-400 duration-300 transform -translate-y-4 scale-75 top-2 z-10 origin-[0] bg-white dark:bg-black px-2 peer-focus:px-2 peer-focus:text-blue-600 peer-focus:dark:text-blue-500 peer-placeholder-shown:scale-100 peer-placeholder-shown:-translate-y-1/2 peer-placeholder-shown:top-1/2 peer-focus:top-2 peer-focus:scale-75 peer-focus:-translate-y-4 rtl:peer-focus:translate-x-1/4 rtl:peer-focus:left-auto start-1"
            >Contestant's Name</label
          >
        </div>
        <div class="min-w-[25%]">
          <div class="relative flex items-center max-w-[8rem]">
            <button
              type="button"
              id="decrement-button"
              aria-label="decrement"
              onclick={() => contestant.id--}
              class="bg-gray-100 dark:bg-gray-700 dark:hover:bg-gray-600 dark:border-gray-600 hover:bg-gray-200 border border-gray-300 rounded-s-lg p-3 h-11 focus:ring-gray-100 dark:focus:ring-gray-700 focus:ring-2 focus:outline-none"
            >
              <svg
                class="w-3 h-3 text-gray-900 dark:text-white"
                aria-hidden="true"
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 18 2"
              >
                <path
                  stroke="currentColor"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M1 1h16"
                />
              </svg>
            </button>
            <input
              type="text"
              id="quantity-input"
              bind:value={contestant.id}
              aria-describedby="helper-text-explanation"
              class="bg-gray-50 border-x-0 border-gray-300 h-11 text-center text-gray-900 text-sm focus:ring-blue-500 focus:border-blue-500 block w-full py-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
              placeholder="999"
              required
            />
            <button
              type="button"
              id="increment-button"
              aria-label="increment"
              onclick={() => contestant.id++}
              data-input-counter-increment="quantity-input"
              class="bg-gray-100 dark:bg-gray-700 dark:hover:bg-gray-600 dark:border-gray-600 hover:bg-gray-200 border border-gray-300 rounded-e-lg p-3 h-11 focus:ring-gray-100 dark:focus:ring-gray-700 focus:ring-2 focus:outline-none"
            >
              <svg
                class="w-3 h-3 text-gray-900 dark:text-white"
                aria-hidden="true"
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 18 18"
              >
                <path
                  stroke="currentColor"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M9 1v16M1 9h16"
                />
              </svg>
            </button>
          </div>
        </div>
        <!-- <input
          class="min-w-[25%]"
          type="number"
          name="contestant-id"
          id="cont-id"
          min="0"
          bind:value={contestant.id}
        /> -->
      </div>
    {/each}
  </form>
</main>
