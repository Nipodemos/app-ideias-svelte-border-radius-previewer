<script lang="ts">
	let borderTopLeftRadius = 0;
	let borderTopRightRadius = 0;
	let borderBottomLeftRadius = 0;
	let borderBottomRightRadius = 0;
	$: style = `
    width: 100px;
    height: 100px;
    background-color:red;
    border-top-left-radius: ${borderTopLeftRadius}%;
    border-top-right-radius: ${borderTopRightRadius}%;
    border-bottom-left-radius: ${borderBottomLeftRadius}%;
    border-bottom-right-radius: ${borderBottomRightRadius}%;
  `;

	let button: HTMLButtonElement;
	let timeout: NodeJS.Timeout;
	function copyToClipboard() {
		clearTimeout(timeout);
		navigator.clipboard.writeText(style);
		button.innerText = 'Copiado!';
		timeout = setTimeout(() => {
			button.innerText = 'Copiar para área de transferência';
		}, 2000);
	}
</script>

<main>
	<div {style} class="box" />
	<div>
		<label for="top-left">Canto Superior Esquerdo</label>
		<input name="top-left" bind:value={borderTopLeftRadius} type="range" min="1" max="100" />
		<span>{borderTopLeftRadius}%</span>
	</div>
	<div>
		<label for="top-left">Canto Superior Direito</label>
		<input name="top-right" bind:value={borderTopRightRadius} type="range" min="1" max="100" />
		<span>{borderTopRightRadius}%</span>
	</div>
	<div>
		<label for="top-left">Canto Inferior Esquerdo</label>
		<input name="bottom-left" bind:value={borderBottomLeftRadius} type="range" min="1" max="100" />
		<span>{borderBottomLeftRadius}%</span>
	</div>
	<div>
		<label for="top-left">Canto Inferior Direito</label>
		<input
			name="bottom-right"
			bind:value={borderBottomRightRadius}
			type="range"
			min="1"
			max="100"
		/>
		<span>{borderBottomRightRadius}%</span>
	</div>

	<h4>CSS resultante:</h4>

	<pre class="code-block">
    {style}
  </pre>
	<button bind:this={button} on:click={copyToClipboard}>Copiar para área de transferência</button>
</main>

<style>
	.code-block {
		background-color: darkslategray;
		padding: 20px;
		font-size: 1.1rem;
		font-weight: bold;
		border-radius: 10px;
		color: white;
	}
</style>
