<template>
    <div class="grid">
        <div class="col-12">
            <div class="card" id="form">
                <h5>GENERAR EL RFC DE UNA PERSONA</h5>
                <div class="p-fluid formgrid grid">
                    <div class="field col-12">
                        <label for="nombre">Nombre(s):</label>
                        <InputText id="nombre" type="text" placeholder="Ingrese su nombre" v-model="nombre"/>
                    </div>
                    <div class="field col-12">
                        <label for="apepat">Apellido Paterno:</label>
                        <InputText id="lastname2" type="text" placeholder="Ingrese su apellido paterno" v-model="apePaterno" />
                    </div>
                    <div class="field col-12">
                        <label for="apemat">Apellido Materno:</label>
                        <InputText id="apemat" type="text" placeholder="Ingrese su apellido materno" v-model="apeMaterno" />
                    </div>
                    <div class="field col-12">
                        <label for="nacimiento">Fecha de Nacimiento:</label>
                        <InputText id="nacimiento" type="date" v-model="fecha" />
                    </div>
                   
                    <div class="field col-12 md:col-6">
                        <Button label="Generar RFC" class="p-button-outlined p-button-success mr-2 mb-2" @click="rfc()"  v-tooltip="'Click al presionar'"></Button>
                    </div>
                    <div class="field col-12">
                        <label for="rfcd">RFC:</label>
                        <InputText id="rfcd" type="text" v-model="RFC" readonly />
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default ({
    data() {
        return {
            nombre: '',
            apePaterno: '',
            apeMaterno: '',
            fecha: '',
            RFC: '',
            show: false,
            message: "Tienes Campos Vacios"
        };
    },
    methods: {
        rfc() {
            const characters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789';
            let result1 = '';
            if (this.nombre === '' || this.apePaterno === '' || this.apeMaterno === '' || this.fecha === '') {
                alert(this.message);

            }
            else {
                this.show = false;
                let fechaRFC = this.fecha.substring(2, 4) + this.fecha.substring(5, 7) + this.fecha.substring(8, 10);
                const charactersLength = characters.length;
                for (let i = 0; i < 3; i++) {
                    result1 += characters.charAt(Math.floor(Math.random() * charactersLength));
                }
                let cadena1 = this.apePaterno.substring(0, 2);
                let cadena2 = this.apeMaterno.substring(0, 1);
                let cadena3 = this.nombre.substring(0, 1);
                this.RFC = cadena1.toUpperCase() + cadena2.toUpperCase() + cadena3.toUpperCase() + fechaRFC + result1;
            }
        }
    }
})
</script>

<!--
<template>
    <div class="grid">
        <div class="col-12 md:col-12">
            <div class="card p-fluid">
                <h5>Generar RFC de una persona</h5>
                <div class="field">
                    <label for="name1">Nombre(s):</label>
                    <InputText id="name1" type="text" />
                </div>
                <div class="field">
                    <label for="name2">Apellido Paterno:</label>
                    <InputText id="name2" type="text" />
                </div>
                <div class="field">
                    <label for="name3">Apellido Materno:</label>
                    <InputText id="name3" type="text" />
                </div>
                <div class="field">
                    <label for="date1">Fecha de nacimiento:</label>
                    <InputText id="date1" type="date" />
                </div>
                <div class="field">
                    <label for="rfc">RFC:</label>
                    <InputText id="rfc" type="text" />
                </div>
                <div class="col-12 md:col-6">
                <Button label="Generar RFC" class="p-button-outlined p-button-success mr-2 mb-2" />
                </div>
            </div>
        </div>
    </div>
</template>
-->

