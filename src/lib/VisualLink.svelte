<script>
    import { onMount } from 'svelte';

    // node counter
    let nodeCounter = 0;
    let decrCounter = 0;
    let nodeValue;

    let allLines = {}

    // create new node 

    const linkNodes = async (start , end)=>{
        const startEl = document.querySelector(`[data-nodeid="${start}"]`)
        const endEl = document.querySelector(`[data-nodeid="${end}"]`)
        console.log(startEl , endEl);
        let line = new LeaderLine(
            startEl,
            endEl,
            {hide: true},
        );
      setTimeout(()=>{
        line.setOptions({
            color: 'orange',
            size: 3 , 
            dash: {animation: true} , 
            endPlug: 'arrow2' , 
            endSocket: 'auto',
            animOptions: 
            {
                duration: 100, 
                timing: [0.58, 0, 0.42, 1]
            },
            positionByWindowResize : false
        })
        line.show('draw');
        
       } , 350)

        let lineObj = {}
        lineObj[`${start}_to_${end}`] = line
        allLines = {...allLines , ...lineObj}

    
    }


    const changeLinePos = ()=>{
        console.log(allLines);
        Object.keys(allLines).forEach(key=>{
            allLines[key].position();
        })
    }
    
    const hideLine = (start , end)=>{
        const objectKey = `${start}_to_${end}`
        const line = allLines[objectKey]

        line.hide()
    }

    // remove new node class
    const removeClass = (el)=>{
        setTimeout(()=>{
            el.classList.remove("new-node")
        },300)
    }

  
 
    const createNode = (val , next , elId) => {
        // new node
        const newNode = `
        <div class="node new-node" data-nodeid="${elId}">
            <!-- value -->
            <div class="value">
                ${val}
            </div>
            <!-- value -->
            <div class="address">
                ${next}
            </div>
        </div>
        `
        return newNode
    }
    

      // add node in the end
    const addEnd = () =>{
        
        // get first element value
        let parentNode = document.querySelector(`[data-nodeid="${nodeCounter}"]`)

        
        // create node
        const elem = createNode(nodeValue , 'null' , nodeCounter+1);

        // get last element adress
        let lastNodeAdress = parentNode.children[1]

        // change prev address
        lastNodeAdress.innerHTML = `@${nodeValue}`

        // add in end
        parentNode.insertAdjacentHTML('afterend',elem)

        // link node 
        linkNodes(nodeCounter , nodeCounter+1)

        // remove new node class
        removeClass(parentNode)

        changeLinePos()

        nodeCounter++
    }

    // add in the start
    const addStart = () =>{
        // get first element value
        let parentNode = document.querySelector(`[data-nodeid="${decrCounter}"]`)


        let firstNodeVal = parentNode.children[0].innerHTML

        const elem = createNode(nodeValue , `@${firstNodeVal}`,decrCounter-1);

        // insert the element before target element

        parentNode.insertAdjacentHTML('beforebegin',elem)

        // link node 
        linkNodes(decrCounter-1 , decrCounter)

        // remove new node class
        removeClass(parentNode)
        // change all lines position
        
        decrCounter--;
        
        changeLinePos()
    }

    // add before
    let elementValue;

    const addBefore = ()=>{
        // get the node
        let allNodes = document.querySelectorAll('.value')

        // check if exist
        allNodes.forEach((e)=>{
            if(parseInt(e.innerHTML) === elementValue){
                const node = e.parentElement
                // address
                const prevAddress = node.children[1];

                const nodeId = parseInt(node.getAttribute('data-nodeid'));

                // get the next element

                const nextEl = document.querySelector(`[data-nodeid="${nodeId+1}"]`)

                // next address
                const nextAddress = nextEl.children[1];


                // create node
                const elem = createNode(nodeValue , nextAddress.innerHTML , nodeId+3);

                // change prev address

                prevAddress.innerHTML = `@${nodeValue}`

                node.insertAdjacentHTML('afterend' , elem)

                hideLine(nodeId , nodeId+1)
                // link prev with new
                linkNodes(nodeId , nodeId+3)

                // link new with next
                linkNodes(nodeId+3 , nodeId+1)
                changeLinePos()
            };
        })
    }

</script>

<main>
    <input type="number" bind:value={nodeValue}>
    <button on:click={addEnd}>in end</button>
    <button on:click={addStart}>in start</button>
    <div>
        <input type="number" placeholder="node" bind:value={elementValue}>
        <input type="number" placeholder="node value" bind:value={nodeValue}>
        <button on:click={addBefore}>Add</button>
    </div>
    <div class="visual-body">
        <!-- nodes -->
        <div class="node" data-nodeid="0">
            <!-- value -->
            <div class="value">
                50
            </div>
            <!-- value -->
            <div class="address" >
                null
            </div>
        </div>
    </div>
</main>

<style>
    main{
        height: 100%;
    }
    .visual-body{
        display: flex;
        align-items: center;
        height: 100%;
        width: 90%;
        margin: 0 auto;
    }
       /* animation for new elemnts */
    @keyframes append-animate {
        from {
            transform: scale(0);
            opacity: 0;
        }
        to {
            transform: scale(1);
            opacity: 1;	
        }
    }

    :global(.new-node){
        animation: append-animate .3s linear;
    }
    :global(.node){
        border-top: 2px solid black;
        border-bottom: 2px solid black;
        border-right: 2px solid black;
        display: flex;
        align-items: center;
        margin-right: 5rem;
        
    }

    :global(.node div){
        padding: 1rem;
        border-left: 2px solid black;
        font-weight: 600;
    }

 
</style>