# Music Artists Database
##### V 1.0.0

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
