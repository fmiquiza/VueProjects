<template>
    <div>
        <h1>{{ titulo }}</h1>
        <div class="filtro">
            Buscar por nombre o correo electrónico (Search by name or email): <input type="search" v-model="textobuscar">
        </div>
        <table>
            <thead>
                <tr>
                    <th>ID</th>
                    <th>name</th>
                    <th>email</th>
                    <th>address</th>
                    <th>phone</th>
                    <th>country</th>
                    <th>city</th>
                    <th></th>
                </tr>
                <tr>
                    <th><input type="text" v-model="contactoNuevoObj.ID"></th>
                    <th><input type="text" v-model="contactoNuevoObj.name"></th>
                    <th><input type="text" v-model="contactoNuevoObj.email"></th>
                    <th><input type="text" v-model="contactoNuevoObj.address"></th>
                    <th><input type="text" v-model="contactoNuevoObj.phone"></th>
                    <th><input type="text" v-model="contactoNuevoObj.country"></th>
                    <th><input type="text" v-model="contactoNuevoObj.city"></th>         
                    <th><button @click="guardaNuevo()">Nuevo</button></th>
                </tr>
                <tr v-if="indexParaEditar !== null">
                    <th><input type="text" v-model="contactoEditarObj.ID"></th>
                    <th><input type="text" v-model="contactoEditarObj.name"></th>
                    <th><input type="text" v-model="contactoEditarObj.email"></th>
                    <th><input type="text" v-model="contactoEditarObj.address"></th>
                    <th><input type="text" v-model="contactoEditarObj.phone"></th>
                    <th><input type="text" v-model="contactoEditarObj.country"></th>
                    <th><input type="text" v-model="contactoEditarObj.city"></th>
                    <th><button @click="guardaEdicion()">Guardar</button></th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(contacto, index) in listacontactosComputada" :key="contacto.ID">
                    <td>{{contacto.ID}}</td>
                    <td>{{contacto.name}}</td>
                    <td>{{contacto.email}}</td>
                    <td>{{contacto.address}}</td>
                    <td>{{contacto.phone}}</td>
                    <td>{{contacto.country}}</td>
                    <td>{{contacto.city}}</td>
                    <td>
                        <button @click="eliminarcontacto(index)">Eliminar</button>
                        <button @click="Editarcontacto(contacto, index)">Editar</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
    name: 'MiComponente',
    data() {
        return {
            titulo: 'Registro - Agenda de Contactos',
            textobuscar: '',
            contactoNuevoObj: { 
                ID: "", 
                name: "", 
                email: "",
                address: "", 
                phone: "", 
                country: "",
                city: ""
            },
            contactoEditarObj: { 
                ID: "", 
                name: "",
                email: "", 
                address: "", 
                phone: "", 
                country: "",
                city: ""
            },  
            indexParaEditar:null, 
            contactos: [
               {"ID":1,"name":"Gibbs Carlson","email":"johnbonachonTESTfilter@myopium.com","address":"302 Montauk Avenue","phone":"+1 (833) 490-3903","country":"Turkmenistan","city":"Strong"},
               {"ID":2,"name":"Landry Chambers","email":"landrychambers@myopium.com","address":"517 Nolans Lane","phone":"+1 (968) 595-3406","country":"Iraq","city":"Lisco"},
               {"ID":3,"name":"Lakisha Mccullough","email":"MccullougLakishaTESTfilter@myopium.com","address":"651 Conover Street","phone":"+1 (974) 415-2100","country":"East Timor","city":"Eagletown"},
               {"ID":4,"name":"Burgess Cote","email":"burgesscote@myopium.com","address":"501 Anthony Street","phone":"+1 (962) 479-3192","country":"Bolivia","city":"Wakarusa"},
            ]
        }
    },
    components: {
        // componentes que se utilizaran.
    },
    methods: {
        // métodos que se pueden llamar desde la plantilla o desde otras partes del componente.
        guardaNuevo(){
            this.contactos.push(Object.assign({}, this.contactoNuevoObj));
        },
        eliminarcontacto(index){
            this.contactos.splice(index,1);
        },
        guardaEdicion(){
            this.contactos[this.indexParaEditar] = Object.assign({},this.contactoEditarObj);
            this.indexParaEditar = null;
        },
        Editarcontacto(contacto, index){
            this.indexParaEditar = index;
            this.contactoEditarObj = Object.assign({},contacto);
        }
    },
    computed: {
        // propiedades computadas que dependen de otras propiedades reactivas
        listacontactosComputada(){
            return this.contactos.filter(item => item.name.toLowerCase().includes(this.textobuscar.toLowerCase())||item.email.toLowerCase().includes(this.textobuscar.toLowerCase()));
        } 
    },
    props: {
        // propiedades que el componente puede recibir.
    },
    emits: [] // los eventos personalizados que el componente puede emitir.
}
</script >

<style scope>
h1 {
    color: #42b983;
}
table {
    width: 100%;
    border-collapse: collapse;
}
th, td {
    border: 1px solid #ddd;
    padding: 8px;
}
th {
    background-color: #f2f2f2;
    text-align: left;
}
</style>