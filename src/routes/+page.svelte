<script>
    
    import Header from "./components/header.svelte";
    import Footer from "./components/footer.svelte";
    import Createformpoll from "./components/createformpoll.svelte";
    import Tabs from "./tabs.svelte";
    import Polllist from "./components/polllist.svelte";
    // tabs

    let items = ['Current Polls','Add new poll'];
    let activeItem = 'Current Polls';

    const tabChange = (e) => {
        activeItem = e.detail;
    }

    let polls = [{
        id:1,
        question:'Python or JavaScript',
        answerA:'Python',
        answerB:'JavaScript',
        votesA:0,
        votesB:0
    }];

    const handleAdd = (e) => {
        let poll = e.detail;
        polls = [poll,...polls];
        console.log(polls);
        activeItem = 'Current Polls';
    }

    const handlevote = (e) => {
        const {id,option} = e.detail;
        let copiedpolls = [...polls];
        let upvotedpoll = copiedpolls.find((poll) => poll.id == id);
        if(option === 'a'){
            upvotedpoll.votesA = upvotedpoll.votesA + 1;
        }
        if(option === 'b'){
           upvotedpoll.votesB = upvotedpoll.votesB + 1;
        } 
        polls = copiedpolls;
    }


</script>

<Header/>

<main>
    <Tabs {activeItem} {items} on:tabchange={tabChange}/>
    {#if activeItem == 'Current Polls'}
        <Polllist {polls} on:vote={handlevote} />
    {:else if activeItem == 'Add new poll'}    
        <Createformpoll on:add={handleAdd}/>
    {/if}    
</main>

<Footer />

<style>
    p {
        max-width: 960px;
        margin: 40px auto;
    }
</style>