# expo-metro-file-map-watcher-error

An error a watcher backend of `@expo/metro-file-map` reports ends the dev server, because nothing listens for it. This repository is `npx create-expo-app@latest --template blank` (Expo 58.0.21, `@expo/metro-file-map` 58.0.5) with `npx expo install --fix` run once, and one folder, `watched/`, holding `value.js`.

## Steps

Linux, npm, the development server only.

1. Clone and install:
   ```sh
   git clone https://github.com/YevheniiKotyrlo/expo-metro-file-map-watcher-error
   cd expo-metro-file-map-watcher-error
   npm install
   ```
2. Start the dev server and wait for `Waiting on http://localhost:8081`:
   ```sh
   npx expo start
   ```
3. In a second terminal, in the same folder, take every permission off the folder:
   ```sh
   chmod 000 watched
   ```

Expected: the watcher reports that it cannot read the folder, and the dev server goes on.

What I see on Ubuntu (WSL 2, Node 26.12.1): the dev server exits with code 7 and `Error: EACCES: permission denied, lstat '…/watched/watched'`, emitted as an `'error'` event from `FallbackWatcher.emitError`.
