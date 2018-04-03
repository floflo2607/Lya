# kalliope-mpd

A neuron to leverage your mpd server


## Synopsis

Make kalliope play songs / playlist via an mpd server

## Installation

  ```
  kalliope install --git-url https://github.com/bacardi55/kalliope-mpd.git
  ```


## Options

| parameter    | required | default   | choices | comment                                                                                    |
|--------------|----------|-----------|---------|--------------------------------------------------------------------------------------------|
| mpd_action   | yes      |           | string  | The action to fire with mpd neuron (see below)                                             |
| mpd_url      | no       | localhost | string  | The url of the mpd server                                                                  |
| mpd_port     | yes      | 6600      | string  | The port of the mpd server                                                                 |
| mpd_password | no       |           | string  | The password of the mpd server                                                             |
| mpd_random   | no       | 0         | 0 or 1  | If playlist will be played randomly or not                                                 |
| mpd_volume   | no       | 100       | Int     | Volume level. Needs to be between 0 and 100                                                |
| query        | no       |           |         | The query (eg: playlist name or artist/song/album to search                                |


Available actions are fow now:
- playlist (*requires query parameters*): run a playlist
- playlist_spotify (**specific to mopidy** - *requires query parameters*): run a playlist
- toggle_play: to toggle play/pause
- search (*requires query parameters*): to search music and play it
- file (*requires query parameters*): to play a simple file (via this, you can run radio via mopidy tuneIn addon)
- play_next: play next song
- play_previsous: play previous song
- play_stop: Stop playing


## Return Values

| Name         | Description                                                                           | Type     | sample   |
| ------------ | ------------------------------------------------------------------------------------- | -------- | -------- |
|              |                                                                                       |          |          |


## Synapses example

Play a playlist by giving its name to kalliope

```yaml
  - name: "play-music"
    signals:
      - order: "start playlist {{query}}"
    neurons:
      - kalliopempd:
          mpd_action: "playlist"
          mpd_url: "xxx.xxx.xxx.xxx"
          mpd_port: "yyyy"
          mpd_random: "1"
          query: "{{query}}"
```

Play a playlist by hard coding it in the arguments

```yaml
  - name: "play-music-hiphop"
    signals:
      - order: "start playing good music"
    neurons:
      - kalliopempd:
          mpd_action: "playlist"
          mpd_url: "xxx.xxx.xxx.xxx"
          mpd_port: "yyyy"
          mpd_random: "1"
          query: "HipHop"
```

Play a spotify "top" playlist

```yaml
  - name: "search-fashion-music"
    signals:
      - order: "put some fashion music"
    neurons:
      - kalliopempd:
          mpd_action: "playlist_spotify"
          mpd_url: "xxx.xxx.xxx.xxx"
          mpd_port: "yyyy"
          mpd_random: "0"
          query: "Spotify/Top tracks/Global"
```

Search and play musics

```yaml
  - name: "search-music"
    signals:
      - order: "search for {{mpd_search}} music"
    neurons:
      - kalliopempd:
          mpd_action: "search"
          mpd_url: "xxx.xxx.xxx.xxx"
          mpd_port: "yyyy"
          mpd_random: "0"
          query: "{{query}}"
```

Search and play musics hard coded in brain

```yaml
  - name: "search-music"
    signals:
      - order: "Play my favorite song"
    neurons:
      - kalliopempd:
          mpd_action: "search"
          mpd_url: "xxx.xxx.xxx.xxx"
          mpd_port: "yyyy"
          mpd_random: "0"
          query: "My favorite song name"
```

Play a file (via mopidy, can play a radio url or other)

```yaml
  - name: "play-radio"
    signals:
      - order: "Play radio {{query}}"
    neurons:
      - kalliopempd:
          mpd_action: "file"
          mpd_url: "xxx.xxx.xxx.xxx"
          mpd_port: "yyyy"
          mpd_random: "0"
          mpd_volume: "75"
          query: "{{query}}"
          
  - name: "play-radio-bbc"
    signals:
      - order: "Play BBC radio"
    neurons:
      - kalliopempd:
          mpd_action: "file"
          mpd_url: "xxx.xxx.xxx.xxx"
          mpd_port: "yyyy"
          mpd_random: "0"
          query: "tunein:station:<stationNumber>"
```

## Template example



see more example in the [sample brain file](https://github.com/bacardi55/kalliope-mpd/blob/master/samples/brain.yml)

* [a post about this neuron](http://bacardi55.org/2017/02/08/kalliope-mpd-neuron.html)
* [my posts about kalliope](http://bacardi55.org/kalliope.html)

