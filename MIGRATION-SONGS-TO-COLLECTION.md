# Songs Migration: CSV to Jekyll Collection

## Summary

Successfully migrated worship songs from a CSV data file to a proper Jekyll collection. This provides better content organization, individual song pages, and easier content management.

## What Changed

### Before
- Songs stored in `_data/worship_songs.csv`
- Single CSV file with all song data
- Lyrics in escaped CSV format
- No individual song pages

### After
- Songs stored in `_songs/` directory
- Each song is its own Markdown file with frontmatter
- Clean, readable lyrics format
- Individual song pages at `/worship/songs/song-title/`
- Collection properly configured in `_config.yml`

## Files Modified

1. **`_config.yml`**
   - Added `songs` collection with output and permalink
   - Added default frontmatter for songs collection

2. **`_includes/worship-album-detail.html`**
   - Updated to use `site.songs` collection instead of `site.data.worship_songs`
   - Simplified template logic for cleaner code
   - Better handling of arrays (themes, scripture references, arrangers)

3. **Created: `_layouts/song.html`**
   - New layout template for individual song pages
   - Includes audio player, lyrics, metadata, and navigation

4. **Created: `_songs/` directory**
   - 16 song files created
   - Each with proper YAML frontmatter and Markdown content
   - README.md with documentation for adding new songs

5. **Backup: `_data/worship_songs.csv.backup`**
   - Original CSV file backed up for reference

## Songs Migrated

### Hosanna to the King (EP)
1. Hosanna to the King
2. Because You're Good
3. All Things Together *(lyrics updated)*
4. Worthy
5. The Resurrected Christ

### Bread From Heaven
1. Captured
2. I Will Cling to You
3. Under Your Wings
4. Safe Refuge
5. Bread From Heaven

### Secured Eternally
1. Inseperable
2. From The East to the West
3. Your Word is a Light To Me
4. Secured Eternally
5. I Was Made to Glorify You

### All Glory, All Honor
1. All Glory, All Honor

## New Features

### Individual Song Pages
Each song now has its own page accessible at:
- `/worship/songs/hosanna-to-the-king/`
- `/worship/songs/all-things-together/`
- etc.

These pages include:
- Full song metadata (composer, themes, scripture, arrangers, key, tempo)
- Audio player (when audio_url is provided)
- Complete lyrics with proper formatting
- Link back to parent album
- Link to Planning Center arrangement

### Better Content Management
- **Easier editing**: Edit song files directly in `_songs/` directory
- **Clear diffs**: Git shows actual lyric changes, not CSV escaping
- **Better structure**: YAML frontmatter is more readable than CSV columns
- **Validation**: Jekyll will warn about missing required fields

### Future-Ready
The collection structure makes it easy to:
- Add custom fields to songs
- Create song search/filtering
- Build playlists or themed collections
- Add sheet music or chord charts
- Create RSS feeds for new songs

## How to Add New Songs

1. Create a new file in `_songs/` directory (e.g., `my-new-song.md`)
2. Add frontmatter with required fields (see `_songs/README.md`)
3. Write lyrics using Markdown headers for sections
4. Build and preview: `bundle exec jekyll serve`
5. Song will appear on album page and have its own URL

## Testing

Build tested and verified:
- ✅ Jekyll builds without errors
- ✅ Album pages render correctly
- ✅ Individual song pages generate
- ✅ All 16 songs migrated successfully
- ✅ "All Things Together" lyrics updated as requested

## Rollback Instructions

If you need to rollback to the CSV approach:

1. Restore CSV: `mv _data/worship_songs.csv.backup _data/worship_songs.csv`
2. Revert `_config.yml` changes (remove songs collection)
3. Revert `_includes/worship-album-detail.html` changes
4. Remove `_songs/` directory and `_layouts/song.html`

## Notes

- **Remember to restart Jekyll** after adding new songs or modifying `_config.yml`
- Individual song pages are optional - they don't break album pages if unused
- The old CSV is kept as `.backup` for reference but is no longer used
- All song URLs are SEO-friendly slugs (e.g., `/worship/songs/all-things-together/`)

---

Migration completed: 2026-07-25
