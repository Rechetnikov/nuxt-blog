<template>
  <article class="post">
    <header class="post-header">
      <div class="post-title">
        <h1>Post title</h1>
        <nuxt-link to="/">
          <i class="el-icon-back"></i>
        </nuxt-link>
      </div>
      <div class="post-info">
        <small>
          <i class="el-icon-time"></i>
          {{ new Date().toLocaleString() }}
        </small>
        <small>
          <i class="el-icon-view"></i>
          42
        </small>
      </div>
      <div class="post-image">
        <img
          src="https://cdn.tripzaza.com/ru/destinations/files/2017/09/Berlin-e1505798693967.jpg"
          alt="post image"
        />
      </div>
    </header>
    <main class="post-content">
      <p>Lorem, ipsum dolor sit amet consectetur adipisicing elit. Autem veritatis accusantium voluptatibus accusamus quos doloremque ut in distinctio, quam delectus?</p>
      <p>Lorem, ipsum dolor sit amet consectetur adipisicing elit. Autem veritatis accusantium voluptatibus accusamus quos doloremque ut in distinctio, quam delectus?</p>
      <p>Lorem, ipsum dolor sit amet consectetur adipisicing elit. Autem veritatis accusantium voluptatibus accusamus quos doloremque ut in distinctio, quam delectus?</p>
    </main>
    <footer>
      <app-comment-form v-if="canAddComment" @created="createCommentHandler"></app-comment-form>
      <div class="comments" v-if="false">
        <app-comment v-for="comment in 4" :key="comment" :comment="comment" />
      </div>
      <div class="text-center" v-else>Комментариев нет</div>
    </footer>
  </article>
</template>

<script>
import appComment from "@/components/main/comment";
import appCommentForm from "@/components/main/commentForm";

export default {
  validate({ params }) {
    return Boolean(params.id);
  },
  methods: {
    createCommentHandler() {
      console.log("created");
      this.canAddComment = false;
    },
  },
  data() {
    return {
      canAddComment: true,
    };
  },
  components: { appComment, appCommentForm },
};
</script>

<style lang="scss" scoped>
.post {
  max-width: 600px;
  margin: 0 auto;
}

.post-title {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;
}

.post-info {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.5rem;
}

.post-image img {
  width: 100%;
  height: auto;
}

.post-header {
  margin-bottom: 1.5rem;
}

.post-content {
  margin-bottom: 2rem;
}
</style>