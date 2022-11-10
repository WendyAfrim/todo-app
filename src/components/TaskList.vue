<template>
    <div>
        <section id="tasks" class="w-1/2 flex mx-12 mt-5">
            <ul class="m-auto justify-center">
                <li :class="{
                    'cursor-pointer': true,  
                    'line-through': task.complete
                }"
                    @click="toggleCompleteHandler(i)" 
                    v-for="(task, i) in tasks" :key="i"
                >
                {{ task.name }} {{ task.complete ? ' - Done !' : ' '}}
                </li>
            </ul>
        </section>
    </div>
</template>

<script>
    export default {
        name: 'TaskList',
        props: {
            tasks: {
                type: Array,
                default: () => [],
            },
        },
        methods: {
            toggleCompleteHandler(i) {
                this.$emit("toggleComplete", i)
            }
        }
    };
</script>

<style scoped>

</style>