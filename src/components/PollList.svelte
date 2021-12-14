<script>
  import PollDetails from "./PollDetails.svelte";
  import PollStore from "../store/PollStore";
  //   import { onDestroy, onMount } from "svelte";

  //   export let polls = [];

  //   const unsubscribe = PollStore.subscribe((data) => (polls = data));

  //   onMount(() => {
  //     console.log("component mounted");
  //   });

  //   onDestroy(() => {
  //     console.log("component destroyed");
  //     unsubscribe();
  //   });
</script>

<div class="poll-list">
  {#each $PollStore as poll (poll.id)}
    <div>
      <PollDetails {poll} />
    </div>
  {/each}
</div>

<style>
  .poll-list {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
  }
</style>
