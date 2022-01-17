<script>
  import { getStore } from './lib/hmr-stores';
  import AddPlayerBtn from './lib/AddPlayerBtn.svelte';
  import PlayerList from './lib/PlayerList.svelte';
  import './lib/TailwindCSS.svelte'

  const players = getStore('players', ['ryan', 'logan'])
</script>

<section class='p-3'>
  <span class='text-3xl font-bold'>BetMaker</span> <AddPlayerBtn />
  <hr class='border-t-2 my-3'>
  <PlayerList />
</section>

