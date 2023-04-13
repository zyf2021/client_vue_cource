<template>
  <div class = "post" v-for="post in posts" :key = "post">
        <h1>Главная страница</h1>
        <p><strong>{{ post.title }}</strong></p>
        <p><strong>{{ post.text }}</strong></p>
        <div>Number of likes 
            <strong>{{ post.likes }}</strong>
            <button @click="addLike(post.id)">Like</button>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        posts: {
            type: Array,
            required: true,
        }
    }

}
</script>

<style>
    .post {
            padding: 15px;
            border: 1px solid teal;
            margin-top: 15px;
        }
</style>