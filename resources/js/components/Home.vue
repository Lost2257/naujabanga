<template>
    <div>
        <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
            <div class="container-fluid">
                    <img :src="getImage()" alt="tag" width="40" height="34" class="d-inline-block align-text-top">
                <h3 class="btn-dark">Nauja banga</h3>
                <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
                    <span class="navbar-toggler-icon"></span>
                </button>
                <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
                    <div class="navbar-nav">
                        <a class="nav-link active"  href="#kontaktai">Kontaktai</a>
                    </div>
                </div>
            </div>
        </nav>
        <main>
            <div class="container px-lg-5">
            <div class="row mx-lg-n5">
                <div class="align-self-center col py-5 px-lg-5">
                    <h4>
                    UAB "Nauja banga" užsiima įvairiais statybos darbais tiek Lietuvoje, tiek užsienio šalyse. Pritaikę vietinę ir tarptautinę projektų įgyvendinimo patirtį ,nuolatos tobulėjame. Siekiame tapti šios srities projektų rinkos lyderiais.O darbuotojams ,labiausiai pageidaujama ir vertinama darbo vieta.
                    </h4>
                </div>
                <div class="align-self-center col py-5 px-lg-5">
                <img :src="getImage2()"  alt="logo">
                </div>
            </div>
    </div>
        </main>
        <footer id="kontaktai" class="bg-dark text-center text-white">
            <div class="container p-4">
                <section class="">
                    <form method="post" @submit.prevent="saveEmail">
                        <div class="row d-flex justify-content-center">
                            <div class="col-auto">
                                <p class="pt-2">
                                    <strong>Prenumeruokite musu naujienlaiški</strong>
                                </p>
                            </div>
                            <div class="col-md-5 col-12">
                                <div class="form-outline form-white mb-4">
                                    <input v-model="fields.email" name="email" type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="El. pašto adressas">
                                    <div class="text-danger" v-if="errors && errors.email">{{ errors.email[0] }}</div>
                                    <label class="form-label" for="exampleInputEmail1"> </label>
                                </div>
                            </div>
                            <div class="col-auto">
                                <button type="submit" class="btn btn-outline-light mb-4">
                                    Prenumeruoti
                                </button>
                            </div>
                        </div>
                    </form>
                </section>
                <section class="mb-2">
                    <p>
                        Kontaktai :
                    </p>
                    <p>
                        <strong>
                            +370 677 04007
                        </strong>
                    </p>
                    <p>
                        <strong>
                            +467 226 65628
                        </strong>
                    </p>
                    <p>
                        <strong>
                            naujabanga9@gmail.com
                        </strong>
                    </p>
                </section>
            </div>
        </footer>
    </div>
</template>

<script>
export default {
    data() {
        return {
            fields: {},
            errors: {},
            loaded: true,
        }
    },
    methods: {
        getImage(){
            return 'image/trikampis.png'
        },
        getImage2(){
            return 'image/banga.jpg'
        },
        saveEmail(){
            if (this.loaded) {
                this.loaded = false;
                this.errors = {};
                axios.post('/api/store',this.fields).then(response => {
                    this.fields = {};
                    this.loaded = true;
                }).catch(error => {
                    const klaidele = 422;
                    if (error.response.status = klaidele) {
                        this.errors = error.response.data.errors || {};
                    }
                });
            }
        },
    },

}
</script>
