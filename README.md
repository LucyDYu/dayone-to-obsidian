# dayone-to-obsidian
Convert a [Day One](https://dayoneapp.com/) JSON export into individual entries for [Obsidian](https://obsidian.md). Each entry is created as a separate page. 

## Additional features
* Supports importing videos, PDFs, audios, in addition to photos.
* Allows adding metadata for media, such as photo creation date and location (if available).
* Supports various media types, including jpeg, png, mov, mp4, and so on (audio type is fixed to m4a due to lack of type information in JSON).
* Easy configuration using YAML.
* Displays locations on a map for the entire entry and individual photos, audios, and videos (requires [the map view plugin](https://github.com/esm7/obsidian-map-view)).
* Includes datetime, weather, and tags in the frontmatter.
* Supports additional tags to display in Obsidian separate from other note tags. (default = From/DayOne)

## Example 
### Entry in Day One:
```markdown
# Hello Obsidian
This is an example entry with a lot of text and media.

## Photo
![[imagefile.jpeg]]

## Audio
![[audiofile.m4a]]

## PDF
![[PDFfile.pdf]]

## Video
![[videofile.mp4]]

```
### Entry after Conversion
filename: Hello Obsidian 2018-01-02
```markdown
---
date: 2018-01-02 18:58:49 Tuesday
weather: City 13°C Mostly Cloudy
tags: From/DayOne, DayOne/Audio
locations: 
---
# Hello Obsidian
This is an example entry with a lot of text and media.

## Photo
![[imagefile.jpeg]]
Date: 2018-01-01T11:33:05Z
Location: [Place, City, Country](geo:latitude,longitude)

## Audio
Duration: 00:01:48
Date: 2018-01-01T15:24:17Z
Recording Device: iPhone Microphone
Location: [Place, City, Country](geo:latitude,longitude)
![[audiofile.m4a]]

## PDF
Title: PDF title
![[PDFfile.pdf]]

## Video
![[videofile.mp4]]
Duration: 00:00:21
Date: 2018-01-02T14:30:05Z
Location: [Place, City, Country](geo:latitude,longitude)

---
[Place, City, Country](geo:latitude,longitude)

```

## Requirements
* Python 3

## Optional requirements
* Obsidian [Icons Plugin](https://github.com/visini/obsidian-icons-plugin) to display calendar marker at start of page heading

## Day One version
This script works with version 2025.24 (1711) of Day One. It has not been tested with any other versions.

## Setup

**DO NOT do this in your current vault. Create a new vault for the purpose of testing. You are responsible for ensuring against data loss**
**This script deletes folders if run a second time**
**This script renames files**
1. Export your journal from [Day One in JSON format](https://help.dayoneapp.com/en/articles/440668-exporting-entries) 
2. Expand that zip file
3. Adjust the *ROOT* variable in config.yaml to point to the location where your zip file was expanded and Journal.json exists. You should also have several media folders here if there were photos audios etc in your journal. Additional settings can also be configured in `config.yaml`.
4. If you **not** are using the [Icons Plugin](https://github.com/visini/obsidian-icons-plugin) to display calendar marker at start of page heading set *includeIcons = False*
5. Run the script
   1. Change to the project directory:
      ```
      cd /path/to/dayone-to-obsidian
      ```
   2. Install the required dependencies:
      ```shell
      pip install -r requirements.txt
      ```
      This command will install the necessary packages listed in the `requirements.txt` file. Alternatively, you can use:
      ```shell
      python3 -m pip install -r requirements.txt
      ```
   3. Run the `splitfile.py` script:
      ```shell
      python splitfile.py
      ```
6. Check results in Obsidian
7. If happy, move all the *journal* and *media* folders to whatever vault you want them in.

## Features
* Processes all entries, including any blank ones you may have.
* Entries organised by year/month/day
* If multiple entries on a day, each additional entry is treated seperately
* Adds metadata for whatever exists
   * Location 
   * Datetime
   * Tags
   * Weather
* Tags can be prefixed (default = DayOne/) to show as subtags in Obsidian separate from other note tags
