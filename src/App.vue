<template>
  <div class="container">
    <div class="post-field">
      <h2>Add post</h2>
      <input type="text" v-model="nickname" placeholder="Nickname">
      <textarea v-model="new_post" placeholder="What are you thinking about?" />
      <button @click="public_post">Public</button>
    </div>
    <div class="post" v-for="post in posts">
      <h3>{{ post.user }}</h3>
      <p>{{ post.content }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      posts: [],
      nickname: '',
      new_post: '',
      websocket: new WebSocket('ws://localhost:8001/')
    }
  },
  methods: {
    public_post() {
      if(this.new_post == '') {
        alert('Cannot add empty post!')
        return
      }

      let new_post_content = {
        user: this.nickname,
        content: this.new_post
      }

      this.websocket.send(JSON.stringify(new_post_content))
      this.nickname = ''
      this.new_post = ''
    }
  },
  created() {
    this.websocket.addEventListener("message", (event) => {
      let result = JSON.parse(event.data)
      this.posts.unshift({
        user: result.user,
        content: result.content
      })
    })
  }
}
</script>