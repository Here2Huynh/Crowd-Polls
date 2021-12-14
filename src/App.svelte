<script>
  import Header from "./components/Header.svelte";
  import Footer from "./components/Footer.svelte";
  import Tabs from "./shared/Tabs.svelte";
  import CreatePollForm from "./components/CreatePollForm.svelte";
  import PollList from "./components/PollList.svelte";

  // tabs
  let tabs = ["Current Polls", "Add New Poll"];
  let activeTab = tabs[0];

  const handleTabChange = (e) => {
    activeTab = e.detail;
  };

  const handleAddPoll = (e) => {
    activeTab = "Current Polls";
  };
</script>

<Header />
<main>
  <Tabs {tabs} {activeTab} on:tabChange={handleTabChange} />
  {#if activeTab === "Current Polls"}
    <PollList />
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
