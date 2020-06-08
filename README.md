# ydl-podcast

A simple tool to generate Podcast like RSS feeds from youtube (or other
youtube-dl supported services) channels, using
[`youtube-dl`](https://github.com/rg3/youtube-dl).

## Setup

Install the requirements:

`pip install -r requirements.txt`

## Configuration

Edit the config.yaml file to list your podcast sources and configure them,
as well as edit general configuration.

The available settings are the following.

### General settings

- `output_dir`: local directory where the downloaded media will be stored, and
  the podcast xml files generated.
- `url_root`: root url for the static files (used in the generation of the XML
  to point to the media files.
- `subscriptions`: a list of feeds to subscribe to.

### Feed settings

#### Mandatory
- `name NAME`: Name of the podcast source. Used as the podcast title, and media
  directory name.
- `url URL`: source url for the youtube (or other) channel.

#### Optional
- `audio_only True/False`: if `True`, audio will be extracted from downloaded
  videos to create an audio podcast.
- `retention_days N`: only download elements newer than `N` days, and
  automatically delete elements older.
- `download_last N`: only download the latest `N` videos.
- `initialize True/False`: if `True`, then downloads everything on the first
  run, no matter the `download_last` or `retention_days` specified.
- `output_dir`: local directory where the downloaded media will be stored, and
  the podcast xml files generated.
- `url_root`: root url for the static files (used in the generation of the XML
  to point to the media files.
- `format`: file format to force youtube-dl to use (eg mp4, webm, mp3 for audio
  only…)

## Usage

Using cron or your favorite scheduler, run:

`./ydl_podcast.py [configfile.yaml]`

You can then use your favorite web server to serve the files (a good idea is to
exclude the `*.json` and `*.part` files from being served as the first might
leak information, and the second is unnecessary.

eg with nginx:

```
root /var/www/static/podcasts/;
location ~ (\.json$|\.part$) {
  return 403;
}
```
