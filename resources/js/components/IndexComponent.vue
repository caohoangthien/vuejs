<template>
  <div>
      <h1>List Post</h1>
        <div class="row">
          <div class="col-md-10"></div>
          <div class="col-md-2">
            <router-link :to="{ name: 'create' }" class="btn btn-primary">Create Post</router-link>
          </div>
        </div><br />

        <table class="table table-bordered table-hover">
            <thead>
            <tr>
                <th>ID</th>
                <th>Title</th>
                <th>Body</th>
                <th class='text-center'>Actions</th>
            </tr>
            </thead>
            <tbody>
                <tr v-for="(post,index) in posts" :key="post.id">
                    <td>{{ ++index }}</td>
                    <td>{{ post.title }}</td>
                    <td>{{ post.body }}</td>
                    <td class='text-center'><router-link :to="{name: 'edit', params: { id: post.id }}" class="btn btn-primary">Edit</router-link>
                        <button class="btn btn-danger" @click.prevent="deletePost(post.id, index)">Delete</button></td>
                </tr>
            </tbody>
        </table>
  </div>
</template>

<script>
  export default {
      data() {
        return {
          posts: []
        }
      },
      created() {
      let uri = 'http://laravelvue.local/api/posts';
      this.axios.get(uri).then(response => {
        this.posts = response.data;
      });
    },
    methods: {
      deletePost(id, index)
      {
        let uri = `http://laravelvue.local/api/post/delete/${id}`;
        this.axios.delete(uri).then(response => {
          this.posts.splice(index-1, 1);
        });
      }
    }
  }
</script>