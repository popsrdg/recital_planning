# Test Class List Handoff

## Current state

- Active development file: `testclasslist.html`
- Latest frozen baseline: `testclasslist_v003.html`
- Version history: `development_notes.md`
- The active file and v003 currently contain the same features.

## Running the page

From the project folder, start a local server:

```text
python -m http.server 8000
```

Open `http://localhost:8000/testclasslist.html` in a browser.

The page uses jQuery and jQuery UI from CDN links, so an internet connection is needed to load those libraries.

## Current data model

The temporary sample data is stored in the `values` array inside `testclasslist.html`. Each record contains:

- `id` - unique class/song record ID
- `name` - class name
- `songName` - song name
- `songLength` - length in seconds
- `students` - student records with `name` and `familyName`
- `hoverValue` - teacher information currently shown by the hover behavior

A class with multiple songs has one record per class/song combination. The class list shows the song beneath the class name only when that class has more than one song.

## Scheduling behavior

- The master class list is `#sortable1`.
- Recital lists are `#sortable2`, `#sortable3`, and `#sortable4`.
- The master list stays sorted by class name and song name.
- A record can be dragged into recital lists multiple times when needed.
- A duplicate record in the same recital is colored pink.
- Colors are based on the class/song record ID across recital lists.
- Dragging a record back to the master list does not create a duplicate.
- `Reset all` repopulates the master list and clears recital lists.

## Display outputs

Clicking `Display` creates or refreshes:

- Recital summary with class count, length, distinct student count, and distinct family count
- Static recital display table
- Family participation table showing each family and its children by recital
- Participation overview showing families and dancers in 1, 2, or 3 recitals

The 2- and 3-recital participation counts have hover details listing the matching families or dancers.

## Important counting rules

- Student counts are distinct within each recital.
- Family counts are distinct within each recital.
- A dancer is identified using the normalized student name together with the normalized family name.
- A family or dancer is counted in a recital when any assigned class/song record contains that person.
- Repeating a class/song record in the same recital does not duplicate a person in the participation counts.

## Planned next feature

Replace the temporary `values` array with data loaded from a shared Google Sheet. The proposed source has two tabs:

- `classes`: class name, teacher name, song name, song length
- `students`: class name, student name, family name

The importer should preserve separate class/song records, including classes with multiple songs, and then feed those records into the existing scheduling and display logic.

## Before making changes

1. Review the current active file and this handoff.
2. Preserve the latest stable version by creating the next numbered `testclasslist_v###.html` snapshot before substantial changes.
3. Keep Google Sheets loading separate from the scheduling and reporting logic.
4. Validate the active file after edits and verify the frozen copy remains unchanged.
