<template>
  <ion-page>
    <ion-header translucent>
      <ion-toolbar>
        <ion-title>Inicio de Sesión</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content class="ion-padding" :fullscreen="true">
      <div class="container">
        <ion-card>
          <ion-card-header>
            <ion-card-title>Inicia Sesión</ion-card-title>
            <ion-card-subtitle>Accede a tu cuenta de residente</ion-card-subtitle>
          </ion-card-header>

          <ion-card-content>
            <form @submit.prevent="iniciarSesion">
              <ion-item>
                <ion-label position="floating">
                  <ion-icon :icon="mailOutline" class="ion-margin-end"></ion-icon>
                  Correo electrónico
                </ion-label>
                <ion-input
                  v-model="form.email"
                  type="email"
                  required
                  placeholder="tu@email.com"
                  class="custom-input"
                ></ion-input>
                <ion-note slot="error" v-if="errors.email">{{ errors.email }}</ion-note>
              </ion-item>

              <ion-item>
                <ion-label position="floating">
                  <ion-icon :icon="lockClosedOutline" class="ion-margin-end"></ion-icon>
                  Contraseña
                </ion-label>
                <ion-input
                  v-model="form.password"
                  :type="showPassword ? 'text' : 'password'"
                  required
                  placeholder="Ingresa tu contraseña"
                  class="custom-input"
                ></ion-input>
                <div class="password-toggle" @click="showPassword = !showPassword">
                  <ion-icon :icon="showPassword ? eyeOff : eye"></ion-icon>
                </div>
                <ion-note slot="error" v-if="errors.password">{{ errors.password }}</ion-note>
              </ion-item>

              <div class="options-row">
                <ion-checkbox v-model="form.recordar">Recordarme</ion-checkbox>
                <a href="/reset-password" class="forgot-password">¿Olvidaste tu contraseña?</a>
              </div>

              <ion-button type="submit" expand="block" class="ion-margin-top">
                <ion-icon :icon="logInOutline" slot="start"></ion-icon>
                Iniciar Sesión
              </ion-button>

              <div class="divider">
                <span>O</span>
              </div>

              <ion-button expand="block" fill="outline" class="social-button">
                <ion-icon :icon="logoGoogle" slot="start"></ion-icon>
                Continuar con Google
              </ion-button>
            </form>

            <div class="register-link">
              ¿No tienes una cuenta? <a href="/sesion">Regístrate</a>
            </div>
          </ion-card-content>
        </ion-card>
      </div>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonCard,
  IonCardHeader,
  IonCardTitle,
  IonCardSubtitle,
  IonCardContent,
  IonItem,
  IonLabel,
  IonInput,
  IonButton,
  IonIcon,
  IonNote,
  IonCheckbox,
  alertController
} from '@ionic/vue'
import {
  mailOutline,
  lockClosedOutline,
  logInOutline,
  eye,
  eyeOff,
  logoGoogle
} from 'ionicons/icons'

const form = ref({
  email: '',
  password: '',
  recordar: false
})

const errors = ref({
  email: '',
  password: ''
})

const showPassword = ref(false)

const validarFormulario = () => {
  let isValid = true
  
  // Resetear errores
  Object.keys(errors.value).forEach(key => {
    if (key in errors.value) {
      (errors.value as Record<string, string>)[key] = ''
    }
  })
  
  // Validar email
  if (!form.value.email) {
    errors.value.email = 'El correo electrónico es obligatorio'
    isValid = false
  } else if (!/^[\w-\.]+@([\w-]+\.)+[\w-]{2,4}$/.test(form.value.email)) {
    errors.value.email = 'Ingresa un correo electrónico válido'
    isValid = false
  }
  
  // Validar contraseña
  if (!form.value.password) {
    errors.value.password = 'La contraseña es obligatoria'
    isValid = false
  }
  
  return isValid
}

const mostrarAlerta = async (header: string, message: string) => {
  const alert = await alertController.create({
    header,
    message,
    buttons: ['OK']
  })
  await alert.present()
}

const iniciarSesion = async () => {
  if (!validarFormulario()) {
    return
  }
  
  try {
    // Aquí iría la lógica para enviar los datos al backend
    console.log('Datos de inicio de sesión:', form.value)
    
    // Simular procesamiento
    await new Promise(resolve => setTimeout(resolve, 1000))
    
    // Simular éxito (en un caso real, aquí iría la redirección al dashboard)
    await mostrarAlerta('¡Bienvenido!', 'Has iniciado sesión correctamente')
    
    // Aquí iría la lógica de redirección o actualización de estado global
  } catch (error) {
    console.error('Error al iniciar sesión:', error)
    await mostrarAlerta('Error', 'Credenciales incorrectas o problemas de conexión.')
  }
}
</script>

<style scoped>
ion-content {
  --background: #f8f9fa;
}

.container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100%;
  padding: 20px;
}

ion-card {
  width: 100%;
  max-width: 450px;
  margin: 0;
  border-radius: 16px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
  overflow: hidden;
}

ion-card-header {
  padding: 24px;
  background-color: #ffffff;
  border-bottom: 1px solid #f0f0f0;
}

ion-card-title {
  font-size: 24px;
  font-weight: 700;
  color: #2c3e50;
  margin-bottom: 6px;
  text-align: center;
}

ion-card-subtitle {
  font-size: 16px;
  color: #7f8c8d;
  text-align: center;
}

ion-card-content {
  padding: 24px;
  background-color: #ffffff;
}

ion-item {
  --padding-start: 0;
  --padding-end: 0;
  --inner-padding-end: 0;
  --background: transparent;
  --border-color: #e0e0e0;
  margin-bottom: 18px;
}

ion-input {
  --padding-start: 0;
  --color: #2c3e50;
  --cursor-color: #3880ff;
}

.custom-input {
  caret-color: #3880ff;
  cursor: text !important;
}

ion-label {
  --color: #7f8c8d;
  font-weight: 500;
}

ion-button {
  --background: #3880ff;
  --background-activated: #3171e0;
  --background-hover: #4d8dff;
  --color: #ffffff;
  --border-radius: 8px;
  margin-top: 16px;
  height: 48px;
  font-weight: 600;
  font-size: 16px;
  text-transform: none;
}

.social-button {
  --background: transparent;
  --background-activated: rgba(0, 0, 0, 0.04);
  --background-hover: rgba(0, 0, 0, 0.04);
  --color: #5f6368;
  --border-color: #dadce0;
}

.password-toggle {
  position: absolute;
  right: 10px;
  top: 50%;
  transform: translateY(-50%);
  z-index: 2;
  padding: 8px;
  color: #7f8c8d;
  cursor: pointer;
}

.options-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 8px;
  margin-bottom: 8px;
  font-size: 14px;
}

.forgot-password {
  color: #3880ff;
  text-decoration: none;
  font-weight: 500;
}

.register-link {
  margin-top: 24px;
  text-align: center;
  color: #7f8c8d;
  font-size: 15px;
}

.register-link a {
  color: #3880ff;
  text-decoration: none;
  font-weight: 500;
}

.divider {
  display: flex;
  align-items: center;
  text-align: center;
  margin: 24px 0;
  color: #7f8c8d;
}

.divider::before,
.divider::after {
  content: '';
  flex: 1;
  border-bottom: 1px solid #e0e0e0;
}

.divider span {
  padding: 0 16px;
  font-size: 14px;
}

ion-note {
  color: #e74c3c;
  font-size: 12px;
  padding-top: 4px;
}

ion-checkbox {
  --size: 18px;
  --checkbox-background-checked: #3880ff;
  margin-right: 8px;
}
</style>