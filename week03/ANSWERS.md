# Week 03 — Vue Components and Reactivity

## 1. Why should we not use the array index as `:key` in EventList?

When the list is filtered, the array indices can change, causing Vue to reuse a component for a different event. This might make local state, such as an open details panel, appear on the wrong card. Using `:key="e.id"` gives each event a unique and stable identity.

## 2. Why is `visible` a computed property instead of a function called from the template?

A computed property caches its result and only recalculates when its reactive dependencies change. When I type in the search box, the `search` ref changes, so Vue automatically updates the `visible` list. A function called from the template may run again whenever the component renders, even if the search data has not changed.

## 3. Why does EventCard emit `book` instead of changing `event.booked` directly?

First, EventCard should not directly modify data owned by its parent component. Second, emitting the `book` event allows App.vue to check seat availability and update the booking information. This keeps the components organized and makes the code easier to maintain.

## 4. Why does `const { booked } = reactive(event); booked++` not update the page?

Destructuring a primitive property from a reactive object loses its reactive connection. Increasing `booked` only changes the local variable, not the original event's property. To update the page, we can modify a writable reactive object's property directly or use `toRefs()` to preserve reactivity.

## 5. Where does `myBookings` live, and why not in EventCard or EventList?

`myBookings` lives in App.vue because App manages the events and booking state. EventCard is responsible for displaying individual events, while EventList handles searching and filtering. Keeping `myBookings` in App allows the application to manage all bookings and update the total booking count.
