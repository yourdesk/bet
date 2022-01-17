<script>
  import { getStore } from './hmr-stores';
  import { flip } from 'svelte/animate';
  import Player from './Player.svelte';

  const players = getStore('players', []);
</script>

<div class='flex flex-wrap items-start p-3 justify-center'>
  {#each $players as player (player) }
    <div animate:flip="{{duration: 300}}">
      <Player name={player} />
    </div>
  {/each}
</div>