# Clairvoyant-Frontend

Clairvoyant-Frontend is a modern web interface built with **Vue 3** and **Vuetify**, designed to present claim verification through an NLI pipeline.

## Features

- 🌐 Built with **Vue 3 Composition API**
- 🎨 Styled using **Vuetify** for a polished Material Design look
- ⚡ Data fetching from backend services
- 📱 Fully responsive layout

## Setup

```bash
git clone https://github.com/tom-avilius/Clairvoyant-Frontend.git
cd Clairvoyant-Frontend
npm install
```

## Run Development Server

```bash
npm run dev
```

## Build for Production

```bash
npm run build
```

## Environment Variables

Create a `.env` file for runtime configuration:

```env
VITE_API_KEY=your_gemini_api_key
```

## Project Structure

- `src/views/` — Vue pages showing results and loading states
- `src/components/` — Reusable Vuetify components
- `src/router/` — Vue Router setup
- `src/assets/` — Static assets like stylesheets and images

## License

GNU GPL v3
