<template>
    <div v-if="posts.length > 0">
        <h3>Список постов</h3>
        <transition-group name="user-list">
            <post-item
                v-for="post in posts"
                :key="post.id"
                :post="post"
                @remove="$emit('remove', post)"
            />
        </transition-group>
    </div>
    <h2 v-else>Список постов пуст</h2>
</template>

<script>
import PostItem from './PostItem.vue'
export default {
  components: { PostItem },
    props: {
        posts: {
            type: Array,
            required: true
        }
    }
}

</script>


<style scoped>
.user-list-item {
  display: inline-block;
  margin-right: 10px;
}
.user-list-enter-active, .user-list-leave-active {
  transition: all .5s;
}
.user-list-enter, .user-list-leave-to /* .list-leave-active до версии 2.1.8 */ {
  opacity: 0;
  transform: translateX(130px);
}
.user-list-move{
    transition: transform .4s;
}
</style>