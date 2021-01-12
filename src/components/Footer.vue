<template>
    <footer class="footer">
        <span class="todo-count">
            <strong>{{todoNum}}</strong>
            <span v-if="todoNum<=1">item left</span>
            <span v-else>items left</span>
        </span>
        <ul class="filters">
            <li><a href="#/all" @click="changeView('all')" :class="{selected:view==='all'}">All</a></li>
            <li><a href="#/active" @click="changeView('active')" :class="{selected:view==='active'}">Active</a></li>
            <li><a href="#/completed" @click="changeView('completed')" :class="{selected:view==='completed'}">Completed</a></li>
        </ul>
        <button class="clear-completed" @click="clearHasCompleted">Clear Completed</button>
    </footer>
</template>

<script>
    export default {
        name:"Footer",
        props:['todoNum','view'],
        methods:{
            changeView(childView){
                this.$parent.view=childView;
            },
            clearHasCompleted(){
                this.$parent.todoDatas=this.$parent.todoDatas.filter((value) => {
                    return !value.hasCompleted;
                })
            }
        }
    }
</script>

<style lang="scss" scoped>

</style>