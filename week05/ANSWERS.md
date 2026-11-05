# Week 05 — Answers

### 1. You refresh the browser on `/events/2` and the page loads. Which program answered that request in development, and what must the production server do so it still works after deployment?

In development, the Vite development server handles the request and serves the Vue application. In production, the web server must be configured to redirect unknown application routes to `index.html` so Vue Router can handle the URL.

### 2. The guard stops students from opening `/events/new`. Can a student still create an event? How, and what must stop them?

Yes. A student could bypass the frontend route guard and send a direct API request to create an event. The backend must check the user's role and reject unauthorized requests.

### 3. EventDetailPage loads its event in a watch on the id with immediate: true, not in onMounted. What bug would onMounted alone cause?

`onMounted` runs only once when the component is first created. If the user navigates from one event ID to another while reusing the same component, the event data would not reload. A watcher detects ID changes and fetches the correct event.

### 4. Why does EventsPage use storeToRefs(store) instead of const { events } = store?

Destructuring `events` directly from a Pinia store can lose its reactivity. `storeToRefs(store)` creates reactive references to the store's state and getters, so the page updates when the data changes.

### 5. Booking makes two requests: POST the booking, then PATCH the seat count. What happens to the data if the second one fails? How could the server avoid this?

The booking may be saved successfully, but the event's booked seat count remains unchanged. This creates inconsistent data between bookings and events. The server can avoid this by using a database transaction so both operations succeed or fail together.
