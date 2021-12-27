## Commands

All commands are run from the root of the project, from a terminal:

| Command           | Action                                       |
|:----------------  |:-------------------------------------------- |
| `npm install`     | Installs dependencies                        |
| `npm run dev`     | Starts local dev server at `localhost:3000`  |
| `npm run build`   | Build your production site to `./dist/`      |
| `npm run preview` | Preview your build locally, before deploying |

## Project Structure

The project structure looks similar to this and I place all my posts in the src/pages/posts/ directory

```
/
├── public/
│   └── favicon.ico
├── src/
│   ├── components/
│   │   └── BlogHeader.astro
│   └── pages/
│       └── posts/
│           └── posts.md
└── package.json
```

Astro looks for `.astro` or `.md` files in the `src/pages/posts/` directory. Each page is exposed as a route based on its file name.

There's nothing special about `src/components/`, but that's where any Astro/React/Vue/Svelte/Preact components live.

Any static assets, like images, can be placed in the `public/` directory.

