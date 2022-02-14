<template>
  <form>
     <label>Email:</label>
     <input type="email" required  v-model="email">
     <label>Password:</label>
     <input type="password" required  v-model="password">
     <label>Role:</label>
     <select v-model="role">
        <option value="developer">developer</option>
        <option value="designer">designer</option>
        <option value="architect">architect</option>
     </select>
     <label>Skills: <span style="font-weight: light">(Press enter to add new skill)</span> </label>
     <input type="text" v-model="tempSkills" @keyup="addSkill">
     <div v-for="skill in skills" :key="skill" class="pill">
        {{ skill }}
     </div>
     <div class="terms">
        <input type="checkbox" v-model="terms" required>
        <label>Accept terms and conditions</label>
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
      }
   },
   methods: {
      addSkill(e){
         if (e.key === "Enter" && this.tempSkills) {
            if (!this.skills.includes(this.tempSkills)) {
               this.skills.push(this.tempSkills)
            } else {
               alert('Skill already added')
            }
            this.tempSkills = '';   
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
</style>