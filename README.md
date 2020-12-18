# Youtube-dl-and-ffmpeg

---

## インストール

```sh
$ brew install ffmpeg youtube-dl
```

## ダウンロード

```sh
$ youtube-dl https://www.youtube.com/watch?v=***********
```

### ファイル形式を指定してダウンロード

ダウンロードできるファイル形式の一覧を取得

```sh
$ youtube-dl https://www.youtube.com/watch?v=*********** -F
```

```
[youtube] ***********: Downloading webpage
[info] Available formats for ***********:
format code  extension  resolution note
249          webm       audio only tiny   50k , opus @ 50k (48000Hz), 1.30MiB
250          webm       audio only tiny   66k , opus @ 70k (48000Hz), 1.73MiB
140          m4a        audio only tiny  130k , m4a_dash container, mp4a.40.2@128k (44100Hz), 3.57MiB
251          webm       audio only tiny  134k , opus @160k (48000Hz), 3.45MiB
394          mp4        256x144    144p   82k , av01.0.00M.08, 24fps, video only, 2.02MiB
278          webm       256x144    144p   97k , webm container, vp9, 24fps, video only, 2.54MiB
160          mp4        256x144    144p  111k , avc1.4d400c, 24fps, video only, 2.70MiB
395          mp4        426x240    240p  181k , av01.0.00M.08, 24fps, video only, 4.33MiB
242          webm       426x240    240p  225k , vp9, 24fps, video only, 5.66MiB
133          mp4        426x240    240p  275k , avc1.4d4015, 24fps, video only, 5.70MiB
396          mp4        640x360    360p  392k , av01.0.01M.08, 24fps, video only, 8.96MiB
243          webm       640x360    360p  411k , vp9, 24fps, video only, 10.17MiB
134          mp4        640x360    360p  565k , avc1.4d401e, 24fps, video only, 10.73MiB
397          mp4        854x480    480p  722k , av01.0.04M.08, 24fps, video only, 15.92MiB
244          webm       854x480    480p  762k , vp9, 24fps, video only, 16.52MiB
135          mp4        854x480    480p  821k , avc1.4d401e, 24fps, video only, 17.00MiB
136          mp4        1280x720   720p 1216k , avc1.4d401f, 24fps, video only, 24.31MiB
398          mp4        1280x720   720p 1292k , av01.0.05M.08, 24fps, video only, 28.46MiB
247          webm       1280x720   720p 1399k , vp9, 24fps, video only, 28.36MiB
399          mp4        1920x1080  1080p 2190k , av01.0.08M.08, 24fps, video only, 48.24MiB
248          webm       1920x1080  1080p 2667k , vp9, 24fps, video only, 63.97MiB
137          mp4        1920x1080  1080p 3907k , avc1.640028, 24fps, video only, 78.96MiB
18           mp4        640x360    360p  716k , avc1.42001E, 24fps, mp4a.40.2@ 96k (44100Hz), 19.75MiB (best)
```

ファイル形式一覧に記載のフォーマットコード / 拡張子を選択してダウンロード

```sh
# format code
$ youtube-dl https://www.youtube.com/watch?v=*********** -f 137

# extension
$ youtube-dl https://www.youtube.com/watch?v=*********** -f mp4

# 最高画質・最高音質
$ youtube-dl https://www.youtube.com/watch?v=*********** -f "bestvideo[ext=mp4]+bestaudio[ext=m4a]/best[ext=mp4]"
```

### 音声のみ

```sh
$ youtube-dl https://www.youtube.com/watch?v=*********** -x --audio-format mp3

# 高音質
$ youtube-dl YouTubeの動画URL -x -f "bestaudio" --audio-format mp3 --audio-quality 0
```

## 動画と音声の結合

```sh
$ ffmpeg -i video.mp4 -i audio.mp3 -c:v copy -c:a aac -map 0:v:0 -map 1:a:0 output.mp4

```

## フォーマット変換

### 拡張子

```sh
$ ffmpeg -i output.mp4 -c:v copy -c:a copy output.avi
$ ffmpeg -i output.mp4 -c:v copy -c:a copy output.flv
$ ffmpeg -i output.mp4 -c:v copy -c:a copy output.mov
```

### フレームレート

```sh
$ ffmpeg -i output.mp4 -r 5 output_framerate.mp4
```

#### 静止画

```sh
# ss：開始秒数　t：終了秒数　r：フレームレート
$ ffmpeg -ss 1 -t 232 -r 1 -i output.mp4 -f image2 output_%03d.png
```

### リサイズ

```sh
$ ffmpeg -i output.mp4 -s 640x360 output_resized.mp4
```
