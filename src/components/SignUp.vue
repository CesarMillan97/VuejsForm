<template>
  <form @submit.prevent="handleSubmit">
     <label>Email:</label>
     <input type="email" required  v-model="email">
     <label>Password:</label>
     <input type="password" required  v-model="password">
     <div v-if="passwordError" class="error">
        {{ passwordError }}
     </div>
     <label>Role:</label>
     <select v-model="role">
        <option value="developer">developer</option>
        <option value="designer">designer</option>
        <option value="architect">architect</option>
     </select>
     <label>Skills: <span style="font-weight: light">(Press enter to add new skill)</span> </label>
     <input type="text" v-model="tempSkills" @keyup.ctrl="addSkill">
     <div v-for="skill in skills" :key="skill" class="pill" @click="Remove(skill)">
        {{ skill }}
     </div>
     <div class="terms">
        <input type="checkbox" v-model="terms" required>
        <label>Accept terms and conditions</label>
     </div>

     <div class="submit">
        <button>Create account</button>
     </div>

  </form>
  <p>Email: {{ email }}</p>
  <p>Password: {{ password }}</p>
  <p>Role: {{ role }}</p>
  <p>Terms: {{ terms }}</p>
  <p>Skills: {{ skills }}</p>
  
</template>

<script>
export default {
   data() {
      return {
         email: '',
         password: '',
         role: '',
         terms: false,
         tempSkills: '',
         skills: [],
         passwordError: '',
      }
   },
   methods: {
      addSkill(e){
         console.log(e);
         if (e.key === ',' && this.tempSkills) {
         console.log('ok');
            if (!this.skills.includes(this.tempSkills)) {
               this.skills.push(this.tempSkills)
            } else {
               alert('Skill already added')
            }
            this.tempSkills = '';   
         }
      },
      Remove(skill){
         this.skills = this.skills.filter((item) => {
            return skill !== item
         })
      },
      handleSubmit(){
         this.passwordError = this.password.length > 5 ?
         '' : 'The password must be at least 6 characters';
         if (!this.passwordError) {
            console.log('email: ' + this.email);
            console.log('password: ' + this.password);
            console.log('role: ' + this.role);
            console.log('terms: ' + this.terms);
            console.log('skills: ' + this.skills);
         }
      }
   }
}
</script>

<style>
form{
   max-width: 420px;
   margin: 30px auto;
   background: white;
   text-align: left;
   padding: 40px;
   border-radius: 10px;
}
label{
   color: #aaa;
   display: inline-block;
   margin: 25px 0 15px;
   font-size: 0.6em;
   text-transform: uppercase;
   letter-spacing: 1px;
   font-weight: bold;
}
input, select{
   display: inline;
   padding: 10px 6px;
   width: 100%;
   box-sizing: border-box;
   border: none;
   border-bottom: 1px solid #ddd;
   color: #555;
}
input[type="checkbox"]{
   display: inline-block;
   width: 16px;
   margin: 0 10px 0 0;
   position: relative;
   top: 2px;
}
.pill{
   display: inline-block;
   margin: 20px 10px 0 0;
   padding: 6px 12px;
   background: #eee;
   border-radius: 20px;
   font-size: 12px;
   letter-spacing: 1px;
   font-weight: bold;
   color: #777;
   cursor: pointer;
}
button{
   background: #0b6dff;
   border: 0;
   padding: 10px 20px;
   margin-top: 20px;
   color: white;
   border-radius: 20px;
}
.submit{
   text-align: center;
}
.error{
   color: #ff0062;
   margin-top: 10px;
   font-size: 0.8em;
   font-weight: bold;
}
</style>