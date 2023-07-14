<script lang="ts">
	import Countdown from './Countdown.svelte';
    import Found from './Found.svelte';
    import Grid from './Grid.svelte';
    import { levels } from './levels';
    import type { Level } from './levels';
	import { shuffle } from './utils';
	import { onMount } from 'svelte';

    const level = levels[0];

    let size = level.size;
    let grid = createGrid(level);
    let found: string[] = [];
    let duration: number = level.duration;
	let remaining: number = level.duration;
    let playing: boolean = false;

    function createGrid(level: Level) {
        const copy = level.emojis.slice();
        const pairs: string[] = [];

        for (let i = 0; i < (level.size ** 2 / 2); i++) {
            const index = Math.floor(Math.random() * copy.length);
            const emoji = copy[index];

            copy.splice(index, 1);
            pairs.push(emoji);
        }

        pairs.push(...pairs);

        return shuffle(pairs);
    }

    function countdown() {
		const start = Date.now();
		const remaining_at_start = remaining;

		function loop() {
			if (playing) { 
                return;
            }

			requestAnimationFrame(loop);

			remaining = remaining_at_start - (Date.now() - start);

			if (remaining <= 0) {
				playing = false;
				//dispatch('lose');
			}
		}

		loop();
	}

    onMount(countdown);
</script>
<div class="game">
    <div class="info">
        <Countdown {remaining} duration={level.duration}
            on:click={() => {
                // TODO
            }}
        />
    </div>

    <div class="grid-container">
        <Grid {grid} on:found={(e) => {
                found = [...found, e.detail.emoji];
            }} 
            {found}
        />
    </div>

    <div class="info">
        <Found {found} />
    </div>
</div>

<style>
    .game {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        height: 100%;
        font-size: min(1vmin, 0.1rem);
    }

    .info {
        width: 80vmin;
        height: 10vmin;
    }

    .grid-container {
        width: 80vmin;
        height: 80vmin;
        /* background: teal; */
    }
</style>