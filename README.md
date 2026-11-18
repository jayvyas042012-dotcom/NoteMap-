# NoteMap

Study helper. Paste a YouTube lesson, an image, or a PDF. NoteMap writes notes for each one, plus a mind map, a quiz, and a memory song.

Made by Jay Vyas, a 15-year-old entrepreneur.

## Run it

```bash
npm install
npm run dev
```

Open http://localhost:8080

Notes and the song voice need an xAI key in the environment:

```bash
export XAI_API_KEY=your_key_here
npm run dev
```

Get a key from the xAI console. Without it, the page still opens, but **Make my notes** cannot write a pack.

## Push to GitHub

```bash
git init
git add .
git commit -m "NoteMap"
git branch -M main
git remote add origin https://github.com/YOUR_NAME/notemap.git
git push -u origin main
```

Create the empty repository on GitHub first. Do not commit `.env` or `node_modules`.


## Deploy to Netlify (prepared configuration)

This project uses TanStack Start. The Netlify adapter is configured in
`vite.config.ts`, and `netlify.toml` installs the adapter during the build
because this prepared archive does not rewrite the existing npm lockfile.

1. Push the project files to a GitHub repository.
2. In Netlify, choose **Add new project → Import an existing project**.
3. Select GitHub and choose this repository.
4. Confirm the publish directory is `dist/client` and use the build command
   in `netlify.toml`.
5. Do not connect a production database or make the app public yet. The shipped
   `.grok/app-env.json` sets `VITE_AUTH_ENABLED` to `false`. With auth disabled
   and no database, the app uses one shared development user; visitors could
   see or overwrite each other's data. If a database is added while auth stays
   disabled, requests fail closed.
6. Before a real public launch, the project owner must provision the deployed
   authentication broker credentials and set `VITE_AUTH_ENABLED=true`,
   `DATABASE_URL`, `BETTER_AUTH_SECRET`, `BETTER_AUTH_URL`, `GROK_AUTH_ISSUER`,
   `GROK_AUTH_CLIENT_ID`, and `GROK_AUTH_CLIENT_SECRET` in Netlify's private
   environment settings. The OAuth broker must be configured for the final
   Netlify domain. Do not invent or reuse the sandbox preview credentials.
7. Add `XAI_API_KEY` privately for AI generation; never prefix it with `VITE_`.
   AI API usage may incur separate charges.
8. After auth and database are configured, deploy and test separate user
   accounts, data isolation, sign-in, PDF/YouTube processing, notes, mind maps,
   quizzes, and songs.

Important:
- Do not commit `.env`, API keys, database URLs, or OAuth secrets.
- The in-memory PGlite fallback is not durable production storage.
- Do not publicly launch the interactive app until real authentication and a
  persistent database have been configured and tested.
- For a more reproducible setup, add `@netlify/vite-plugin-tanstack-start` as
  a devDependency and regenerate/commit `package-lock.json` from a computer or
  cloud development environment.
