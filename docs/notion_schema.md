# Notion Schema

Atlas uses six Notion databases. Create them, then record each database ID in `00_Resources/notion_map.md` so agents never have to search for them.

## Hierarchy

```
Area (Level 1)
└── Project (Level 2)           ← sub-projects link only to their parent project
    ├── Task (Level 3)
    └── Note (Level 3)          ← sub-notes link only to their parent note
Standalone tasks link directly to an Area. Nothing is left without a parent.
```

## Databases

### Areas
| Property | Type |
| :-- | :-- |
| `Name` | title |
| `Projects` | relation → Projects |
| `Tasks` | relation → Tasks |
| `Notes` | relation → Notes |

Example areas: Work & Career · Learning & Growth · Hobbies & Creativity · Finance · Health & Fitness · Home & Relationships

### Projects
| Property | Type | Notes |
| :-- | :-- | :-- |
| `Name` | title | |
| `Status` | status | Not started / In progress / Done |
| `Priority` | select | High / Medium / Low |
| `Date` | date | |
| `Areas` | relation → Areas | parent projects only |
| `Parent item` / `Sub-item` | relation → Projects | sub-projects |
| `tasks` | relation → Tasks | |
| `Notes` | relation → Notes | |
| `Tags` | relation → Tags | |
| `archive` | checkbox | archived pages are ignored everywhere |
| `pinned` | checkbox | "keep in view" |

### Tasks
| Property | Type | Notes |
| :-- | :-- | :-- |
| `task` | title | |
| `Status` | status | Not started / In progress / Done |
| `priority` | select | High / Medium / Low |
| `due` | date | deadline |
| `Date` | date | planned time (when you will do it) |
| `projects` | relation → Projects | |
| `Areas` | relation → Areas | standalone tasks only |
| `Parent item` / `Sub-item` | relation → Tasks | |
| `archive` | checkbox | |

### Notes
| Property | Type |
| :-- | :-- |
| `Name` | title |
| `Summary` | rich text |
| `projects` | relation → Projects |
| `Areas` | relation → Areas |
| `Parent item` / `Sub-item` | relation → Notes |
| `Last Edited` | last edited time |
| `archive` | checkbox |

### Tags
| Property | Type |
| :-- | :-- |
| `Name` | title |
| `projects`, `tasks`, `notes` | relations |
| `Archived` | checkbox |

### Agent Mailbox
| Property | Type | Values |
| :-- | :-- | :-- |
| `subject` | title | |
| `from` | select | agent names, `user` |
| `to` | select | agent names, `user` |
| `Body` | rich text | structured message |
| `priority` | select | Urgent / High / Normal / Low |
| `Status` | status | Unread / Processing / Done |
| `Device` | select | any / laptop / server |
| `Created At` | created time | |
