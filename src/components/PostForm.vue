<template>
   <div >
        <form @submit.prevent>
            <h1>Создание поста</h1>
            <input class = "input" 
                   type = "title" 
                   placeholder="Название"
                   v-bind:value="post.title" 
                   @input = "post.title = $event.target.value"
            >
            <input class = "input" 
                   type = "text" 
                   placeholder="Описание" 
                   v-bind:value="post.text"
                   @input = "post.text = $event.target.value"
            >
            <button class="btn" @click = "addPost">
                Создать
            </button>
        </form>
    </div>
</template>

<script>
export default {
    data(){
        return {
            post: {
                title: '',
                text: '',
            }
        }
    }
}
</script>

<style>
    .btn {
        margin-top: 15px;
        align-self: flex-end;
        padding: 10px;
        background: None;
        color: teal;
    }
    .input {
        width: 100%;
        border: 1px solid teal;
        padding: 10px;
        margin-top: 10px;
    }
    form {
        display:flex;
        flex-direction: column;
    }
</style>