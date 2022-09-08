<script>
    import {flip} from 'svelte/animate';

    export let backgroundColor ='red';
    export let topname= 'Tier List';


    let list = [{name: "a", id: 0}, {name: "", id: 1},
        {name: "awa", id: 2}, {name: "aaas", id: 3}];



    let hovering = false;
    let name ="";

    let id = 0;



    let selectorofitem =  0;

    const repeat = () =>
    {
        {
            list = [];
            console.log("je suis dans la fonction repeat", selectorofitem, "y'a que dalle dans la " , list)
            // pourquoi mon counter au dessus est toujours a zero //
            for (let iterator = 0 ; iterator < selectorofitem; iterator++, id++)



            {

                list.push({name:id, id:id})
                console.log("list name", list.name);
                console.log("nique")
                list = list
              /*  list = [
                    ...list,
                    {
                        id: Math.random(),
                        name,

                    }
                ];
                name = "";*/
                console.log(list);

            }



        }


    }


    const addItem = () => {
        list = [
            ...list,
            {
                id: Math.random(),
                name,

            }
        ];
        name = "";
    };



    const remove = item => {
        list = list.filter(i => i !== item);
    };

    const drop = (event, target) => {
        event.dataTransfer.dropEffect = 'move';
        const start = parseInt(event.dataTransfer.getData("text/plain"));
        const newTracklist = list

        if (start < target) {
            newTracklist.splice(target + 1, 0, newTracklist[start]);
            newTracklist.splice(start, 1);
        } else {
            newTracklist.splice(target, 0, newTracklist[start]);
            newTracklist.splice(start + 1, 1);
        }
        list = newTracklist
        hovering = null
    }

    const dragstart = (event, i) => {
        event.dataTransfer.effectAllowed = 'move';
        event.dataTransfer.dropEffect = 'move';
        const start = i;
        event.dataTransfer.setData('text/plain', start);
    }

</script>


<div>
    <h1> {topname} 🏆️</h1>

    <label> Choisis un nombre <input type="number" bind:value={selectorofitem} min=0 max=25 on:input={ repeat }></label>

    <!--{list} affiche le contenu de la liste-->

    <form on:submit|preventDefault={addItem}>
        <label for="name">Ajouter</label>
        <input id="name" type="text" bind:value={name} />
    </form>

<div class="list">
    {#each list as n, index  (n.name)}
        <div
                class="list-item"
                animate:flip
                draggable={true}
                on:dragstart={event => dragstart(event, index)}
                on:drop|preventDefault={event => drop(event, index)}
                ondragover="return false"
                on:dragenter={() => hovering = index}

                class:is-active={hovering === index}>  <input value={index+1} type="text" id="rank" name="name"
                                                              required minlength="0" maxlenght="20" size="10" >
            <input type="text"  id="ranked" name="name"
                   required minlength="0" maxlenght="20" size="10" >
            <span>{n.name}</span>
<!-- pourquoi il faut attendre pour faire la liste -->

            {n.name}
        </div>
    {/each}
</div>








   <!--     {#each list as item}
            <li class:done={item.done}>

                <input type="checkbox" bind:checked={item.done} />
                <span>{item.name}</span>
                <button on:click={() => remove(item)}>&times;</button>
            </li>
        {/each}
    </ul>-->
</div>



<!-- kfokfofkfofkofkfofko -->

<style>
    .list {
        background-color: white;
        border-radius: 4px;
        box-shadow: 0 2px 3px rgba(10, 10, 10, 0.1), 0 0 0 1px rgba(10, 10, 10, 0.1);
    }

    .list-item {
        display: block;
        padding: 0.5em 1em;
        color: #1a1a1a;
    }

    .list-item:not(:last-child) {
        border-bottom: 1px solid #dbdbdb;
    }

    .list-item.is-active {
        background-color: #280a0a;
        color: #fff;
    }

    span{
        display:none;
    }
</style>

<div style="background-color:{backgroundColor}"> </div>
