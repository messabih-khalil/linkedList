<script>
    // tabs
    let operation = ["Create" , "Insert" , "Delete" , "Search"];

    let activeTabs = operation[0]

    // cahnge active method
    const changeActive = (e) =>{
        activeTabs = e;
    }

    let dropDown = '';

    const showDropDown = (drop) => {
        (dropDown === '')? 
        dropDown = drop : 
        dropDown = ''
        
    }
</script>

<main>
    <!-- tabs operation -->
    <ul>
        {#each operation as o }
            <button on:click={()=> changeActive(o)}>
                <li class:active={o === activeTabs} >{o}</li>
            </button>
        {/each}
    </ul>
    <!-- operation body -->
    <div class="operation-body">
        {#if activeTabs === "Create"}
            <div class="operation-body-action">
                <button class="operation-body-action-title" on:click={()=> showDropDown("randomList")}>
                    <p>
                        Random List
                    </p>
                    <!-- icon -->
                    <i class="ri-arrow-drop-down-line"></i>
                </button>
                <!-- operation drop down -->
                <div class="operation-dropdown" class:show-dropdown={dropDown === "randomList"}>
                    <div class="input"> 
                        <input type="number" placeholder="List Length">
                    </div>
                    <button>Generate</button>
                </div>
            </div>
            <!-- User define -->
            <div class="operation-body-action">
                <button class="operation-body-action-title" on:click={()=> showDropDown("userCreate")}>
                    <p>
                        User Define List
                    </p>
                    <!-- icon -->
                    <i class="ri-arrow-drop-down-line"></i>
                </button>
                <!-- operation drop down -->
                <div class="operation-dropdown" class:show-dropdown={dropDown === "userCreate"}>
                    <div class="input" > 
                        <input type="text" placeholder="[1,5,7,81,45,12,10,11]">
                    </div>
                    <button>Send</button>
                </div>
            </div>
        {/if}
        {#if activeTabs === "Insert"}
        <div class="operation-body-action">
            <button class="operation-body-action-title" on:click={()=> showDropDown("insertHead")}>
                <p>
                    Add in first
                </p>
                <!-- icon -->
                <i class="ri-arrow-drop-down-line"></i>
            </button>
            <!-- operation drop down -->
            <div class="operation-dropdown" class:show-dropdown={dropDown === "insertHead"}>
                <div class="input"> 
                    <input type="number" placeholder="Value">
                </div>
                <button>Add</button>
            </div>
        </div>
        <!-- in the end -->
        <div class="operation-body-action">
            <button class="operation-body-action-title" on:click={()=> showDropDown("insertTail")}>
                <p>
                    Insert at the end
                </p>
                <!-- icon -->
                <i class="ri-arrow-drop-down-line"></i>
            </button>
            <!-- operation drop down -->
            <div class="operation-dropdown" class:show-dropdown={dropDown === "insertTail"}>
                <div class="input" > 
                    <input type="text" placeholder="Value">
                </div>
                <button>Add</button>
            </div>
        </div>

        <!-- Before -->
        <div class="operation-body-action">
            <button class="operation-body-action-title" on:click={()=> showDropDown("insertBefore")}>
                <p>
                    Insert Before
                </p>
                <!-- icon -->
                <i class="ri-arrow-drop-down-line"></i>
            </button>
            <!-- operation drop down -->
            <div class="operation-dropdown" class:show-dropdown={dropDown === "insertBefore"}>
                <div class="input" > 
                    <input type="text" placeholder="Value">
                </div>
                <button>Add</button>
            </div>
        </div>
          <!-- After -->
          <div class="operation-body-action">
            <button class="operation-body-action-title" on:click={()=> showDropDown("InsertAfter")}>
                <p>
                    Insert After
                </p>
                <!-- icon -->
                <i class="ri-arrow-drop-down-line"></i>
            </button>
            <!-- operation drop down -->
            <div class="operation-dropdown" class:show-dropdown={dropDown === "InsertAfter"}>
                <div class="input" > 
                    <input type="text" placeholder="Value">
                </div>
                <button>Add</button>
            </div>
        </div>
        {/if}
        {#if activeTabs === "Delete"}
            <!-- Delete first elements -->
        <div class="operation-body-action">
            <button class="operation-body-action-title" on:click={()=> showDropDown("deleteHead")}>
                <p>
                    Delete Head
                </p>
                <!-- icon -->
                <i class="ri-arrow-drop-down-line"></i>
            </button>
            <!-- operation drop down -->
            <div class="operation-dropdown" class:show-dropdown={dropDown === "deleteHead"}>
                <div class="input" > 
                    <input type="text" placeholder="Value">
                </div>
                <button>Delete</button>
            </div>
        </div>
        <!-- Delete last elements -->
        <div class="operation-body-action">
            <button class="operation-body-action-title" on:click={()=> showDropDown("deleteTail")}>
                <p>
                    Delete Tail
                </p>
                <!-- icon -->
                <i class="ri-arrow-drop-down-line"></i>
            </button>
            <!-- operation drop down -->
            <div class="operation-dropdown" class:show-dropdown={dropDown === "deleteTail"}>
                <div class="input" > 
                    <input type="text" placeholder="Value">
                </div>
                <button>Delete</button>
            </div>
        </div>

        <!-- Delete specified element -->
        <div class="operation-body-action">
            <button class="operation-body-action-title" on:click={()=> showDropDown("deleteElements")}>
                <p>
                    Delete specified element
                </p>
                <!-- icon -->
                <i class="ri-arrow-drop-down-line"></i>
            </button>
            <!-- operation drop down -->
            <div class="operation-dropdown" class:show-dropdown={dropDown === "deleteElements"}>
                <div class="input" > 
                    <input type="text" placeholder="Value">
                </div>
                <button>Delete</button>
            </div>
        </div>
        {/if}
        {#if activeTabs === "Search"}
            <!-- Search element -->
        <div class="operation-body-action">
            <button class="operation-body-action-title" on:click={()=> showDropDown("search")}>
                <p>
                    Find an item
                </p>
                <!-- icon -->
                <i class="ri-arrow-drop-down-line"></i>
            </button>
            <!-- operation drop down -->
            <div class="operation-dropdown" class:show-dropdown={dropDown === "search"}>
                <div class="input" > 
                    <input type="text" placeholder="Value">
                </div>
                <button>Search</button>
            </div>
        </div>
        {/if}
    </div>
</main>

<style>
    main{
        background-color: grey;
        height: 100%;
        overflow-y: scroll;
    }
    ul{
        display: flex;
        align-items: center;
        border-bottom: 2px solid black;
        padding: 1rem;
    }
    ul button{
        background-color: transparent;
        border: none;
    }
    li{
        list-style: none;
        margin-right: 1.5rem;
        font-size: 1.2rem;
        font-weight: 500;
        cursor: pointer;
    }
    .active{
        color: greenyellow;
    }

    .operation-body{
        padding: 2rem 1rem;
    }

    .operation-body-action{
        margin-bottom: 1.5rem;
    }

    .operation-body-action-title{
        display: flex;
        justify-content: space-between;
        align-items: center;
        font-size: 1.1rem;
        padding: 1rem;
        border: 1px solid white;
        color: white;
        font-weight: 600;
        cursor: pointer;
        background-color: black;
        width: 100%;
    }

    .operation-dropdown{
        padding: 1rem;
        background-color: blueviolet;
        width: 100%;
        display: none;
    }
    .show-dropdown{
        display: inline-block;
    }

    .operation-body .input{
        background-color: grey;
        width: 100%;
    }

    .operation-body .input input{
        padding: .5rem;
        width: 100%;
        font-size: 1.1rem;
        outline: none;
    }

    .operation-dropdown button{
        padding: .5rem 3rem;
        margin-top: 1rem;
        font-weight: 600;
        background-color: greenyellow;
        border: none;
        font-size: 1.05rem;
        cursor: pointer;
    }
   
</style>