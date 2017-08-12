# Introduction

A Cytoid level is essentially custom gameplay elements (music, background, info...) archived into a `.cytoidlevel` file. By default, `.cytoidlevel` files will be automatically opened and imported in Cytoid. They are similar to `.osz` files of [osu!](https://osu.ppy.sh/help/wiki/osu!_File_Formats).

A Cytoid level should, at bare minimum, consist of:
- **a music file**

    Currently only the `.mp3` format is supported. If the file does not play correctly in game, please use a file converter to convert the file into the standard MPEG format.

    It is recommended to keep the file size below 3 MB, as larger files take significantly more time to load. Also it is **strongly recommended** to make a 30-seconds preview clip that is compressed under 500 KB.

- **a background image file**

    Currently `.jpg` and `.png` formats are supported.

    It is recommended to use a `.jpg` file and keep the file size below 2 MB. Resolution above 1920px * 1080px is preferred.

- **a chart text file**

    Currently only the Cytus format, or [Rayark v2 modified](https://github.com/TigerHix/Cytoid/wiki/Chart-formats) format is supported. **If you already have a Cytus custom chart, you do not need to modify the chart at all.**

- **a `level.json` file**

    This [JSON](https://json.org) file declares necessary information of the level.

# level.json

Below we analyze a sample `level.json` file. Don't worry, it's easy stuff.

```
{
  
  "version": 1, // Allows versioning of the level. Must be an integer.
  
  "id": "decnoe.hopes_and_dreams", // An unique identifier of the level. More explanations below.
  "title": "Hopes and Dreams", // Title of the level. Preferably, use the music title.
  "artist": "Toby Fox", // Name of the music artist.
  "illustrator": "masyu_0331", // Name of the background illustrator.
  "charter": "Decnoe", // Name of the charter, i.e. chart creator.
  
  "music": {
    "path": "Hopes and Dreams.mp3" // Relative path to the music file.
  },
  "music_preview": {
    "path": "preview.mp3" // Relative path to the music preview file.
  },
  "background": {
    "path": "background.jpg" // Relative path to the background image file.
  },
  "charts": [ // Here you can define at least one and at most three charts.
    {
      "type": "easy", // Type of the chart. Currently available types: "easy", "hard" and "extreme", all in lowercase.
      "difficulty": 8, // If you were to put your chart into Cytus, what difficulty would you assign for it? --This option is for that. Can be any integer, even beyond 9.
      "path": "chart.easy.txt" // Relative path to the chart text file.
    },
    {
      "type": "hard",
      "difficulty": 9,
      "path": "chart.hard.txt",
      "music_override" : {
        "path": "Hopes and Dreams (Alt).mp3" // You can choose to override the music used in this difficulty. Similar to hidden songs of Cytus.
      }
    }
  ]
  
}
```

And the folder structure:

```
.
├── background.jpg
├── chart.easy.txt
├── chart.hard.txt
├── Hopes and Dreams.mp3
├── Hopes and Dreams (Alt).mp3
└── level.json
```

It may seem obvious, but filenames are not hardcoded as `background.jpg`, `chart.xxx.txt`; you can change them to whatever you like, just make sure the relative paths in your `level.json` point to the correct files.

# Unique identifier

The `id` property in `level.json` is not necessary for local Cytoid gameplay, but required for uploading your level on [CytoidDB](cytoid.io/browse). It is the unique identifier for your level, as properties like `title` would easily have duplicates. (For coders, it is essentially a `package` in Java or a `namespace` in C++. Borrowed concepts!)

Your `id` must contain `a~z`, `0~9`, `.` and `_` only. These are valid `id`s:

- io.cytoid.tutorial
- john_doe.freedom_dive
- decnoe.undertale.hopes_and_dreams

# Create your first level

Now we are done with explanations, let's try creating a level and import it into Cytoid. The steps are simple:

1. Grab your music, background and chart files.
2. Create the `level.json` file. Use the [template](http://cytoid.io/level.json)!

That's it! Now you just need to copy them into your Cytoid data folder. Note that it is recommended to create an appropriately named folder and drag all the files in, to be better organized.

- On Android: Copy the enclosing folder into the `Cytoid` folder of your external storage (Usually `sdcard`).
- On iOS: Connect your device and open iTunes, navigate to `Apps -> iTunes File Sharing -> Cytoid`, drag the enclosing folder into the box at the right.

Open Cytoid and you should see your level in the level selection menu, beautifully presented. 👍

# Upload on CytoidDB

[CytoidDB](http://cytoid.io/browse) is a place for sharing your levels with other players. Chart information will be [automatically parsed and displayed to visitors](http://cytoid.io/browse/io.cytoid.glow_dance), and we do not have ads! (?)

The steps are simple as well:

1. Compress all the files into a `.zip` file. On latest operating systems, you should be able to do it by simply selecting all the files, right-click on them, and select "Compress" from the context menu. Do not compress the enclosing folder - just compress the files directly so that they are at the root of your `.zip` archive.
2. Create an account.
3. Start uploading. The uploader will inform you anything wrong with your level file, and if there's no errors, you will be brought to your very own level page.

Now you can simply share the page to others; upon downloading the `.cytoidlevel` file (which by the way, is just your `.zip` file with the file extension changed), they can open it with Cytoid and your level will be automatically imported into the data folder. Isn't that nice?