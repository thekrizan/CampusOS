# CampusOS

A simple campus issue management web app built using Svelte.

CampusOS lets students add campus issues, search for them, filter them by status, and mark them as resolved. It's a small prototype for a bigger idea of bringing useful campus services together in one place.

## Features

- Add a campus issue
- Search issues by title
- Filter issues by All, Open, and Resolved
- Mark issues as resolved
- View total, open, and resolved issue counts
- Responsive layout for desktop and mobile

## Built With

- Svelte 5
- JavaScript
- HTML and CSS
- Vite

## Run Locally

Make sure Node.js and npm are installed.

Clone the repository:

```bash
git clone https://github.com/thekrizan/CampusOS.git
cd CampusOS
```

Install the dependencies:

```bash
npm install
```

Start the development server:

```bash
npm run dev
```

Open the local URL shown in the terminal, usually `http://localhost:5173/`.

## Open on Mobile

You can open CampusOS on your phone if your phone and computer are connected to the same Wi-Fi network.

1. Start the development server with:

   ```bash
   npm run dev -- --host 0.0.0.0
   ```

2. Look for the **Network** URL displayed in the terminal.
3. Open that URL in your phone's browser.

If it doesn't work, check your firewall settings and make sure both devices can communicate over the Wi-Fi network.

## Current Limitations

- Issues are not saved permanently, so refreshing the page resets them.
- There is no backend or database yet.
- This is a student project prototype, not an official campus system.

## Future Plans

The idea is to add more campus-related features and gradually expand CampusOS into a platform for campus services.

## Project Status

A working prototype built to practise Svelte, JavaScript, and responsive web development.
