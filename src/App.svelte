<script>
  import Navbar from "./Navbar.svelte";
  import Player from "./Player.svelte";
  import AddPlayer from "./AddPlayer.svelte";


  let players = [
	  {
		  name: "John Doe",
		  points: 53
	  }, 
	  {
		  name: "Sam Smith",
		  points: 45
	  },
	  {
		  name: "Sara Wilson",
		  points: 34
	  }
  ]

  const addPlayer = (e) => {
	  const newPlayer = e.detail;
	  players = [...players, newPlayer];
  }

  const removePlayer = (e) => {
	  players = players.filter(player => player.name !== e.detail);
  }

  const sortHighest = () => {
	  players = players.sort((a, b) => b.points - a.points);
  }

  const sortLowest = () => {
	  players = players.sort((a, b) => a.points - b.points);
  }
</script>

<Navbar />
<div class="container"> 
	<AddPlayer on:addplayer={addPlayer}/>
	<button class='sort-highest' on:click={sortHighest}>
		Sort Highest
	</button>
		<button class='sort-lowest' on:click={sortLowest}>
		Sort Lowest
	</button>
	{#if players.length === 0}
		<p>No Players</p>
	{:else}
		{#each players as player}
			<Player name={player.name} points={player.points} 
				on:removeplayer={removePlayer}/>
		{/each}
	{/if}
</div>