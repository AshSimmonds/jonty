<script>
	import CardList from './list/cards.svelte';
	import Card from '$lib/components/card.svelte';

	let basics;
	let holos;
	let galaxies;
	let radiant;
	let basicGallery;
	let vee;
	let veeUltra;
	let veeAlt;
	let veeMax;
	let veeMaxAlt;
	let veeStar;
	let trainerHolo;
	let rainbow;
	let gold;
	let veeGallery;
	let jontyCards;

	const getCards = async () => {
		let promiseArray = [];

		let cardFetch = await fetch('/data.json');
		let cards = await cardFetch.json();
		// @ts-ignore
		window.cards = cards;

		jontyCards = [cards[0], cards[6], cards[12], cards[15], cards[60], cards[18], cards[21], cards[27], cards[24], cards[36], cards[39], cards[42], cards[48], cards[51], cards[63]];

		basics = cards.slice(0, 1);
		holos = cards.slice(6, 7);
		galaxies = cards.slice(12, 13);
		radiant = cards.slice(15, 16);
		basicGallery = cards.slice(60, 61);
		vee = cards.slice(18, 19);
		veeUltra = cards.slice(21, 22);
		veeAlt = [...cards.slice(27, 28), ...cards.slice(33, 34)];
		veeMax = cards.slice(24, 25);
		veeMaxAlt = [cards[36]];
		veeStar = cards.slice(39, 40);
		trainerHolo = cards.slice(42, 43);
		rainbow = cards.slice(48, 49);
		gold = cards.slice(51, 52);
		veeGallery = cards.slice(63, 64);

		return cards;
	};
</script>

<main>
	<header>
		<div class="showcase">
			{#await getCards()}
				loading...
			{:then cards}
				<Card
					img={cards[0].images.large}
					name={cards[0].name}
					number={cards[0].number}
					supertype={cards[0].supertype}
					subtypes={cards[0].subtypes}
					rarity={cards[0].rarity}
					showcase={true}
				/>
			{/await}
		</div>
	</header>

	<h1>Jonty<sup>verse</sup> Trading Simulator</h1>


	<CardList>
		{#await getCards()}
			loading...
		{:then cards}
			{#each jontyCards as card, id}
				<Card
					img={card.images.large}
					name={card.name}
					number={card.number}
					supertype={card.supertype}
					subtypes={card.subtypes}
					rarity={card.rarity}
				/>
			{/each}
		{/await}
	</CardList>

</main>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Roboto+Condensed:wght@700&family=Roboto:ital,wght@0,300;0,700;1,300;1,700&display=swap');

	main {
		color: white;
		padding: 50px;
		max-width: 1200px;
		margin: auto;
	}

	header {
		margin-bottom: 4rem;
		display: grid;
		grid-template-columns: 1fr;
		grid-gap: 30px;
		max-width: 900px;
	}

	@media screen and (min-width: 900px) {
		header {
			grid-template-columns: 60% 1fr;
		}
	}

	.showcase {
		z-index: 99;
		max-width: min(330px, 80vw);
		margin: auto;
	}

	h1 {
		margin-top: 0;
		margin-bottom: 0.25em;
	}

	p {
		margin: 0 0 0.25em;
		line-height: 1.5;
	}

	p.small {
		font-size: 0.875rem;
		opacity: 0.75;
	}

	h1,
	h2,
	h3 {
		font-family: 'Roboto Condensed';
	}

	h2 {
		margin-top: 4em;
		margin-bottom: 0.25em;
	}

	h2 + p,
	h2 + p + p {
		font-style: italic;
		margin-bottom: 1em;
	}

	hr {
		border: none;
		background: white;
		height: 1px;
		opacity: 0.25;
		margin: 1em -1em;
	}

	h1 sup {
		font-weight: 300;
		font-size: 0.5em;
	}

	h2 sup {
		font-weight: 300;
		font-size: 0.75em;
	}

	mark {
		background: #006065;
		color: white;
		font-style: italic;
		font-weight: bold;
		padding-inline: 0.25em;
		border-radius: 3px;
	}

	:global(*) {
		box-sizing: border-box;
	}

	:global(body, html) {
		height: 100%;
		padding: 0;
		margin: 0;
		scroll-behavior: smooth;
	}

	:global(body) {
		font-family: 'Roboto';
		background-color: rgb(57, 60, 66);
	}
</style>
