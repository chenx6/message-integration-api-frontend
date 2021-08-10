<script>
  import "bootstrap/dist/css/bootstrap.min.css";
  import "bootstrap";

  import ZoneList from "./lib/ZoneList.svelte";
  import Header from "./lib/Header.svelte";

  const apiURL = "http://localhost:8000"//`${location.protocol}//${location.host}`;
  let routers = [];
  let currRouter;

  
  const limit = 10;
  let currStart = 0;
  let hasNewPage = true;
  let items = [];

  let scrollY, innerHeight;

  const getJson = async (url) => {
    let response = await fetch(url);
    let json = await response.json();
    return json;
  };

  const getContent = async () =>
    await getJson(
      `${apiURL}${currRouter.path}?start=${currStart}&limit=${limit}`
    );

  const newTab = async (index) => {
    currStart = 0;
    hasNewPage = true;
    currRouter = routers[index];
    const json = await getContent();
    items = [...json.items];
  };

  const nextPage = async () => {
    currStart += 10;
    const json = await getContent();
    if (json.items.length === 0) {
      hasNewPage = false;
    }
    items = [...items, ...json.items];
  };

  (async () => {
    routers = await getJson(`${apiURL}/api/routers`);
    currRouter = routers[0];
    const json = await getContent();
    items = [...json.items];
  })();

  $: {
    // https://stackoverflow.com/questions/3898130/check-if-a-user-has-scrolled-to-the-bottom
    let scrollHeight = document.body.scrollHeight;
    // console.log(scrollY, innerHeight, scrollHeight);
    if (scrollY + innerHeight === scrollHeight && hasNewPage) {
      nextPage();
    }
  }
</script>

<svelte:window bind:scrollY bind:innerHeight />

<main>
  <Header />
  <div class="container">
    <div class="row p-1">
      <div class="col">
        <ul class="nav nav-tabs" role="navigation">
          {#each routers as router, i}
            <li class="nav-item">
              <button class="nav-link" on:click={() => newTab(i)}>
                {router.name}
              </button>
            </li>
          {/each}
        </ul>
      </div>
    </div>
    {#if routers.length !== 0 && items.length !== 0}
      <ZoneList {items} />
    {/if}
  </div>
</main>

<style>
</style>
