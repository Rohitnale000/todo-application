<script>
    export let i;
    export let item;
    export let deleteItem;
    import { scale, slide, fly } from 'svelte/transition';
</script>

<div class="card" style="border: 1px solid blue;" in:slide="{{ x: 500, y: 200, duration:1500}}">
    <div class="card-item">
      <div class="inner-items">
        <span class="item-checkbox">
          {#if item.status === false}
            <input
              type="checkbox"
              bind:checked={item.status}
              class="largeCheck"
            />
          {:else}
            <input
              type="checkbox"
              bind:checked={item.status}
              class="largeCheck"
            />
          {/if}
        </span>

        <span class="item-title"
          ><span class={`newTodo ${item.status ? "strike" : ""}`}
            >{item.Title}</span
          ></span
        >
      </div>
      <span style="margin-right: 50px; font-weight: bold;"
        >{item.date}</span
      >
      <!-- svelte-ignore a11y-click-events-have-key-events -->
      <i
        class="fa fa-trash-o fa-2x"
        style="cursor: pointer;
          margin-right: 10px;"
        on:click={() => {
          deleteItem(i);
        }}
      />
    </div>
  </div>