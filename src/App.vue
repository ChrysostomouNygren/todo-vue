<script setup>
import { ref } from "vue";

let id = 0;
const newTodo = ref("");
const todos = ref([]);

// ***************************************
// Lägga till så att det ej går att skicka tomma newTodos!
// ***************************************

function addTask() {
  todos.value.push({
    id: id++,
    text: newTodo.value,
    done: false,
  });

  newTodo.value = "";
}

function validTask(){
  if (newTodo.value < 3) {
    return;
} else {
  addTask();
}
  }

function removeTask(todo) {
  todos.value = todos.value.filter((t) => t !== todo);
}
</script>

<template>
  <main>
    <div>
      <h1>Todo:</h1>
      <div class="input-field">
        <input v-model="newTodo" @keyup.enter="validTask" autofocus />
        <button @click="validTask">
          <img
            alt="svgImg"
            src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHg9IjBweCIgeT0iMHB4Igp3aWR0aD0iMjQiIGhlaWdodD0iMjQiCnZpZXdCb3g9IjAgMCAyNCAyNCIKc3R5bGU9IiBmaWxsOiMwMDAwMDA7Ij48cGF0aCBkPSJNIDEyIDIgQyA2LjQ4ODk5NzEgMiAyIDYuNDg4OTk3MSAyIDEyIEMgMiAxNy41MTEwMDMgNi40ODg5OTcxIDIyIDEyIDIyIEMgMTcuNTExMDAzIDIyIDIyIDE3LjUxMTAwMyAyMiAxMiBDIDIyIDYuNDg4OTk3MSAxNy41MTEwMDMgMiAxMiAyIHogTSAxMiA0IEMgMTYuNDMwMTIzIDQgMjAgNy41Njk4Nzc0IDIwIDEyIEMgMjAgMTYuNDMwMTIzIDE2LjQzMDEyMyAyMCAxMiAyMCBDIDcuNTY5ODc3NCAyMCA0IDE2LjQzMDEyMyA0IDEyIEMgNCA3LjU2OTg3NzQgNy41Njk4Nzc0IDQgMTIgNCB6IE0gMTEgNyBMIDExIDExIEwgNyAxMSBMIDcgMTMgTCAxMSAxMyBMIDExIDE3IEwgMTMgMTcgTCAxMyAxMyBMIDE3IDEzIEwgMTcgMTEgTCAxMyAxMSBMIDEzIDcgTCAxMSA3IHoiPjwvcGF0aD48L3N2Zz4="
          />
        </button>
      </div>
      <ul>
        <li v-for="todo in todos" :key="todo.id">
          <input class="checkeliboxeli" type="checkbox" v-model="todo.done" />
          <span :class="{ done: todo.done }">{{ todo.text }}</span>
          <button @click="removeTask(todo)">🗑️</button>
        </li>
      </ul>
    </div>
  </main>
</template>

<style>
/* ************************************** */
/* Färg/bild css */
/* ************************************** */

body {
  text-align: center;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='615' height='615' viewBox='0 0 800 800'%3E%3Cg fill='none' stroke='%23000000' stroke-width='2.1'%3E%3Cpath d='M769 229L1037 260.9M927 880L731 737 520 660 309 538 40 599 295 764 126.5 879.5 40 599-197 493 102 382-31 229 126.5 79.5-69-63'/%3E%3Cpath d='M-31 229L237 261 390 382 603 493 308.5 537.5 101.5 381.5M370 905L295 764'/%3E%3Cpath d='M520 660L578 842 731 737 840 599 603 493 520 660 295 764 309 538 390 382 539 269 769 229 577.5 41.5 370 105 295 -36 126.5 79.5 237 261 102 382 40 599 -69 737 127 880'/%3E%3Cpath d='M520-140L578.5 42.5 731-63M603 493L539 269 237 261 370 105M902 382L539 269M390 382L102 382'/%3E%3Cpath d='M-222 42L126.5 79.5 370 105 539 269 577.5 41.5 927 80 769 229 902 382 603 493 731 737M295-36L577.5 41.5M578 842L295 764M40-201L127 80M102 382L-261 269'/%3E%3C/g%3E%3Cg fill='%23000000'%3E%3Ccircle cx='769' cy='229' r='5'/%3E%3Ccircle cx='539' cy='269' r='5'/%3E%3Ccircle cx='603' cy='493' r='5'/%3E%3Ccircle cx='731' cy='737' r='5'/%3E%3Ccircle cx='520' cy='660' r='5'/%3E%3Ccircle cx='309' cy='538' r='5'/%3E%3Ccircle cx='295' cy='764' r='5'/%3E%3Ccircle cx='40' cy='599' r='5'/%3E%3Ccircle cx='102' cy='382' r='5'/%3E%3Ccircle cx='127' cy='80' r='5'/%3E%3Ccircle cx='370' cy='105' r='5'/%3E%3Ccircle cx='578' cy='42' r='5'/%3E%3Ccircle cx='237' cy='261' r='5'/%3E%3Ccircle cx='390' cy='382' r='5'/%3E%3C/g%3E%3C/svg%3E");
}
main {
  background-color: rgba(221, 221, 221, 0.966);
  border-style: dotted;
}
button {
  background-color: transparent;
  border: 0px transparent;
  width: 21px;
}
.input-field {
  display: flex;
  justify-content: center;
  align-items: center;
}
.done {
  color: rgba(0, 0, 0, 0.445);
}
.checkeliboxeli {
  accent-color: black;
}



/* ************************************** */
/* Padding & avstånd css */
/* ************************************** */
main {
  margin: 100px 150px;
  padding-top: 20px;
  padding-bottom: 50px;
  border-radius: 10%;
}
ul {
  padding: 0px;
}

/* ************************************** */
/* Textbaserad css */
/* ************************************** */
@import url("https://fonts.googleapis.com/css2?family=IM+Fell+French+Canon+SC&display=swap");

h1 {
  font-size: 300%;
}
.done {
  text-decoration: line-through;
}
li {
  list-style-type: none;
  font-size: 150%;
}
</style>
