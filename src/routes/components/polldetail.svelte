<script>
    import Card from "../card.svelte";
    import { createEventDispatcher } from "svelte";
    const dispatch = createEventDispatcher();

    $: totalVotes = Number(poll.votesA) + Number(poll.votesB);

    export let poll =[];

    const handlevote = (option,id) => {
        dispatch('vote',{option,id})
    }
</script>
<Card>
<div class="poll">
    <h3>
        { poll.question }
    </h3>
    <!-- total votes -->
    <p>Total votes : { totalVotes }</p>
    <div class="answer" on:click={ () => handlevote('a',poll.id) }>
        <div class="persent percent-a">
            
        </div>
        <span>{ poll.answerA } ({ poll.votesA }) </span>
    </div>

    <div class="answer" on:click={ () => handlevote('b',poll.id) }>
        <div class="persent percent-b">
            
        </div>
        <span>{ poll.answerB } ({ poll.votesB }) </span>
    </div>
</div>
</Card>
<style>
      h3{
    margin: 0 auto;
    color: #555;
  }
  p{
    margin-top: 6px;
    font-size: 14px;
    color: #aaa;
    margin-bottom: 30px;
  }
  .answer{
    background: #fafafa;
    cursor: pointer;
    margin: 10px auto;
    position: relative;
  }
  .answer:hover{
    opacity: 0.6;
  }
  span{
    display: inline-block;
    padding: 10px 20px;
  }
</style>