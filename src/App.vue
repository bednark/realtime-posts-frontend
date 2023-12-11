<template>
  <div class="container">
    <div class="post-field">
      <h2>Add post</h2>
      <textarea v-model="new_post" />
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
      posts: [
        {
          user: 'Guest 1',
          content: `Lorem ipsum dolor, sit amet consectetur adipisicing elit. Fuga neque eligendi
          a omnis dolorem similique illo architecto beatae quidem, repellendus officia
          eos animi blanditiis dolore optio commodi itaque, quaerat nam?`
        },
        {
          user: 'Guest 2',
          content: `Lorem ipsum dolor, sit amet consectetur adipisicing elit. Fuga neque eligendi
          a omnis dolorem similique illo architecto beatae quidem, repellendus officia
          eos animi blanditiis dolore optio commodi itaque, quaerat nam?`
        }
      ],
      new_post: ''
    }
  },
  methods: {
    public_post() {
      if(this.new_post == '') {
        alert('Cannot add empty post!')
        return
      }

      this.posts.unshift({
        user: 'Another Guest',
        content: this.new_post
      })

      this.new_post = ''
    }
  }
}
</script>