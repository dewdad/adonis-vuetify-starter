<template>
    <v-app id="inspire">
        <v-content>
            <v-container fluid fill-height>
                <v-layout align-center justify-center>
                    <v-flex xs12 sm8 md4>
                        <v-form @submit.prevent="doLogin" lazy-validation>
                        <v-card class="elevation-12">
                            <v-toolbar dark color="primary">
                                <v-toolbar-title>Login form</v-toolbar-title>
                            </v-toolbar>
                            <v-card-text>
                                
                                    <v-text-field prepend-icon="person" name="login" label="Email" type="email" v-model="user.email" required></v-text-field>
                                    <v-text-field prepend-icon="lock" name="password" label="Password" id="password" type="password" v-model="user.password" required></v-text-field>
                                
                            </v-card-text>
                            <v-card-actions>
                                <router-link :to="{ name: 'register' }" class="btn btn--depressed">
                                    Register
                                </router-link>
                                <v-spacer></v-spacer>
                                <v-btn type="submit" color="primary">Login</v-btn>
                            </v-card-actions>
                        </v-card>
                        </v-form>
                    </v-flex>
                </v-layout>
            </v-container>
        </v-content>
    </v-app>
</template>

<script>
    export default {
        name: 'LoginForm',
        data: () => ({
            user: {email: '', password: ''}
        }),

        mounted () 
        {},

        methods: {

            doLogin () 
            {
                this.$http.post(`${window.basePath}/auth/login`, this.user)
                    .then(response => {
                        this.$auth.setToken(response.data.token)
                        this.$router.push({ path: '/' })
                    })
                    .catch(err => {
                        alert('verify your credentials')
                    })
            }

        }
    }
</script>