<script lang="ts">
	import { get_twemoji_url } from './utils';


    export let emoji: string;
    export let selected: boolean;
    export let found: boolean;
</script>

<div class="square" class:flipped={selected}>
    <button on:click />
    {#if !found}
        <img alt={emoji} src={get_twemoji_url(emoji)} />
    {/if}
</div>

<style>
    .square {
        background: yellow;

        display: flex;
        justify-content: center;
        align-items: center;
    }

    button {
        position: absolute;
        width: 100%;
        height: 100%;    
    }

    .flipped button {
        background: red;
    }

    img {
        width: 12em;
        height: 12em;
        pointer-events: none;
    }
</style>