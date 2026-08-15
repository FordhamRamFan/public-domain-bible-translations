# public-domain-bible-translations

A collection of public domain Bible translations in a consistent, machine-readable JSON format. Organized by language, with one JSON file per book per translation. Every translation in this repository is in the public domain and free to use without restriction.

## Available Translations

| Language | Translation | Abbreviation | Year | Canon | License |
|---|---|---|---|---|---|
| Arabic | Smith-Van-Dyck Bible | SVD | 1865 | Protestant (66 books) | public domain |
| Chinese | Chinese Union Version | CUV | 1919 | Protestant (66 books) | public domain |
| Coptic | Coptic Bohairic New Testament (Horner) | CopBohHorner | 1898 | NT only (27 books), chapter-granularity — see note below | public domain |
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
| Hungarian | Revideált Károli Biblia 1908 | HunKar | 1908 | Protestant (66 books) | public domain |
| Hindi | Hindi Holy Bible | HHB | — | Protestant (66 books) | public domain |
| Italian | Diodati Bible | DIO | 1649 | Protestant (66 books) | public domain |
| Italian | Riveduta Bible | RIV | 1927 | Protestant (66 books) | public domain |
| Japanese | Kougo-yaku | KJA | 1955 | Protestant (66 books) | public domain |
| Korean | Korean Revised Version | KRV | 1961 | Protestant (66 books) | public domain |
| Latin | Clementine Vulgate | VUL | 1592 | Catholic (73 books) | public domain |
| Norwegian | Det Norske Bibelselskap 1930 | NO1930 | 1930 | Protestant (66 books) | public domain |
| Persian | Old Persian Translation | OPT | 1895 | Protestant (66 books) | public domain |
| Portuguese | Almeida Bible | ALM | — | Protestant (66 books) | public domain |
| Russian | Russian Synodal Bible | RSB | 1876 | Protestant (66 books) | public domain |
| Spanish | Reina-Valera | RVR | 1909 | Protestant (66 books) | public domain |
| Swedish | Swedish Bible 1917 | Swe1917 | 1917 | Protestant (66 books) | public domain |

### Note on the Coptic Bohairic New Testament (CopBohHorner)

This translation is **chapter-granularity, not verse-granularity**: every chapter's `verses` array contains exactly one entry (`"verse": 1`) whose `text` is the full running text of that chapter, rather than one entry per actual verse like every other translation in this repository. Consumers expecting per-verse lookup will not get it from this file as-is.

Source and method, in full:

- Digitized from public-domain page scans (archive.org — University of Toronto and Google Books copies) of George William Horner's critical edition, *The Coptic Version of the New Testament in the Northern Dialect, otherwise called Memphitic and Bohairic* (Oxford: Clarendon Press, 1898–1905). The edition itself is in the public domain; only this particular OCR pass is new.
- Text was extracted with Tesseract's Coptic-language model, with an automated step to detect and exclude each page's small-print critical-apparatus footnotes.
- Verse-level splitting was attempted but abandoned: verse-number superscripts in this print are frequently misread or dropped entirely by OCR (including cases where the print itself uses a Coptic letter-numeral instead of an Arabic digit), which made automated verse boundaries unreliable enough to risk silently merging verses. Chapter-level text was judged safer than wrong verse boundaries.
- Chapter boundaries were instead derived from the chapter/verse-range headers printed on the facing English-translation pages (OCR'd separately), not from the Coptic text itself. This means a page's content can occasionally bleed into the wrong neighboring chapter at a boundary. One larger instance of this is known: in Acts, most of chapter 21's content landed in chapter 22's bucket instead, traced to a specific OCR character-fusion artifact on one page. The text isn't lost, just misfiled.
- Not proofread verse-by-verse against the original volumes. Treat as best-effort pending review.
- Incidental finding from this edition worth knowing: it places **Hebrews between 2 Thessalonians and 1 Timothy** rather than after Philemon (an old canonical ordering also seen in some Greek manuscripts), and it does include Revelation.

A future pass could add real verse-level splits (e.g. by aligning against another Coptic NT source) and tighten the Acts 21/22 boundary; until then this entry is a usable but rougher-than-usual addition compared to the rest of the repository.

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
- `license` — always `"public domain"` in this repository
- `attribution` — always `null`, since only public domain translations are included

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

This repository contains public domain translations only. All texts here are free to use, copy, modify, and redistribute without restriction.

Earlier revisions of this repository included a small number of translations released under open-but-not-public-domain licenses (e.g. CC-BY-SA 4.0, CC-BY-NC-SA). These have been removed to keep the repository strictly public domain.
