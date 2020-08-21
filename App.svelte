<style>
	main {
	  font-family: sans-serif;
	  font-size: 18px;
	}
	textarea {
	  padding: 5px;
	  font-family: sans-serif;
	  font-size: 16px;
	  width: 200px;
	  height: 60px;
	}
	button {
	  background: #ff3e00;
	  color: white;
	  border: none;
	  padding: 8px 12px;
	  border-radius: 2px;
	  margin: 2px;
	}
	button:active {
	  background: #e95858;
	  outline: none;
	}
	td {
	  padding: 5px;
	  text-align: center;
	}
</style>

<script>
	let team1count = 0;
	let team2count = 0;
	let teamMembers = "";
	let team1 = "";
	let team2 = "";

	const reset = () => {
	  team1count = 0;
	  team2count = 0;
	  teamMembers = "";
	  team1 = "";
	  team2 = "";
	};

	const shuffleTeam = () => {
	  let members = teamMembers.split(",");
	  members = members.map(v => v.trim()).filter(v => v !== "");

	  //shuffle
	  for (let i = members.length - 1; i > 0; i--) {
	    const j = Math.floor(Math.random() * (i + 1));
	    [members[i], members[j]] = [members[j], members[i]];
	  }

	  const halfIdx = Math.ceil(members.length / 2);
	  team1 = members.splice(0, halfIdx).join(", ");
	  team2 = members.splice(-halfIdx).join(", ");
	};
</script>

<main>
<button on:click={reset}>
	Reset
</button>
<button on:click={shuffleTeam}>
	Shuffle team
</button>
<hr/>
<table>
	<tr>
		<th>Team members</th>
		<td colspan="3"><textarea style="width:300px; height: 100px" bind:value={teamMembers}/></td>
	</tr>
	<tr>
		<th>Team 1</th>
		<td><textarea bind:value={team1}/></td>
		<td>{team1count}</td>
		<td>
			<button on:click={() => team1count++}>+</button>
			<button on:click={() => team1count == 0 ? 0 : team1count--}>-</button>
		</td>
	</tr>
	<tr>
		<th>Team 2</th>
		<td><textarea bind:value={team2}/></td>
		<td>{team2count}</td>
		<td>
			<button on:click={() => team2count++}>+</button>
			<button on:click={() => team2count == 0 ? 0 : team2count--}>-</button>
		</td>
	</tr>
</table>
</main>