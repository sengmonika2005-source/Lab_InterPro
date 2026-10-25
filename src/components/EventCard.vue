<script setup lang="ts">
import { computed } from "vue";
import type { CampusEvent } from "../types";
import { formatDate, seatsLeft } from "../format";

// TODO 1: Receive event data from parent
const props = defineProps<{
  event: CampusEvent;
}>();

// TODO 2: Emit booking event with event id
const emit = defineEmits<{
  book: [id: number];
}>();

// TODO 3: Computed values
const left = computed(() => seatsLeft(props.event));

const isFull = computed(() => left.value <= 0);

const almostFull = computed(() => left.value >= 1 && left.value <= 5);
</script>

<template>
  <!-- TODO 4 & 5: Display event data and full class -->
  <article class="card" :class="{ full: isFull }">
    <p class="category">{{ event.category }}</p>

    <h2>{{ event.title }}</h2>

    <p class="meta">{{ formatDate(event.startsAt) }} · {{ event.location }}</p>

    <!-- TODO 6: Full badge or remaining seats -->
    <p v-if="isFull" class="badge">Full</p>

    <p v-else class="seats" :class="{ warn: almostFull }">
      {{ left }} {{ left === 1 ? "seat" : "seats" }} left
    </p>

    <!-- TODO 7: Booking button -->
    <button :disabled="isFull" @click="emit('book', event.id)">
      Book a seat
    </button>
  </article>
</template>

<style scoped>
.card {
  background: white;
  border-radius: 10px;
  padding: 16px;
  display: flex;
  flex-direction: column;
  gap: 6px;
}
.card.full {
  opacity: 0.7;
}
h2 {
  font-size: 1.1rem;
  margin: 0;
}
.category {
  text-transform: uppercase;
  font-size: 0.75rem;
  letter-spacing: 0.05em;
  color: #3178c6;
  margin: 0;
}
.meta {
  color: #6b7280;
  margin: 0;
}
.seats,
.badge {
  margin: 0;
  font-weight: 600;
}
.warn {
  color: #d73a49;
}
.badge {
  color: white;
  background: #d73a49;
  align-self: flex-start;
  padding: 2px 10px;
  border-radius: 999px;
}
button {
  margin-top: auto;
  align-self: flex-start;
}
</style>
