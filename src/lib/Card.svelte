<script>
  export let item;
</script>

<div class="card mb-3 overflow-hidden" style="max-height: 150px;">
  <div class="row g-0">
    <div class="col-3 col-md-1">
      {#if item.img !== null}
        <img src={item.img} class="rounded-start card-img" alt="Loading" />
      {:else}
        <svg
          class="bd-placeholder-img bd-placeholder-img-lg rounded-start"
          width="100%"
          height="250"
          xmlns="http://www.w3.org/2000/svg"
          role="img"
          aria-label="Placeholder: Responsive image"
          preserveAspectRatio="xMidYMid slice"
          focusable="false"
        >
          <title>Placeholder</title>
          <rect width="100%" height="100%" fill="#868e96" />
          <text x="10%" y="10%" fill="#dee2e6" dy=".3em">Loading</text>
        </svg>
      {/if}
    </div>
    <div class="col-9 col-md-11">
      <div class="card-body">
        <h6 class="card-title text-truncate">
          {item.title}
        </h6>
        <p class="card-text text-truncate">
          {item.message}
        </p>
        <a href={item.url} target="_blank" class="card-text">链接</a>
        <p class="card-text">
          <small class="text-muted">
            {item.update_time}
          </small>
        </p>
      </div>
    </div>
  </div>
</div>

<style>
</style>
