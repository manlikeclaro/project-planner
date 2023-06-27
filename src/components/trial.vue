<template>
    <div class="trial">
        <h3 @click.self="temp =!temp">{{ project.name }} </h3> 
        <p>{{ project.email }}</p>
        <div  v-if="temp">
            <p @click="filter">{{ project.body }}</p>
        </div>
    </div>
</template>

<script>
export default {
    props: ['project'],
    data(){
        return {
            temp: false,
            filte: this.project.postId
        }
    },

    methods: {
        filter(){
            this.$emit('filter')
            console.log('executed')
        }
    },

    mounted(){
        
    }

}
</script>

<style>
    .trial{
        background: white;
        width: 600px;
        border: none;
        border-radius: 15px;
        margin: 10px;
        padding: 20px;
        box-shadow: 1px 2px 3px;
    }
</style>