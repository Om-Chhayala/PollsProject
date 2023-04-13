<script>
    import { createEventDispatcher } from "svelte";
    let fields = {question: '', answerA: '', answerB: ''}
    const dispatch = createEventDispatcher();
    import Button from "../button.svelte";

    let errors = {question: '', answerA: '', answerB: ''}
    let valid = false;

    const submithandler = () => {
        valid = true;

        if (fields.question.trim().length < 5){
            valid = false;
            errors.question="It must contain 5 character"
        }else{
            errors.question=""
        }

        if (fields.answerA.trim().length < 1){
            valid = false;
            errors.answerA="It must contain 1 character"
        }else{
            errors.answerA=""
        }

        if (fields.answerB.trim().length < 1){
            valid = false;
            errors.answerB="It must contain 1 character"
        }else{
            errors.answerB=""
        }

        if(valid) {
            let poll = {...fields,votesA:0, votesB:0, id:Math.random()}
            dispatch('add',poll);
        }
    }
</script>

<form on:submit|preventDefault={submithandler}>
    <div class="form-field">
        <div class="la-bel"><label for="question">Poll Question</label><div class="la-bel"></div>
        <input type="text" id="question" bind:value={fields.question}>
    </div>
    <div class="error"> {errors.question} </div>

    <div class="form-field">
        <div class="la-bel"><label for="answer-a">Answer-A</label><div class="la-bel"></div>
        <input type="text" id="answer-a" bind:value={fields.answerA}>
    </div>
    <div class="error"> {errors.answerA} </div>

    <div class="form-field">
        <div class="la-bel"><label for="answer-b">Answer-B</label><div class="la-bel"></div>
        <input type="text" id="answer-b" bind:value={fields.answerB}>
    </div>
    <div class="error"> {errors.answerB} </div>
    <Button type='secondary' flat='true'>Add Poll</Button>
</form>

<style>
    form{
        width: 400px;
        margin: 0 auto;
        text-align: center;
    }
    .form-field{
        margin: 18px auto;
    }
    input{
        width: 100%;
        border-radius: 4px;
        border-style: solid;
    }
    .la-bel{
        margin: 10px auto; 
        text-align: left;
    }
</style>