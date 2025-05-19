<template>
<div class="container-fluid mt-3" id="app">
        <input type="text" class="form-control m-2" v-model="criterioNombre"
            placeholder="Ingresar nombre o apellido">
        <input type="text" class="form-control m-2" v-model="criterioDni"
            placeholder="Ingresar DNI">

       <div v-if="mensajeAdvertencia" class="alert alert-warning" role="alert">
            {{ mensajeAdvertencia }}
        </div>

        <br>
        <div class="card-deck m-0">
            <div class="row">
                <div class="col" v-for="persona in personasFiltradas">
                    <div class="card mb-3">
                        <div class="card-body">
                            <h5 class="card-title">{{getNombreCompleto(persona)}}</h5>
                            <p class="card-text">dni {{persona.dni}}</p>
                            <a href="#" class="card-link">{{persona.correo}}</a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Filtro',
    props: [],
    data() {
        return {
            criterioNombre: '',
            criterioDni:'',
                    personas: [
                        {
                            nombre: "Daniel",
                            apellido: "Sanchez",
                            correo: "danielsanchez68@hotmail.com",
                            dni: "20442873"
                        },
                        {
                            nombre: "Juan",
                            apellido: "Perez",
                            correo: "j@p.gmail.com",
                            dni: "12345678"
                        },
                        {
                            nombre: "Ana",
                            apellido: "Suarez",
                            correo: "a@s.gmail.com",
                            dni: "87654321"
                        },
                        {
                            nombre: "Pablo",
                            apellido: "Merlo",
                            correo: "pm@email.com",
                            dni: "12345678"
                        },
                    ]
        }
    },
    methods: {
       getNombreCompleto(persona) {
                    return `${persona.nombre} ${persona.apellido}`
                }
    },
    computed: {
        personasFiltradas() {
                    return this.personas.filter((persona) => {

                        let getNombreCompletoFiltro = `${persona.nombre} ${persona.apellido}`;
                        let getDniFiltro = `${persona.dni}`;
                        return  getNombreCompletoFiltro.toLowerCase().includes(this.criterioNombre.toLowerCase()) &&
                                getDniFiltro.includes(this.criterioDni);
                    });
                },

        mensajeAdvertencia() {
        
            let nombreInvalido = this.criterioNombre.length > 0 && this.criterioNombre.length < 3;
            let dniInvalido = this.criterioDni.length > 0 && this.criterioDni.length < 3;

            if (nombreInvalido && dniInvalido) {
                return "El nombre y el DNI deben tener al menos 3 caracteres";
            } else if (nombreInvalido) {
                return "El nombre debe tener al menos 3 caracteres";
            } else if (dniInvalido) {
                return "El DNI debe tener al menos 3 caracteres";
            } else {
                return "";
                
            }

    }
        
    }
}
</script>

<style scoped>

</style>