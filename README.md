# public-domain-bible-translations

A collection of public domain Bible translations in a consistent, machine-readable JSON format. Organized by language, with one JSON file per book per translation.

## Available Translations

| Language | Translation | Abbreviation | Year | Canon |
|---|---|---|---|---|
| Arabic | Smith-Van-Dyck Bible | SVD | 1865 | Protestant (66 books) |
| Chinese | Chinese Union Version | CUV | 1919 | Protestant (66 books) |
| English | American Standard Version | ASV | 1901 | Protestant (66 books) |
| English | Darby Bible | DBY | 1890 | Protestant (66 books) |
| English | Douay-Rheims-Challoner | DRC | 1752 | Catholic (73 books) |
| English | JPS Tanakh | JPS | 1917 | Hebrew Bible (Old Testament only) |
| English | King James Version | KJV | 1769 | Protestant (66 books) |
| English | World English Bible | WEB | 2000 | Protestant (66 books) |
| English | Young's Literal Translation | YLT | 1898 | Protestant (66 books) |
| French | Louis Segond | LSG | 1910 | Protestant (66 books) |
| German | Luther Bible | LUT | 1912 | Protestant (66 books) |
| Hindi | Hindi Holy Bible | HHB | — | Protestant (66 books) |
| Italian | Diodati Bible | DIO | 1649 | Protestant (66 books) |
| Italian | Riveduta Bible | RIV | 1927 | Protestant (66 books) |
| Japanese | Kougo-yaku | KJA | 1955 | Protestant (66 books) |
| Korean | Korean Revised Version | KRV | 1961 | Protestant (66 books) |
| Latin | Clementine Vulgate | VUL | 1592 | Catholic (73 books) |
| Portuguese | Almeida Bible | ALM | — | Protestant (66 books) |
| Russian | Russian Synodal Bible | RSB | 1876 | Protestant (66 books) |
| Spanish | Reina-Valera | RVR | 1909 | Protestant (66 books) |

## File Structure

```
{Language}/
  {Translation-Name}/
    metadata.json
    01-Gen.json
    02-Exod.json
    ...
    66-Rev.json
```

Catholic translations (DRC, VUL) include 7 additional deuterocanonical books numbered 67–73:

```
67-Tob.json   (Tobit)
68-Jdt.json   (Judith)
69-Wis.json   (Wisdom)
70-Sir.json   (Sirach)
71-Bar.json   (Baruch)
72-1Macc.json (1 Maccabees)
73-2Macc.json (2 Maccabees)
```

## JSON Schema

### `metadata.json`

```json
{
  "name": "American Standard Version",
  "abbreviation": "ASV",
  "language": "en",
  "year": 1901,
  "copyright": "public domain"
}
```

### Book file (e.g. `40-Matt.json`)

```json
{
  "book": "Matthew",
  "abbreviation": "Matt",
  "number": 40,
  "testament": "NT",
  "chapters": [
    {
      "chapter": 1,
      "superscription": null,
      "heading": null,
      "verses": [
        {
          "verse": 1,
          "heading": null,
          "text": "The book of the generation of Jesus Christ...",
          "footnotes": []
        }
      ]
    }
  ]
}
```

**Field notes:**
- `number` — canonical book number (1–66 for Protestant; 1–73 for Catholic)
- `testament` — `"OT"`, `"NT"`, or `"DC"` (deuterocanonical)
- `superscription` — the psalm title/heading that appears before verse 1 (e.g. *A Psalm of David*); `null` if absent
- `heading` — a section heading at the chapter or verse level; `null` if absent
- `footnotes` — array of footnote strings; empty array if none

## License

All translations in this repository are in the public domain.
