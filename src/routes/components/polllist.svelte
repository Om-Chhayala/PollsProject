<script>
    import Polldetail from "./polldetail.svelte";
    export let polls = [];
</script>

<div class="poll-list">
    {#each polls as poll (poll.id)}
        <div>
            <Polldetail {poll} on:vote />
        </div>
    {/each}
</div>

<style>
    .poll-list{
        display: grid;
        grid-template-columns: 1fr 1fr;
        grid-gap:20px;
    }
</style>