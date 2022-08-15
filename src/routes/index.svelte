<script lang="ts">
	let containerToMove: HTMLDivElement;
	let wheelScroll = 0;

	function scroll(event: WheelEvent) {
		if (event.wheelDelta >= -1) {
			wheelScroll -= event.deltaY;
			containerToMove.scroll({ left: -wheelScroll, behavior: 'smooth' });
		} else {
			wheelScroll += event.deltaY;
			containerToMove.scroll({ left: wheelScroll, behavior: 'smooth' });
		}
	}
</script>

<svelte:window on:wheel={scroll} />

<div id="scroll-container">
	<div id="note">Horizontal scroll on vertical scroll.</div>
	<div id="moving-container-wrapper">
		<div bind:this={containerToMove} id="moving-container">
			Hello. Scroll down (or up) with your mousewheel and witness the text just move. Hello. Scroll
			down (or up) and witness the text just move. Hello. Scroll down (or up) with your mousewheel
			and witness the text just move.
		</div>
	</div>
	<div id="description">
		Added an event listener on mousewheel event that checks the WheelEvent's wheelDelta to determine
		the mousewheel scroll direction (either up or down). If wheelDelta is >= -1, I scroll the text
		container to the left by the deltaY of the WheelEvent. Else, I scroll to the right.
	</div>
	<div id="note">
		Works for <b>desktop only</b> (because you gotta have a mousewheel, sorry).
	</div>
</div>

<style>
	:global(body, html) {
		height: 100%;
		margin: 0;
		font-family: 'Gilroy';
		font-style: normal;
		font-weight: 800;
	}

	:global(#sveltekit-container) {
		height: 100%;
	}

	#scroll-container {
		display: flex;
		justify-content: center;
		align-items: center;
		flex-direction: column;
		height: 100%;
	}

	#moving-container-wrapper {
		border-top: black 1px solid;
		border-bottom: black 1px solid;
		padding: 8px 0px;
		width: 300px;
	}

	#moving-container {
		transition: 0.2s ease;
		overflow-x: hidden;
		white-space: nowrap;
	}

	#description {
		padding: 24px 0px;
		font-weight: 300;
		text-align: center;
		line-height: 1.5;
		max-width: 300px;
	}

	#note {
		font-weight: 300;
		text-align: center;
		line-height: 1.5;
		max-width: 300px;
		padding-bottom: 16px;
	}
</style>
