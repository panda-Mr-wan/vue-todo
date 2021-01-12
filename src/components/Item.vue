<template>
    <li :class="{completed:todo.hasCompleted,editing:todo==this.editedList}">
        <div class="view">
            <input type="checkbox" class="toggle" v-model="todo.hasCompleted">
            <label for="toggle" @dblclick="editTodo(todo)">{{todo.value}}</label>
            <button class='destroy' @click="delTodo(todo.id)"></button>
        </div>
        <input type="text" class="edit" v-model="editedList.value" v-focus="todo===editedList" @keyup.enter="doneEdit" @blur="doneEdit" @keyup.esc="cannelEdit(index)">
    </li>
</template>

<script>
    export default {
        name:"Item",
        props:['todo','index'],
        data(){
            return {
                editedList:"",
                value:""
            }
        },
        methods:{
            delTodo(id){
                this.$parent.todoDatas=this.$parent.todoDatas.filter((value) => {
                    if(value.id==id){
                        return false;
                    }
                    return value;
                })
            },
            editTodo(todo){
                this.value=todo.value;
                this.editedList=todo;
            },
            doneEdit(){
                this.editedList="";
            },
            cannelEdit(index){
                this.$parent.todoDatas[index].value=this.value;
                this.editedList="";
            }
        },
        directives:{
            focus(el){
                el.focus();
            }
        }
    }
</script>

<style lang="scss" scoped>

</style>