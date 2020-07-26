<script lang="ts">
	let data = (() => fetch(	"https://binaryjazz.us/wp-json/genrenator/v1/genre/20").then(x => x.json()))()

	let counter = 0
	let disabled

</script>

<style lang="scss">
  section{
		width: 60%;
		height: 40%;
		background: hsl(265, 45%, 15% );
		margin: auto;
		display: flex;
		flex-direction: column;
		padding: 0 20%;
		box-sizing: border-box;
		justify-content: center;
		footer{
			display: flex;
			margin-bottom: auto;
			button:nth-of-type(1){
				flex: 1;
			}
		
		}
		&.o-card{
			box-shadow: 4px 4px 0 hsla(265, 45%, 0%, 0.3 );
			border-radius: 0.6rem;
		}
	}
	dialog{
		width: 100%;
		display: block;
		border: none;
		box-shadow: inset -4px -4px 0 hsla(265, 45%, 0%, 0.3 );
		border-radius: 0.6rem;
		position: relative;
		margin-bottom: 0;
		box-sizing: border-box;
	}
</style>

<template>
	<section id="quote-box" class="o-card">
		<dialog id="author">
			{#await data}
				<blockquote>
					waiting..			
				</blockquote>
			{:then genre}
				<h1>{genre[counter]}</h1>
			{:catch error}
				<blockquote>
					Oh no!
				</blockquote>
			{/await}
		</dialog>
		<footer>
			<button id="new-quote" on:click={() => counter >= 19 ? counter=0 : counter++  }>New quote</button>
			<button id="tweet-quote">popo</button>
		</footer>
	</section>
</template>
