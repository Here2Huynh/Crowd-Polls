<script>
  import Header from "./components/Header.svelte";
  import Footer from "./components/Footer.svelte";
  import Tabs from "./shared/Tabs.svelte";

  // tabs
  let tabs = ["Current Polls", "Add New Poll"];
  let activeTab = tabs[0];

  const handleTabChange = (e) => {
    activeTab = e.detail;
  };
</script>

<Header />
<main>
  <Tabs {tabs} {activeTab} on:tabChange={handleTabChange} />
  {#if activeTab === "Current Polls"}
    <p>poll list</p>
    <!-- Poll grid -->
  {:else if activeTab === "Add New Poll"}
    <p>add poll</p>
    <!-- form to create poll -->
  {/if}
</main>
<Footer />

<style>
  main {
    max-width: 960px;
    margin: 40px auto;
  }
</style>
