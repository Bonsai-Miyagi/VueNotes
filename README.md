# VueNotes - A simple app to add notes

![Notes-List](https://github.com/IntuiTekPR/VueNotes/assets/139397019/5a4e2a38-7d04-4478-86f1-a7e3cfb9299f)

![Note-Modal](https://github.com/IntuiTekPR/VueNotes/assets/139397019/e402cc9b-ff2a-49c2-a22f-b33bf87af1a1)


This project is a note-taking application built with Vue.js 3 using the composition API. The application allows users to create notes with text and stores them in a local state. Each note has a random background color and a timestamp.

## VueJS 3 - Composition Api and Vite



## Methods and Template

Using ref from Vue to handle state and dayjs module to format dates on note footer. 

Two functions are defined, getRandomColor to generate a random color for each note, and addNote to add a new note to the notes state. 
addNote also validates that the note has at least 10 characters before adding it.

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```

### Additional Module for date format: dayjs

```sh
npm install dayjs
```
