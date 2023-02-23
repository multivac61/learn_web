<script>
	import { onMount } from 'svelte';

	onMount(() => {
		const letters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';

		// @ts-ignore
		document.querySelector('h1').onmouseover = (event) => {
			let iteration = 0;

			let interval = null;
			clearInterval(interval);

			interval = setInterval(() => {
				event.target.innerText = event.target.innerText
					.split('')
					.map((letter, index) => {
						if (index < iteration || letter === ' ') {
							return event.target.dataset.value[index];
						}

						return letters[Math.floor(Math.random() * 26)];
					})
					.join('');

				if (iteration >= event.target.dataset.value.length) {
					clearInterval(interval);
				}

				iteration += 1 / 3;
			}, 30);
		};

    window.onpointermove = (event) => {
        const { clientX, clientY } = event;

		const blob = document.getElementById('blob');
        if (blob)
            blob.animate(
                {
                    left: `${clientX}px`,
                    top: `${clientY}px`
                },
                { duration: 3000, fill: 'forwards' }
            );
    };
	});
</script>

<div class="body">
	<div id="blob" />
	<div id="blur" />
	<h1 data-value="ANDREA HELGA">ANDREA HELGA</h1>
</div>

<style>
	.body {
		background-color: black;
		height: 100vh;
		margin: 0rem;
		overflow: hidden;
	}

	@keyframes rotate {
		from {
			rotate: 0deg;
		}

		50% {
			scale: 1 1.5;
		}

		to {
			rotate: 360deg;
		}
	}

	#blob {
		background-color: white;
		height: 34vmax;
		aspect-ratio: 1;
		position: absolute;
		left: 50%;
		top: 50%;
		translate: -50% -50%;
		border-radius: 50%;
		background: linear-gradient(to right, aquamarine, red, orange);
		animation: rotate 20s infinite;
		opacity: 0.8;
	}

	#blur {
		height: 100%;
		width: 100%;
		position: absolute;
		z-index: 2;
		backdrop-filter: blur(12vmax);
	}

	h1 {
		font-family: 'Space Mono', monospace;
		font-size: clamp(1rem, 6vw, 6rem);
		color: white;
		padding: 0rem clamp(1rem, 2vw, 3rem);
		border-radius: clamp(0.4rem, 0.75vw, 1rem);
		margin: 0rem;
		position: absolute;
		left: 50%;
		top: 50%;
		translate: -50% -50%;
		z-index: 3;
	}
</style>
