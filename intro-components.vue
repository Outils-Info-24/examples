<!-- App.vue -->
<template>
  <div>
    <h1>Composant Parent</h1>
    <ChildComponent :message="parentMessage" @customEvent="handleCustomEvent" />
    <p>{{ receivedMessage }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import ChildComponent from './ChildComponent.vue'

// Déclare un message à passer au composant enfant
const parentMessage = 'Bonjour depuis le parent!'

// Réception du message depuis l'événement
const receivedMessage = ref('')

const handleCustomEvent = (message) => {
  receivedMessage.value = message
}
</script>


<!-- ChildComponent.vue -->
<template>
  <div>
    <h2>Composant Enfant</h2>
    <p>{{ message }}</p>
    <button @click="sendEvent">Envoyer un événement</button>
  </div>
</template>

<script setup>
// Déclaration de la prop `message`
const props = defineProps({
  message: String
})

// Émission d'un événement avec un message
const emit = defineEmits(['customEvent'])

const sendEvent = () => {
  emit('customEvent', 'Message envoyé depuis l\'enfant!')
}
</script>
