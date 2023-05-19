<script setup>
import { reactive } from "vue";
import InputNew from "./inputNew.vue";

    let boards = reactive([
        {
            id: crypto.randomUUID(),
            name: "tablero 1",
            items: [
                {
                    id: crypto.randomUUID(),
                    title: "Feature de archivos",
                },
                {
                   id: crypto.randomUUID(),
                   title: "Resolver bug", 
                }
            ]
        },
        {
            id: crypto.randomUUID(),
            name: "tablero 2",
            items: [
                {
                    id: crypto.randomUUID(),
                    title: "Mandar reporte",
                },
                {
                   id: crypto.randomUUID(),
                   title: "Code review", 
                }
            ]
        }
    ])

function handleNewItem(text,board){
    console.log(text.value, board.id, board.name)
    board.items.push({
        id: crypto.randomUUID(),
        title: text.value,
    })
}
function handleNewBoard(){
    const name = prompt("Name of the board")
    if(!!name){
        boards.push({
            id: crypto.randomUUID(),
            name: name,
            items: [],
        })
    }
}

</script>

<template>
    <nav>
        <ul>
            <li><a href="#" @click.prevent="handleNewBoard">Create boards</a></li>
        </ul>
    </nav>

    <div class="boards-container">
        <div class="boards">
            <div class="board" v-for="board in boards" :key="board.id">
                <div>{{ board.name}}</div>
                <InputNew @on-new-item="(text) => handleNewItem(text, board)" />
                <div class="items">
                    <div class="item" v-for="item in board.items" :key="item.id">
                        {{ item.title }}
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>

    .boards{
        display: flex;
        gap: 10px;
    }
    .board{
        background: #efefef;
        padding: 10px;
    }
    .items{
        display: flex;
        flex-direction: column;
        gap: 5px;
    }
    .item{
        background-color: white;
        padding: 10px;
        box-sizing: border-box;        
    }

</style>
