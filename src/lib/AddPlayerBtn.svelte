<script>
import { getStore } from './hmr-stores';

let playerName;
const players = getStore('players', []);
function addPlayer() {
  if ($players.includes(playerName) || playerName == undefined) {
    return;
  }

  $players = $players.concat(playerName);
  console.log($players)
}
</script>

<button on:click={addPlayer} class='btn btn-sm float-right'>add player</button>
<input bind:value={playerName} class='input input-sm input-bordered float-right mx-3' placeholder='player name'>