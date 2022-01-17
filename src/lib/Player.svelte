<script>
  import { scale, slide } from 'svelte/transition';
  import { flip } from 'svelte/animate';
  import { getStore } from './hmr-stores';
  import Bet from './Bet.svelte';
  import Divider from './Divider.svelte';

  export let name;

  let addAmt = "1";
  let subAmt = "1";
  let setAmt = "0";

  const chips = getStore(name, 0);
  const bets = getStore(name + '_bets', []);
  const players = getStore('players', []);

  export const increment = () => {
    $chips += parseInt(addAmt);
  };

  export const decrement = () => {
    $chips -= parseInt(subAmt);
  };

  export const set = () => {
    $chips = parseInt(setAmt);
  };

  let betDesc, betValue;

  function addBet() {
    if ($bets.map(x => x.desc).includes(betDesc)) {
      return;
    }

    if (betDesc == undefined || betValue == undefined) {
      return;
    }

    $chips -= parseInt(betValue);
    $bets = $bets.concat({desc: betDesc, value: parseInt(betValue)});
    console.log($bets);
  }

  function removePlayer() {
    $players = $players.filter(p => p !== name);
  }

</script>

<div class='border-2 rounded-md p-2 m-1 text-left' transition:scale>
  <span class='font-bold text-2xl'>{name}</span> <button on:click={removePlayer} class='btn btn-sm float-right'>remove</button>
  <Divider />
  
  <p class='pb-2 text-lg'>Chips: {$chips}</p>

  <button on:click={increment} class='btn btn-sm w-20'>add</button> 
  <input class='input input-sm input-bordered my-1 w-64' placeholder='number' bind:value={addAmt}> <br>

  <button on:click={decrement} class='btn btn-sm w-20'>sub</button> 
  <input class='input input-sm input-bordered my-1 w-64' placeholder='number' bind:value={subAmt}> <br>

  <button on:click={set} class='btn btn-sm w-20'>set</button> 
  <input class='input input-sm input-bordered my-1 w-64' placeholder='number' bind:value={setAmt}> <br>

  <button on:click={addBet} class='btn btn-sm w-20'>add bet</button> 
  <input bind:value={betDesc} placeholder='bet name' class='input input-sm input-bordered my-1 w-40'> 
  <input bind:value={betValue} placeholder='value' class='input input-sm input-bordered my-1 w-22'> <br>

  {#each $bets as bet (bet) }
    <div class='rounded-md mt-3 p-3 border-gray-500 border-2' animate:flip="{{duration:300}}" transition:slide='{{duration: 300}}'>
      <Bet desc={bet.desc} value={bet.value} _for={name} />
    </div>
  {/each}
</div>