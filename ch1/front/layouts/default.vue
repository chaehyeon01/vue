<template>
<v-app>
    <nav>
        <v-toolbar dark color="green">
            <v-toolbar-title>
                <nuxt-link to="/" :style="{color:'#fff', textDecoration:'none'}" ><h2>NodeBird</h2></nuxt-link>
            </v-toolbar-title>
            <v-spacer></v-spacer>
            <v-toolbar-items>
                <v-text-field prepend-icon="mdi-magnify" label="검색" hide-details :style="{display:'flex',alignItems:'center'}" />
                <v-btn text nuxt to="/profile" :style="{display:'flex',alignItems:'center'}"> 
                    <div>프로필</div>
                </v-btn>
                <v-btn text nuxt to="/signup" :style="{display:'flex',alignItems:'center'}">
                    <div>회원가입</div>
                </v-btn>
            </v-toolbar-items>
        </v-toolbar>
    </nav>
    <v-row no-gutters>
        <v-col cols="12" md="4">
            <login-form />
        </v-col>
        <v-col cols="12" md="8">
            <nuxt />
        </v-col>
    </v-row>
</v-app>
    
</template>
<script>
import LoginForm from '~/components/LoginForm';
export default {
    components: {
        LoginForm,
    },
    data(){
        return{
            name:'Nuxt.js',
        }
    },
    head() {
    return{
        title:'연습'
    }
}
}
</script>
<style>

</style>