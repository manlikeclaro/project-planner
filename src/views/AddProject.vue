<template>
  <form @submit.prevent="handlesubmit">
    <label>Title:</label>
    <input type="text" v-model="title" required>
    <label>Details</label>
    <textarea v-model="details" required></textarea>
    <button>add project</button>
  </form>
</template>

<script>
export default {
    data(){
        return{
            title: '',
            details: '',
            url: "http://localhost:3000/projects/"
        }
    },

    methods: {
        handlesubmit(){
            let project = {
                title: this.title,
                details: this.details,
                complete: false
            } 
            
            fetch(this.url, { 
                method: 'POST',
                headers: { "Content-Type" : "application/json" },
                body: JSON.stringify(project)
            }) 
                .then(() => { this.$router.push('/') })
                .catch(err => console.log(err.message))
        }
    }
}
</script>

<style>
    form{
        background: white;
        padding: 20px;
        border-radius: 10px;
        margin: 20px;
    }

    label{
        display: block;
        color: #b6b4b4;
        text-transform: uppercase;
        font-size: 14px;
        font-weight: bold;
        letter-spacing: 1px;
        margin: 20px 0 10px 0;
    }

    input{
        padding: 10px;
        border: 0;
        border-radius: 5px;
        border-bottom: 1px solid #ddd;
        width: 100%;
        box-sizing: border-box;
    }

    textarea{
        border: 1px solid #ddd;
        padding: 10px;
        width: 100%;
        height: 100px;
        box-sizing: border-box;
    }

    form button{
        margin: 20px auto;
        display: block;
        background: #00ce89;
        color: white;
        padding: 10px;
        border: 0;
        border-radius: 5px;
        font-size: 16px;
        cursor: pointer;
    }

</style>