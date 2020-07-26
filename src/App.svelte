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
		h3{
			color: hsl(565, 45%, 55% );
			margin-top: auto;
			}
		footer{
			display: flex;
			margin-bottom: auto;
			button{
				padding: 0.5rem;
				background: transparent;
				border: 2px solid  hsl(565, 45%, 55% );
				color:  hsl(565, 45%, 55% );
				font-weight: bold;
				margin-top: 0.5rem;
				cursor: pointer;
				&:hover{
					background: hsl(565, 45%, 55% );
					box-shadow: 2px 2px 0 hsla(565, 45%, 55%, 0.3 );
					color: black;
				}
			}
			button:nth-of-type(1){
				flex: 1;
				margin-right: 0.5rem;
			}
			#tweet-quote, a:visited{
				color:  hsl(565, 45%, 55% );
				&:hover{
					color: black;
				}
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
		box-shadow: inset -4px -4px 0 #a7a7a74d, inset 4px 4px 0 hsla(265, 55%, 0%, 0.3 );
		border-radius: 0.6rem;
		position: relative;
		margin: 0;
		box-sizing: border-box;
		background: hsl(265, 45%, 35% );

	}
</style>

<template>
	<section id="quote-box" class="o-card">
		<h3>Random Genre Generator</h3>
		<dialog id="quote-box">
			{#await data}
				<blockquote>
					waiting..			
				</blockquote>
			{:then genre}
				<h1 id="text">{genre[counter]}</h1>
				<em id="author">binaryjazz</em>
			{:catch error}
				<blockquote>
					Oh no!
				</blockquote>
			{/await}
		</dialog>
		<footer>
			<button classs="button" id="new-quote" on:click={() => counter >= 19 ? counter=0 : counter++  }>New quote</button>
			{#await data then genre}
			<a href={"https://twitter.com/intent/tweet?text=check this new out genre"+genre[counter]+"by gracrys genre generator thanks to binaryjazz api"} target="_blank" id="tweet-quote" class="o-button"><button >&#x1F3B6;</button></a>
			{/await}
		</footer>
	</section>
</template>
