# Videogames-Database
#### Author: Bocaletto Luca

[![License: MIT](https://img.shields.io/badge/License-MIT-green)](https://github.com/bocaletto-luca/Videogames-Database/blob/main/LICENSE) [![SQL](https://img.shields.io/badge/Format-SQL-blue)](https://github.com/bocaletto-luca/Videogames-Database)

Videogames-Database is a unified, SQL-based archive capturing over 11,300 video game records across 32 platforms from 1980 to 2017. It brings together titles, genres, publishers, release years and platforms into a consistent schema—ideal for analytics, dashboards, academic research, and app development.

---

## Table of Contents

- [Features](#features)  
- [Schema](#schema)  
- [Platforms & Genres](#platforms--genres)  
- [Repository Structure](#repository-structure)  
- [Quick Start](#quick-start)  
- [Example Queries](#example-queries)  
- [Contributing](#contributing)  
- [License](#license)  

---

## Features

- 32 platform-specific tables plus a consolidated `all_platform` view  
- Uniform table schema for seamless cross-platform queries  
- Coverage of 11,364 entries spanning 1980–2017  
- Ready-to-use with SQLite or any SQL-compliant RDBMS  
- Detailed breakdown by genre, publisher, and release year  

---

## Schema

All tables share this structure:

| Column         | Type     | Description                              |
| -------------- | -------- | ---------------------------------------- |
| id             | INTEGER  | Primary key                              |
| game_name      | TEXT     | Title of the video game                  |
| genre_name     | TEXT     | Genre (e.g., Action, RPG, Puzzle)        |
| platform_name  | TEXT     | Release platform (e.g., SNES, X360)      |
| publisher_name | TEXT     | Publishing company                       |
| release_year   | INTEGER  | Year of release                          |

---

## Platforms & Genres

**Platforms (32 total)**  
2600, 3DO, 3DS, DC, DS, GB, GBA, GC, GEN, GG, N64, NES, NG, PC, PCFX,  
PS, PS2, PS3, PS4, PSP, PSV, SAT, SCD, SNES, TG16, Wii, WiiU, WS,  
X360, XB, XOne, all_platform  

**Genres (12 total)**  
Action, Adventure, Fighting, Misc, Platform, Puzzle, Racing,  
Role-Playing, Shooter, Simulation, Sports, Strategy  

---

## Repository Structure

```text
.github/
  gitattributes

LICENSE
README.md
database.sql

2600.sql      3do.sql       3ds.sql      dc.sql
ds.sql        gb.sql        gba.sql      gc.sql
gen.sql       gg.sql        n64.sql      nes.sql
ng.sql        pc.sql        pcfx.sql     ps.sql
ps2.sql       ps3.sql       ps4.sql      psp.sql
psv.sql       sat.sql       scd.sql      snes.sql
tg16.sql      wii.sql       wiiu.sql     ws.sql
x360.sql      xb.sql        xone.sql
all_platform.sql
```

- **database.sql**: Full import script  
- **`*.sql` files**: Individual table dumps per platform  
- **all_platform.sql**: Aggregated view of all entries  
- **.gitattributes**: Ensures consistent line endings  

---

## Quick Start

Clone the repository and import into SQLite:

```bash
git clone https://github.com/bocaletto-luca/Videogames-Database.git
cd Videogames-Database
sqlite3 videogames.db < database.sql
```

Connect with any SQL client or integrate into your application.

---

## Example Queries

```sql
-- 1. Count games by genre in the 1990s
SELECT genre_name,
       COUNT(*) AS total
  FROM all_platform
 WHERE release_year BETWEEN 1990 AND 1999
 GROUP BY genre_name
 ORDER BY total DESC;

-- 2. Top 5 publishers on PS2
SELECT publisher_name,
       COUNT(*) AS releases
  FROM PS2
 GROUP BY publisher_name
 ORDER BY releases DESC
 LIMIT 5;

-- 3. Platform debut years
SELECT platform_name,
       MIN(release_year) AS first_release
  FROM all_platform
 GROUP BY platform_name
 ORDER BY first_release;
```

---

## Contributing

Corrections, data additions and improvements are welcome. Please open an issue or submit a pull request against this repository. Ensure that new records follow the established schema.

---

## License

This project is licensed under the [GPL License](https://github.com/bocaletto-luca/Videogames-Database/blob/main/LICENSE).
