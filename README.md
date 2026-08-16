
# Atmos — Living Weather 🌦️

**Приложение, которое выглядит дороже чем iPhone Weather.** Каждая деталь продумана до атома.

![Build](https://github.com/yourname/atmos/actions/workflows/build-apk.yml/badge.svg)

## Фишки

- 🎥 **Живые видео-фоны** — 16 видео меняются от погоды + времени суток (утро/день/вечер/ночь) с crossfade 800ms
- 🌓 **Система времени** — `isDay` по реальному восходу/закату, полярный день/ночь учтен
- 🎨 Glassmorphism карточки с blur 20px
- 📈 Bezier-график температуры на 48 часов
- 🌅 Анимированная дуга солнца
- 💨 Компас ветра который вращается в реальном времени
- 📦 Оффлайн кэш Hive + бейдж "Обновлено 2 часа назад"

## Скриншоты

| Day | Night | Rain |
|-----|-------|------|
| ☀️ | 🌙 | 🌧️ |

## Установка

### 1. Получи ключ OpenWeatherMap
https://openweathermap.org/api/one-call-3-0 — бесплатно 1000 запросов/день

### 2. Добавь секрет в GitHub
Repo → Settings → Secrets and variables → Actions → New repository secret
- Name: `WEATHER_API_KEY`
- Value: твой ключ

### 3. Скачай APK
После push в `main` иди в Actions → Build Atmos APK → Artifacts → `atmos-apk-universal`

### Локально
```bash
cp .env.example .env
# вставь ключ в .env
flutter pub get
flutter run --dart-define=WEATHER_API_KEY=YOUR_KEY
# release
flutter build apk --release --dart-define=WEATHER_API_KEY=YOUR_KEY
```

## Архитектура

```
lib/
  core/
    theme/ — AppTheme с glassmorphism
    utils/ — weather_mapper, time_helper
  data/ — datasource, models
  domain/ — entities, repository
  presentation/
    bloc/ — WeatherBloc
    screens/ — home, search, settings
    widgets/ — карточки
```

## API

- `GET /geo/1.0/direct?q={city}`
- `GET /data/3.0/onecall?lat=&lon=&exclude=minutely&units=metric&lang=ru`
- `GET /data/2.5/air_pollution`

Ключ берется из `--dart-define` → fallback `.env` → никогда не хардкодится.

## Видео фоны

16 видео MP4 720p 8-15s seamless loop <4MB:
`clear_day, clear_night, partly_cloudy_day/night, cloudy_day/night, rain_day/night, heavy_rain_day/night, thunderstorm_day/night, snow_day/night, fog_day/night`

Если видео не загрузилось — fallback MeshGradient.

## Лицензия
MIT
