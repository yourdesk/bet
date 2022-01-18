<script>
  import { getStore } from './lib/hmr-stores';
  import AddPlayerBtn from './lib/AddPlayerBtn.svelte';
  import PlayerList from './lib/PlayerList.svelte';
  import './lib/TailwindCSS.svelte'

  const players = getStore('players', ['ryan', 'logan'])
  const winFormula = getStore('winFormula', 'value * 2')
</script>

<section class='p-3'>
  <span class='text-3xl font-bold'>BetMaker</span>
  <a href='/components/modal#setWinFormula' class='btn btn-sm float-right ml-2'>set win formula</a> 
  <div id='setWinFormula' class='modal'>
    <div class='modal-box'>
      <p>this will determine how many chips a player gets back when they win. all values are rounded down </p>
      <p class='font-mono bg-gray-800 rounded-md p-2'>
        $chips -> current number of chips <br /> 
        value -> value of the bet
      </p>
      <textarea class='textarea textarea-bordered mt-2 w-full font-mono' bind:value={$winFormula}></textarea>
      <div class='modal-action'>
        <a href='/components/modal#' class='btn btn-sm'>Close</a>
      </div>
    </div>
  </div>

  <AddPlayerBtn />
  <hr class='border-t-2 my-3'>
  <PlayerList />
</section>

