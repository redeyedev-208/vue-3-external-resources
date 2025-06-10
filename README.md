# 📚 Vue 3 Resource Guide

A simple and accessible Vue 3 application for managing and viewing educational resources.  
Designed as a learning tool and reference for Vue.js best practices, accessibility, and UI patterns.

---

## ✨ Features

- Add and remove resource links with title and description
- Persist resources using `localStorage`
- Accessible form fields with helper descriptions
- Landmarks and ARIA labels for screen reader support
- Toggle to show/hide accessibility guidance
- Opens external links in new tabs with proper `rel` attributes
- Modular, component-based structure using Vue 3 Composition API

---

## 🚀 Technologies Used

- Vue.js 3 (Composition API)
- Custom reusable components (`BaseCard`, `BaseButton`, `BaseDialog`)
- Scoped styles with accessibility-first CSS practices
- `localStorage` for client-side persistence

---

## 📷 Preview

![vue-3-a11y-demo](https://github.com/user-attachments/assets/82740cb9-4284-4bd3-850d-a23199b3bf16)


---

## 📦 Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) (v18 or higher recommended)
- npm or Yarn

### Installation

```bash
git clone git@github.com:redeyedev-208/vue-3-external-resources.git
cd vue3-resource-guide
npm install
```

---
## Run the App Locally
`npm run dev`
---
## Usage
- [ ] Click "Add Resource" to enter a title, description, and a valid URL

- [ ] Click "Stored Resources" to view your saved items

- [ ] Toggle Accessibility Helper Descriptions for screen reader hints

- [ ] Click "Delete" to remove any item

- [ ] Resources are saved automatically to your browser's localStorage

---

## Accessibility Highlights
- [ ] Correct usage of aria

- [ ] Addressing Critical and Serious Issues (Moderate is only on the resource link)

- [ ] Screen-reader friendly helper descriptions on form inputs

- [ ] Keyboard navigable with clear focus styles

- [ ] Minimal use of dynamic content without appropriate roles



