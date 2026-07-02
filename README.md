# public-domain-bible-translations

A collection of Bible translations in a consistent, machine-readable JSON format. Organized by language, with one JSON file per book per translation. Most translations are in the public domain; a small number are released under open licenses (e.g. CC-BY-SA 4.0) and require attribution — see each translation's `metadata.json` for details.

## Available Translations

| Language | Translation | Abbreviation | Year | Canon | License |
|---|---|---|---|---|---|
| Arabic | Smith-Van-Dyck Bible | SVD | 1865 | Protestant (66 books) | public domain |
| Amharic | Amharic Unlocked Literal Bible | AmULB | 2019 | Protestant (66 books) | CC-BY-SA 4.0 |
| Bengali | Bengali Bible 1909 | BEN | 1909 | Protestant (64 of 66 books) | public domain |
| Chinese | Chinese Union Version | CUV | 1919 | Protestant (66 books) | public domain |
| English | American Standard Version | ASV | 1901 | Protestant (66 books) | public domain |
| English | Darby Bible | DBY | 1890 | Protestant (66 books) | public domain |
| English | Douay-Rheims-Challoner | DRC | 1752 | Catholic (73 books) | public domain |
| English | JPS Tanakh | JPS | 1917 | Hebrew Bible (Old Testament only) | public domain |
| English | King James Version | KJV | 1769 | Protestant (66 books) | public domain |
| English | World English Bible | WEB | 2000 | Protestant (66 books) | public domain |
| English | Young's Literal Translation | YLT | 1898 | Protestant (66 books) | public domain |
| French | Bible J.N. Darby | JND | 1885 | Protestant (66 books) | public domain |
| French | Louis Segond | LSG | 1910 | Protestant (66 books) | public domain |
| German | Luther Bible | LUT | 1912 | Protestant (66 books) | public domain |
| Greek | Robinson-Pierpont Greek New Testament | RP2018 | 2018 | NT only (27 books) | public domain |
| Hebrew | Westminster Leningrad Codex | WLC | 1008 | Hebrew Bible (OT only, 39 books) | public domain |
| Indonesian | Alkitab Yang Terbuka | AYT | 2011 | Protestant (66 books) | CC-BY-NC-SA |
| Hungarian | Revideált Károli Biblia 1908 | HunKar | 1908 | Protestant (66 books) | public domain |
| Hindi | Hindi Holy Bible | HHB | — | Protestant (66 books) | public domain |
| Italian | Diodati Bible | DIO | 1649 | Protestant (66 books) | public domain |
| Italian | Riveduta Bible | RIV | 1927 | Protestant (66 books) | public domain |
| Japanese | Kougo-yaku | KJA | 1955 | Protestant (66 books) | public domain |
| Korean | Korean Revised Version | KRV | 1961 | Protestant (66 books) | public domain |
| Latin | Clementine Vulgate | VUL | 1592 | Catholic (73 books) | public domain |
| Persian | Old Persian Translation | OPT | 1895 | Protestant (66 books) | public domain |
| Portuguese | Almeida Bible | ALM | — | Protestant (66 books) | public domain |
| Russian | Russian Synodal Bible | RSB | 1876 | Protestant (66 books) | public domain |
| Spanish | Reina-Valera | RVR | 1909 | Protestant (66 books) | public domain |
| Swedish | Swedish Bible 1917 | Swe1917 | 1917 | Protestant (66 books) | public domain |
| Swahili | Swahili Unlocked Literal Bible | SWHULB | 2019 | Protestant (66 books) | CC-BY-SA 4.0 |
| Tamil | Tamil Unlocked Literal Bible | TamULB | 2019 | Protestant (66 books) | CC-BY-SA 4.0 |

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

OT-only translations (e.g. WLC, JPS) contain files `01-Gen.json` through `39-Mal.json`.
NT-only translations (e.g. RP2018) contain files `40-Matt.json` through `66-Rev.json`.

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

Five fields, always present.

```json
{
  "name": "American Standard Version",
  "abbreviation": "ASV",
  "language": "en",
  "year": 1901,
  "license": "public domain",
  "attribution": null
}
```

**Field notes:**
- `license` — `"public domain"` for expired-copyright works; otherwise a standard license identifier such as `"CC-BY-SA 4.0"`
- `attribution` — `null` for public domain translations; a required credit string for any licensed translation (e.g. `"© 2019 Door43 World Missions Community"`)

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

Public domain translations in this repository are free to use without restriction. Translations with a `license` value other than `"public domain"` must be used in accordance with their stated license and the credit text in their `attribution` field must be displayed when the translation is shown or distributed.
