<script>
	// import component
	import Modal from "./Modal.svelte";

	let name = "Ninja";
	let num = 0;
	let beltColor = "green";

	const increaseOne = () => num++;
	const decreaseOne = () => num--;

	const handleInput = (e) => (beltColor = e.target.value);
	const changeBeltColorRed = () => (beltColor = "red");

	// reactive values
	let firstName = "Idham";
	let lastName = "Adzani";

	$: fullName = `${firstName} ${lastName}`;
	$: {
		console.log(beltColor);
		console.log(fullName);
	}

	let people = [
		{ name: "Yoshi", beltColor: "black", age: 25, id: 1 },
		{ name: "Mario", beltColor: "orange", age: 35, id: 2 },
		{ name: "Luigi", beltColor: "red", age: 15, id: 3 },
	];

	const deletePerson = (id) => {
		people = people.filter((person) => person.id != id);
	};

	let showModal = false;
	const toogleModal = () => (showModal = !showModal);
</script>

<!-- if conditionals -->
{#if num > 10}
	<p>limit 10!</p>
{:else if num > 7}
	<p>mendekati limit</p>
{/if}

<!-- use imported component with props -->
<Modal
	message="Hey, I am a prop value"
	isPromo={true}
	{showModal}
	on:click={toogleModal}
/>
<button on:click={toogleModal}>show modal</button>

<main>
	<h1>Hello {name}!</h1>
	<p>{num}</p>
	<button on:click={increaseOne}>+ 1</button>
	<button on:click={decreaseOne}>- 1</button>

	<!-- binding -->
	<!-- <p style="color: {beltColor}">{beltColor} belt</p> -->
	<!-- one way binding -->
	<!-- <input type="text" on:input={handleInput} value={beltColor} /> -->
	<!-- two way binding -->
	<!-- <input type="text" bind:value={beltColor} /> -->
	<!-- <button on:click={changeBeltColorRed}>change belt color to red</button> -->

	<!-- reactive values -->
	<p>{fullName} - {beltColor}</p>
	<input type="text" bind:value={firstName} />
	<input type="text" bind:value={lastName} />
	<input type="text" bind:value={beltColor} />

	<!-- loop -->
	{#each people as person (person.id)}
		<div>
			<h4>{person.name}</h4>
			{#if person.beltColor === "black"}
				<p><strong>NINJA MASTER</strong></p>
			{/if}
			<p>{person.age} years old, {person.beltColor} belt.</p>
			<button on:click={() => deletePerson(person.id)}>x</button>
		</div>
	{:else}
		<!-- if people has 0 person-->
		<p>There are no people to show...</p>
	{/each}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
