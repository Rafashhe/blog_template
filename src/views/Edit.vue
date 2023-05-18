<script>
import PostForm from '../componentes/PostForm.vue';

export default {
    props: {
        posts: Array,
    },
    data() {
        return {
            post: this.posts [this.$route.params.id],
        };
    },
    components: {
        PostForm,
    },
};

</script>
<!-- o "this" eu só coloco no script-->
<template>
   
<PostForm :post="post" />

</template>
