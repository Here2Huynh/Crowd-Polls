<script>
  import Header from "./components/Header.svelte";
  import Footer from "./components/Footer.svelte";
  import Tabs from "./shared/Tabs.svelte";
  import CreatePollForm from "./components/CreatePollForm.svelte";
  import PollList from "./components/PollList.svelte";

  // tabs
  let tabs = ["Current Polls", "Add New Poll"];
  let activeTab = tabs[0];

  let polls = [
    {
      id: 1,
      question: "Python or Javascript",
      answerA: "Python",
      answerB: "Javascript",
      voteA: 9,
      voteB: 15,
    },
  ];

  const handleTabChange = (e) => {
    activeTab = e.detail;
  };

  const handleAddPoll = (e) => {
    polls = [...polls, e.detail];
    activeTab = "Current Polls";
    console.log(polls);
  };
</script>

<Header />
<main>
  <Tabs {tabs} {activeTab} on:tabChange={handleTabChange} />
  {#if activeTab === "Current Polls"}
    <PollList {polls} />
  {:else if activeTab === "Add New Poll"}
    <CreatePollForm on:addPoll={handleAddPoll} />
  {/if}
</main>
<Footer />

<style>
  main {
    max-width: 960px;
    margin: 40px auto;
  }
</style>
