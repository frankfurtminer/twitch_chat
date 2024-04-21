<script>
	import './styles.css';
	import { fade, fly } from 'svelte/transition';
	import tmi from 'tmi.js';
	const channel = import.meta.env.VITE_CHANNEL;

	let messages = [
		{
			name: 'fwefwegwedfw',
			message:
				'gogowoefoweofwoeff fwoef owe w foweof woe ofweofowieeiwieiof wfo woefo woe foweo fowe'
		},
		{ name: 'brorogorgo', message: 'goroto939393939' }
	];

	const client = tmi.Client({
		channels: [channel]
	});

	client.connect();

	client.on('message', (channel, tags, message, self) => {
		messages = [...messages, { name: tags['display-name'], message: message }];
	});
</script>

<div class="chat">
	{#each messages as item}
		<div class="message-box" transition:fade>
			<span class="username">{item.name}:</span>
			<span class="message" transition:fly>{item.message}</span>
		</div>
	{/each}
</div>

<style>
	.chat {
		margin-bottom: 1em;
		margin-right: 1em;
		background-color: transparent;
		padding: 1em;
		border: 5px solid pink;
		border-radius: 1em;
		display: flex;
		flex-direction: column;
		gap: 0.2em;
		max-width: 25em;
	}

	.message-box {
		background-color: lightpink;
		padding: 0.4em;
		border-radius: 0.2em;
	}

	.username {
		font-size: 20px;
		font-family: monospace;
	}

	.message {
		overflow-wrap: anywhere;
		font-size: 20px;
		border: 1px solid black;
		font-family: monospace;
		background-color: orange;
	}
</style>
