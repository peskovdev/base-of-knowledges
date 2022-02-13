# YouTube-dl


## Загрузка видео
```
youtube-dl [url]
```
---
1. По-дефолту название видоса такое-же как указанно на странице. Опция -o
позволяет дать произвольное название, а так же указать путь:
    ```
    youtube-dl -o 'Произвольное название' [url]
    youtube-dl -o '~/path/to/file/name' [url]
    ```

2. Просмотр вариантов для скачивания
    ```
    youtube-dl -F [url]
    ```

3. Скачивание конкретного формата
    ```
    youtube-dl -f 140 [url]
    ```

4. Скачивание максимального качества видео и аудио + объединение в формат mp4
    ```
    youtube-dl -f best --merge-output-format mp4 [url]
    youtube-dl -f worst --merge-output-format mp4 [url]
    ```

## Загрузка плейлиста
```
youtube-dl -f best --merge-output-format mp4 --yes-playlist
youtube-dl -f worst --merge-output-format mp4 --yes-playlist
youtube-dl -i -f mp4 --yes-playlist [url]
```

## Загрузка аудио в формате mp3

```
youtube-dl -f bestaudio --output "%(title)s.%(ext)s" --extract-audio --audio-format mp3 [url]
```

## Alias:
```
# Download only audio
alias ydm='youtube-dl -f bestaudio --output "%(title)s.%(ext)s" --extract-audio --audio-format mp3'

# Simple download
alias yd='youtube-dl'
# Download worst
alias ydw='youtube-dl -f worst --merge-output-format mp4'
# Download best
alias ydb='youtube-dl -f best --merge-output-format mp4'

# Download playlist
alias ydpl='youtube-dl -i -f mp4 --yes-playlist'
# Download playlist worst
alias ydplw='youtube-dl -f worst --merge-output-format mp4 --yes-playlist'
# Download playlist best
alias ydplb='youtube-dl -f best --merge-output-format mp4 --yes-playlist'
```
