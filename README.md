[![](https://jitpack.io/v/TopiSenpai/Sponsorblock-Plugin.svg)](https://jitpack.io/#TopiSenpai/sponsorblock-plugin)

# SponsorBlock-Plugin

A [Lavalink](https://github.com/freyacodes/Lavalink) plugin to skip [SponsorBlock](https://sponsor.ajay.app) segments in [YouTube](https://youtube.com) videos

## Installation

> **Warning** This plugin requires Lavalink v4 or higher

To install this plugin either download the latest release and place it into your `plugins` folder or add the following
into your `application.yml`

```yaml
lavalink:
  plugins:
    - dependency: "com.github.topi314.sponsorblock:sponsorblock-plugin:x.x.x" # replace x.x.x with the latest release tag!
      repository: "https://maven.topi.wtf/releases"
```

Snapshot builds are available in https://maven.topi.wtf/snapshots with the short commit hash as the version

## Usage

### Get Categories

```
GET /v4/sessions/{sessionId}/players/{guildId}/sponsorblock/categories
```

Response:

```
[
  "sponsor",
  "selfpromo"
]
```

---

### Put Categories

```
PUT /v4/sessions/{sessionId}/players/{guildId}/sponsorblock/categories
```

Request:

```
[
  "sponsor",
  "selfpromo"
]
```

---

### Delete Categories

```
DELETE /v4/sessions/{sessionId}/players/{guildId}/sponsorblock/categories
```

---

### [Segment Categories](https://wiki.sponsor.ajay.app/w/Segment_Categories):

* `sponsor`
* `selfpromo`
* `interaction`
* `intro`
* `outro`
* `preview`
* `music_offtopic`
* `filler`

---

There are also two new events:

### SegmentsLoaded

which is fired when the segments for a track are loaded

```json5
{
  "op": "event",
  "type": "SegmentsLoaded",
  "guildId": "...",
  "segments": [
    {
      "category": "...",
      "start": 0, // in milliseconds
      "end": 3000 // in milliseconds
    }
  ]
}
```

### SegmentSkipped

which is fired when a segment is skipped

```json5
{
  "op": "event",
  "type": "SegmentSkipped",
  "guildId": "...",
  "segment": {
    "category": "...",
    "start": 0, // in milliseconds
    "end": 3000 // in milliseconds
  }
}
```

### ChapterStarted

which is fired when the chapters for a track are loaded

```json5
{
  "type": "ChapterStarted",
  "op": "event",
  "guildId": "...",
  "chapter": {
    "name": "Prelude",
    "start": 0, // in milliseconds
    "end": 0, // in milliseconds
    "duration": "PT0S" // ISO-8601
  }
}
```

### ChapterStarted

which is fired when a new Chapter starts
```json5
{
  "type": "ChapterStarted",
  "op": "event",
  "guildId": "...",
  "chapter": {
    "name": "Prelude",
    "start": 0, // in milliseconds
    "end": 0,// in milliseconds
    "duration": "PT0S" // ISO-8601
  }
}
```

## Example

An example implementation in Go can be found [here](https://github.com/TopiSenpai/sponsorblock-plugin-example)
