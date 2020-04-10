<template>
    <div>
        <!-- Content Header (Page header) -->
        <div class="content-header">
            <div class="container-fluid">
                <div class="row mb-2">
                    <div class="col-sm-6">
                        <h1 class="m-0 text-dark">Roles</h1>
                    </div><!-- /.col -->
                    <div class="col-sm-6">
                        <ol class="breadcrumb float-sm-right">
                            <li class="breadcrumb-item"><a href="#">Home</a></li>
                            <li class="breadcrumb-item active">Roles</li>
                        </ol>
                    </div><!-- /.col -->
                </div><!-- /.row -->
            </div><!-- /.container-fluid -->
        </div>
        <!-- /.content-header -->

        <!-- Main content -->
        <div class="content">
            <div class="container-fluid">
                <div v-if='page == "INDEX"' >
                     <div class="card">
                        <div class="card-header">
                            <h3 class="card-title">List</h3>

                            <div class="card-tools">
                                <div class="input-group input-group-sm" >
                                    <input type="text" name="table_search" class="form-control float-right" placeholder="Search">

                                    <div class="input-group-append">
                                        <button type="submit" class="btn btn-default"><i class="fas fa-search"></i></button>
                                        <button v-on:click="page = 'CREATE'" type="button" class="btn btn-block btn-primary btn-sm">Create</button>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <!-- /.card-header -->
                        <div class="card-body table-responsive p-0" style="height: 300px;">
                            <table class="table table-hover">
                                <thead>
                                <tr>
                                    <th>ID</th>
                                    <th>Code</th>
                                    <th>Name</th>
                                </tr>
                                </thead>
                                <tbody>
                                <tr v-bind:key="index"  v-for="(role, index) in roles">
                                    <td>{{role.code}}</td>
                                    <td>{{role.name}}</td>
                                </tr>
                                </tbody>
                            </table>
                        </div>
                        <!-- /.card-body -->
                    </div>
                    <!-- /.card -->
                </div>
                <div v-if='page == "CREATE"' >
                    <div class="card card-info">
                        <div class="card-header">
                            <h3 class="card-title">New Role</h3>
                        </div>
                        <!-- /.card-header -->
                        <!-- form start -->
                        <form class="form-horizontal" @submit.prevent="onSubmit" @keydown="form.errors.clear()">
                            <div class="card-body" style="height: 239px;">
                                <div class="form-group row">
                                    <label for="code" class="col-sm-2 col-form-label">Code</label>
                                    <div class="col-sm-10">
                                        <input type="text" class="form-control" id="code" name="code" required autocomplete="code" autofocus placeholder="code" v-model="form.code">
                                        <span class="invalid-feedback d-block" role="alert" v-if="form.errors.has('code')" v-text="form.errors.get('code')"></span>
                                    </div>
                                </div>
                                <div class="form-group row">
                                    <label for="name" class="col-sm-2 col-form-label">Name</label>
                                    <div class="col-sm-10">
                                        <input type="text" class="form-control" id="name" name="name" required autocomplete="name" autofocus placeholder="Name" v-model="form.name">
                                        <span class="invalid-feedback d-block" role="alert" v-if="form.errors.has('name')" v-text="form.errors.get('name')"></span>
                                    </div>
                                </div>
                            </div>
                            <!-- /.card-body -->
                            <div class="card-footer">
                                <button type="submit" class="btn btn-info" :disabled="form.errors.any()">Create</button>
                            </div>
                            <!-- /.card-footer -->
                        </form>
                    </div>
                </div>

            </div>
            <!-- /.container-fluid -->

        </div>
        <!-- /.content -->

    </div>

</template>

<script>

    export default {

        data() {
            return {
                roles : [],
                page : "INDEX", // INDEX | DETAIL | EDIT | CREATE
                form: new Form({
                    'code': '',
                    'name': ''
                })
            }

        },

        created() {
            axios.get('api/v1/roles')
                .then(({roles}) => this.roles = roles)
                .catch(error => {
                    roles = []
                });
        },

        methods: {
            onSubmit(){
                this.form.password_confirmation = this.form.password; // Temp for this form only.
                this.form
                    .post('api/v1/roles')
                    .then( role => this.roles.push(role) );
            }
        }
    }

</script>
