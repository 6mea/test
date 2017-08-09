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

Below we use the `level.json` file from [an user level]() for demonstrative purposes:

```json
{
  
  "version": 1, # Allows versioning of the level. Must be an integer.
  
  "id": "decnoe.hopes_and_dreams", # An unique identifier of the level. More explanations below.
  "title": "Hopes and Dreams", # Title of the level. Preferably, use the music title.
  "artist": "Toby Fox", # Name of the music artist.
  "illustrator": "masyu_0331", # Name of the background illustrator.
  "charter": "Decnoe", # Name of the charter, i.e. chart creator.
  
  "music": {
    "path": "Hopes and Dreams.mp3" # Relative path to the music file.
  },
  "music_preview": {
    "path": "preview.mp3" # Relative path to the music preview file.
  },
  "background": {
    "path": "background.jpg" # Relative path to the background image file.
  },
  "charts": [ # Here you can define at least one and at most three charts.
    {
      "type": "easy", # Type of the chart. Currently available types: "easy", "hard" and "extreme", all in lowercase.
      "difficulty": 8, # If you were to put your chart into Cytus, what difficulty would you assign for it? --This option is for that. Can be any integer, even beyond 9.
      "path": "chart.easy.txt" # Relative path to the chart text file.
    },
    {
      "type": "hard",
      "difficulty": 9,
      "path": "chart.hard.txt",
      "music_override" : {
        "path": "Hopes and Dreams (Alt).mp3" # You can choose to override the music used in this difficulty. Similar to hidden songs of Cytus.
      }
    }
  ]
  
}
```

The folder structure should be something like this:

```
.
├── background.jpg
├── chart.easy.txt
├── chart.hard.txt
├── Hopes and Dreams.mp3
├── Hopes and Dreams (Alt).mp3
└── level.json
```

Although it may seem obvious, filenames are not hardcoded as `background.jpg`, `chart.xxx.txt`; you can change them to whatever you like, just make sure the relative paths in your `level.json` point to the correct files.

# Unique identifier (`id`)

The `id` property in `level.json` is not necessary for local Cytoid gameplay, but required for uploading your level on [CytoidDB](cytoid.io/browse). It is used as an unique identifier for your level, as properties like `title` would easily have duplicates. (For coders, it is `package` in Java or `namespace` in C++. Borrowed concepts!)

Your `id` must only contain `a~z`, `0~9` and `.` only. These are valid `id`s:

    ✅
    ✅
    ✅

    ❎
    ❎
    ❎