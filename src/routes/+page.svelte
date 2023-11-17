<script lang="ts">
	let newItem = '';
	let error = '';
	let todoList = [
		{ task: 'Faire les courses', done: false },
		{ task: 'Finir le projet', done: false },
		{ task: 'Aller courir', done: true },
		{ task: 'Lire un livre', done: false },
		{ task: 'Appeler maman', done: true }
	];

	function addToList() {
		if (newItem != '') {
			todoList = [...todoList, { task: newItem, done: false }];
			newItem = '';
			error = '';
		} else {
			error = 'Votre tache est vide, veuillez remplir le champ';
		}
	}

	/**
	 * @param {number} index
	 */
	function goToDone(index) {
		todoList[index].done = true;
	}

	/**
	 * @param {number} index
	 */
	function removeFromList(index) {
		todoList.splice(index, 1);
		todoList = todoList;
	}
</script>

<div class="h-screen main">
	<div class="container">
		<h1>TODO LIST</h1>

		<input bind:value={newItem} type="text" placeholder="Nouvelle tache" />
		<div class="error">
			{error}
		</div>
		<button class="add" on:click={addToList}>Ajouter</button>
		<div class="twoList">
			<div class="todo list">
				<h2>A faire</h2>
				{#each todoList as item, index}
					{#if item.done === false}
						<div class="card cardContainer">
							<div class="delete">
								<button on:click={() => removeFromList(index)}>X</button>
							</div>
							{item.task}
							<div>
								<button class="goTo" on:click={() => goToDone(index)}>></button>
							</div>
						</div>
					{/if}
				{/each}
			</div>
			<div class="done list">
				<h2>Fait</h2>
				{#each todoList as item, index}
					{#if item.done === true}
						<div class="card cardContainer">
							<div class="delete">
								<button on:click={() => removeFromList(index)}>X</button>
							</div>
							<p>{item.task}</p>
						</div>
					{/if}
				{/each}
			</div>
		</div>
	</div>
</div>

<style>
	.main {
		background-color: whitesmoke;
	}

	h1 {
		font-size: 1.5rem;
		font-weight: 700;
	}

	h2 {
		font-size: 1.25rem;
		font-weight: 500;
	}

	.container {
		width: 95vw;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}

	.error {
		color: red;
	}

	.add {
		background-color: grey;
		padding: 10px;
		margin: 10px;
		border-radius: 5px;
	}

	.cardContainer {
		min-height: 150px;
	}

	.goTo {
		color: green;
		font-weight: 700;
		font-size: 1.5rem;
	}

	.delete {
		display: flex;
		justify-content: end;
	}

	.delete button {
		color: red;
		padding: 5px;
		border-radius: 5px;
	}

	.twoList {
		display: flex;
	}

	.list {
		width: 40%;
		min-height: 200px;
		min-width: 500px;
		display: flex;
		flex-direction: column;
		text-align: center;
		padding: 5px;
	}

	.card {
		margin: 5px;
	}
</style>
