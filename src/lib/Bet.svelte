<script>
  import { getStore } from "./hmr-stores";

  export let desc;
  export let value;
  export let _for;

  const chips = getStore(_for, 0);
  const bets = getStore(_for + '_bets', []);
  const winFormula = getStore('winFormula', 'value * 2');
  
  const won = () => {
    $chips += Math.floor(eval($winFormula));
    remove()
  }

  function refundBet() {
    $chips += value;
    remove()
  }

  function remove() {
    $bets = $bets.filter(b => b.desc !== desc)
  }
</script>

<span class='font-bold text-lg'>{desc}</span> <button on:click={refundBet} class='btn btn-xs float-right'>refund</button> <br>
<p>value: {value}</p>
<button on:click={won} class='btn btn-xs'>won</button>
<button on:click={remove} class='btn btn-xs'>lost</button>
