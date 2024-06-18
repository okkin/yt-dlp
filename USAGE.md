# yt-dlp Guidance

## Activate python vritual environment
```bash
pyenv activate ytdlp-env
```

## Basic Usage
```bash
python3 -m yt_dlp "<video_url>"
```

## Include Embeded English Subtitles
```bash
python3 -m yt_dlp --write-subs --embed-subs --sub-langs en
```

## Output Templates

The `-o` option in `yt-dlp` specifies the output template for the downloaded files. This template determines how the filenames of the downloaded videos and subtitles will be structured.

### Breakdown of the Template

- `-o`: This is the option flag that tells `yt-dlp` you are specifying an output template.
- `'%(title)s.%(ext)s'`: This is the actual template string.

Let's break down the components of the template string:

- `%(title)s`: This placeholder will be replaced by the title of the video. For example, if the video's title is "My Awesome Video," this part of the filename will become "My Awesome Video."
- `%(ext)s`: This placeholder will be replaced by the file extension of the downloaded file. For example, if the file is an MP4 video, this part of the filename will become "mp4."

### Example

If you download a video with the title "My Awesome Video" and it is in MP4 format, using the template `'%(title)s.%(ext)s'` will result in a filename like:

```
My Awesome Video.mp4
```

### Customizing the Output Template

You can customize the output template to include other metadata or structure the filename differently. Here are some examples:

1. **Include Upload Date:**

   ```sh
   python3 -m yt_dlp -o '%(upload_date)s_%(title)s.%(ext)s' <URL>
   ```

   This will result in filenames like `20230101_My Awesome Video.mp4`.

2. **Include Channel Name:**

   ```sh
   python3 -m yt_dlp -o '%(channel)s/%(title)s.%(ext)s' <URL>
   ```

   This will create a directory named after the channel and save the video inside it, e.g., `ChannelName/My Awesome Video.mp4`.

3. **Include Video ID:**

   ```sh
   python3 -m yt_dlp -o '%(title)s_%(id)s.%(ext)s' <URL>
   ```

   This will add the unique video ID to the filename, e.g., `My Awesome Video_ABC123.mp4`.

### Full List of Placeholders

Here are some commonly used placeholders:

- `%(title)s`: Title of the video
- `%(ext)s`: File extension
- `%(upload_date)s`: Upload date (YYYYMMDD)
- `%(uploader)s`: Uploader name
- `%(channel)s`: Channel name
- `%(id)s`: Video ID
- `%(duration)s`: Duration of the video in seconds

For a complete list of available placeholders, you can refer to the [yt-dlp documentation](https://github.com/yt-dlp/yt-dlp#output-template).

## Multiple URLS

You can supply multiple URLs in one command to `yt-dlp` by simply listing them one after another, separated by spaces. Here is the general syntax:

```sh
python3 -m yt_dlp <URL1> <URL2> <URL3> ...
```

### Example

If you want to download three videos from different URLs, you can do it like this:

```sh
python3 -m yt_dlp https://www.youtube.com/watch?v=VIDEO_ID1 https://www.youtube.com/watch?v=VIDEO_ID2 https://www.youtube.com/watch?v=VIDEO_ID3
```

### Using a Text File for Multiple URLs

If you have a large number of URLs, it might be more convenient to store them in a text file and then pass that file to `yt-dlp`. Each URL should be on a new line in the text file.

1. **Create a text file (e.g., `urls.txt`) with the URLs:**

   ```plaintext
   https://www.youtube.com/watch?v=VIDEO_ID1
   https://www.youtube.com/watch?v=VIDEO_ID2
   https://www.youtube.com/watch?v=VIDEO_ID3
   ```

2. **Use the `-a` option to specify the file containing the URLs:**

   ```sh
   python3 -m yt_dlp -a urls.txt
   ```

This approach makes it easier to manage and update your list of URLs.

### Additional Options

You can combine multiple options with multiple URLs. For example, if you want to specify an output template while downloading multiple videos, you can do it like this:

```sh
python3 -m yt_dlp -o '%(title)s.%(ext)s' https://www.youtube.com/watch?v=VIDEO_ID1 https://www.youtube.com/watch?v=VIDEO_ID2 https://www.youtube.com/watch?v=VIDEO_ID3
```

Or, if you're using a text file:

```sh
python3 -m yt_dlp -o '%(title)s.%(ext)s' -a urls.txt
```

By using these methods, you can efficiently download multiple videos in a single command.