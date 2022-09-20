<script>
    import Nested from './Nested.svelte';
    import PackageInfo from './PackageInfo.svelte';
    import Thing from './Thing.svelte';
    import { onMount } from "svelte";
    
    let name = 'Gago';
    let src = 'https://images.pexels.com/photos/7703737/pexels-photo-7703737.jpeg?auto=compress&cs=tinysrgb&w=700&h=300&dpr=1'
    let string = `this <i>string</i> contains some <strong>HTML!!!</strong>`;

    let count = 0;
    $: doubled = count * 2;
    
    function handleClick() {
        count += 1;
    }

    function increment() {
        count += 1;
    }

    $: if (count >= 10) {
        alert('10 na gago');
        count = 0;
    }

	let numbers = [1, 2, 3, 4];

	function addNumber() {
		numbers = [...numbers, numbers.length + 1];
	}

	$: sum = numbers.reduce((t, n) => t + n, 0);

    const pkg = {
        name: 'svelte',
        version: 3,
        speed: 'blazing',
        website: 'https://svelte.dev'
    };

    let user = { loggedIn: false };

    function toggle() {
    user.loggedIn = !user.loggedIn;
    }

    let x = 7;

	let cats = [
		{
			id: 'J---aiyznGQ',
			name: 'Keyboard Cat'
		},
		{
			id: 'z_AbfPXTKms',
			name: 'Maru'
		},
		{
			id: 'OUtn3pvWmpg',
			name: 'Henri The Existential Cat'
		}
	];

	let things = [
		{ id: 1, name: 'apple' },
		{ id: 2, name: 'banana' },
		{ id: 3, name: 'carrot' },
		{ id: 4, name: 'doughnut' },
		{ id: 5, name: 'egg' }
	];

	function handleKeyedClick() {
		things = things.slice(1);
	}

    let promise = Object;

    onMount(getNumber);

    async function getNumber() {
		const res = await fetch(
			`https://www.randomnumberapi.com/api/v1.0/random?min=100&max=1000`
		);
		const text = await res.text();
        promise = text;
		if (res.ok) {
			return text;
		} else {
			throw new Error(text);
		}
	}

	function handleAsyncClick() {
		getNumber();
	}

</script>

<p>Part 1: Introduction to Svelte</p>

<p>Intro: First component</p>
<h1>Welcome to {name.toUpperCase()}</h1>

<p>Intro: Dynamic attributes</p>
<img {src} alt="namo" />

<p>Intro: Styling</p>

<p>Intro: Nested components</p>
<Nested answer={23} />

<p>Intro: HTML Tags</p>
<p>{@html string}</p>

<p>Reactivity: Assignments</p>
<button on:click={increment}>
	Clicked {count}
	{count === 1 ? 'time' : 'times'}
</button>

<p>Reactivity: Declarations</p>
<button on:click={handleClick}>
	Clicked {count}
	{count === 1 ? 'time' : 'times'}
</button>
<p>{count} doubled is {doubled}</p>

<p>Reactivity: Statements</p>

<p>Reactivity: Updating arrays and objects</p>
<p>{numbers.join(' + ')} = {sum}</p>
<button on:click={addNumber}>
	Add a number
</button>

<p>Props: Declaring props</p>

<p>Props: Default values</p>
<Nested />

<p>Props: Spread props</p>
<PackageInfo {...pkg} />

<p>Logic: If blocks</p>
{#if user.loggedIn}
	<button on:click={toggle}>
		Log out
	</button>
{/if}

{#if !user.loggedIn}
	<button on:click={toggle}>
		Log in
	</button>
{/if}


<p>Logic: Else blocks</p>
{#if user.loggedIn}
	<button on:click={toggle}>
		Log out
	</button>
{:else}
	<button on:click={toggle}>
		Log in
	</button>
{/if}

<p>Logic: Else-if blocks</p>
{#if x > 10}
	<p>{x} is greater than 10</p>
{:else if 5 > x}
	<p>{x} is less than 5</p>
{:else}
	<p>{x} is between 5 and 10</p>
{/if}

<p>Logic: Each blocks</p>
<h1>The Famous Cats of YouTube</h1>

<ul>
	{#each cats as { id, name }, i}
		<li>
			<a
				target="_blank"
				href="https://www.youtube.com/watch?v={id}"
			>
				{i + 1}: {name}
			</a>
		</li>
	{/each}
</ul>

<p>Keyed each blocks</p>
<button on:click={handleKeyedClick}>
	Remove first thing
</button>

{#each things as thing (thing.id)}
	<Thing name={thing.name} />
{/each}

<!--
You can use any object as the key, as Svelte uses a Map internally
— in other words you could do (thing) instead of (thing.id).
Using a string or number is generally safer, however,
since it means identity persists without referential equality,
for example when updating with fresh data from an API server.    
-->

<p>Await blocks</p>
<button on:click={handleAsyncClick}>
	generate random number
</button>

{#await promise}
	<p>...waiting</p>
{:then number}
	<p>The number is {number}</p>
{:catch error}
	<p style="color: red">{error.message}</p>
{/await}

<p>Events: DOM Events</p>
<!--
    As we've briefly seen already,
    you can listen to any event on
    an element with the on: directive:

    <div on:mousemove={handleMousemove}>
	    The mouse position is {m.x} x {m.y}
    </div>
-->

<p>Events: Inline handlers</p>
<!--
    You can also declare event handlers inline:

    <div on:mousemove="{e => m = { x: e.clientX, y: e.clientY }}">
        The mouse position is {m.x} x {m.y}
    </div>    
-->

<style>
    p {
        color: purple;
        font-family: 'Comic Sans MS', cursive;
        font-size: 1em;
    }
</style>