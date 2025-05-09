<template>
    <ion-content class="ion-padding">
      <ion-grid>
        <!-- Tarjetas resumen -->
        <ion-row>
          <ion-col size="12" size-md="3" v-for="(card, index) in resumenFacturas" :key="index">
            <ion-card :color="card.color">
              <ion-card-header>
                <ion-card-subtitle>{{ card.titulo }}</ion-card-subtitle>
                <ion-card-title>{{ card.valor }}</ion-card-title>
              </ion-card-header>
              <ion-card-content v-if="card.porcentaje">
                {{ card.porcentaje }}
              </ion-card-content>
            </ion-card>
          </ion-col>
        </ion-row>
  
        <!-- Tabla -->
        <ion-card>
          <ion-card-header>
            <ion-card-title>Facturas de Residentes</ion-card-title>
          </ion-card-header>
          <ion-card-content>
            <ion-grid>
              <ion-row class="tabla-encabezado">
                <ion-col size="2">Residente</ion-col>
                <ion-col size="2">Unidad</ion-col>
                <ion-col size="2">Factura #</ion-col>
                <ion-col size="1">Periodo</ion-col>
                <ion-col size="1">Total</ion-col>
                <ion-col size="1">Fecha Límite</ion-col>
                <ion-col size="1">Estado</ion-col>
                <ion-col size="2">Acciones</ion-col>
              </ion-row>
  
              <ion-row v-for="(factura, index) in facturasPaginadas" :key="index" class="tabla-fila">
                <ion-col size="2">{{ factura.residente }}</ion-col>
                <ion-col size="2">{{ factura.unidad }}</ion-col>
                <ion-col size="2">{{ factura.numero }}</ion-col>
                <ion-col size="1">{{ factura.periodo }}</ion-col>
                <ion-col size="1">{{ factura.total }}</ion-col>
                <ion-col size="1">{{ factura.fecha }}</ion-col>
                <ion-col size="1">
                  <ion-badge :color="estadoColor(factura.estado)">{{ factura.estado }}</ion-badge>
                </ion-col>
                <ion-col size="2">
                  <ion-button size="small" fill="clear">Ver</ion-button>
                  <ion-button size="small" fill="outline" color="tertiary">Recordar</ion-button>
                </ion-col>
              </ion-row>
            </ion-grid>
          </ion-card-content>
        </ion-card>
  
        <!-- Paginación -->
        <ion-row class="ion-justify-content-center ion-margin-top">
          <ion-button v-for="page in totalPaginas" :key="page" size="small" :fill="paginaActual === page ? 'solid' : 'outline'" @click="paginaActual = page">
            {{ page }}
          </ion-button>
        </ion-row>
      </ion-grid>
    </ion-content>
  </template>
  
  <script setup lang="ts">
  import {
    IonContent,
    IonGrid,
    IonRow,
    IonCol,
    IonCard,
    IonCardHeader,
    IonCardTitle,
    IonCardSubtitle,
    IonCardContent,
    IonBadge,
    IonButton
  } from '@ionic/vue'
  import { ref, computed } from 'vue'
  
  // Datos resumen
  const resumenFacturas = [
    { titulo: 'Total Facturas', valor: 142, color: 'primary' },
    { titulo: 'Pagadas', valor: 98, color: 'success', porcentaje: '69%' },
    { titulo: 'Pendientes', valor: 32, color: 'warning', porcentaje: '22%' },
    { titulo: 'Vencidas', valor: 12, color: 'danger', porcentaje: '9%' }
  ]
  
  // Datos estáticos de facturas
  const facturas = ref([
    { residente: 'Carolina Mendoza', unidad: 'Torre Norte, Apto 502', numero: 'F-2025-0342', periodo: 'Abril 2025', total: '$420.400', fecha: '01/04/2025', estado: 'Pendiente' },
    { residente: 'Luis Ramírez', unidad: 'Torre Sur, Apto 304', numero: 'F-2025-0343', periodo: 'Abril 2025', total: '$385.600', fecha: '01/03/2025', estado: 'Pago' },
    { residente: 'Ana Gómez', unidad: 'Torre Central, Apto 105', numero: 'F-2025-0344', periodo: 'Abril 2025', total: '$365.200', fecha: '01/03/2025', estado: 'Pendiente' },
    { residente: 'Roberto Jiménez', unidad: 'Torre Norte, Apto 801', numero: 'F-2025-0345', periodo: 'Abril 2025', total: '$420.600', fecha: '01/01/2025', estado: 'Pago' },
    { residente: 'Sofía Martínez', unidad: 'Torre Sur, Apto 702', numero: 'F-2025-0346', periodo: 'Abril 2025', total: '$385.600', fecha: '01/12/2024', estado: 'Vencida' },
    // Agrega más si lo deseas
  ])
  
  // Paginación
  const paginaActual = ref(1)
  const itemsPorPagina = 5
  
  const totalPaginas = computed(() =>
    Math.ceil(facturas.value.length / itemsPorPagina)
  )
  
  const facturasPaginadas = computed(() =>
    facturas.value.slice((paginaActual.value - 1) * itemsPorPagina, paginaActual.value * itemsPorPagina)
  )
  
  const estadoColor = (estado: string): string => {
    switch (estado.toLowerCase()) {
      case 'pago':
        return 'success'
      case 'pendiente':
        return 'warning'
      case 'vencida':
        return 'danger'
      default:
        return 'medium'
    }
  }
  </script>
  
  <style scoped>
  .tabla-encabezado {
    font-weight: bold;
    border-bottom: 1px solid var(--ion-color-step-150);
  }
  .tabla-fila {
    border-bottom: 1px solid var(--ion-color-step-100);
    padding: 8px 0;
  }
  </style>
  