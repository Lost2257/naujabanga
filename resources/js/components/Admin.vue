<template>
    <div class="container-fluid">
<!--    <ul v-for="email in emails.data">-->
<!--        <li>{{ email.email }}</li>-->
<!--    </ul>-->
<table class="table table-dark">
    <thead>
    <tr class="table-active">
        <th scope="col">ID</th>
        <th scope="col">Email</th>
        <th scope="col">Actions</th>
    </tr>
    </thead>
    <tbody v-for="email in emails.data " :key=email.id>
    <tr class="table-active">
        <th scope="row">{{ email.id }}</th>
        <td>{{ email.email }}</td>
        <td>
            <span class="btn btn-danger" v-on:click="deleteEmail(email.id)">
                <i class="fas fa-trash-alt"></i>
                Delete
            </span>
        </td>
    </tr>
    </tbody>
</table>
            <pagination :data ="emails" @pagination-change-page="loadEmails"></pagination>
    </div>
</template>

<script>
export default {
    data() {
        return {
            emails: [],
            currentPage: 1,
            rows: 10,
            perPage: 5,
        }
    },
    mounted() {
        this.loadEmails();
    },
    methods: {
        loadEmails: function (page = 1) {
            axios.get('/api/stats?page=' + page)
                .then((response) => {
                    this.emails = response.data;
                })
            this.emails = {}
        },
        deleteEmail: function (email) {
            if (!window.confirm('are you sure to delete ')) {
                return ;
            }
            try {
                axios.get('/api/delete' + email).then((response) => {
                    this.loadEmails();
                })
            }catch (errors) {

            }
        },
    }
}
</script>
