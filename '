<script lang="ts">
	import { onMount } from 'svelte';

	const data = `
á ć é ǵ í ḱĺḿńóṕ ŕś ú ẃ ýź
à   è   ì    ǹò     ù ẁ ỳ
â ĉ ê ĝĥîĵ    ô   ŝ û ŵ ŷẑ
ǎ čďě ǧȟǐǰǩľ ňǒ  řšťǔ    žǯ
              ő     ű
ȁ   ȅ   ȉ     ȍ  ȑ  ȕ
ȧḃċḋėḟġḣ    ṁṅȯṗ ṙṡṫ  ẇẋẏż
ạḅ ḍẹ  ḥị ḳḷṃṇọ  ṛṣṭụṿẉ ỵẓ
ä   ë   ï     ö     ü   ÿ
ă   ĕ ğ ĭ     ŏ     ŭ
ȃ   ȇ   ȋ     ȏ  ȓ  ȗ
ã   ẽ   ĩ    ñõ     ũṽ  ỹ
ā   ē ḡ ī     ō     ū   ȳ
  ç ȩ      ļ ņ    ş
ą   ę      į  ǫ     ų
å                   ů ẘ ẙ
æ             œ   ß
`;
	const MODE_NONE = 0;
	const MODE_WAITING = 1;
	const MODE_ACUTE = 2;
	const MODE_GRAVE = 3;
	const MODE_CIRCUMFLEX = 4;
	const MODE_HACEK = 5;
	const MODE_DOUBLE_ACUTE = 6;
	const MODE_DOUBLE_GRAVE = 7;
	const MODE_DOT_ABOVE = 8;
	const MODE_DOT_BELOW = 9;
	const MODE_DIARESIS = 10;
	const MODE_BREVE = 11;
	const MODE_INVERTED_BREVE = 12;
	const MODE_TILDE = 13;
	const MODE_MACRON = 14;
	const MODE_CEDILLA = 15;
	const MODE_OGONEK = 16;
	const MODE_RING_ABOVE = 17;
	const MODE_EXTRA = 18;
	let mode = MODE_NONE;

	let area: HTMLTextAreaElement;

	onMount(() => {
		area.addEventListener('keydown', (e) => {
			if (e.key.length > 1) return;

			if (e.key === '\\') {
				if (mode === MODE_NONE) {
					e.preventDefault();
					mode = MODE_WAITING;
				} else {
					mode = MODE_NONE;
				}
			} else if (mode === MODE_WAITING) {
				switch (e.key) {
					case "'":
						mode = MODE_ACUTE;
						break;
					case '`':
						mode = MODE_GRAVE;
						break;
					case '^':
						mode = MODE_CIRCUMFLEX;
						break;
					case '~':
						mode = MODE_TILDE;
						break;
					case ':':
						mode = MODE_DIARESIS;
						break;
					case '.':
						mode = MODE_DOT_BELOW;
						break;
					case 'd':
						mode = MODE_DOT_BELOW;
						break;
					case 'v':
						mode = MODE_HACEK;
						break;
					case 'u':
						mode = MODE_BREVE;
						break;
					case 'r':
						mode = MODE_RING_ABOVE;
						break;
					case ',':
						mode = MODE_CEDILLA;
						break;
					case 'o':
						mode = MODE_OGONEK;
						break;
					case 'm':
						mode = MODE_MACRON;
						break;
					case 'x':
						mode = MODE_EXTRA;
						break;
					default:
						mode = MODE_NONE;
						break;
				}

				setTimeout(() => {
					area.selectionStart = area.value.length - 1;
					area.selectionend = area.value.length;
				}, 0);
			} else if (mode !== MODE_NONE && e.key !== '\\') {
				const lastChar = e.key.toLowerCase();
				const lines = data.split('\n');
				let foundOne = lines[mode - 1].charAt(lastChar.charCodeAt(0) - 97);

				if (foundOne && foundOne !== ' ') {
					e.preventDefault();
					if (e.key.toUpperCase() === e.key) {
						foundOne = foundOne.toUpperCase();
					}
					area.value = area.value.slice(0, -1) + foundOne;
				}

				mode = MODE_NONE;
			}
		});
	});
</script>

<div class="background">
	<textarea bind:this={area} autofocus class="textarea" />
</div>

<style>
	@import url('https://fonts.googleapis.com/css2?family=EB+Garamond:ital,wght@0,400..800;1,400..800&display=swap');

	.background {
		height: 100vh;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.textarea {
		resize: none;
		border: none;
		box-sizing: border-box;
		outline: none;
		flex: 1;
		width: 100%;
		font-size: 1.2rem;
		padding: 1rem;
		font-family: 'EB Garamond', serif;
	}
</style>
