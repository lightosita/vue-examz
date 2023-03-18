<template>
  <div class="signin">
    <h1>create an account</h1>
    <label>
      <input type='text' placeholder='Email' v-model="email" required>

    </label>
    <label>
      <input type='password' placeholder='password' v-model="password" required>
      <p v-if="errMsg">{{errMsg}}</p>

    </label>
    <p><button @click="login">login</button></p>
    
    <p><button @click="signInWithGoogle">Sign In With Google</button></p>
    

  </div>
</template>
<script setup>
import{ref} from "vue";
import { getAuth, signInWithEmailAndPassword } from "Firebase/Auth";
import { useRouter } from 'vue-router';

const email = ref("");
const password = ref("");
const errMsg = ref();//error message
const router = useRouter();//to get a reference from vue router

const login = () => {
  // a.value is used with ref()
  const auth = getAuth(); //get a reference to the auth service
  signInWithEmailAndPassword(getAuth(),email.value, password.value)
  .then((userCredential) => {
    // Signed in 
    console.log("successful login!")
    console.log('auth.currentUser')
    // const user = userCredential.user;
    router.push('/products') //redirects
    // ...
  }) 
  .catch((error) =>{
    console.log(error.code);
    switch(error.code){
      case "auth/invalid-email":
        errMsg.value = "Invalid email address";
        break;
        case "auth/user-not-found":
        errMsg.value = "account not found";
          break;
          case"auth/wrong-password":
            errMsg.value = "wrong password";
            break;
            default:
              errMsg.value = "Email or Password Incorrect";
              break;

    };
  });
  
};
const signInWithGoogle = () => {
  
}
</script>
