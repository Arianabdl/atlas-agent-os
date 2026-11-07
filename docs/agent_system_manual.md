---
aliases: ["Agent System Manual"]
---
# Agent System Manual

The operating manual every agent follows. The root persona links here; workstation personas link here for routing and message rules.

## 1. Memory management

### The 100-line limit
Every `*_persona.md` and `*_memory.md` file stays **under 100 lines**. Blank lines, headers, bullets and routing pointers all count.

### When a memory file approaches 100 lines
```
Is memory.md close to 100 lines?
├─ Yes → Can outdated items be summarized or deleted?
│        ├─ Yes → Do it. Stay under 100.
│        └─ No (everything matters) → Overflow procedure
└─ No → Continue.
```

### Overflow procedure
1. Pick a self-contained section (Contacts, Archived Decisions, Completed Tasks, Reference Data).
2. Move it into a sub-file in the same workstation: `contacts.md`, `archived_tasks.md`, `reference_data.md` or `<topic>.md`.
3. Leave a routing pointer in the main memory file:
   ```markdown
   ## Memory Routing
   - Contacts → see [[contacts.md]]
   - Archived tasks → see [[archived_tasks.md]]
   ```
4. The main memory file always keeps: **Active Tasks**, current **Key Decisions**, and the **routing table**.

| Keep | Archive or remove |
| :-- | :-- |
| Active tasks with upcoming deadlines | Completed tasks older than 2 weeks |
| Current decisions | Superseded decisions |
| Active contacts | One-time contacts |
| Rules that change current behavior | Historical notes |

## 2. Routing

### Hybrid model
- **Flat:** an agent asks a peer directly when it needs one piece of information, the task clearly belongs to the peer, and nothing conflicts.
- **Hierarchical:** go through the planner (a local planning session, or the always-on server agent) when work spans domains, has a scheduling or priority conflict, involves three or more agents, or the right owner is unclear.

### Sending a message
Write a page to the **Agent Mailbox** database:
```
subject:  clear, specific subject line
from:     your_agent_name
to:       target_agent_name
Body:     structured message (section 3)
priority: Normal | High | Urgent
Status:   Unread
```

### Example agent network
| Agent | Domain | Route here when… |
| :-- | :-- | :-- |
| `hermes` | Always-on server agent: Telegram, Notion capture, digests, reminders | work must happen while the laptop is off, or you report finished work |
| `planning` | Weekly planning, conflicts, prioritization | timing or cross-domain conflicts |
| `librarian` | Research and note synthesis, Area → Project → Task taxonomy | you need knowledge from notes |
| `notion_agent` | Database structure and the schema map | a Notion property or view changed |
| `maintenance` | Scripts, bots, server code — the only agent allowed to change code | anything needs a code change |
| `architect` | Changelog of the system's architecture | you made or saw a structural change |
| `github` | Repository audits, READMEs, secret scans | code is about to be published |
| domain agents | career, resume, thesis, sport, music, drawing, cooking… | the task is in their domain |

### Devices
| Device | Agents |
| :-- | :-- |
| Laptop ("Atlas Primary", on demand) | every workstation, in local CLI sessions |
| Small server ("Atlas Server", 24/7) | `hermes` only |

### Architecture changelog rule
Any agent that makes or observes a structural change (routing rules, infrastructure, message protocol, new agents, memory structure) sends `architect` a mailbox message: subject `[CHANGELOG] <short description>`, body with date, what changed, why, and impact.

## 3. Structured message format
```
## Request
What you need from the target agent. Be specific.

## Context
Relevant background, under 5 lines.

## Constraints
Deadlines, priorities, rules.

## Expected Output
The format and content you expect back.
```

## 4. Key references
| Resource | Location | Purpose |
| :-- | :-- | :-- |
| `00_Resources/notion_map.md` | workspace root | Database IDs and property schemas |
| `global_memory.md` | workspace root | Cross-domain facts and preferences |
| Agent Mailbox | Notion | All inter-agent messages |
| This manual | `00_Resources/agent_system_manual.md` | Routing, memory and message rules |

## 5. Anti-patterns
| Don't | Do instead |
| :-- | :-- |
| Write JSON files to local folders as messages | Write to the Agent Mailbox |
| Handle tasks outside your domain | Route them to the right agent |
| Echo persona rules or memory back in replies | Answer with the actionable result only |
| Reply to acknowledgments (creates loops) | Output `[END_CONVERSATION]` when no reply is needed |
| Overwrite whole memory files during a sync | Edit specific sections only |
| Keep everything in one giant memory file | Use overflow sub-files with routing pointers |
| Hardcode tokens in scripts | Read secrets from `.env`; never commit it |
