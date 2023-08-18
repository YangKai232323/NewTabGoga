<script lang="ts">
	import { onMount } from 'svelte';
	let search = '';
	let input: HTMLInputElement;
	let searchList: string[] = JSON.parse(localStorage.getItem('searches') || 'null');
	$: results = searchList.filter((item) => item.includes(search));
	
	$: {
		localStorage.setItem('searches', JSON.stringify(searchList))
	}

	function isElementInList(element: string, list: string[]) {
		if (list.includes(element)) {
			return true;
		}
		return false;
	}

	function onKeyDown(e: any) {
		switch (e.key) {
			case 'Tab':
				console.log('Tab');
				e.preventDefault();
				break;
			case '+':
				if (isElementInList(search, searchList) === false) {
					searchList = [...searchList, search];
					search = '';
				}
				e.preventDefault();
				break;
			case 'Alt':
				e.preventDefault();
				break;
			case 'Enter':
				console.log('Enter');
				let url = `https://google.com/search?q=${encodeURIComponent(search.replaceAll(' ', '+'))}`;
				window.open(url);
				break;

			default:
				if (
					(e.keyCode >= 48 && e.keyCode <= 90) ||
					(e.keyCode >= 96 && e.keyCode <= 111) ||
					(e.keyCode >= 186 && e.keyCode <= 222)
				) {
					input.focus();
				}
				break;
		}
	}
</script>

<div class="main">
	<ul>
		<!-- <li><a href="#">Test</a></li> -->
		{#each results as result}
			<li><p>{result}</p></li>
		{/each}
	</ul>

	<div class="hint">
		<p><kbd>Tab</kbd> for search first variant</p>
		<p><kbd>Enter</kbd> for search your question</p>
		<p><kbd>+</kbd> for add your question to list</p>
	</div>

	<input type="text" placeholder="Search here" bind:value={search} bind:this={input} />
	<a href="https://tasklisttry.pages.dev">Мне повезёт!</a>
</div>

<svelte:window on:keydown={onKeyDown} />

<style>
	.main {
		display: flex;
		justify-content: center;
		align-items: center;
		flex-direction: column;
		gap: 2em;
	}
	kbd {
		font-style: italic;
		font-weight: 900;
		font-size: large;
	}
</style>
