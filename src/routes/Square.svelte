<script lang="ts">
    export let emoji: string;
</script>

<div class="square">
    <span>{emoji}</span>
</div>

<style>
    .square {
        background: yellow;

        display: flex;
        justify-content: center;
        align-items: center;
    }

    span {
        font-size: 10em;
    }
</style>