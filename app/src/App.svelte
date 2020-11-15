<script>
import { onMount } from 'svelte';

	import Main from './Main.svelte';

	const SERVER = "localhost";
	const DEBUG = true;

	document.title = "shitty chat app";

	let logged_in = DEBUG;
	let name = DEBUG ? 'jaddison' : '';

	function login() {
		logged_in = !(name==='')
	}

	function inputKeypress(event) {
		if (event.key === "Enter") { login() }
	}

	let nameInput;
	onMount(function() {
		if (!logged_in) {nameInput.focus(); }
	});

</script>

{#if !logged_in}
<p>Name: </p>
<input bind:value = {name} on:keydown={inputKeypress} type = "text" bind:this = {nameInput}/>
<button on:click = {login}>Log me in!</button>
{:else}
<Main name = {name} SERVER = {SERVER} DEBUG = {DEBUG}/>
{/if}