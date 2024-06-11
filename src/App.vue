<template>
  <section class="container">
    <user-data  :first-name="firstName" :last-name="lastName" ></user-data>
    <!-- <h2>{{ userName }}</h2>     -->
    <!-- <h3>{{ age }}</h3> -->
    <!-- <h2>{{ user.name }}</h2> -->
    <!-- <h3>{{ user.age }}</h3> -->

    <button @click="setAge">Change Age</button>
    <div>
      <input type ="text" placeholder="First Name" @input="setFirstName" v-model="firstName"/>
      <input type ="text" placeholder="Last Name" v-model="lastName" ref="lastNameInput"/>
      <button @click="setLastName">Set Last Name</button>
    </div>
  </section>
</template>

<script>
import { ref, 
  computed,
  watch, provide,
  // reactive, isReactive, isRef, toRefs 
} from 'vue';
import UserData from './components/UserData.vue';

export default {
  components: {
    UserData,
  },
  setup(){
    // const uName = ref('Maximilian');
    const uAge = ref(31);
    // const user = reactive({
    //   name : 'Maximilian',
    //   age: 31,
    // });
    const firstName = ref('');
    const lastName = ref('')
    const lastNameInput = ref(null);

    
    provide('userAge', uAge);

    const uName = computed(function(){
      return firstName.value + ' ' + lastName.value;
    });

    
    watch([uAge, uName], function(newValues, oldValues){
      console.log('Old Age: '+ oldValues[0]);
      console.log('New Age: '+ newValues[0]);
      console.log('Old Name: '+ oldValues[1]);
      console.log('New Name: '+ newValues[1]);
    });

    // uName.value = 'Max';
    // console.log(uAge.value)
    // console.log(user.name, user.age);
    // console.log(isRef(uAge))
    // console.log(isReactive(user), user.age);
    

    // setTimeout(function(){
    //   // uName.value = 'Max';
    //   // uAge.value = 32;
    //   // user.value.name = 'Max',
    //   // user.value.age = 32;
    //   user.name = 'Max',
    //   user.age = 32;
    // },2000);

    // const userRefs = toRefs(user);


    function setNewAge(){
      // user.age = 33;
      uAge.value = 33;
    }

    // function setFirstName(event){
    //   firstName.value = event.target.value;
    // }

    // function setLastName(event){
    function setLastName(){
      // lastName.value = event.target.value;
      // lastName.value = this.$refs.lastNameInput.value;
      lastName.value = this.lastNameInput.value.value;
    }



    return {
      userName: uName,
      age : uAge,
      // userName : user.value.name,
      // age: user.value.age,
      // user : user,
      // userName : userRefs.name, age: userRefs.age,
      setAge : setNewAge,
      // setFirstName : setFirstName,
      setLastName : setLastName,
      firstName,
      lastName,
      lastNameInput,
    };
  },
  // data() {
  //   return {
  //     userName: 'Maximilian',
  // age: 31,
  //   };
  // },
  // methods: {
  //   setNewAge() {
  //     this.age = 32;
  //   },
  // },
  // computed: {},
  // watch: {
  //   age(val) {
  //     console.log(val);
  //   },
  // },
  // provide(){
  //   return {age: this.age};
  // }
};
</script>

<style>
* {
  box-sizing: border-box;
}

html {
  font-family: sans-serif;
}

body {
  margin: 0;
}

.container {
  margin: 3rem auto;
  max-width: 30rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 1rem;
  text-align: center;
}
</style>
