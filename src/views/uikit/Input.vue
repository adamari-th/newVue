<template>

<div class="p-grid">
		<div class="p-col-12">
			<div class="card">
			<Panel header="PUNTO DE VENTA (POS)" style="height: 100%">
				<Toolbar class="p-mb-4"> <!--BARRA DE HERRAMIENTA-->
				<template v-slot:start> <!--START: SE AGREGA LOS TEXTOS-->
                                                                                        <!--CON EL v-model SE PASA AL OBJETO. TODO ESTO PARA PODER INGRESAR UN DATO-->
					<InputText type="text" size="40" placeholder="Nombre del producto..." v-model="productoItem.nomProducto"/>
					<InputText type="text" placeholder="Cant" v-model="productoItem.cantidad"/>
					<InputText type="text" placeholder="$ Precio U." v-model="productoItem.precioUnitario"/>									
				</template>
				<template v-slot:end> <!--END: SE AGREGA EL BOTON. LA PARTE FINAL-->
					<Button label="Registrar" icon="pi pi-plus" class="p-button-success p-mr-2" @click="registrarCompra" />	
				</template>
				</Toolbar>
				<br>

                <DataTable :value="tablaCompras" v-model:selection="productoItem" class="p-datatable-gridlines" dataKey="cns" :rows="5" 
				paginatorTemplate="FirstPageLink PrevPageLink PageLinks NextPageLink LastPageLink CurrentPageReport RowsPerPageDropdown"
				:rowsPerPageOptions="[5,10,25]"
				currentPageReportTemplate="Visualizando {last} de {totalRecords} productos"
				style="margin-bottom: 20px" :paginator="true" responsiveLayout="scroll">
                
                <!--FIELD: UN INDICADOR AL QUE SE REFIERE, ES EL QUE BUSCA A NIVEL DE DATO
                        HEADER: ES LO QUE SE VE, LA PARTE VISIBLE-->				
			
				<Column field="cns" header="Cns" :sortable="true" style="width:50px"></Column>
				<Column field="nomProducto" header="Nombre del Producto" style="width:370px"></Column>				
				<Column field="precioUnitario" header="Precio U." dataType="numeric" style="width:80px">
					<template #body="slotProps">
                            {{ formatoMoneda(slotProps.data.precioUnitario) }}
                    </template>
				</Column>
				<Column field="cantidad" header="Cant." style="width:60px;text-align:center"></Column>
				<Column field="precioParcial" header="Precio P." style="width:80px">
					<template #body="slotProps">
                            			{{ formatoMoneda(slotProps.data.precioParcial) }}
                    			</template></Column>
				<Column style="width:140px">
					<template #header>
						Acciones
					</template>
					<template #body="slotProps">
                        <Button icon="pi pi-pencil" type="button" class="p-button-success p-mr-2 p-mb-1" @click="editarProductos(slotProps.data)"></Button>
                        <Button icon="pi pi-trash" type="button" class="p-button-danger p-mb-1" @click="confirmaEliminarProductos(slotProps.data)"></Button>
					</template>
				</Column>
			</DataTable>

                <br>
				<Toolbar class="p-mb-4">
				<template v-slot:start>
				
				</template>
				<template v-slot:end>
                    <label for="subtotal">SubTotal: </label>
					<InputText type="text" placeholder="$ "/>	
                    <label for="iva">IVA (16%): </label>
					<InputText type="text" placeholder="$ "/>	
					<label for="total">Total: </label>
					<InputText type="text" placeholder="$ "/>	
				</template>
				</Toolbar>
			</Panel>

            <!--MENSAJE-->
			<Toast/>  
			</div>	
		</div>
	</div>
    
</template>

<script>
export default {
    data() {
        return {                			
			tablaCompras: [
			{"cns": 1, "nomProducto": "Impresora LaserJet Color", "cantidad": 2, "precioUnitario": 5200.00, "precioParcial": 10400.00},
			{"cns": 2, "nomProducto": "Monitor LED 31 plg.", "cantidad": 3, "precioUnitario": 1700.00, "precioParcial": 5100.00},
            {"cns": 3, "nomProducto": "Escritorio moderno.", "cantidad": 10, "precioUnitario": 2100.00, "precioParcial": 21000.00}
			],
			productoItem: {
				cns: null,
				nomProducto: null,
				cantidad:null,
				precioUnitario:null,
				precioParcial:null
			}
		}
		},
		created() {
			
		},		
		methods: {
			formatoMoneda(value) {
				if(value)
					return value.toLocaleString('en-US', {style: 'currency', currency: 'USD'});
				return;
			},	
			registrarCompra(){	
                //aqui se ingresa como sacar el precio parcial
                this.productoItem.precioParcial = this.productoItem.precioUnitario * this.productoItem.cantidad;

                //METODO push: SIRVE PARA AGREGAR UN NUEVO VALOR (PARECIDO A LAS LISTAS lista1.add(obj))
                //PUSH: EMPUJAR			
				this.tablaCompras.push(this.productoItem);
                //MENSAJE DE CONFIRMACION CON EL METODO toast
				this.$toast.add({severity:'success', summary: 'Confirmación', detail: 'Nueva compra registrada', life: 3000});
			},		
			editarProductos() {				
							
			},
			confirmaEliminarProductos() {
						
			}
        }    
}
</script>