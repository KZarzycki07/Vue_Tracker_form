<template>
<div class="body">
  <div class="container">
    <form class="form" @submit.prevent="handleSubmit">
      <h2>Formularz rekrutacyjny:</h2>

      <div class="input"> 
        <label for="name">Imię</label>
        <input type="text" id="name" name="Imię" placeholder="Imię" required v-model="name"/>
      </div>

      <div class="input"> 
        <label for="surname">Nazwisko</label>
        <input type="text" id="surname" name="Nazwisko" placeholder="Nazwisko" required v-model="surname"/>
      </div>

      
<input type="hidden" name="_next" value="https://projekt-kz.surge.sh/">
      <div class="input">
        <label for="skills">Wymagane Umiejętności</label>
        <div class="skill-mobile">
          <input type="text" id="skills" placeholder="Umiejętności" v-model="tempSkills" @keydown.enter.prevent="addskill"/>
          <button type="button" @click="addskill" class="skill-mobile-btn">+</button>
        </div>
        
        <div v-for="skill in skills" :key="skill" class="skill">
          {{ skill }}
          <div class="delete-wrap">
            <button type="button" @click="deleteSkill(skill)" class="delete">x</button>
          </div>  
        </div>
      </div>

  <div class="level-wrap">
        <div class="level">
          <input type="radio" name="Poziom" v-model="picked" value="Junior"> Junior
        </div>
        <div class="level">
          <input type="radio" name="Poziom" v-model="picked" value="Mid"> Mid
        </div>
        <div class="level">
          <input type="radio" name="Poziom" v-model="picked" value="Senior"> Senior
        </div>
      </div>


      <div>
        <label>Specjalizacja</label>
        <select v-model="role" required>
          <option value="Front">Frontend</option>
          <option value="Back">Backend</option>
        </select>
      </div>

<h3 v-if="role === 'Back'">
  Niestety,zajmuję sie tylko Frontendem :)</h3>

      <div class="advice-wrap">
<label for="warnings">Uwagi/rady rekrutera</label>
      <div class="input">


<input type="text" id="uwaga" v-model="warning" @keydown.enter.prevent="warnings" placeholder="Co można poprawić?">   
<div v-for="(advice,index) in AdviceCard" :key="advice"> 

<ol>
  <li>{{ advice }}</li>
</ol>

</div>
</div>

</div>

    

      <div class="btn">
        <button type="submit" id="btnsend" v-bind:disabled="role === 'Back'">Wyślij formularz</button>
        
      </div>
    </form>
    
  </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const role = ref("")
const warning = ref("")
const AdviceCard = ref<string[]>([])
const name = ref("")
const surname = ref("")
const picked = ref("Junior")
const skills = ref<string[]>([])
const tempSkills = ref("")

function warnings() {
  const warn = warning.value.trim() // wpis propzycji

  if(!warn) return // jesli wiadomość pusta,zakoncz dzialanie
    if(AdviceCard.value.includes(warn)) return //jesli sie powatarza,zakoncz dzialanie
  AdviceCard.value.push(warn) // jesli wszystko ok,dodaj do tablicy

  warning.value = '' //wyczysc inputa po dodaniu


}


function addskill() {
  

  
  const trimmed = tempSkills.value.trim() // ustawienie wartosci trimmed

   
  if(!trimmed) return //jezeli wiadomość jest pusta to zakoncz zadanie

  if(skills.value.includes(trimmed)) return //jezeli jezyk sie powtarza to zakoncz dzialanie i nic nie dodawaj

  skills.value.push(trimmed) //jezeli wszystko poprawne to dodaj do listy
  
  tempSkills.value = '' //wyczysc input po dodaniu jezyka


}

function deleteSkill(skill : string) {
  skills.value = skills.value.filter(item => 
    item !== skill
  )
}

async function handleSubmit() {
  if (skills.value.length === 0) {
    alert("Prosimy podać przynajmniej jedną umiejętność");
    return;
  }


  const formData = {
    Imie: name.value,
    Nazwisko: surname.value,
    Poziom: picked.value,
    Specjalizacja: role.value,
    Umiejetnosci: skills.value.join(', '), 
    UwagiRekrutera: AdviceCard.value.join(', ')
  };

  try {

    const response = await fetch("https://formsubmit.co/ajax/zarzyckiinteria@gmail.com", {
      method: "POST",
      headers: { 
        "Content-Type": "application/json",
        "Accept": "application/json"
      },
      body: JSON.stringify(formData)
    });

    if (response.ok) {
      alert("Formularz został pomyślnie wysłany na maila!");
      

      name.value = '';
      surname.value = '';
      skills.value = [];
      tempSkills.value = '';
      warning.value = '';
      AdviceCard.value = [];
      role.value = '';
      picked.value = 'Junior';


      window.location.href = "https://projekt-kz.surge.sh/";
    } else {
      alert("Wystąpił błąd podczas wysyłania. Spróbuj ponownie.");
    }
  } catch (error) {
    console.error("Błąd sieci:", error);
    alert("Nie udało się połączyć z serwerem pocztowym.");
  }
}


</script>

<style scoped>
.container {
  max-width: 500px;
  min-height: 450px;
  margin: 40px auto;
  padding: 20px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background: linear-gradient(#ffffff, #e6e6e6);
  border-radius: 12px;
  box-shadow: 10px 4px 25px rgba(0, 0, 0, 0.2);
}

.input {
  display: flex;
  flex-direction: column;
  margin-bottom: 12px;
  width: 100%;

}

.skills-input {
    width: 100%;
    box-sizing: border-box;
}

.skill-mobile {
  display: flex;
  flex-direction: column;

}

.skill-mobile-btn {
  width: 7%;
  margin-top: 15px;
  background-color: gray;
  transition: 0.3s;
  border: none;
  padding: 10px;
  background-color: #21d764;;
}

#skills,#surname,#name,#uwaga {
  padding: 10px;
  border-radius: 7px;
  border: none;
  border: 0.3px solid black;
}

.level-wrap {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  margin-bottom: 10px;
}

.skill-mobile-btn:hover {
  background-color: #00ff5e;
}

#btnsend {
  width: 25%;
  padding: 10px;
}

.btn {
  display: flex;
  justify-content: flex-end;
  border: none;
}

.skill {
  font-size: 28px;
  display: flex;
  align-items: flex-start;
  margin-top: 20px;
  
}

.delete {
font-size: 14px;
border: none;
background-color: #ababab;
transition: 0.3s;
margin-left: 5px;
}

.delete:hover {
  background-color: #474747;
}


.delete-wrap {
  display: flex;
justify-content: flex-end;
}



.advice-wrap {
  margin-top: 30px;
}


select {
  padding: 3px;
  margin: 10px 8px 0px 10px;
}

:global(body) {
    background-color: #ffffff;

}

@media(max-width: 768px) {
  .skill-mobile-btn {
 width: 10%;
 padding: 15px;
  }
}
 
</style>
