<script>
  import { tweened } from "svelte/motion";

  import Card from "../shared/Card.svelte";
  import PollStore from "../store/PollStore";
  import Button from "../shared/Button.svelte";

  export let poll;

  $: totalVotes = poll.voteA + poll.voteB;
  $: percentA = Math.floor((100 / totalVotes) * poll.voteA) || 0;
  $: percentB = Math.floor((100 / totalVotes) * poll.voteB) || 0;

  const tweenedA = tweened(0);
  const tweenedB = tweened(0);
  $: tweenedA.set(percentA);
  $: tweenedB.set(percentB);
  // $: console.log($tweenedA, $tweenedB);

  const handleVote = (option, id) => {
    PollStore.update((currentPoll) => {
      let copiedPolls = [...currentPoll];
      let upvotedPoll = copiedPolls.find((poll) => poll.id === id);

      if (option === "a") {
        upvotedPoll.voteA++;
      }
      if (option === "b") {
        upvotedPoll.voteB++;
      }

      return copiedPolls;
    });
  };

  const handleDelete = (pollId) => {
    PollStore.update(
      (currentPolls) =>
        (currentPolls = currentPolls.filter((poll) => poll.id != pollId))
    );
  };
</script>

<Card>
  <div class="poll">
    <h3>{poll.question}</h3>
    <p>Total votes: {totalVotes}</p>
    <div class="answer" on:click={() => handleVote("a", poll.id)}>
      <div class="percent percent-a" style="width: {$tweenedA}%">
        <!--  -->
      </div>
      <span>{poll.answerA} ({poll.voteA})</span>
    </div>
    <div class="answer" on:click={() => handleVote("b", poll.id)}>
      <div class="percent percent-b" style="width: {$tweenedB}%">
        <!--  -->
      </div>
      <span>{poll.answerB} ({poll.voteB})</span>
    </div>
    <div class="delete">
      <Button flat={true} on:click={() => handleDelete(poll.id)}>Delete</Button>
    </div>
  </div>
</Card>

<style>
  h3 {
    margin: 0 auto;
    color: #555;
  }
  p {
    margin-top: 6px;
    font-size: 14px;
    color: #aaa;
    margin-bottom: 30px;
  }
  .answer {
    background: #fafafa;
    cursor: pointer;
    margin: 10px auto;
    position: relative;
  }
  .answer:hover {
    opacity: 0.6;
  }
  span {
    display: inline-block;
    padding: 10px 20px;
  }
  .percent {
    height: 100%;
    position: absolute;
    box-sizing: border-box;
  }
  .percent-a {
    background: rgba(217, 27, 66, 0.2);
    border-left: 4px solid #d91b42;
  }
  .percent-b {
    background: rgba(69, 196, 150, 0.2);
    border-left: 4px solid #45c496;
  }
  .delete {
    margin-top: 30px;
    text-align: center;
  }
</style>
