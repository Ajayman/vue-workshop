<template>
  <div class="container">
    <div class="card">
      {{newComment.length}}
      <div class="comment">
        <div class="comment__img">
          <img src="../assets/ts.jpg" alt="Profile picture" />
        </div>
             
        <div class="comment__content">
          <ul class="comment-list" v-for="(comment, index) in commentList" :key="index">
            <li>
              <span>{{ comment }} <button name="deletecomment" @click="deleteComment(index)">X</button></span>
            </li>
          </ul>
          <div class="no-comments" v-if="!commentList.length">
            <p>No comments added yet</p>
          </div>
          <div v-else>
            comments ({{commentList.length}})
          </div>
        </div>
        <div class="comment-box">
          <textarea class="form-control" rows="3" placeholder="Write a comment" v-model.trim="newComment" @keyup.enter="addNewComment"></textarea>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "PhotoComment",
  data () {
    return {
      newComment: '',
      commentList: []
    }
  },
  methods: {
    addNewComment() {
      if(this.newComment){
        this.commentList.push(this.newComment)
        this.newComment = ''
      }     
    },
    deleteComment(indexOfComment) {
      this.commentList.splice(indexOfComment, 1)
    }
  }
};
</script>

<style scoped lang="scss">
.container {
  margin: 0 auto;
  max-width: 768px;
}

.card {
  box-shadow: 0 2px 3px rgba(10, 10, 10, 0.1), 0 0 0 1px rgba(10, 10, 10, 0.1);
}

.comment {
  &__img {
    > img {
      width: 100%;
    }
  }
  &__content {
    padding: 18px;

    .comment-list {
      > li {
        &:not(:last-child) {
          margin-bottom: 12px;
        }
        > span {
          background-color: #f2f3f5;
          border-radius: 68px;
          padding: 8px 12px;
          font-size: 14px;
          display: inline-block;
        }
      }
    }
  }
  .comment-box {
    textarea {
      border: 1px solid #f2f2f2;
      width: 100%;
      padding: 12px;
    }
  }
}
</style>
