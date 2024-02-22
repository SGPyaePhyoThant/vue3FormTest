<template>
  <form @submit.prevent="handleSubmit">
    <label for="email">メールアドレス:</label>
    <input type="email" id="email" required v-model="email">
    <label for="password">パスワード:</label>
    <input type="password" id="password" required v-model="password">
    <div v-if="passwordError" class="error">{{passwordError}}</div>
    <label for="">キャリア</label>
    <select v-model="career">
        <option value="developer">開発者</option>
        <option value="UIUXDesigner">UIUXデザイナー</option>
    </select>
    <div class="terms">
        <input type="checkbox" required v-model="agreement">
        <label>利用規約に同意する</label>
    </div>
    <div>
        <label for="">スキル</label>
        <input type="text" v-model="tempSkill" @keyup.alt="addSkills">
        <div v-for="skill in skills" :key="skill" class="pill" >
            <span @click="removeSkill(skill)">{{skill}}</span>
        </div>
    </div>
    <div class="submit">
        <button>サーバーに登録</button>
    </div>
  </form>
</template>

<script>
export default {
    data(){
        return {
            email:'',
            password:'',
            career:'',
            agreement:true,
            tempSkill:'',
            skills:[],
            passwordError:''
        }
    },
    methods:{
        addSkills(e){
            if(e.key === ',' && this.tempSkill){
                if(!this.skills.includes(this.tempSkill)){
                    this.skills.push(this.tempSkill)
                }
                this.tempSkill = ''
            }
        },
        removeSkill(skillData){
             this.skills = this.skills.filter(param => {
        // if(skillData == param){
        //             let index = this.skills.indexOf(param);
        //             if (index > -1) {
        //                 this.skills.splice(index, 1);
        //             }
                return param !== skillData
                
                // console.log('this.skill',this.skills)
             });
        },
        handleSubmit(){
            this.passwordError = this.password.length > 5 ?
             '' : 'パスワードは五つの以上です。'
            if(!this.passwordError){
                console.log('email',this.email)
                console.log('password',this.password)
                console.log('career',this.career)
                console.log('agreement',this.agreement)
                console.log('tempSkill',this.tempSkill)
                console.table(this.skills)
            }
        }
    }
}
</script>

<style scoped>
form{
    max-width: 420px;
    margin: 30px auto;
    background:#ffff;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}
label{
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6rem;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}
input,select{
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
}
input[type=checkbox]{
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position:relative;
    top: 2px;
}
.pill{
    display:inline-block;
    margin:20px 10px 0 0;
    padding:6px 12px;
    background:#eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor:pointer;
}
button{
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: #fff;
    border-radius: 20px;
    font-size: 10px;
}
.submit{
    text-align: center;
}
.error{
    color: #e81e1e;
    margin-top: 10px;
    font-size: 0.6rem;
    font-weight: bolder;
}
</style>