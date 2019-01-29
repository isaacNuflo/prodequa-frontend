<template>
    <div>
        <div class="bg-contact3" style="background-image: url('images/bg-01.jpg');">
		<div class="container-contact3">
			<div class="wrap-contact3">
				<form class="contact3-form validate-form" @submit.stop.prevent="submit">
					<span class="contact3-form-title">
						Contact Us
					</span>

					<div class="wrap-contact3-form-radio">
						<div class="contact3-form-radio m-r-42">
							<input class="input-radio3" id="radio1" type="radio" name="choice" value="say-hi" checked="checked" @click="flag=false">
							<label class="label-radio3" for="radio1">
								Say Hi
							</label>
						</div>

						<div class="contact3-form-radio">
							<input class="input-radio3" id="radio2" type="radio" name="choice" value="get-quote" @click="flag=true">
							<label class="label-radio3" for="radio2">
								Get a Quote
							</label>
						</div>
					</div>

					<div class="wrap-input3 validate-input" data-validate="Name is required" v-if="flag">
						<input class="input3" type="text" name="name" placeholder="Your Name" v-model="persona.nombre">
						<span class="focus-input3"></span>
					</div>

					<div class="wrap-input3 validate-input" data-validate = "Valid email is required: ex@abc.xyz">
						<input class="input3" type="text" name="email" placeholder="Your Email" v-model="persona.correo">
						<span class="focus-input3"></span>
					</div>

					<div class="wrap-input3 input3-select">
						<div>
							<select class="select2" name="budget" v-model="persona.departamento">
								<option v-for="depa in departamentos" :key="depa.id_ubigeo" @click="mostrarProvincia(depa.id_ubigeo)">{{depa.nombre_ubigeo}}</option>
							</select>
						</div>
						<span class="focus-input3"></span>
					</div>

					<div class="wrap-input3 input3-select">
						<div>
							<select class="select-2" name="service" v-model="provincia">
								<option v-for="prov in provinciasById" :key="prov.id_ubigeo" @click="mostrarDistritos(prov.id_ubigeo)">{{prov.nombre_ubigeo}}</option>
							</select>
						</div>
						<span class="focus-input3"></span>
					</div>

					<div class="wrap-input3 validate-input" data-validate = "Message is required">
						<textarea class="input3" name="message" placeholder="Your Message"></textarea>
						<span class="focus-input3"></span>
					</div>

					<div class="container-contact3-form-btn">
						<button class="contact3-form-btn" type="submit">
							Obtener Descuento
						</button>
					</div>
				</form>
			</div>
		</div>
	</div>


	<div id="dropDownSelect1"></div>
    </div>
</template>

<script>
import axios from 'axios'
import departamentos from './departamentos'
import provincias from './provincias'
import distritos from './distritos'
export default {
	name: 'form',
	data(){
		return {
			flag:false,
			persona:{},
			departamentos: [],
			provincias: [],
			distritos: [],
			provinciasById:[],
			distritosById:[]
		}
	},
	methods: {
		async submit (){
			const headers = {
			'Access-Control-Allow-Origin': '*',
			'Access-Control-Allow-Methods': 'GET,PUT,POST,DELETE',
			'Access-Control-Allow-Headers': 'Content-Type'
			};
			
			const res = await axios.post('http://prodequa-backend.herokuapp.com/persona',this.persona,headers)
			const datos = await res.data
			return datos
		},
		mostrarProvincia(id){
			for(const prov in this.provincias){
				if(id === prov){
					this.provinciasById= this.provincias[prov];
				}
				}
		},
		mostrarDistritos(id) {
			for(const dis in this.distritos){
				if(id === dis){
					this.distritosById= this.distritos[dis];
				}
			}
		}
	},
	mounted(){
		this.departamentos = departamentos
		this.provincias = provincias
		this.distritos = distritos
  },
}
</script>

<style lang="es">
    
</style>