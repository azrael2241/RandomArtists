# Music Artists Database
##### V 1.0.0
##### 415 Total Artists as of 10/2/25
A simple SQLite database containing a collection of music artists, ready to use for your projects, applications, or personal needs.

## What's Included

- **`artistDB.db`** - A SQLite database file with artist names
- Easy to integrate into any project that supports SQLite
- Lightweight and portable format

## Database Structure

The database contains a simple `artists` table with the following structure:

| Column | Type | Description |
|--------|------|-------------|
| `id` | INTEGER | Unique identifier for each artist (auto-incrementing primary key) |
| `name` | TEXT | The artist's name |

## Why No Songs?

This database only contains artist names, not their songs. Here's why:

- **Copyright concerns**: Song titles and lyrics are protected by copyright
- **Database size**: Including songs would make the database much larger and harder to manage
- **API availability**: Song data is better accessed through dedicated music APIs (see below)

### Getting Songs for Artists

If you need song information for an artist from this database, you can combine it with music APIs:

**Recommended: Genius API**
1. Get an artist from this database
2. Use the [Genius API](https://docs.genius.com/) to search for their songs
(Or alternatively, if you know the song, search for song name by artist from the database to ensure correct song is retreived)
3. Requires a free Genius account and API key

**Example workflow:**
```python
import sqlite3
import requests

# Get artist from our database
conn = sqlite3.connect('artistDB.db')
cursor = conn.cursor()
cursor.execute("SELECT name FROM artists WHERE id = 12") # 12 is Coldplay from source. We could lookup by name if we wanted to, but id works too
artist_name = cursor.fetchone()[0]

# Use Genius API to get songs (requires API key)
genius_url = f"https://api.genius.com/search?q={artist_name}"
headers = {"Authorization": "Bearer YOUR_GENIUS_API_KEY"}
response = requests.get(genius_url, headers=headers)
songs = response.json()
```

**Other music APIs you can use:**
- [Spotify Web API](https://developer.spotify.com/documentation/web-api/)
- [Last.fm API](https://www.last.fm/api)
- [MusicBrainz API](https://musicbrainz.org/doc/MusicBrainz_API)

##### Please keep in mind of what each API is tailored towards:
- Spotify Web API provides metadata, audio features, album art, and playback control. **No lyric content**
- LastFM API provides metadata, scrobbling, charts, and artist/track info, **no lyric content**
- MusicBrainz API provides metadata, artist, releases, recordings, identifiers, **no lyric content**
- Genius API provides metadata, artist, song, album info, some lyric content.
- Genius API usually provides a link to the lyrics due to licensing, so you'd need to scrape the page with something like [BS4](https://pypi.org/project/beautifulsoup4/) or use [LyricsGenius: a Python client for the Genius.com API](https://github.com/johnwmillr/LyricsGenius) by [John W. Miller](https://github.com/johnwmillr) and 28 contributors on Github

## How to Use

### Opening the Database
You can open and view the database using:
- **SQLite command line**: `sqlite3 artistDB.db`
- **[DB Browser for SQLite](https://sqlitebrowser.org/)** (GUI application)
- **[SQLite Viewer Web App](https://sqliteviewer.app/)** (Browser application)
- **Any programming language with SQLite support** (Python, JavaScript, etc.)

### Example Queries
```sql
-- Get all artists
SELECT * FROM artists;

-- Find a specific artist using name
SELECT * FROM artists WHERE name = 'Coldplay';

-- Find a specific artist using id
-- When using this method, make sure the id is correct within your database structure, if modified from source
SELECT * FROM artists WHERE id = 12; -- In source, 12 is Coldplay

-- Get a random artist
SELECT * FROM artists ORDER BY RANDOM() LIMIT 1;

-- Count total artists
SELECT COUNT(*) FROM artists;
```

### Programming Examples

**Python**
```python
import sqlite3

# Connect to the database
conn = sqlite3.connect('artistDB.db')
cursor = conn.cursor()

# Get a random artist
cursor.execute("SELECT name FROM artists ORDER BY RANDOM() LIMIT 1")
random_artist = cursor.fetchone()[0]
print(f"Random artist: {random_artist}")

conn.close()
```

**JavaScript (Node.js)**
```javascript
const sqlite3 = require('sqlite3').verbose();

const db = new sqlite3.Database('artistDB.db');

// Get all artists
db.all("SELECT * FROM artists", (err, rows) => {
    if (err) throw err;
    rows.forEach(row => {
        console.log(`${row.id}: ${row.name}`);
    });
});

db.close();
```

## Use Cases

- **Music recommendation systems**
- **Random playlist generators**
- **Testing and development data**
- **Learning SQL/database concepts**
- **Building music-related applications**

## Contributing

Feel free to fork this repository and add more artists or improve the database structure. Pull requests are welcome!

**Note**: Please do not push code. If you update, add artists, fix a bug, make a new table you think is relevant, etc., please only submit the updated database file, as well as any changes to this documentation that are needed to showcase the new changes and additions.

## License

This database is provided as-is for educational and development purposes. Artist names are factual data.
