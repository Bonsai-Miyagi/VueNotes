<script setup>
  import { ref } from "vue"; //State
  import dayjs from 'dayjs'; // Import dayjs(date format)

  const showModal = ref(false);
  const newNote = ref(""); //two way binding(v-model directive)
  const notes = ref([]); //All notes will be here
  const errorMessage = ref("");

  //add notes with random colors
  function getRandomColor() {
    return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
  }

  const addNote = () => {
    if(newNote.value.length < 10) {
      return errorMessage.value = "Note needs to be 10 characters or more"
    }
    notes.value.push({
      id: Math.floor(Math.random() * 1000000),
      text: newNote.value,
      date: dayjs().format('YYYY-MM-DD HH:mm:ss'),
      backgroundColor: getRandomColor(),
    });
    showModal.value = false; //close modal after creating note
    newNote.value = ""; //Clear the modal textarea after creating the note
    errorMessage.value = "";
  }
</script>

<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea v-model.trim="newNote" name="note" id="note" cols="30" rows="10"></textarea>
        <p v-if="errorMessage">{{ errorMessage }}</p><!---->
        <button @click="addNote">Add Note</button>
        <button class="close" @click="showModal = false">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal = true">+</button>
      </header>
        <div class="cards-container">
          <div v-for="(note, index) in notes" :key="note.id" class="card" :style="{backgroundColor: note.backgroundColor}">
            <p class="main-text">{{ note.text }}</p>
            <p class="date">{{ note.date }}</p>
          </div>
        </div>
    </div>
  </main>
</template>

<style scoped>
  main {
    font-family: 'Roboto';
    width: 100vw;
    height: 100vh;
  }

  .container {
    max-width: 1000px;
    padding: 10px;
    margin: 0 auto;
  }

  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  h1 {
    font-weight: bold;
    margin-bottom: 25px;
    font-size: 75px;
  }

  header button {
    border: none;
    padding: 10px;
    width: 50px;
    height: 50px;
    cursor: pointer;
    background-color: rgb(219, 223, 233);
    border-radius: 100%;
    color: rgb(40, 47, 69);
    font-size: 20px;
  }

  .card {
    width: 225px;
    height: 225px;
    background-color: rgb(237, 182, 44);
    padding: 10px;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-right: 20px;
    margin-bottom: 20px;
    color: rgb(37, 40, 59);
    font-size: 20px;
  }

  .date {
    font-size: 12.5px;
    font-weight: bold;
  }

  .cards-container {
    display: flex;
    flex-wrap: wrap;
  }

  .overlay {
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.77);
    z-index: 10;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .modal {
    width: 750px;
    background-color: rgb(244, 244, 244);
    border-radius: 10px;
    padding: 30px;
    position: relative;
    padding: 30px;
    position: relative;
    display: flex;
    flex-direction: column;
  }

  .modal button {
    padding: 10px 20px;
    font-size: 20px;
    width: 100%;
    background-color: blueviolet;
    border: none;
    color: white;
    cursor: pointer;
    margin-top: 15px;
  }

  .modal .close {
    background-color: rgb(193, 15, 15);
    margin-top: 7px;
  }

  .modal textarea {
    background-color: rgb(117, 130, 174);
    border-radius: 6px;
    resize: none;
    outline: none;
    border: none;
    padding: 12px;
    font-size: 25px;
    color: white;
  }

  .modal p {
    color: rgb(255, 53, 53);
  }
</style>
