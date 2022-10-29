

         <template>
           <div class="form-register container">
        <form class="card-panel green-text" @submit.prevent="Registerform" novalidate>
           <h2 class="center">Enregistrement</h2>
          <div class="field">
           <label for="nom">Nom</label>
           <input id="nom" type="text"  v-model="etudiant.nom" placeholder="Entrer nom" @blur="$v.etudiant.nom.$touch()">
              <template v-if="$v.etudiant.nom.$error">
           <p class="errorMessage" v-if="!$v.etudiant.nom.required"> Le nom est requis*</p>
           <p class="errorMessage" v-if="!$v.etudiant.nom.minLength"> Le nom doit avoir au moins 3 lettres</p>
           <p class="errorMessage" v-if="!$v.etudiant.nom.containuser"> Le nom ne doit pas contenir le mot "marc"</p>
            </template>
                   </div>
              <div class="field">
            <label for="email">Email</label>
             <input id="email" type="email" v-model="etudiant.email" placeholder="Entrer email" @blur="$v.etudiant.email.$touch()">
              <template v-if="$v.etudiant.email.$error">
                <p class="errorMessage" v-if="!$v.etudiant.email.required"> Email est requis*</p> 
                <p class="errorMessage" v-if="!$v.etudiant.email.email"> Email est invalide*</p>
                <p class="errorMessage" v-if="!$v.etudiant.email.containemail"> Email ne doit pas contenir le domaine "yahoo.fr"*</p> 
             </template>
               </div>
               <div class="field">
              <label for="date">Date</label>
              <input id="date" type="date"   v-model="etudiant.date"  placeholder="Entrer date"  @blur="$v.etudiant.date.$touch()">
              <template v-if="$v.etudiant.date.$error">
               <p class="errorMessage" v-if="!$v.etudiant.date.required"> Date est requis*</p>
               <p class="errorMessage" v-if="!$v.etudiant.date.CheckDate"> Date est incorrecte*</p>
             </template>

                  </div>
                 <div class="field center">
                 <button class="btn green" type="submit " :disabled="$v.$invalid">Enregistrer</button>

                   </div>


               </form>

               </div>
             </template> 

          <script>

       

        import{required,minLength,email } from 'vuelidate/lib/validators';

        export default{
          name:"RegisterForm",
        data(){
          return{
            etudiant:{
              nom:'',
              email:'',
              date:''
            },
            feedback:''
          }
        }, 
        methods:{
          Registerform(){
            this.$v.$touch();
            if(!this.$v.$invalid){
              console.log('etudiant ajouter avec success');
              console.log(this.etudiant);
        
            
          }
        },
  
        },
        validations:{
        etudiant:{
          nom:{
            required,minLength: minLength(3),
            containuser(value){
          return !value.includes('marc') }
          
          },
          email:{
            required,email,
            containemail(value){
          return !value.includes('yahoo.fr')
        }
          },
          date:{
            required,
       
        
        
          }
        }
        },

        }
        </script>
        <style >
        .form-register{
          max-width: 600px;
          margin-top: 70px;
        } 
        .form-register h2{
          font-size: 2.4em;
        }
        .form-register .field{
          margin-bottom:16px;
        }
        .errorMessage{
          color:red;
          font-weight: bold;
        }
        </style>