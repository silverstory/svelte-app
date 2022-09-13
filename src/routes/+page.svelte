<script>
    import Nested from './Nested.svelte';
    import PackageInfo from './PackageInfo.svelte';
    
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

</script>

<p>Part 1: Introduction to Svelte</p>

<p>First component</p>
<h1>Welcome to {name.toUpperCase()}</h1>

<p>Dynamic attributes</p>
<img {src} alt="namo" />

<p>Styling</p>

<p>Nested components</p>
<Nested answer={23} />

<p>HTML Tags</p>
<p>{@html string}</p>

<p>Assignments</p>
<button on:click={increment}>
	Clicked {count}
	{count === 1 ? 'time' : 'times'}
</button>

<p>Declarations</p>
<button on:click={handleClick}>
	Clicked {count}
	{count === 1 ? 'time' : 'times'}
</button>
<p>{count} doubled is {doubled}</p>

<p>Statements</p>

<p> Updating arrays and objects</p>
<p>{numbers.join(' + ')} = {sum}</p>
<button on:click={addNumber}>
	Add a number
</button>

<p>Declaring props</p>

<p>Default values</p>
<Nested />

<p>Spread props</p>
<PackageInfo {...pkg} />

<style>
    p {
        color: purple;
        font-family: 'Comic Sans MS', cursive;
        font-size: 1em;
    }
</style>