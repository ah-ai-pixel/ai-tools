# Anime AI 🎨

Flutter MVP-застосунок: користувач завантажує фото, а нейромережа (через Replicate API)
генерує його версію у стилі японського аніме.

## Як це працює

1. Користувач обирає фото з галереї або робить нове фото камерою.
2. Фото кодується в base64 і надсилається у Replicate API (модель AnimeGANv2 / img2img).
3. Застосунок опитує статус генерації, поки вона не завершиться.
4. Готове аніме-фото показується на екрані, його можна зберегти в галерею.

API токен користувач вводить один раз при першому запуску — зберігається локально
через `flutter_secure_storage`, ніколи не потрапляє в код чи git.

## Структура проєкту

```
lib/
  main.dart                        # точка входу, перевірка збереженого токена
  screens/
    api_key_setup_screen.dart      # введення API токена (перший запуск)
    home_screen.dart               # вибір фото, генерація, результат
  services/
    replicate_service.dart         # логіка звернення до Replicate API
```

## Запуск локально

1. Встановіть [Flutter SDK](https://docs.flutter.dev/get-started/install) (≥3.0).
2. Встановіть залежності:
   ```bash
   flutter pub get
   ```
3. (Опціонально) створіть `.env` на основі `.env.example` — але зазвичай токен
   зручніше ввести прямо в застосунку при першому запуску.
4. Запустіть на підключеному пристрої/емуляторі:
   ```bash
   flutter run
   ```

## Отримати Replicate API токен

Зареєструйтесь на [replicate.com](https://replicate.com), токен буде тут:
https://replicate.com/account/api-tokens — є безкоштовний ліміт для тестів.

## Заміна AI-моделі

У файлі `lib/services/replicate_service.dart` є константа `_modelVersion`.
Можна замінити на будь-яку іншу img2img/style-transfer модель з
[replicate.com/explore](https://replicate.com/explore) — просто вставте
її `owner/model:version`.

## Наступні кроки для продакшн-версії

- Додати кешування результатів та історію згенерованих фото.
- Обробити ліміти/помилки API (rate limits, невалідне фото).
- Додати вибір різних аніме-стилів (Studio Ghibli, Shonen, Chibi тощо).
- Розглянути власний backend, щоб не зберігати API-ключ на пристрої користувача.

---

## Як завантажити цей код на свій GitHub

Виконайте в терміналі в папці проєкту:

```bash
git init
git add .
git commit -m "Initial commit: Anime AI Flutter MVP"
git branch -M main
git remote add origin https://github.com/ВАШ_ЛОГІН/НАЗВА_РЕПОЗИТОРІЮ.git
git push -u origin main
```

Перед цим створіть порожній репозиторій на github.com (без README/gitignore,
щоб уникнути конфліктів) і підставте його URL у команду `git remote add origin`.
