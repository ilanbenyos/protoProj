<template>
  <transition name="fade">
    <div>
     =={{msg}}==
      <button class="button" @click="initMsg">initMsg</button>
      <button class="button" @click="getMsgFromStore">getMsgFromStore</button>
      <button class="button" @click="getMsgFromServer($event)">getMsgFromServer</button>
        <div>
            <button class="button" @click="getUsers">getUsers</button>
                last user:<div class="users" >users.length:{{users.length}}</div>
          <div>
              <div  v-for="(user1,idx) in users" ><div v-if= "idx<7" >{{idx}}:{{user1.userName}}/{{user1.password}}</div></div>
          </div>
        </div>

        curr user:<div class="user" >{{user}}</div>
        <div>
            userName:<input v-model="tempUser.userName" class="input" placeholder="Choose username" ></input>
            pass:<input v-model="tempUser.password" class="input" placeholder="Choose password" ></input>
            txt:<input v-model="tempUser.txt" class="input" placeholder="free txt" ></input>
            <div>
              <button class="button" @click="submit">submit</button>
              <button class="button" @click="updateUser">updateUser</button>
              <button class="button" @click="deleteUser">deleteUser</button>
            </div>
        </div>
        <div>
            dog name:<input v-model="dog.name" class="input" placeholder="dog name" ></input>
            dog type:<input v-model="dog.type" class="input" placeholder="dog type" ></input>
            <button class="button" @click="insertDog">insertDog</button>
        </div>
    </div>
  </transition>

</template>

<script>
import { LOG_IN } from '../store/store'
import { SENDMSG } from '../store/store'

export default {
  data() {
    return {
      msg:'login',
      users:[],
      user: {},
      dog:{_id:null,name:'',type:''},
      tempUser:{
                login: '',
                password: '',
                txt:''
                }
      }
  },
    created() {//fetchGetDog
    this.users = this.$store.getters.fetchGetUsers;
    this.dog = this.$store.getters.fetchGetDog;

    var currUserInit1 = this.$store.getters.fetchGetUser;
    var currUserInit = this.cloneDeep(currUserInit1)
    console.log('Edit - created - currUserInit:', currUserInit)
    if (currUserInit) this.tempUser = currUserInit;
  },

  mounted(){
      this.msg = this.$store.getters.fetchGetMsg;//fetchGetList
  },
  watch:{
      msg1: function(newMsg){
        this.msg = this.$store.getters.fetchGetMsg;
      },
      user1: function(newUser){
        this.user = this.$store.getters.fetchGetUser;
      },
      users1: function(newUsers){
        this.users = this.$store.getters.fetchGetUsers;
      },
      dog1: function(newDog){
        this.dog = this.$store.getters.fetchGetDog;
      },

  },
    computed: {
    msg1() {return this.$store.getters.fetchGetMsg;},
    user1() {return this.$store.getters.fetchGetUser;},
    users1() {return this.$store.getters.fetchGetUsers;},
},
  methods: {//
      getUser(){
        this.user = this.$store.getters.fetchGetUser;
      },
    cloneDeep(obj){
      var myJSON = JSON.stringify(obj);
      return JSON.parse(myJSON)
    },
      initMsg(){
          this.msg = "initMsg";
          // this.$router.push('Browse');
      },
      getMsgFromStore(){
          this.msg = this.$store.getters.fetchGetMsg;
          console.log('getMsgFromStore')
      },
      deleteUser(e){
          const act = { actType: 'deleteUser', user:this.user._id};
          const params = { event:e,askFrom:'server'}
          this.sendMsg({ act,params})
      },
      getMsgFromServer(e){
          const act = { actType: 'getMsgFromServer', txt:this.msg};
          const params = { event:e,askFrom:'server'}
          this.sendMsg({ act,params})
      },
      getUsers(e){
          const act = { actType: 'getList', list:'users'};
          const params = { event:e,askFrom:'server'}
          this.sendMsg({ act,params})
      },//
      insertDog(e){
        const act = { actType: 'insertDog', data: this.dog , collection: 'dogs'}
        const params = { event:e,askFrom:'server'}
          this.sendMsg({ act,params})
      },
      submit(e){
        const act = { actType: 'addUser', data: this.tempUser, collection: 'users' }
        const params = { event:e,askFrom:'server'}
          this.sendMsg({ act,params})
         this.tempUser = {login: '',password: '',txt:''}
      },
      updateUser(e){
        this.tempUser._id = this.user._id;
        const act = { actType: 'updateUser', data: this.tempUser }
        const params = { event:e,askFrom:'server'}
          this.sendMsg({ act,params})
         this.tempUser = {login: '',password: '',txt:''}
      },
      sendMsg(msg){
          this.$store.dispatch({ type: SENDMSG, msg })
      },
      cLog(msg){
        //   this.$store.dispatch({ type: SENDMSG, msg })
      },


  }
}
  
</script>

<style lang="scss" scoped>



</style>
