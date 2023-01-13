<script>
  let titleOfCourse = "";
  let status = false;
  let itemStatus = "";
  let iCnt = 0;
  let itemOfCourse = [];
  const addItem = () => {
	titleOfCourse = titleOfCourse.trim();
	if(titleOfCourse===""){
		return;
	}
	console.log("dhjkjhf");
    iCnt = 3;
    let objectOfItem = {
      id: itemOfCourse.length + 1,
      Title: titleOfCourse,
      status: status,
      itemStatus: itemStatus,
    };
    itemOfCourse = [...itemOfCourse, objectOfItem];
  };

  const deleteItem = (i) => {
    itemOfCourse.splice(i, 1);
    itemOfCourse = itemOfCourse;
	if(itemOfCourse.length===0){
		iCnt = 0;
	}
  };

  const isUnCompleted = () => {
    if (status === false) {
      iCnt = 1;
    }
  };
  const isCompleted = () => {
    iCnt = 2;
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
			  titleOfCourse=""
			  
            }
            {
            }
          }} 
        />
      </div>

      <div class="container">
        <ul>
          {#if iCnt === 3}
            {#each itemOfCourse as item, i}
              <div class="card">
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
            {/each}
            <div class="card">
              <div class="card-item">
                <a href="#" class="isCompleted" on:click={isCompleted}
                  >Completed</a
                >
                <a href="#" class="isCompleted" on:click={isUnCompleted}
                  >Incompleted</a
                >
                <a href="#" class="isCompleted" on:click={isAll}>Display All</a>
              </div>
            </div>
          {/if}
        </ul>
        <ul>
          {#if iCnt === 2}
            <h3>Completed Course list</h3>
            {#each itemOfCourse as item, i}
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
                        {/if}
                      </span>
                      <span class="item-title"
                        ><span class={`newTodo ${item.status ? "strike" : ""}`}
                          >{item.Title}</span
                        ></span
                      >
                    </div>
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
            {/each}
            <div class="card">
              <div class="card-item">
                <a href="#" class="isCompleted" on:click={isCompleted}
                  >Completed</a
                >
                <a href="#" class="isCompleted" on:click={isUnCompleted}
                  >Incompleted</a
                >
                <a href="#" class="isCompleted" on:click={isAll}>Display All</a>
              </div>
            </div>
          {/if}
        </ul>
        <ul>
          {#if iCnt === 1}
            <h3>Incompleted Course list</h3>
            {#each itemOfCourse as item, i}
              {#if item.status === false}
                <!-- <li>{item.id}______{item.Title}______{'Incompleted'}______<button on:click={()=>{deleteItem(i)}} class="btn btn-outline-danger btn-lg">Delete</button></li> -->

                <div class="card">
                  <div class="card-item">
                    <div class="inner-items">
                      <span class="item-checkbox">
                        {#if item.status === false}
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
            {/each}
            <div class="card">
              <div class="card-item">
                <a href="#" class="isCompleted" on:click={isCompleted}
                  >Completed</a
                >
                <a href="#" class="isCompleted" on:click={isUnCompleted}
                  >Incompleted</a
                >
                <a href="#" class="isCompleted" on:click={isAll}>Display All</a>
              </div>
            </div>
          {/if}
        </ul>
        <ul>
          {#if iCnt === 0 && itemOfCourse.length > 0}
            <h3>All Course list</h3>
            {#each itemOfCourse as item, i}
              <div class="card">
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
            {/each}
            <div class="card">
              <div class="card-item">
                <a href="#" class="isCompleted" on:click={isCompleted}
                  >Completed</a
                >
                <a href="#" class="isCompleted" on:click={isUnCompleted}
                  >Incompleted</a
                >
                <a href="#" class="isCompleted" on:click={isAll}>Display All</a>
              </div>
            </div>
          {/if}
        </ul>
      </div>
    </div>
  </div>

<style>
  #todo {
    font-size: 18px;
    margin: 10px;
    width: 49%;
    height: 60px;
	border-radius: 25px;
	text-align: center;
  }
  ul {
    list-style-type: none;
    line-height: 55px;
	margin-left: -75px;
  }

  .strike {
    text-decoration: line-through;
  }

  .container {
    display: flexbox;
    margin-inline: auto;
	
  }
  .todotitle {
    text-align: center;
    background: #ffffff14;
    backdrop-filter: blur(3px);
    color: transparent;
    text-shadow: 0 0 0px rgb(32, 31, 31);
	font-weight: bold;
	
  }
  .itemList {
    margin: 30px;
    margin-left: 30%;
  }
  .largeCheck {
    width: 20px;
    height: 20px;
  }
  .statusCompleted {
    width: 20px;
    height: 20px;
  }
  .btn-div {
    margin: 10px;
    margin-left: 390px;
  }
  .card-item {
    display: flex;
    align-items: center;
  }

  .container {
    margin-inline: 350px;
  }
  .card {
    width: 50%;
  }

  .item-id {
    margin: 10px;
    font-size: 24px;
  }
  .item-title {
    margin: 20px;
    font-size: 24px;
  }
  .item-checkbox {
    font-size: 20px;
    margin: 40px;
  }
  .isCompleted {
    font-size: 20px;
    margin: 10px;
  }

  .isCompleted:hover {
    color: black;
    cursor: pointer;
    border: 1px solid rgba(255, 173, 158, 0.679);
	border-radius: 20px;
	background: transparent;
  }
  .inner-items {
    width: 90%;
  }
</style>
