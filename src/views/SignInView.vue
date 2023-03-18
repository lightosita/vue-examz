<template>
  <div class="signin">
    <h1>create an account</h1>
    <label>
      <input type='text' placeholder='Email' v-model="email" required>

    </label>
    <label>
      <input type='password' placeholder='password' v-model="password" required>

    </label>
    <p><button @click="signIn">Submit</button></p>
    
    <p><button @click="signInWithGoogle">Sign In</button></p>
    

  </div>
</template>
<script setup>
import{ref} from "vue";
import { getAuth, createUserWithEmailAndPassword,GoogleAuthProvider,SignInWithPopup, } from "firebase/Auth";

const email = ref("");
const password = ref("");
const signIn = () => {
  createUserWithEmailAndPassword(getAuth(),email.value, password.value)
  .then((userCredential) => {
    // Signed in 
    console.log("successfully signedup!")
    console.log('auth.currentUser')
    // const user = userCredential.user;
    router.push('/products') //redirects
    // ...
  }) 
  .catch((error) =>{
    console.log(error.code);
    alert(error.message);
  });
  
};
const signInWithGoogle = () => {
  const provider = new GoogleAuthProvider();
  SignInWithPopup(getAuth(),provider)
  .then((result)=>{
console.log(result.user);
router.push("/product")
  })
  .catch((error)=>{
    //handle error
    alert("error")
  })
}
</script>
