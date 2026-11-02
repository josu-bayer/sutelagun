# Sutelagun

A recipe tracker and diet planner with a Basque interface (western Bizkaian). Every time a recipe is cooked again, a whole-recipe attempt is saved with a note on what changed, so older versions can always be restored.

## Contents

- [Features](#features)
- [How it is built](#how-it-is-built)
- [Data model](#data-model)
- [Running your own copy](#running-your-own-copy)
- [Security](#security)

## Features

- Whole-recipe version snapshots with notes: the cook view shows the current attempt and the History tab restores older ones.
- A Diet tab that follows a rolling 28-day meal plan, with a log of what was eaten each day.
- Installable on a phone, with offline use and sync on reconnect.

## How it is built

- A single `index.html` with inline HTML, CSS and JavaScript. No framework, no build step.
- Firebase Cloud Firestore and Hosting, loaded from the Firebase CDN.
- A network-first service worker, a web manifest and icons, so it installs on a phone.

## Data model

- `errezetak`: one document per recipe, with an append-only list of versions. Restoring only moves a pointer to the current version.
- `ezarpenak/dieta`: diet settings and the 28-day cycle.
- `egunerokoa`: one document per calendar date with the logged meals.

## Running your own copy

This repository ships with placeholder Firebase settings, so it needs your own project.

1. Create a Firebase project and enable Cloud Firestore.
2. Replace the `YOUR_...` values in the `firebaseConfig` object in `index.html` with your project values.
3. Run `firebase use --add`, then `firebase deploy`.

The app reads a second Firebase project for the shared shopping list (see zerrenda). If you do not use it, remove the second configuration block.

## Security

`firestore.rules` allows reads and writes without sign-in. That matches how the app was used, by one person and a few friends on a private link, and it is not suitable for anything sensitive on a public address. Add Firebase Authentication and owner-only rules before storing real data.

## Licence

MIT. See [LICENSE](LICENSE).
