# ffmpeg

## Склейка
```
ffmpeg -i concat:"audio.mp3|another.mp3|audio.mp3" -c copy video.mp3
```

## Обрезка видео и аудио
```
# Видео
ffmpeg -ss 00:00:00 -i .mp4 -to 00:00:45 -c copy .mp4
# Аудио
ffmpeg -ss 00:00:00 -i .mp3 -to 00:00:45 -c copy .mp3
```

## Конвертация в mp3
```
ffmpeg -i .wav -codec:a libmp3lame -qscale:a 2 .mp3
```

## Конвертация видео в gif
```
ffmpeg -i .mp4. .gif
```

#### Полезные ссылки:
[Больше команд на losst.ru](https://losst.ru/poleznye-komandy-ffmpeg)
