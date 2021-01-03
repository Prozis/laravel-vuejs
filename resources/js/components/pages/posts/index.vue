<template>
    <div>
        <form @submit.prevent="addPost" class="mb-3">
            <div class="form-group">
                <label for="title">Заголовок</label>
                <input v-model="post.title" type="text" class="form-control" id="title" placeholder="Enter email">

            </div>
            <div class="form-group">
                <label for="text">текст</label>
                <textarea v-model="post.text" class="form-control" id="text" rows="3"></textarea>
            </div>

            <button v-if="edit" type="submit" class="btn btn-primary">Сохранить изменения</button>
            <button v-else="edit" type="submit" class="btn btn-primary">Создать пост</button>
        </form>


        <h1>Все посты</h1>


        <div v-if="errored" class="alert alert-danger">Ошибка загрузки</div>

        <table v-else="errored" class="table table-striped">
            <thead>
            <tr>
                <th scope="col">id</th>
                <th scope="col">Название</th>
                <th scope="col">Текст</th>
                <th scope="col">кнопки</th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="post in posts" :key="post.id">
                <th> {{ post.id }}</th>
                <td> {{ post.title }}</td>
                <td> {{ post.text }}</td>
                <td>
                    <button @click="editPost(post)" class="btn btn-success">edit<i class="far fa-pencil"></i></button>
                    <button @click="deletePost(post.id)" class="btn btn-danger">del<i class="far fa-trash"></i></button>
                </td>

            </tr>
            </tbody>
        </table>

    </div>
</template>

<script>
export default {
    name: "index",
    data() {
        return {
            posts: [],
            post: {
                id: '',
                title: '',
                text: '',
            },
            pagination: {},
            edit: false,
            loading: true,
            errored: false,
        }
    },
    mounted() {
        this.getPosts()
    },
    methods: {
        getPosts() {
            axios
                .get('api/posts')
                .then(response => {
                    this.posts = response.data
                    //console.log(response.data)
                })
                .catch(error => {
                    console.log(error)
                    this.errored = true
                })
                .finally(() => this.loading = false)

        },
        addPost() {
            if (this.edit == false) {
                axios
                    .post('api/posts', {
                        title: this.post.title,
                        text: this.post.text
                    })
                    .then(response => {
                        this.getPosts()
                        this.post.text = ''
                    })
                    .catch(error => {
                        console.log(error)
                        this.errored = true
                    })
                    .finally(() => this.loading = false)
            } else {
                axios
                    .put(`api/posts/${this.post.id}`, {
                        title: this.post.title,
                        text: this.post.text
                    })
                    .then(response => {
                        this.getPosts()
                        this.post.title = ''
                        this.post.text = ''
                        this.post.edit = false
                    })
                    .catch(error => {
                        console.log(error)
                        this.errored = true
                    })
                    .finally(() => this.loading = false)
            }
        },
        editPost(post) {
            this.edit = true
            this.post.id = post.id
            this.post.title = post.title
            this.post.text = post.text

        },
        deletePost(id) {
            axios
                .delete(`api/posts/${id}`)
                .then(response => {
                    this.getPosts()
                })
                .catch(error => {
                    console.log(error)
                    this.errored = true
                })
                .finally(() => this.loading = false)
        }


    }
}
</script>

<style scoped>

</style>
