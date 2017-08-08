# Getting started

A Cytoid level is essentially custom gameplay elements (music, background, info...) archived into a `.cytoidlevel` file. By default, `.cytoidlevel` files will be automatically opened and installed in Cytoid. They are similar to `.osz` files of [osu!](https://osu.ppy.sh/help/wiki/osu!_File_Formats).

A Cytoid level should, at bare minimum, consist of:
- **a music file**

    Currently only the `.mp3` format is supported. If the file does not play correctly in game, please use a file converter to convert the file into the standard MPEG format.

    It is recommended to keep the file size below 3 MB, as larger files take significantly more time to load.

- **a background image file**

    Currently `.jpg` and `.png` formats are supported.

    It is recommended to use a `.jpg` file and keep the file size below 1 MB.

- **a chart text file**

    Currently only the [Rayark v2 modified](https://github.com/TigerHix/Cytoid/wiki/Chart-formats) format is supported. 

- **a `level.json` file**

    This [JSON](https://json.org) file declares necessary information of the level.

# level.json

Below is a sample `level.json` file:

```json
{
  
  "format": "beta", 
  "version": 1,
  
  "title": "Hopes and Dreams",
  "composer": "Toby Fox",
  "illustrator": "masyu_0331",
  "charter": "Decnoe",
  
  "music": {
    "path": "HnD.mp3"
  },
  "music_preview": {
    "path": "preview.mp3"
  },
  "background": {
    "path": "background.jpg"
  },
  "charts": [
    {
      "type": "easy",
      "difficulty": 8,
      "path": "chart.easy.txt"
    },
    {
      "type": "hard",
      "difficulty": 9,
      "path": "chart.hard.txt",
      "music_override" : {
        "path": "HnD B.mp3"
      }
    }
  ]
  
}
```

```
.
├── dir1
│   ├── file11.ext
│   └── file12.ext
├── dir2
│   ├── file21.ext
│   ├── file22.ext
│   └── file23.ext
├── dir3
├── background.jpg
└── level.json
```