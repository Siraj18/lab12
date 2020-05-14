<template>
    <div id="app">
        <p>Имя:
            <br>
            <input v-model="currentNotes.fName">
        </p>
        
        <p>Фамилия:
            <br>
            <input v-model="currentNotes.sName">
        </p>
        <p>Отчество:
            <br>
            <input v-model="currentNotes.tName">
        </p>
        <p>Номер телефона:
            <br>
            <input v-model="currentNotes.phone">
        </p>
        <p>Избранный?
            <input type="checkbox" v-model="currentNotes.favorite">
        </p>
        <p>По имени
            <input value="name" type="radio" v-model="sort" v-on:click="toggleSorting('name')">
        </p>
        <p>По фамилии
            <input value="second_name" type="radio" v-model="sort" v-on:click="toggleSorting('second_name')">
        </p>
        <p>
            <button v-on:click="toggleConfirm()">Сохранить</button>
        </p>
        <li v-for="(item, index) in notes" v-bind:key=index>
            {{item.sName}} {{item.fName}}  {{item.tName}} {{item.phone}}
            <span v-if="item.favorite"> Избранный</span>
        </li>

    </div>
</template>
<script>
    export default {
        name: "nodes_book",
        data() {
            return {
                sort: "name",
                notes: [],
                state: -1, 
                currentNotes: {
                    fName: "",
                    sName: "",
                    tName: "",
                    phone: "",
                    favorite: false
                }
                
            }
        },
        methods: {
            async toggleConfirm() {
                if (this.currentNotes.phone !== "") {
                    if (this.state === -1) {
                        this.notes.push({
                            fName: this.currentNotes.fName,
                            sName: this.currentNotes.sName,
                            tName: this.currentNotes.tName,
                            phone: this.currentNotes.phone,
                            favorite: this.currentNotes.favorite
                        });
                    
                    } else {
                        this.notes[this.state] = {
                            id: this.currentNotes.id,
                            fName: this.currentNotes.fName,
                            sName: this.currentNotes.sName,
                            tName: this.currentNotes.tName,
                            phone: this.currentNotes.phone,
                            favorite: this.currentNotes.favorite
                        };
                        
                        this.state = -1;
                    }
                    if (this.sort === "name") this.notes.sort((a, b) => a.fName < b.fName ? 1 : -1);
                    else if (this.sort === "second_name")this.notes.sort((a, b) => a.sName < b.sName ? 1 : -1);
                    this.notes.sort((a, b) => a.favorite < b.favorite ? 1 : -1);
                    this.currentNotes.fName = "";
                    this.currentNotes.sName = "";
                    this.currentNotes.tName = "";
                    this.currentNotes.phone = "";
                    this.currentNotes.favorite = "";
                } else 
                    alert("Пустые данные!");
            },
            toggleSorting (value) {
                if (value === "name") this.notes.sort((a, b) => a.fName < b.fName ? 1 : -1);
                else if (value === "second_name") this.notes.sort((a, b) => a.sName < b.sName ? 1 : -1);
                this.notes.sort((a, b) => a.favorite < b.favorite ? 1 : -1);
            }
            
           
        }
    }
</script>
<style scoped>
button {
    cursor: pointer;
    min-width: 200px;
    padding: 10px 5px;
    text-transform: uppercase;
    vertical-align: middle;
    background: #3da35a;
    border: none;
    color: #ffffff;
    font-weight: 200;
    border-radius: 5px;
    box-shadow: 0 0 10px rgb(56,100,38);
  }

input {
    color: #333;
    padding: 1rem 1rem;
    border-radius: 0.2rem;
    background-color: rgb(255, 255, 255);
    border: none;
    width: 10%;
    border-bottom: 0.3rem solid transparent;
}

  
li {
    padding: 5px;
}
</style>