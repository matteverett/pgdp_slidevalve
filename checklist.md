# Guiguts PP Process Checklist

_The slide valve, simply explained._ by Tennant, William J.

## Project Info
* Project Name: slidevalve
* Title: The slide valve, simply explained.
* Author: Tennant, William J.
* [Project Page](https://www.pgdp.net/c/project.php?id=projectID660f13a39eb78)
* [Project Comments](https://www.pgdp.net/c/project.php?id=projectID660f13a39eb78#project-comments)
* [Project Forum](https://www.pgdp.net/phpBB3/viewtopic.php?t=81437)
* [Github Repository](https://github.com/matteverett/pgdp_slidevalve)
* [Project Gutenberg listing (not yet posted)]

## Project Setup

### Create Project
* [x] Choose a project name
  * Choose a short, simple project name, e.g. `pascal` for “*The Provincial Letters of Blaise Pascal*”
  * Should be simple, no spaces, lowercase, e.g. "missfairfax" was used for "Miss Fairfax of Virginia".
  * This is used by scripts and to name the GitHub repo, so use it consistently.
* [x] Run the setup script
  * ```shell
    cd ~/dp/util
    . venv/bin/activate
    ./make_project.py
    ```
  * Setup script fetches the project resources and creates the Github repository

### Review Project Details
* [x] Read the project comments
* [x] Subscribe to the project forum
* [x] Read all forum posts

### Setup Guiguts
* [x] Open `slidevalve-src.txt` in Guiguts
* [x] Configure page labels
  * `File → Project → Configure Page Labels...`
* [x] Check for roman numerals and unnumbered pages
* [x] Go to end of book to check page numbers line up

### Open Images  
* [x] Open images in Pixea: `open -a Pixea pngs`

## Preliminary Review

### Illustrations
* [x] Note illustrations in `README.md`
* [x] Move illustrations to `illustrations/` folder

### Languages
* [x] Note languages other than the main book language in `README.md`
  * In HTML they can be labeled with `<span lang="fr">..</span>`
  * If they're in italic print, that's handled later during italic handling

### HTML Notes
* [x] Note things that will need attention in the HTML in `README.md`, for example:
  * Author cross-references like "`(p. 150)`" and "`see page 222`" that should become links.
  * How the editor laid out special sections such as tables and sidebars.

### Check balanced markup
* [x] `Tools → Unmatched → DP Markup...`
  * whiSearches for the regular expression `\<(\w+)>\n?[^<]+<(?!/\1>)`, that is any markup starting in `<..>` that doesn't end in an identical closing markup.
  * Note: this regular expression sees `<tb>` as unbalanced, and shows the text from the `<tb>` to the next markup as an error. (If you can devise a better regex please do!)
  * Possible alternate that explicitly lists all current markup `\<(i|b|sc|g||f|u)>\n?[^<]+<(?!/\1>)`
  * Because it includes a newline, the search may take several seconds to return the first result.
  * [x] Correct any errors and click search until no more are found.

* [x] `Tools → Unmatched → Block Markup...`
  * [x] Correct any errors and click search until no more are found.

### Check Formatting
* Proper spacing for chapters and paragraphs:
  * [x] Before chapter start: 4 blank lines
  * [x] Between chapter head and subhead: 1 blank line
  * [x] Between head (or subhead) and chapter body: 2 blank lines
  * [x] Pages should **not** start with a blank line unless starting a new chapter, section, or paragraph.
  * [x] Each overall block should have blank lines before & after

* [x] Proper markup of `<i>italic</i>` and `<b>bold</b>`
  * Watch for punctuation wrongly contained in markup, such as `<i>(ibid.</i>` or `<b>Subtopic.</b>`.

* Proper markup of foreign languages:
  * [x] Greek and other transliterations

* Proper markup of all block material:
  * [x] Poetry, misc. tabular in `/* */`
  * [x] Block quotes in `/# #/`

* Proper markup of illustrations:
  * [x] Figures properly marked as `[Illustration: caption]`
  * [x] For captionless (`[Illustration: ]`), remove colon & whitespace
  * [x] Caption text agrees with List of Illustrations (if any)
  * [x] Consistent spelling, abbreviation, capitalization in captions

* [x] Search `(</i>)([!?;:])` & replace `\2\1` to find punct that should move inside quotes

* [x] Look for malformed thought-breaks (5 stars). Regex: `\*\s*\*\s*\*\s*\*\s*\*`

## Preliminary Fixup

### Basic Fixup
* [x] Open `Tools → Basic Fixup...`
* [x] Correct entries as appropriate

### Fix Block Markups 
* [x] Use the `Search` menu to step through all `/* */` blocks.
  * Regex: `^(/\*|\*/)`
  * Check for a blank line before and after markup
  * Make sure correct [Rewrap Markers](https://www.pgdp.net/wiki/PPTools/Guiguts/Guiguts_Manual/Tools_Menu#Rewrap_Markers) are used
  * Close-up where broken at page boundaries, if not already done
  * Apply specific [indent value](https://www.pgdp.net/wiki/PPTools/Guiguts/Guiguts_Manual/Tools_Menu#Table_Indent) if desired
  * Make sure poetry line numbers are at least two spaces to the right of the line.

* [x] Use the `Search` menu to step through all `/#..#/` blocks.
  * Regex: `^(/#|#/)`
  * Check for a blank line before and after markup
  * Make sure correct [Rewrap Markers](https://www.pgdp.net/wiki/PPTools/Guiguts/Guiguts_Manual/Tools_Menu#Rewrap_Markers) are used
  * Close-up where broken at page boundaries, if not already done
  * Check consistent indentation of block text
  * Apply specific [margin values](https://www.pgdp.net/wiki/PPTools/Guiguts/Guiguts_Manual/Tools_Menu#Block_Quote_Indent_and_Margins) if desired

### Fix Page Formatting
* [x] Remove the extra block markers around page boundaries
* [x] Join words hyphenated across page boundary
* Handle blank pages:
  * [x] Check that `[Blank Page]` are blank
  * [x] Remove blank pages

### Fix Footnotes and Illustrations
* [x] Fix Footnotes and Illustrations still inside a paragraph
  * Move outside paragraph to next or prior page, as appropriate
  * Don't worry about duplicate footnote numbers/symbols for now
  * Sidenotes are handled later

* [x] Use `Tools → Footnote Fixup`. This will help you validate and move any footnotes.
  * `First Pass`
  * `Next / Prev FN` to navigate
  * Look for `*` and use `Join with Previous` to join them
  * THERE SHOULD BE NO ERRORS AT TOP OF WINDOW
    * Exception: sometimes a footnote is really long (brown)
    * Exception: multiple anchors per footnote can confuse it (teal)

* [x] Move footnotes between paragraphs
  * `Footnote Fixup`, `First Pass`
  * `All to Number`, `Reindex`
  * `First Pass`, `Move FNs to Para`

### Fix Sidenotes
* [x] Step through sidenotes
  * Read the [discussion](https://www.pgdp.net/wiki/PPTools/Guiguts/Fixup#Sidenotes).
  * Search & Replace of `[S`, not regex, not whole word, ignore case. Click `Search` to find each Sidenote.
* [x] Compare to page image. Move note above paragraph if feasible.
  * Otherwise, position it above the sentence to which it applies, with blank lines to prevent rewrapping if you decide that is best.

### Fix Poetry Line Numbers
* [x] If the book has poetry that uses line numbers, read [this page](https://www.pgdp.net/wiki/PPTools/Guiguts/Fixup#Poetry_Line_Numbers) and align the line numbers consistently.

## Preliminary Corrections

### Errata
* [x] If original book had errata, apply it and note in TN

### Fix Proofer Comments
* [x] `Search → Find Next Proofer Comment`. Resolve all proofer's notes.
* [x] `Search → Find Orphaned DP Markup`.

### Fix Front Matter
* [x] Edit the TOC. Find each matching chapter head; make sure heads are 1:1 with TOC. Note that your TOC will probably need to be indented to prevent rewrapping, particularly if you use multiple spaces to align page numbers.
* [x] If book has illustrations, edit or create *List of Illustrations* (**Note:** this is not a requirement). Make sure it is 1:1 with `[Illustration]` captions.

### Unicode dashes
* [x] Long dash: S/R `([^-])----([^-]|$)` → `\1——\2`
  * There exists a “long dash” Unicode character (TWO-EM DASH, U+2E3A). However, display support for it is not broad, so it’s better to use two consecutive EM DASH, which is widely supported.

* [x] Em dash: S/R `([^-])--([^-]|$)` → `\1—\2`
  * There exists another dash (HORIZONTAL BAR, U+2015) which one PM/PP prefers to EM DASH (using two bars for one EM DASH), based on appearance in text version. I opted not to use this in favor of using the EM DASH character in both text and HTML.

* [x] [En dash](https://www.pgdp.net/wiki/En-dash): S/R `([^-])-([^-]|$)` → `\1–\2`
  * Range of numbers `12–15`
  * Mathematical minus sign `15 – 12 = 3`
  * Negative numbers `–14º`
  * **Do not** use en-dash for fractions like `1-1/2` (or Convert Fractions function will be confused)

* Any dashes not covered above are simple hyphens.

### Convert to Curly Quotes
* [x] `Tools → Convert to Curly Quotes`.
  * [x] Correct any issues
* [x] Search for remaining upright single quotation marks and replace them with either a ‘ or a ’.
* [x] Check for lingering straight quotes: `['"]`
* [x] `Tools → Check Curly Quotes`
  * [x] Correct any issues
* [x] Validate quotes pairings by searching for `[“”‘’]`

## Tool Checks

### Apply Word-Frequency Checks
* [ ] Open `Tools → Word Frequency`
  * Double click on a word to search for it.
* [ ] Set the `Frq` switch; click `All Words`. List is now sorted by word frequency; scroll to the end and skim up the list of words that only appear 1 time looking for oddities and obvious misspellings.
* [ ] Click `Character Cnts`.
  * Note characters that appear only once, check usage.
  * Check for equal counts of left & right parens and brackets.
* [ ] Set the `Alph` switch; click `All Words`. Scroll to the word Footnote and write down count for later use. (If the count is large, click once on Footnote and click 1st Harm. The harmonic window shows you any of the common misspellings of "Footnote" that occur.)
* [ ] Click `Emdashes`. This shows words with emdashes in them as well as similar words without emdashes (aka: suspects) marked with `****`. Check suspects against the text and page images. Preserve author's intent even when inconsistent. **Hint**: Enable the `Suspects` flag and click `Emdashes` again to see only suspects words.
* [ ] Click `Hyphens`. Same as Emdashes above but for Hyphens.
* [ ] Click `Alpha/num`. Scan list for `one/ell` and `oh/zero` errors.
* [ ] Click `ALL CAPS`. Scan list looking for oddities.
* [ ] Click `MiXeD CasE`. Scan list looking for letters such as o that sometimes OCR wrongly as uppercase. `Oh/zero` errors can show up here, too.
* [ ] Click `Check Accents`. Scan list looking for mistakes, inconsistent usages.
* [ ] Click `Check , Upper`. Scan list for comma-for-period errors.
* [ ] Click `Check . Lower`. Scan list for period-for-comma errors.
* [ ] Click `Ital/Bold/SC`. Scan list for incorrect or inconsistent use of italics, bold face, and small caps.
* [ ] Click `Ligatures`. Scan list for [incorrect or inconsistent use](https://www.pgdp.net/wiki/Æ_and_œ_ligatures) of `ae` and `oe` ligatures.
  * ```text
    æ Æ    <Opt> '    /ai/ to rhyme with “eye”.
    œ Œ    <Opt> q    /ɔɪ/ to rhyme with “oi” in “foil”
    <shift> for capital letter
    ```
* [ ] Look for missed ligature / diacritical transliterations. Regex: `\[[^*]`

### Apply Bookloupe
* [ ] Open `Tools → Bookloupe...`
  * Forward slash
  * HTML tag
  * No CR
  * Non-ASCII character
  * Non-ISO-8859 character
* [ ] Correct entries as appropriate

### Apply Spellcheck
* [ ] Use `Tools → Spelling...`
* [ ] Correct words or add them to the project dictionary as appropriate.

### Apply PPtxt
* [ ] Use `Tools → PPtxt...`
* [ ] Correct entries as appropriate

### Apply Jeebies
* [ ] Use `Tools → Jeebies...`
* [ ] Examine its report of possible `he/be` errors
* [ ] Correct entries as appropriate

### Apply Stealth Scannos
* [ ] Use `Tools → Stealth Scannos` with `Auto Advance`.
  * [ ] Start scanno searching based on `en-commn.rc`. Work through the list.
  * [ ] Apply scanno searching based on `regex.rc`. Work through the list.
* [ ] Correct entries as appropriate

### Apply Word Distance Check
* [ ] Use `Tools → Word Distance Check...`
* [ ] Correct entries as appropriate

### Misc Checks
* [ ] Check for chapter/section spacing. Regex: `\n\n\n`
* [ ] Check spaces around hyphens. Regex: `(\s+-|-\s+)`
* [ ] Check spaces before punctuation. Regex: `\s+[.!?;:,]`
* [ ] Check spaces around quotes. Regex: `(\s+['"][^\s]|[^\s]['"]\s+)`
* [ ] Check spaces around brackets. Regex: `(\s+[({[\]})]|[({[\]})]\s+)`
* [ ] Search regex `(Dr|M(me|lle|essrs|rs?)|St|Fr|Rev)\s` and add missing period if needed
* [ ] Check `A.M.`, `P.M.` and similar for spacing to match book - regex: `[AP]\.\s*M\.`
  * Note these to do `&nbsp;` in HTML, to avoid line wrap mid-abbreviation
* [ ] Does book use small-caps A.D. B.C.?
  * Search `[A-Z]\.\s*[A-Z]\.`, add `<sc>` and note for `&nbsp;` if needed
* [ ] Check for multiple consecutive spaces which are not in a no-wrap block
* [ ] Look at `<tb>` and look for improper uses
* [ ] Check all ellipses. Regex: `\.\.\.`
* [ ] Check for 3 dashes (not either 2 or 4). Regex: `[^-]---[^-]`
* [ ] Look for spaces around em- or long-dash. Regex: `\s+--(--)?\s+`
* [ ] Check adjacent letters and numbers. Regex: `([0-9][A-Za-z]|[A-Za-z][0-9])`
* [ ] Superscripts (search `^` without regex). Can use `^` or `^{th}` form
  * Add TN to text version about this superscript notation

### Add Transcriber's Notes
* [ ] Add Transcriber's Notes to the end of the book

### Final Check
* [ ] Look at the revisit list for anything to handle
* [ ] Check for unexpected `*` to make sure no stray proofer notes or split-word/fn markers were missed

### Save Edited Markup
* [ ] Save any unsaved changes
* [ ] Sync with github repository

### Validation
* [ ] Run [PWBB](https://www.pgdp.net/ppwb/index.php) pptext check
* [ ] Run text checks at [pptools](https://pptools.tangledhelix.com)

## Create Ppgen File

### Add Front Matter
* [ ] Add `frontmatter.txt` to the start of the file.

### Join page boundaries
* [ ] Replace page boundaries with `.pm new-page`
  * Search Regex: `-----File: (\d\d\d).png---------------------------------------------------------`
  * Replace with: `.pm new-page-break $1`

### Insert Breaks
* [ ] Insert chapter and section breaks as appropriate
* [ ] Convert `.pm new-page` to `.pm new-page-break` as appropriate

### Illustrations
* [ ] Fixup illustrations:
  * [ ] Illustration #1
  * [ ] Illustration #2
  * [ ] etc.

### Front Matter
* [ ] Adjust front matter font sizes:
  * `.h1`: 1.4 em
  * `.h2`: 1.2 em
  * `.h3`: 1.2 em

### Generate HTML and Txt Files
* [ ] Run ppgen on `{{project}}-src.txt`
  * `python3.11 ~/pgdp/ppgen/ppgen.py -i {{project}}-src.txt`

### Run PP Toolbox:
`https://www.pgdp.net/ppwb/`
* [ ] pptext
* [ ] pphtml
* [ ] W3C HTML markup validator
* [ ] W3C CSS validator
* [ ] Gutenberg online bookmaker

## References
### Post-Processing
* [PP FAQs](https://www.pgdp.net/wiki/DP_Official_Documentation:PP_and_PPV/Post-Processing_FAQ)
* [PP Workbench](https://www.pgdp.net/wiki/DP_Official_Documentation:PP_and_PPV/Post-Processing_Workbench)
* [PP Process Checklist](https://www.pgdp.net/wiki/Guiguts_PP_Process_Checklist)
* [Getting your PP Project Ready for PPV](https://www.pgdp.net/wiki/Getting_your_PP_Project_Ready_for_PPV)

### Guidance
* [Beginner PP advice](https://www.pgdp.net/wiki/Beginner_PP_advice)
* [PP Advice](https://www.pgdp.net/wiki/Post-Processing_Advice)
* [HTML Best Practices](https://www.pgdp.net/wiki/DP_Official_Documentation:PP_and_PPV/DP_HTML_Best_Practices/Best_Practices)
* [Poetry Case Study](https://www.pgdp.net/wiki/DP_Official_Documentation:PP_and_PPV/DP_HTML_Best_Practices/Case_Studies/Poetry)

### Ppgen
* [Ppgen Wiki](https://www.pgdp.net/wiki/PPTools/Ppgen)
* [Ppgen Manual](https://www.pgdp.net/wiki/PPTools/Ppgen/Manual)
* [Ppgen Example Books](https://www.pgdp.net/dp-genmgr/ppgen_source/)
* [Ppgen Coding Samples](https://www.pgdp.net/dp-genmgr/ppgen_samples/)

### Guiguts
* [Guiguts Tutorial](https://www.pgdp.net/wiki/Guiguts_Tutorial)
* [Guiguts Manual](https://www.pgdp.net/wiki/PPTools/Guiguts/Guiguts_2_Manual)

### Github Repositories
* [mmeverett](https://github.com/matteverett?tab=repositories)
* [Ppgen Source Code](https://github.com/wf49670/ppgen)
* [PP Utilities](https://github.com/tangledhelix/dp_pp_utils)