<template>
    <div>
        <ul>
            <li v-for="(todoItem, index) in propsdata" v-bind:key="todoItem.item" class="shadow">
                <i class="checkBtn fas fa-check" v-bind:class="{checkBtnCompleted: todoItem.complated}" 
                    v-on:click="toggleComplete(todoItem)"></i>
                <span v-bind:class="{textCompleted: todoItem.textCompleted}"> {{ todoItem.item }} </span>
                <span class="removeBtn" v-on:click="removeTodo(todoItem, index)"> 
                    <i class="fas fa-trash-alt">-</i>
                </span>
            </li>
        </ul>
    </div>
</template>

<script> 
export default {
    props: ['propsdata'],
    methods: {
        removeTodo: function(todoItem, index) {  
            this.$emit('removeItem', todoItem, index);

        },
        toggleComplete: function(todoItem) {
            todoItem.completed = !todoItem.completed;
            localStorage.removeItem(todoItem.item);
            localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
        }
    },
}


</script>

<style scoped>
ul {
    list-style-type: none;
    padding-left: 0px;
    margin-top: 0;
    text-align: left;
}
li {
    display: flex;
    min-height: 50px;
    height: 50px;
    line-height: 50px;
    margin: 0.5rem 0;
    padding:0 0.9rem;
    background: white;
    border-radius:5px;
}
.removeBtn {
    margin-left: auto;
    color: #de4343;
}
.checkBtn {
    line-height: 45px;
    color: #62acde;
    margin-right: 5px;
}
.checkBtnCompleted {
    color: #b3adad;
}
.textComplete {
    text-decoration: line-through;
    color: #b3adad;
}
</style>