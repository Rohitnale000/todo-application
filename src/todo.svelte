<script>
	import Displayall from './Blocks/displayall.svelte';
	import Searchdate from './Blocks/searchdate.svelte';
    import Addlist from "./Blocks/addlist.svelte";
    import { fade, fly } from 'svelte/transition';
  import Complete from './Event/complete.svelte';

  let selectDate = "";
  let searchDate = "";
  let titleOfCourse = "";
  let status = false;
  let iCnt = 0;
  export let itemOfCourse

  const addItem = () => {
    titleOfCourse = titleOfCourse.trim();
    if (titleOfCourse === "") {
      return 0;
    }
    iCnt = 3;
    let objectOfItem = {
      id: itemOfCourse.length + 1,
      Title: titleOfCourse,
      status: status,
      date: selectDate,
    };
    itemOfCourse = [...itemOfCourse, objectOfItem];

    
    itemOfCourse.sort((a, b) => {
      let da = new Date(a.date),
        db = new Date(b.date);
      return da - db;
    });
  };

  const deleteItem = (i) => {
    itemOfCourse.splice(i, 1);
    itemOfCourse = itemOfCourse;
    if (itemOfCourse.length === 0) {
      iCnt = 0;
    }
  };
  const isUnCompleted = () => {
    if (status === false) {
      iCnt = 1;
    }
  };
  const isCompleted = (event) => {
    
    iCnt = event.detail.iCnt;
  };
  const isAll = () => {
    iCnt = 0;
  };
</script>

<div class="container-md">
  <div class="border-dark">
    <h1 class="todotitle">To Do List</h1>
    <div style="text-align: center;">
      <input
        type="text"
        name="todo"
        id="todo"
        placeholder="What needs to be done?"
        required
        bind:value={titleOfCourse}
        on:keypress={(event) => {
          if (event.keyCode == 13) {
            addItem();
            titleOfCourse = "";
            selectDate = "";
          } else if (selectDate === "") {
            const date = new Date();

            let day = date.getDate();
            let month = String(date.getMonth() + 1).padStart(2, "0");
            let year = date.getFullYear();

            let currentDate = `${year}-${month}-${day}`;
            selectDate = currentDate;
          }
        }}
      />
      <input
        type="date"
        id="date"
        bind:value={selectDate}
        on:keypress={(event) => {
          if (event.keyCode === 13) {
            addItem();
            selectDate = "";
          }
        }}
      />
    </div>

    <div class="container">
      <ul>
        {#each itemOfCourse as item, i}
          {#if iCnt === 3}
            <Addlist {item}{deleteItem}{i}/>
          {/if}

          {#if iCnt === 5 &&  item.date === searchDate}
           <Searchdate {deleteItem}{item}{i} />
          {/if}

          {#if iCnt === 2}
            {#if item.status === true}
              <!-- <li>{item.id}______{item.Title}______{'Completed'}______<button on:click={()=>{deleteItem(i)}} class="btn btn-outline-danger btn-lg">Delete</button></li> -->
              <div class="card">
                <div class="card-item">
                  <div class="inner-items">
                    <span class="item-checkbox">
                      {#if item.status === true}
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
                    style="cursor: pointer;"
                    on:click={() => {
                      deleteItem(i);
                    }}
                  />
                </div>
              </div>
            {/if}
          {/if}

          {#if iCnt === 1}
            {#if item.status === false}
              <!-- <li>{item.id}______{item.Title}______{'Incompleted'}______<button on:click={()=>{deleteItem(i)}} class="btn btn-outline-danger btn-lg">Delete</button></li> -->

              <div class="card" transition:fly="{{x:-100, y: 200, duration: 2000 }}">
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
                    style="cursor: pointer;"
                    on:click={() => {
                      deleteItem(i);
                    }}
                  />
                </div>
              </div>
            {/if}
          {/if}

          {#if iCnt === 0 && itemOfCourse.length > 0}
            <!-- display all -->
            <Displayall {deleteItem}{item}{i} />
          {/if}
        {/each}
        <div class="{itemOfCourse.length!=0 ? 'card' : 'newcard'}">
          <div class="card-item">
          <!-- <a href="#" class="isCompleted" on:click={isCompleted}>Completed</a> -->
          <Complete on:message={isCompleted}/>
          <a href="#" class="isCompleted" on:click={isUnCompleted}>Incompleted</a>
          <a href="#" class="isCompleted" on:click={isAll}>Display All</a>

            <input
              id="searchBar"
              placeholder="Search by date"
              onfocus="(this.type='date')"
              bind:value={searchDate}
              on:change={() => {
                iCnt = 5;
              }}
            />
          </div>
        </div>
      </ul>
    </div>
  </div>
</div>


