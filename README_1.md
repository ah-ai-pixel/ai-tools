# Anime AI 🎨

A Flutter MVP app: the user uploads a photo, and a neural network (via the Replicate API)
generates a version of it in Japanese anime style.

## How it works

1. The user picks a photo from the gallery or takes a new one with the camera.
2. The photo is encoded as base64 and sent to the Replicate API (AnimeGANv2 / img2img model).
3. The app polls the generation status until it's complete.
4. The finished anime photo is shown on screen and can be saved to the gallery.

The user enters their API token once, on first launch — it's stored locally
via `flutter_secure_storage` and never ends up in the code or in git.

## Project structure

```
lib/
  main.dart                        # entry point, checks for a saved token
  screens/
    api_key_setup_screen.dart      # API token input (first launch)
    home_screen.dart               # photo picker, generation, result
  services/
    replicate_service.dart         # logic for calling the Replicate API
```

## Running locally

1. Install [Flutter SDK](https://docs.flutter.dev/get-started/install) (≥3.0).
2. Install dependencies:
   ```bash
   flutter pub get
   ```
3. (Optional) create a `.env` file based on `.env.example` — though it's usually
   more convenient to enter the token directly in the app on first launch.
4. Run on a connected device/emulator:
   ```bash
   flutter run
   ```

## Getting a Replicate API token

Sign up at [replicate.com](https://replicate.com), then get your token here:
https://replicate.com/account/api-tokens — there's a free tier for testing.

## Swapping the AI model

The `_modelVersion` constant lives in `lib/services/replicate_service.dart`.
You can replace it with any other img2img/style-transfer model from
[replicate.com/explore](https://replicate.com/explore) — just paste in
its `owner/model:version`.

## Next steps for a production version

- Add result caching and a history of generated photos.
- Handle API limits/errors (rate limits, invalid photo).
- Add a choice of different anime styles (Studio Ghibli, Shonen, Chibi, etc.).
- Consider a dedicated backend so the API key isn't stored on the user's device.

---

## How to upload this code to your own GitHub

Run these commands in the project folder in your terminal:

```bash
git init
git add .
git commit -m "Initial commit: Anime AI Flutter MVP"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
git push -u origin main
```

Before that, create an empty repository on github.com (without a README/gitignore,
to avoid conflicts) and use its URL in the `git remote add origin` command.
