# Newsletter

This project helps generate monthly and quarterly newsletters for the following communities.

* Monthly
    * Copilot
    * Purview
    * Threat Protection
        * To: ftwwthreatprotectsme@service.microsoft.com
        * CC: svdirect@microsoft.com; rcdeliverylt@microsoft.com; bryall@microsoft.com; BryanFPSDirects@microsoft.com
        * From: dmcwee@microsoft.com
    * Win365
* Quarterly
    * Incubation & Quick Start

The community leads should use the `TCOE_Template.html` as the standard template, and should provide a markdown file with all of their content to be inserted into the newsletter. You will understand which TCOE solution area you are generating the newsletter for because it will be the top level header in the markdown file.

When updating the template be sure to update all references to the current solution area.
  
Use powershell for any scripts you need to run to update the template.

## Newsletter Sections

Newsletter section should be determined by the second level headers in the markdown file, and each section should use to update the email header with the only the sections found in this email.

## Outputs

You should provide both an html output file that can be reviewed in the browser and you should also provide a .EML file that can be opened by outlook to be sent to the community. In the EML file properly populate the To, CC, and from values based on the solution area list above. When saving the HTML and EML files use the Email Subject for the file name.

### Montly Newsletter Subject

In the EML file create an Email Subject similar to `TCOE [Solution Area] - Community Newsletter [Month] [Year]`.

### Quarterly Newsletter Subjet

In the EML file create an Email Subject similar to `TCOE [Solution Area] - Quarterly Newsletter [Quarter]`. To determine the correct quarter you should use the *legal year* which begins on July 1st of the preceeding calendar year. Example: September 2026 is Q1 2027, January 2027 is Q3 2027.

## Template Reference

The `TCOE_Template.html` uses `{{TOKEN}}` placeholders and HTML comments to mark where content should be inserted. When generating a newsletter, replace all `{{TOKENS}}` with values derived from the markdown file and remove the comment wrappers around optional sections that are present in the content.

### Token Mapping

| Token | Source |
| --- | --- |
| `{{SOLUTION_AREA}}` | Derived from the H1 header (e.g. "Threat Protection") |
| `{{H1_TITLE}}` | Full H1 text (e.g. "Threat Protection Community News") |
| `{{MONTH_YEAR}}` | Current month and year (e.g. "March 2026") |
| `{{NAV_ITEMS}}` | Auto-generated from H2 headers, formatted as `<b>Section</b>&nbsp;&nbsp;• &nbsp;` |

### Section-to-Pattern Mapping

| Markdown Structure | Template Pattern |
| --- | --- |
| `## Success Measures` | Section header + blue underline. Contains sub-sections below. |
| `### Insight Yield Rate (IYR)` | Blue left-bordered card with 4 KPI stat boxes (25% width each) |
| `### Time-to-Respond (TTR)` | Green left-bordered card with 2 KPI stat boxes (50% each) + data table |
| `### SME Request Theme Analysis` | Purple left-bordered card with KPI stat boxes equally sized with theme title at the top and the theme percentage in larger font below the title + optional bullet list |
| `### SME-Derived-Growth (SDG)` | Teal left-bordered card with 2 stacked-value KPI boxes + data table |
| `## Key Events & Community Calls` | 3-column event card grid with colored top borders |
| `## Insights` | Green left-bordered callout box |
| `## Pod Updates` | 2-column card grid with colored left stripes |
| `## Incubation` | 2-column card grid with colored top borders |
| `## Spotlight` | Green left-bordered callout (same as Insights, 14pt title) |
| `## News & Events` | Bulleted list of hyperlinks |
| `## Key Resources` | 3-column icon card grid with emoji + linked title |
| `> **Important Reminder**` | Orange left-bordered callout (placed before first H2 section) |
| `## Incubations` | Section header + blue underline. Conatins stack of horizontal incubation cards. |
| `## Quick Starts` | Section header + green underline 2-column card grid of quick start cards. |
| `## Scope Expansions` | Section header + red underline 2-column card grid of incubation cards. |

### Color Palette

These brand colors are used throughout the template for borders, stripes, and accents. They cycle through in the order listed to give visual variety to repeated card patterns.

| Color | RGB | Usage | Note |
| --- | --- | --- | --- |
| Blue | `rgb(0, 120, 212)` | IYR border, section underlines, KPI cards, links | MS Color |
| Light Blue | `rgb(141, 200, 232)` | | MS Color |
| Dark Blue | `rgb(42, 68, 111) | | MS Color |
| Green | `rgb(141, 233, 113)` | TTR border, Insights/Spotlight callout border, table values | MS Color |
| Purple | `rgb(134, 97, 197)` | Theme Analysis border, card stripes/borders | MS Color |
| Dark Purple | `rgb(70, 54, 104)` | | MS Color |
| Teal | `rgb(73, 197, 177)` | SDG border, card stripes/borders | MS Color |
| Orange | `rgb(255, 92, 57)` | KPI cards, Important Reminder border, card stripes/borders | MS Color |
| Red | `rgb(244, 54, 76)` | Event card top borders, card stripes | MS Color |
| Header Blue | `rgb(12, 100, 192)` | Header/subtitle background, SME count banner | Non-MS Color |
| Footer Navy | `rgb(27, 58, 92)` | Footer background | Non-MS Color |

### Repeatable Patterns

The template contains `<!-- REPEAT: ... -->` comments marking elements that should be duplicated for each data item. When generating output:

1. **KPI Cards**: Generate one card per bullet group under the `###` header. Use `prior → current` format when both values exist, or just the current value.
1. **Data Tables**: Generate one `<tr>` per markdown table row. Preserve alternating row backgrounds for theme tables.
1. **Event Cards**: Fill rows of 3. Cycle top-border colors: red, purple, teal, blue, green, orange.
1. **Pod Update Cards**: Fill rows of 2. Cycle left-stripe colors: blue, purple, green, orange, red, teal.
1. **Incubation Cards**: Fill rows of 2. Cycle top-border colors: blue, purple, teal, orange.
1. **Resource Cards**: Fill rows of 3. Assign emoji: 📄 📋 👥 📈 💡 ✉ (use ✉ for mailto: links).
1. **Horizontal Incubation Cards**: Generate one card per bullet group header under the `##` header. The left border color of the card will use the status background color. Each card will have a two columns, the left column being 30% width and the right column will be 70% width. The left column will contain the Status Pill of the incubation below that will be the title of the incubation and below the title will display start and end using `start - end`. The right column of the card will contain the `description`.
1. **Quick Start Cards**: Fill rows of 2. Cycle top-border colors: blue, light blue, dark blue.
1. **Status Pill**: Oval shape containing the status text and where the status New has a Light Blue background color with black text, In Progress has a Green background with black text, and In Delivery has a Orange backgroud with white text.

### Optional Sections

Sections wrapped in `<!-- ... -->` comment blocks in the template are optional. Only uncomment and populate them if the corresponding H2 header exists in the markdown content:
- **Important Reminder**: Include if a blockquote with "Important Reminder" appears
- **Spotlight**: Include if `## Spotlight` exists
- **News & Events**: Include if `## News & Events` exists

### News & Events

This section should have a minimum of 3 links. If the newsletter content file has fewer than 3 items then use the following conditions to suplement this sections with appropriate content. If a community is not represented here, and no content exists in the provided markdown then skip this section.

| Community | Prompt |
|--- | --- |
| Threat Protection | Find article about cyber security events, breaches, or vendor events. The articles should be specific to an event and should be unique articles/events. The articles should be published in the last 1-3 months. Use the article's title as the text for the link and include the source of the article. |

### Status to Color Formatting

| Status | Background | Text Color |
| --- | --- | --- |
| New | Light Blue | Black |
| In Progress | Yellow | Black |
| In Delivery | Orange | White |
| Complete | Green | Black |