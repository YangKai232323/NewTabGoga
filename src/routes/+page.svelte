<script lang="ts">
    let search = ''
    let input: HTMLInputElement 
	function onKeyDown(e: any) {
		switch (e.key) {
			case 'Tab':
				console.log('Tab');
				break;
			case 'Enter':
				console.log('Enter');
                let url = `https://google.com/search?q=${encodeURIComponent(search.replaceAll(' ', '+'))}`
                window.open(url)
				break;
            
            default:
                if ((e.keyCode >=48 && e.keyCode<=90) || (e.keyCode >= 96 && e.keyCode <= 111) || (e.keyCode>= 186 && e.keyCode <= 222)) {
                    input.focus()
                    break;
                }
                else {
                    break
                }

		}
	}

</script>

<div class="main">
	<ul>
		<li><a href="#">Test</a></li>
	</ul>

	<div class="hint">
		<p><kbd>Tab</kbd> for search first variant</p>
		<p><kbd>Enter</kbd> for search your question</p>
	</div>

	<input type="text" placeholder="Search here" bind:value={search} bind:this={input}/>
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

