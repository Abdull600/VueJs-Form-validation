<template>
  <form @submit.prevent="handleSubmit">
    <label>EMAIL:</label>
    <input type="email" v-model="email">

    <label>PASSWORD: </label>
    <input type="password" v-model="password">
    <div v-if="passwordError" class="error">{{ passwordError }}</div>

    <label>role</label>
    <select v-model="role">
        <option value="Web Developer">Web Developer</option>
        <option value="Web Designer">Web Designer</option>
    </select>

    <label>skills (press alt + comma to add)</label>
    <input type="text" v-model="tempSkill" @keyup.alt="addSkill">
    <div v-for="skill in skills" :key="skill" class="skill-box">
        <span @click="deleteSkill(skill)">{{ skill }}</span>
    </div>

    <div class="terms">
        <input type="checkbox" v-model="terms">
        <label>Accept terms and conditions</label>
    </div>

    <div class="submit">
        <button>Create an Account</button>
    </div>
  </form>
</template>

<script>
export default {
    data(){
        return {
            email: '',
            password: '',
            role: '',
            tempSkill: '',
            skills: [],
            terms: false,
            passwordError: ''
        }
    },
    methods: {
        addSkill(e){
            if(e.key === ',' && this.tempSkill){
               if(!this.skills.includes(this.tempSkill)) {
                    this.skills.push(this.tempSkill)
               }
                this.tempSkill = ''
            }
        },
        deleteSkill(skill){
            this.skills = this.skills.filter((item) => {
                return skill !== item
            })
        },
        handleSubmit(){
            this.passwordError = this.password.length > 5 ? 
            '' : 'Password must be at least 6 characters long'
        }
    }
}
</script>

<style>
form {
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}
label {
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}
input, select {
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
}
input[type="checkbox"] {
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
}
.skill-box{
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
.submit{
    text-align: center;
}
button{
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
}
.error{
    margin-top: 10px;
    color: #ff0062;
    font-size: 0.8em;
    font-weight: bold;
}
</style>