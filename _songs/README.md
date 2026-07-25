# Songs Collection

This directory contains individual song files for the Bread From Heaven Worship catalog. Each song is a Markdown file with YAML frontmatter containing metadata and the song content containing the lyrics.

## Structure

Each song file follows this format:

```markdown
---
title: Song Title
album: Album Name
track_number: 1
composer: Composer Name
themes:
  - Theme 1
  - Theme 2
key: D
tempo: 120
planning_center_link: https://...
demo_track: https://...
mix_track_folder: https://...
audio_url: https://...
scripture_references:
  - Psalm 1
  - John 3:16
arrangers:
  - Arranger 1
  - Arranger 2
song_note: Brief description of the song's message
---

## Verse 1

Lyrics go here...

## Chorus

More lyrics...
```

## Adding a New Song

1. Create a new `.md` file in this directory with a kebab-case filename (e.g., `amazing-grace.md`)
2. Add the frontmatter with all required fields (title, album, track_number, composer, key, tempo)
3. Write the lyrics using Markdown headers (##) for song sections
4. The song will automatically appear on the album page and have its own individual page at `/worship/songs/song-title/`

## Required Fields

- `title` - Song title
- `album` - Album or EP name (must match an entry in `_data/worship_albums.yml`)
- `track_number` - Track number on the album
- `composer` - Composer or artist name
- `key` - Musical key
- `tempo` - Tempo in BPM

## Optional Fields

- `themes` - Array of theme strings
- `planning_center_link` - Link to Planning Center arrangement
- `demo_track` - Link to demo track
- `mix_track_folder` - Link to mix track folder
- `audio_url` - URL to the audio file (Cloudinary or other CDN)
- `scripture_references` - Array of scripture references
- `arrangers` - Array of arranger names
- `song_note` - Brief description of the song's message or context

## Lyrics Format

Use Markdown headers (##) to denote song sections:

- `## Verse 1`, `## Verse 2`, etc.
- `## Chorus`
- `## Pre-Chorus`
- `## Bridge`
- `## Tag`
- `## Final Chorus`

Lyrics are automatically rendered with proper formatting on the album and individual song pages.

## Individual Song Pages

Each song automatically gets its own page at:
- `/worship/songs/song-title/`

These pages include:
- Full song metadata
- Audio player (if audio_url is provided)
- Complete lyrics
- Link back to the album
- Link to Planning Center (if provided)

## Migration Notes

This collection replaced the previous `_data/worship_songs.csv` file. The Jekyll collection approach provides:
- Better content organization
- Cleaner frontmatter vs CSV columns
- Individual song pages
- Easier lyrics editing (no need to escape newlines)
- Better version control (clearer diffs)
