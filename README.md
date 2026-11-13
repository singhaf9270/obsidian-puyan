# Puyan

**هر هدف، یک مسیر؛ هر گام، یک پیشرفت.**

Puyan is a bilingual progress-tracking plugin for Obsidian. It turns Markdown task lists into a modern glassmorphic progress widget, records start and completion dates, calculates elapsed duration, generates reusable checklists, and celebrates completion with confetti. You can track tasks in the current note or display their progress from another note.

## Features

### Progress widget
- Shows completed tasks, total tasks, and completion percentage in a glassmorphic, color-themed widget.
- Icon and accent color change based on progress (rocket → lightning → moon → flame → trophy).
- Animated shimmer fill, glowing progress bar, and stat chips.
- Displays the source note's basename under the title when the widget is inserted cross-note.
- A compact icon-only **Open source note** button appears **only** when the widget is placed in a different note than the one it tracks. Inside the tracked note itself, the button is hidden.
- Click the trophy banner at 100% to replay the confetti celebration.
- Fully RTL/LTR aware and responsive on desktop and mobile.

### Progress tracking
- Tracks tasks in the note containing the widget, or in a separately selected target note.
- Automatically records the start date when the first task is checked.
- Automatically records the completion date when all tracked tasks are checked.
- If a task is added after completion, the completion date is cleared until the list is complete again.
- If all tracked tasks are unchecked, the start date and completion date are cleared.
- Calculates and stores the elapsed duration in days.
- Optionally saves the calculated progress percentage to Frontmatter — **the property is removed when progress reaches 0%**, and re-created when tasks are checked again.

### Dates and Frontmatter
- Supports Jalali (Persian) and Gregorian calendars.
- Offers configurable date formats.
- Can reformat existing tracked dates when the calendar or date format setting is changed.
- Lets you customize the Frontmatter property names for start date, completion date, duration, and progress.
- Accepts Persian, Arabic-Indic, and Latin digits as input.
- Lets you choose whether generated/displayed numbers use Persian or Latin digits.

### Checklist generator
- Creates numbered checklists using a total and an interval. For example, a total of 30 and interval of 10 creates 10, 20, and 30.
- Creates fixed lists from items entered in settings, such as weekdays.
- Allows the activity title to be left empty.
- Lets you customize the generated line template with placeholders.
- Supports per-item dates with a configurable date step.


### Built-in checklist presets

Puyan includes seven ready-to-use templates: weekdays, steps of ten, dated steps, four Pomodoro sessions, a seven-day habit, twelve book chapters, and a 30-day workout. Each preset includes a category, icon, color, and controls for whether it appears in the checklist wizard or as an individual command. The default setting also controls whether the progress widget is inserted before or after the generated checklist. Existing custom presets are preserved when upgrading.

### Language, layout, and appearance
- Persian and English interface.
- Settings and modal layouts adapt to RTL or LTR according to the selected language.
- Responsive widget for desktop and mobile screens.
- Configurable display options for the widget.
- **Confetti celebration** — both inside the widget and across the entire Obsidian window when progress reaches 100%.

## Quick start

1. Add Markdown tasks to a note.
2. Insert the following code block where you want the progress widget to appear:

~~~puyan
~~~

By default, the widget tracks tasks in the same note that contains the code block.

### Track tasks from another note

You can place the widget in one note and track tasks in a different note by adding a `note:` line inside the code block.

Using a vault-relative path:

~~~puyan
note: Projects/Book.md
~~~

Or using a wikilink:

~~~puyan
note: [[Book]]
~~~

The widget appears in the current note, while task tracking and Frontmatter updates apply to the target note. When the widget is cross-note, a small **open source note** icon appears next to the task counter; clicking it opens the target note in the current tab (Ctrl/Cmd-click opens it in a new tab).

### Custom title

You can override the default status label (e.g. "In progress", "Completed") by adding a `title:` line:

~~~puyan
title: Read Atomic Habits
~~~

The custom title is displayed as the widget heading. If omitted, the widget falls back to the status-based label derived from the completion percentage.

### Full example

~~~puyan
note: Projects/Book.md
title: Read Atomic Habits
~~~

## Checklist generator

Open the Command Palette and run **Create step checklist**.

Choose the checklist type in **Settings → Puyan**.

### Numbered steps

Enter a total and an interval. For example:

- Total: `30`
- Interval: `10`

The generated numbers are 10, 20, and 30.

You can customize the line template with these placeholders:

| Placeholder | Description |
| --- | --- |
| `{n}` | Current number |
| `{total}` | Total amount |
| `{title}` | Activity title |
| `{date}` | Date of that step (when dates are enabled) |

Examples:

- `- [ ] {n}` creates checkboxes containing only the numbers.
- `{n}` creates plain numbered lines.
- `- [ ] {title} — {n} از {total}` includes the title, current number, and total.

The activity title is optional. If it is left empty, the generator does not require a title.

### Saved checklist templates

Create multiple reusable templates from **Settings → Puyan** using the plus icon. Each template can be fixed (items separated by commas) or step-based (total, interval, and a custom line template). Use the edit and delete icons to manage saved templates. Run **Create checklist from template** from the Command Palette to choose which saved template to insert.

Fixed-list items are entered as comma-separated values. For example: `شنبه، یکشنبه، دوشنبه، سه‌شنبه، چهارشنبه، پنجشنبه، جمعه`.

You can optionally enable dates in the command window and choose a starting date. Puyan adds consecutive dates to the generated items, using the selected calendar and date format.

### Fixed list

Select a saved fixed-list template in the command window. For example:

~~~text
شنبه
یکشنبه
دوشنبه
سه‌شنبه
چهارشنبه
پنجشنبه
جمعه
~~~

The generator creates one checklist item for each line.

Both Persian and Latin digits are accepted. Generated numbers follow the digit-display setting.

## Frontmatter properties

Puyan uses these property names by default:

| Property | Description |
| --- | --- |
| `شروع` | Date the first task is checked |
| `پایان` | Date all tracked tasks are completed |
| `مدت انجام` | Elapsed duration in days |
| `پیشرفت` | Completion percentage, when saving progress is enabled |

You can change the property names in **Settings → Puyan**. The widget updates the configured properties in the note whose tasks are being tracked.

**Note on `پیشرفت` (progress):** when progress drops to 0% (all tasks unchecked), Puyan removes this property entirely instead of writing `0`. The property is re-created automatically as soon as at least one task is checked.

## Settings

The settings let you configure:

- Interface language (Persian or English).
- Calendar (Jalali or Gregorian) and date format.
- Output digit style (Persian or Latin).
- Frontmatter property names.
- Whether progress percentage is saved.
- Which progress details are shown in the widget (counter, start date, completion date, duration, note title, open-note button).
- **Confetti celebration** at 100% (on by default).
- Checklist generator type, fixed-list items, and numbered-line template.

## Installation

Download `main.js`, `manifest.json`, and `styles.css` from the GitHub release and place them in:

`.obsidian/plugins/puyan/`

Then enable **Puyan** from Obsidian's Community Plugins settings.

## Requirements

- Obsidian 1.5.0 or newer.
- No Dataview or Templater dependency.
- Works on desktop and mobile.

## License

MIT

## What's new in 1.2.0

- Smooth, animated progress-bar movement when tasks are checked or unchecked, with support for reduced-motion preferences.
- Added seven built-in checklist presets: weekdays, steps of ten, dated steps, four-session Pomodoro, seven-day habit, twelve book chapters, and a 30-day workout.
- Added preset categories, icons, colors, wizard/command visibility, and default widget placement.
- Existing custom checklist templates are preserved when upgrading.

## What's new in 1.1.0

- **Redesigned glassmorphic widget** with SVG icons, accent-themed glow, animated shimmer fill, and dedicated stat chips.
- **Dynamic icon** based on progress: rocket (start), lightning (doing), moon (halfway), flame (near), trophy (complete).
- **Compact icon button** for opening the source note — shown only when the widget is used cross-note, hidden when the widget lives inside its own note.
- **Custom widget title** via a new `title:` line inside the `puyan` code block.
- **Confetti celebration** when progress reaches 100% — both inside the widget and as a global full-screen burst across the Obsidian window. Toggleable in settings, and replayable by clicking the completion banner.
- **Progress property is removed** from Frontmatter when progress is 0%, instead of writing `0`.
- Improved SVG rendering (real DOM nodes instead of string parsing) for reliable display across Obsidian versions.
- Minor UI polish: refined modal layouts, better RTL/LTR handling, updated support section in settings.

## Follow Puyan updates

For tutorials, plugin updates, and practical Obsidian tips, follow the channels:

- **Bale:** [ble.ir/obsidiantut](https://ble.ir/obsidiantut)
- **Telegram:** [t.me/obsidiantut](https://t.me/obsidiantut)
- **YouTube:** [youtube.com/@obsidiantut](https://youtube.com/@obsidiantut)

## Support

If you find Puyan useful, you can support its continued development:

[Support Puyan on Reymit](https://reymit.ir/singhaf9270)

---

## Changelog

### 1.2.0
- Added smooth progress-bar animation when task completion changes, respecting reduced-motion preferences.
- Added seven built-in checklist presets with category, icon, color, visibility, and default widget placement settings.
- Preserved user-created checklist templates during settings migration.


### 1.1.0
- Redesigned the widget with glassmorphic cards, SVG icons, dynamic accent colors, animated progress bar and shimmer.
- Added a compact icon button for opening the source note, shown only in cross-note widgets.
- Added a `title:` option inside the `puyan` code block to customize the widget heading.
- Added confetti celebration at 100% — inside the widget and across the full Obsidian window.
- Progress Frontmatter property is now removed when progress is 0%.
- Switched SVG rendering to real DOM nodes for reliable display across Obsidian versions.
- Misc UI fixes and RTL/LTR refinements.

### 1.0.3
- Updated the checklist template workflow with reusable fixed and step-based templates.
- Added support for step templates with customizable placeholders, including step number, total, activity title, and date.
- Improved the date-picker button icon, including clearer sizing, alignment, and accessibility labeling.
- Refined the settings footer with consistent channel cards and a dedicated donation section.
- Added direct links to the Bale, Telegram, and YouTube channels in the README.
