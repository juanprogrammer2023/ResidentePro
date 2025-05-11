<template>
  <ion-page>
    <ion-content class="ion-padding">
      <div class="header-section">
        <h2>Bienvenido a <strong>residentePro</strong></h2>
        <p>Gestiona tus facturas y pagos de administración de forma fácil y segura.</p>
        <div class="actions">
          <ion-button color="primary" size="small">Ver facturas</ion-button>
          <ion-button fill="outline" size="small">Conoce más</ion-button>
        </div>
      </div>

      <ion-grid>
        <ion-row>
          <ion-col size-md="6">
            <ion-card>
              <ion-card-header>
                <ion-card-title>Facturas Residentes</ion-card-title>
              </ion-card-header>
              <ion-card-content>
                <table class="factura-table">
                  <thead>
                    <tr>
                      <th>Periodo</th>
                      <th>Total</th>
                      <th>Fecha Límite</th>
                      <th>Estado</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="factura in facturas" :key="factura.periodo">
                      <td>{{ factura.periodo }}</td>
                      <td>{{ factura.total }}</td>
                      <td>{{ factura.fechaLimite }}</td>
                      <td>
                        <ion-badge :color="getEstadoColor(factura.estado)">
                          {{ factura.estado }}
                        </ion-badge>
                      </td>
                    </tr>
                  </tbody>
                </table>
                <ion-button size="small" fill="clear">Ver historial completo →</ion-button>
              </ion-card-content>
            </ion-card>
          </ion-col>

          <ion-col size-md="6">
            <ion-card>
              <ion-card-header>
                <ion-card-title>Información de Residente</ion-card-title>
              </ion-card-header>
              <ion-card-content>
                <p><strong>Nombre:</strong> Carolina Mendoza Rojas</p>
                <p><strong>Unidad:</strong> Torre Norte, Apto 502</p>
                <p><strong>Código:</strong> RES-0135</p>
                <p><strong>Email:</strong> c.mendoza@example.com</p>
                <p><strong>Teléfono:</strong> +57 312555333111</p>
              </ion-card-content>
            </ion-card>
          </ion-col>
        </ion-row>
      </ion-grid>

      <h3 class="services-title">Nuestros Servicios</h3>
      <ion-grid>
        <ion-row>
          <ion-col size="12" size-md="4" v-for="servicio in servicios" :key="servicio.titulo">
            <ion-card class="service-card">
              <ion-card-content>
                <ion-icon :icon="servicio.icono" size="large"></ion-icon>
                <h4>{{ servicio.titulo }}</h4>
                <p>{{ servicio.descripcion }}</p>
              </ion-card-content>
            </ion-card>
          </ion-col>
        </ion-row>
      </ion-grid>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { IonPage, IonContent, IonGrid, IonRow, IonCol, IonCard, IonCardHeader, IonCardTitle, IonCardContent, IonButton, IonBadge, IonIcon } from '@ionic/vue';
import { cashOutline, documentTextOutline, notificationsOutline } from 'ionicons/icons';

const facturas = [
  { periodo: 'Abril 2025', total: '$420.400', fechaLimite: '15/04/2025', estado: 'Pendiente' },
  { periodo: 'Marzo 2025', total: '$420.400', fechaLimite: '15/03/2025', estado: 'Pago' },
  { periodo: 'Febrero 2025', total: '$420.600', fechaLimite: '15/02/2025', estado: 'Pago' }
];

const servicios = [
  { titulo: 'Pago en línea', descripcion: 'Realiza tus pagos de administración de forma segura a través de nuestra plataforma.', icono: cashOutline },
  { titulo: 'Historial de pagos', descripcion: 'Accede a todo tu historial de pagos y descarga tus comprobantes cuando lo necesites.', icono: documentTextOutline },
  { titulo: 'Notificaciones', descripcion: 'Recibe alertas sobre vencimientos y nuevas facturas directamente en tu correo.', icono: notificationsOutline }
];

function getEstadoColor(estado: string) {
  if (estado === 'Pago') return 'success';
  if (estado === 'Pendiente') return 'warning';
  return 'danger';
}
</script>

<style scoped>
.header-section {
  text-align: center;
  margin-bottom: 1.5rem;
}
.actions {
  margin-top: 1rem;
}
.factura-table {
  width: 100%;
  border-collapse: collapse;
  font-size: 0.9rem;
}
.factura-table th, .factura-table td {
  border-bottom: 1px solid #ccc;
  padding: 0.4rem 0.6rem;
  text-align: left;
}
.services-title {
  margin-top: 2rem;
  text-align: center;
  font-weight: bold;
}
.service-card ion-icon {
  color: var(--ion-color-primary);
  margin-bottom: 0.5rem;
  display: block;
}
</style>
