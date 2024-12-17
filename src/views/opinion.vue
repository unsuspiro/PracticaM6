<template>
    <div>
        <h1> Escribe tu opinion para el juego: {{ name_game }}</h1>
        <div>
            <form>
                <div class="form-group">
                    <label for="Nombre">Nombre</label>
                    <input type="text" v-model="name" id="Nombre" />
                </div>
                <div class="form-group">
                    <label for="Opinion">Opinion</label>
                    <textarea v-model="opinion" id="Opinion"></textarea>
                </div>
                <div class="form-group">
                    <button v-if="edit == null" @click.prevent="agregar">Agregar</button>
                    <button v-else @click="editEnding">Actualizar</button>
                </div>
            </form>

            <div>
                <div class="accordion" id="accordionExample">
                    <div class="accordion-item" v-for="(opinion, index) in opiniones" :key="index">
                        <h2 class="accordion-header">
                            <button class="accordion-button" type="button" data-bs-toggle="collapse"
                                :data-bs-target="'#collapse' + index" aria-expanded="true" aria-controls="collapseOne">
                                Opinion creada por: {{ opinion.name }}
                            </button>
                        </h2>
                        <div :id="'collapse' + index" class="accordion-collapse collapse" data-bs-parent="#accordionExample">
                            <div class="accordion-body">
                                {{ opinion.opinion }}
                                <div>
                                    <button @click="borrar(index)">Eliminar</button>
                                    <button @click="editar(index)">Editar</button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'opinion-view',
    props: {
        name_game: {
            type: String,
            required: true
        }
    },
    data: function () {
        return {
            name: '',
            opinion: '',
            opiniones: [],
            edit: null
        };
    },
    methods: {
        agregar() {
            let myOpinion = {
                name: this.name,
                opinion: this.opinion
            };
            this.opiniones.push(myOpinion);
            this.name = '';
            this.opinion = '';
        },
        borrar(index) {
            this.opiniones.splice(index, 1);
        },
        editar(index) {
            this.name = this.opiniones[index].name;
            this.opinion = this.opiniones[index].opinion;
            this.edit = index;
        },
        editEnding() {
            let editOpinion = {
                name: this.name,
                opinion: this.opinion
            };
            this.opiniones.splice(this.edit, 1, editOpinion);
            this.name = '';
            this.opinion = '';
            this.edit = null;
        }
    }
};
</script>

<style scoped>
/* Agregar márgenes y estilos al formulario */
form {
    margin: 20px;
    padding: 15px;
    border: 1px solid #ddd;
    border-radius: 8px;
    background-color: #f9f9f9;
}

.form-group {
    margin-bottom: 15px;
}

.form-group label {
    display: block;
    font-weight: bold;
    margin-bottom: 5px;
}

.form-group input,
.form-group textarea {
    width: 60%;
    padding: 10px;
    margin: 5px 0 10px 0;
    border: 1px solid #ccc;
    border-radius: 5px;
}

button {
    padding: 10px 15px;
    margin: 5px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

button:hover {
    background-color: #0056b3;
}

.accordion {
    margin-top: 20px;
}

.accordion-button {
    font-weight: bold;
}

.accordion-body {
    padding: 15px;
    background-color: #f1f1f1;
}

.accordion-item {
    margin-bottom: 10px;
}
</style>
