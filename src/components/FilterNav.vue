<template>
  <nav class="filter-nav">
    <button @click="updatefilter('all')" :class="{active: current === 'all'}">
        view all
    </button>
    <button @click="updatefilter('complete')" :class="{active: current === 'complete'}">
        view complete
    </button>
    <button @click="updatefilter('ongoing')" :class="{active: current === 'ongoing'}">
        view ongoing
    </button>
  </nav>
</template>

<script>
export default {
    props: ['current'],

    methods: {
        updatefilter(by){
            this.$emit('filter', by)
        }
    }
}
</script>

<style>
    .filter-nav button{
        background: none;
        border: 0;
        color: #bbb;
        outline: none;
        font-size: 12px;
        text-transform: uppercase;
        margin: 10px;
        font-weight: bold;
        cursor: pointer;
    }

    .filter-nav button.active{
        color: #555;
    }
</style>