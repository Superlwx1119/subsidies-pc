import Vue from 'vue'
import Vuex from 'vuex'
Vue.use(Vuex)


export default new Vuex.Store({
    state:{
        token:window.sessionStorage.getItem('token'),
        show:false
    },
    actions:{
        showDetail(val,show){
            val.commit('showDetail',show)
        },
        userLogin({ commit }, data){
            commit('LOGIN', data);
		},
		userLogout({ commit }){
		    commit('LOGOUT');
		},
    },
    mutations:{
        showDetail(state,show){
            state.show=!show;
        },
        LOGIN(state, data){
            //更改token的值
            state.token = data;
            window.sessionStorage.setItem('token', data);
            },
        LOGOUT:(state) => {
            //登出的时候要清除token
            state.token = null;
            window.sessionStorage.removeItem('token');
        },
    }
})