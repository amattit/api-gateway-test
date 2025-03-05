# /api/wave/v1/personal

# Описание метода получения треков для волны

Метод позволяет получить треки для волны, отправить фидбек пользователя на прослушанный трек, а также передавать настроение, выставленное пользователем в тюнере. Контракт в сервисе `personalwave-gateway` см. на странице `query personalWaveContent`.

## Параметры запроса

### Метод POST

### Заголовки (Headers)

| Параметр           | Описание                                       | Тип | По умолчанию | Обязательность | Пример                                |
|---------------------|----------------------------------------------|------------|-----------------------|-------------------------|---------------------------------------|
| X-API-KEY         | Партнерский ключ доступа к Endpoint           | string     | -                     | Да                       | 066138de590d4f108000bfc5c9313a02    |
| X-Auth-Token      | Токен пользователя                           | string     | -                     | Да                       | 066138de590d4f108000bfc5c9313a02    |
| x-zvuk-profile-type | Тип профиля пользователя. Возможные значения: "kid", "guest" | enum | - | Нет | guest |
| x-zvuk-profile-id | Идентификатор профиля пользователя            | bigint     | -                     | Нет                      | 1242143155                          |

### Параметры запроса (Query Parameters)

| Параметр               | Описание                                      | Тип | По умолчанию | Обязательность | Пример                                |
|-------------------------|----------------------------------------------|------------|-----------------------|--------------------------|---------------------------------------|
| include_stream_links  | Определяет, включать ли ссылки на стримы. | boolean | false | Нет | false |

### Тело запроса (Body)

| Параметр               | Описание                                      | Тип | По умолчанию | Обязательность | Обязательность значения | Пример                                |
|-------------------------|----------------------------------------------|------------|-----------------------|--------------------------|-------------------------|---------------------------------------|
| limit                | Количество треков в ответе. | integer | 1 | Нет | Нет | 1 (максимум 2) |
| settings.filter_explicit | Флаг фильтрации треков с признаком 18+. | boolean | False | Нет | Нет | False |
| settings.diversity    | "любимое-новое". В диапазоне [0: 1] | float | - | Нет | Нет | 0.3 |
| settings.mood.energy  | "настроение". В диапазоне [0: 1] | float | 0.5 | Нет | Нет | 0.5 |
| settings.mood.fun     | "настроение". В диапазоне [0: 1] | float | 0.5 | Нет | Нет | 0.5 |
| settings.popular      | "популярное". В диапазоне [0: 1] | float | - | Нет | Нет | 0.1 |
| settings.vocal        | "есть вокал". В диапазоне [0: 1] | float | - | Нет | Нет | 0.1 |
| settings.language     | "язык". Возможные значения: "russian", "foreign" | enum | - | Нет | Нет | russian |
| settings.situation    | "ситуация" | string | - | Нет | Нет | - |
| settings.genre        | "жанр" | string | - | Нет | Нет | - |
| listened_track        | Объект | Object | - | Нет | Нет | - |
| listened_track.id     | Уникальный идентификатор прослушанного трека | integer | - | Нет | Да | 2432536 |
| listened_track.duration | Длительность трека | integer | - | Нет | Да | 70 |
| listened_track.is_skipped | Признак того, что пользователь пропустил трек | boolean | - | Нет | Да | True |
| listened_track.play_duration | Время (сек) прослушивания трека пользователем | integer | - | Нет | Да | 12 |
| listened_track.user_reaction | Отклик пользователя по треку. Возможные значения: LIKED – если в течение прослушивания трек был добавлен в коллекцию; DISLIKED – если на момент переключения трек был заблокирован | enum | - | Нет | Нет | LIKED |

## Маппинг на параметры запроса

| Параметр               | Маппинг на параметры запроса                 |
|-------------------------|----------------------------------------------|
| X-API-KEY             | -                                            |
| X-Auth-Token          | -                                            |
| x-zvuk-profile-type   | x-zvuk-profile-type                        |
| x-zvuk-profile-id     | x-zvuk-profile-id                          |
| limit                 | -                                            |
| include_stream_links  | -                                            |
| settings.filter_explicit | PersonalWaveOptions.filterExplicit         |
| settings.diversity    | PersonalWaveOptions.diversity              |
| settings.mood.energy  | PersonalWaveOptions.mood                   |
| settings.mood.fun     | PersonalWaveOptions.mood                   |
| settings.popular      | PersonalWaveOptions.popular                |
| settings.vocal        | PersonalWaveOptions.vocal                  |
| settings.language     | PersonalWaveOptions.language               |
| settings.situation    | PersonalWaveOptions.situation              |
| settings.genre        | PersonalWaveOptions.genre                  |
| listened_track.id     | PersonalWave.ContentInput.trackId          |
| listened_track.duration | PersonalWave.ContentInput.trackDuration    |
| listened_track.is_skipped | PersonalWave.ContentInput.isSkipped       |
| listened_track.play_duration | PersonalWave.ContentInput.playDuration    |
| listened_track.user_reaction | PersonalWave.ContentInput.userReaction    |