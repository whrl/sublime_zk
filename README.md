# Sublime ZK

This is a plugin for SublimeText3 to enable ID-based, Wiki-style links, and #tags in your documents.

If you follow the (plain-text) Zettelkasten method (as proposed by [Zettelkasten.de](https://zettelkasten.de) or [takesmartnotes.com](http://takesmartnotes.com/#moreinfo)), this might appeal to you.

In short, it helps you manage an archive of interlinked notes that look like this:

![screenshot](https://user-images.githubusercontent.com/30892199/32403197-25d9ccd2-c134-11e7-93c6-62257f35e518.png)

See the [Usage](#usage) section below to see how this package might support your workflow.

## Features
* This plugin enables you to place wiki style links like `[[this]]` or `[this]` (and old-school links like this `§201711111709`) into your notes to link to other notes in your note archive.
* Clicking such a link and pressing `[ctrl]+[enter]` will open the corresponding note.
* Alternatively, double-clicking the link while holding the `[alt]` key down, will also open the corresponding note.
* Clicking such a link and pressing `[alt]+[enter]` will search for all notes also referencing the linked note [('friend notes')](#searching-for-friends).
* Typing `[[` will open a list of existing notes so you can quickly link to existing notes.
* Typing `[ctrl]+[space]` (or `[alt]+[/]` on Linux) will trigger note-link auto-completion for even quicker insertion of links to other notes.
* Typing `[shift]+[enter]` lets you enter a name for a new note. The new note is then created with a new note ID.
* Implicit note creation via links to non-existing notes' titles, see [below](#implicitly-creating-a-new-note-via-a-link).
* The ID format is YYYYMMDDHHMM - eg: 201710282111
* Highlighting of note links
* Highlighting of #tags
* Highlighting of footnote references `[^like this one]`
* Typing `[#][!]` will create a scratch file containing all your **#tags**, sorted
* `[#][?]` opens up a list of all your **#tags** and lets you fuzzy search and select them (like note-links).
* Clicking a **#tag** and pressing `[ctrl]+[enter]` will search for all notes containing this tag.
* Alternatively `[alt]` + double clicking the tag will do the same thing.
* Support for `ag`, [The Silver Searcher](#installing-the-silver-searcher)
* **NEW**: [Expansion of overview notes with selective refresh](#expansion-of-overview-notes-with-selective-refresh)!!!

## Installation

### Automatic Installation & Updates

Sublime Text comes with Package Control, a feature which allows you to easily install and update third party packages. You can use it to install this package and keep it up to date:

1. Install [Sublime Text 3](http://www.sublimetext.com/3)
2. Use the Command Palette (Tools > Command Palette...) and run **Install Package Control**. Sublime Text will alert you when the installation has finished.
3. Use the Command Palette and run **Package Control: Add Repository**
4. Add the URL of this repository `https://github.com/renerocksai/sublime_zk` into the panel that appears at the bottom of the window and press `Enter`.
5. Use the Command Palette and run **Package Control: Install Package** and search for `sublime_zk` from the list of available packages. Select it and press `Enter` to install the package.
6. You can keep your packages up to date by running **Package Control: Upgrade Package** from the Command Palette.

### Manual Installation

The following steps cover all dependencies and prerequisites. Skip the steps you don't need:

1. Install [Sublime Text 3](http://www.sublimetext.com/3)
2. Download the sublime_zk zip from [this repo](https://github.com/renerocksai/sublime_zk).
3. Unzip the sublime_zk plugin. You should get a `sublime_zk` folder.
4. Under Preferences, go to 'Browse Packages...'. This opens the package location of SublimeText in your file browser.
5. Copy the `sublime_zk` folder into the package location folder from the previous step.

You should be all set.

### Installing The Silver Searcher

This plugin can make use of `ag`, [The Silver Searcher](https://github.com/ggreer/the_silver_searcher), to **dramatically speed up** and improve the [search for all tags](#getting-an-overview-of-all-your-tags), the [tag selector](#experimental-tag-selector), [tagged notes search](#searching-for-notes-containing-specific-tags), and [friend note search](#searching-for-friends) features. According to its [Installation Instructions](https://github.com/ggreer/the_silver_searcher#installing), it is fairly easy to install on macOS, Linux, BSD and Windows:

- [macOS installation](https://github.com/ggreer/the_silver_searcher#macos)
- [Linux installation](https://github.com/ggreer/the_silver_searcher#linux)
- [BSD installation](https://github.com/ggreer/the_silver_searcher#bsd)
- [Windows installation](https://github.com/ggreer/the_silver_searcher#windows)
  - Alternate Windows installation using [Chocolatey](https://chocolatey.org/): `choco install ag`
  - Alternate Windows installation using [Scoop](http://scoop.sh/): `scoop install ag`
  - Note: If you use the [Unofficial daily builds](https://github.com/k-takata/the_silver_searcher-win32) make sure when you download them, to put them into a folder referenced by your PATH environment variable so they can be found by the plugin.

**Note:** You **really want** to install _The Silver Searcher_. It makes this plugin much more useful. If `ag` is present, the plugin makes use of a permanent search results file that gets updated with the results of searches for tags, referencing notes, the tag list, etc. This really shines when [searching for tagged notes](#searching-for-notes-containing-specific-tags) and [searching for friend notes](#searching-for-friends).

The permanent search results file is like a navigation-window and is especially useful when using a non-single layout, like in this screenshot:

![silver-tags](https://user-images.githubusercontent.com/30892199/32641877-b27b28fc-c5d0-11e7-89ac-20f1f83db586.png)


## Configuration


### Zettelkasten note folder
No further configuration is necessary. This Zettelkasten plugin works with SublimeText projects. It will use exactly the same directory where your SublimeText project file is located.

#### How do I create a project in SublimeText?
That's easier than it might look. This is how I do it:

##### Automatic approach
Just start working and [create a new note](#creating-a-new-note)! Hit `shift+enter` in an empty SublimeText window with no project or file open. After entering the note's title, SublimeText will ask you where to save your new note and its corresponding project file. From then on, you'll be working in the very project directory that you just selected or created.

##### Manual approach
If you want to create an empty project first and then start creating notes, here is what I would do:

* Start with a fresh SublimeText window (containing no open files or projects).
* Use the menu: "Projects" -> "Save Project As ..." and save this empty project into your desired Zettelkasten folder, giving the project file a name other than untitled if you like.
* Now add the Zettelkasten folder to your project: "Project" -> "Add Folder To Project..." and select your Zettelkasten folder.
* Done! :-)


### Markdown filename extension
By default, the extension `.md` is used for your notes. If that does not match your style, you can change it in the `sublime_zk.sublime-settings` file. Just replace `.md` with `.txt` or `.mdown` or whatever you like.

### Single or double brackets
Whether you want to use `[[this link style]]` or `[that link style]` is totally up to you. Both work. But you need to configure which style you prefer, so automatically inserted links will match your style. `[[double bracket]]` links are the default, and if you want to change that to single bracket links, set the `double_brackets` parameter to `false` in the `sublime_zk.sublime-settings`.

### IDs in titles of new notes
When you create a new note, its title will automatically be inserted and an ID will be assigned to it (see [Creating a new note](#creating-a-new-note)). If you want the ID to be part of the title, change the setting `id_in_title` from `false` to `true`.

Example for a note created with ID:

```markdown
# 201710310128 This is a note with its ID in the title
tags=

The setting id_in_title is set to true.
```

Example for a note created without ID:

```markdown
# A note without an ID
tags =

The setting id_in_title is set to false.
```

You can find this setting in the file `sublime_zk.sublime-settings`.

### Highlight references to other notes
By default, this plugin highlights links to other notes by underlining them.
**Note:** This only applies to links containing an ID, like this one: [[201710290256]].
It also shows a bookmark symbol in the gutter to the left of your text. These features can be controlled via the following settings in `sublime_zk.sublime-settings`:

```json
    // highlight links to other notes?
    "highlight_note_links": true,

    // when highlighting: also show bookmark symbols in the gutter?
    "show_bookmarks_in_gutter": true,
```

### Configuring SublimeText's line spacing
When looking at the screenshot at the beginning of this document, you might have noticed the line spacing. I find it very pleasant to work with text this way. To configure SublimeText to use this line spacing:

* use the menu: "Preferences" --> "Settings - Syntax specific"
* SublimeText will show you two files side-by-side
* change the one on the right side (also named `sublime_zk.sublime-settings`) as follows:

```json
// These settings override both User and Default settings for the sublime_zk syntax
{
	"line_padding_bottom": 3,
	"line_padding_top": 3,
}
```
**Note:** The above file is part of your "User" settings and will be created by SublimeText automatically. It is not the one you downloaded with this plugin. So please don't confuse the two :-)


## Usage

### Creating a new note
* Press `[shift]+[enter]`. This will prompt you for the title of the new note at the bottom of your SublimeText window.
* Press `[ESC]` to cancel without creating a new note.
* Enter the note title and press `[enter]`.

A new note will be created and assigned the timestamp based ID in the format described above.

Example: Let's say you entered "AI is going to kill us all" as the note title, then a file with the name `201710282118 AI is going to kill us all.md` will be created and opened for you.

The new note will look like this:

```markdown
# AI is going to kill us all
tags =

```

### Syntax Coloring for #tags and footnotes
To enable highlighting of #tags and footnotes in your newly created note, and for all your Zettelkasten notes, switch Sublime Text's syntax to `Markdown Zettelkasten`. You can use the menu: 'View' -> 'Syntax' -> 'Open all with current extension as...', and select 'Markdown Zettelkasten'.

This package uses a custom scope for note links. While underlining them is done in the plug-in, you have to manually tweak your color scheme. Google is your friend - here is an example that needs to be added to (a copy of) your favourite color scheme:

```xml
    <dict>
      <key>name</key>
      <string>Markup: Zettelkasten note link</string>
      <key>scope</key>
      <string>markup.zettel.link</string>
      <key>settings</key>
      <dict>
        <key>fontStyle</key>
        <string>underline</string>
        <key>foreground</key>
        <string>#6080ef</string>
      </dict>
    </dict>
```

To get you started, this package provides the color scheme "Monokai Extended - Zettelkasten". You can select it via the menu: Preferences -> Color Scheme... -> Monokai Extended - Zettelkasten.
_(The original Monokai Extended for SublimeText has been created by [@jonschlinkert](https://github.com/jonschlinkert/sublime-monokai-extended))._


### Creating a link
Let's assume, you work in the note "201710282120 The rise of the machines":

```markdown
# The rise of the machines
tags = #AI #world-domination

Machines are becoming more and more intelligent and powerful.

This might reach a point where they might develop a consciensce of their own.
```

You figure, a link to the "AI is going to kill us all" note is a good fit to expand on that aspect of the whole machine-rise story, so you want to place a link in there.

You start typing:

```markdown
# The rise of the machines
tags = #AI #world-domination

Machines are becoming more and more intelligent and powerful.

This might reach a point where they might develop a consciensce of their own.

As a consequence, they might turn evil and try to kill us all ........... [[
```

The moment you type `[[`, a list pops up with all the notes in your archive. You enter "kill" to narrow down the selection list and select the target note. Voila! You have just placed a link into your note, which now looks like this:

```markdown
# The rise of the machines
tags = #AI #world-domination

Machines are becoming more and more intelligent and powerful.

This might reach a point where they might develop a consciensce of their own.

As a consequence, they might turn evil and try to kill us all ........... [[201710282118]]
```

**Note:** Only files ending with the extension specified in `sublime_zk.sublime-settings` (`.md` by default) will be listed in the popup list. If your files end with `.txt`, you need to change this setting.

If you now click into `[[201710282118]]` and press `[ctrl]+[enter]`, the target note will be opened where you can read up on how AI is potentially going to kill us all.

Here you can see what the list of notes to choose from looks like:
![screenshot2](https://user-images.githubusercontent.com/30892199/32403198-25f55650-c134-11e7-8f62-58fdbfb13c2b.png)

### Using auto-completion to insert note-links
A different way to insert a link to another note is via auto-completion. This differs from the previous one in the following ways:

* auto-completion is triggered via [ctrl]+[space] (or `[alt]+[/]` on Linux)
* the list of notes is displayed at the location of your cursor
* the font of the list is smaller, making it overall less obtrusive

You can, just as before, narrow the list auf auto-completion suggestions down by just continuing typing. However, once you write something that does not match anything in your note-list, the suggestions disappear. This is just how auto-completion works: it doesn't want to get in your way when you type something new.

Which ever method for link insertion you use is up to you.

Here is a screenshot so you can compare:
![screenshot2](https://user-images.githubusercontent.com/30892199/32403199-260fb374-c134-11e7-99ad-59e22852a095.png)

### Implicitly creating a new note via a link
There is another way to create a new note: Just create a link containing its title and follow the link.

To showcase this, let's modify our example from above: Say, the "AI is going to kill us all" does **not** exist and you're in your "The rise of the machines" note.

This is what it might look like:

```markdown
# The rise of the machines
tags = #AI #world-domination

Machines are becoming more and more intelligent and powerful.

This might reach a point where they might develop a consciensce of their own.
```

You now want to branch into the new thought you just had, that AI might potentially eventually be going to kill us all. You prepare for that by mentioning it and inserting a link, like this:

```markdown
# The rise of the machines
tags = #AI #world-domination

Machines are becoming more and more intelligent and powerful.

This might reach a point where they might develop a consciensce of their own.

As a consequence, they might turn evil and try to kill us all ........... [[AI is going to kill us all]]
```

**Note:** You will have to press `[ESC]` after typing `[[` to get out of the note selection that pops up, before entering the note title.

**Note:** Of course this also works if you use a single quote link: `[AI is going to kill us all]`.

Now, in order to actually create the new note and its link, all you have to do is to click inside the new note's title and press `[control]+[enter]`, just as you would if you wanted to open a regular linked note.

And voila! A new note `201710282118 AI is going to kill us all.md` will be created and opened for you.

But the really cool thing is, that the link in the original note will be updated to the correct ID, so again you will end up with the following in the parent note:

```markdown
# The rise of the machines
tags = #AI #world-domination

Machines are becoming more and more intelligent and powerful.

This might reach a point where they might develop a consciensce of their own.

As a consequence, they might turn evil and try to kill us all ........... [[201710282118]]
```

**Note** how the note title "AI is going to kill us all" has been replaced by the note's ID "201710282118".

The new note will be pre-filled with the following text:

```markdown
# AI is going to kill us all
tags =

```

### Searching for friends
If you see a link in a note and wonder what **other** notes also reference this note, then that is easy enough to do: Just click inside the link and press `[alt]+[enter]`.

**Note:** If you have `ag` installed, the list of all referencing notes will pop up immediately in the permanent search result file:

![silver-friends](https://user-images.githubusercontent.com/30892199/32641876-b25dae12-c5d0-11e7-8e03-f9b204902771.png)

However, if `ag` is not installed, a _find-in-files_ panel will be opened, automatically pre-filled to search for the note-ID.

![friend-search](https://user-images.githubusercontent.com/30892199/32442529-0aa52de8-c2fc-11e7-87fa-1f42b2a1c56b.png)

Just press `[enter]` to start the search. The resulting notes will be displayed in a new tab "Find Results":

![friend-results](https://user-images.githubusercontent.com/30892199/32442334-54ff1a76-c2fb-11e7-87ad-a551a9396f37.png)

**Note:** The *Find Results* tab will be re-used in subsequent searches. In the screenshot above I have used a split layout; the results will always show up in the tab at the bottom.



### Working with tags

#### Getting an overview of all your tags
Over time you might collect quite a number of **#tags** assigned to your notes. Sometimes it helps to get an overview of all of them, maybe to check for synonyms before creating a tag, etc.

When you press `[#][!]` (that is the `#` key followed by the `!` key) quickly, a scratch file listing all your #tags will be created and showed right next to your text:

![taglist](https://user-images.githubusercontent.com/30892199/32422037-fd32b18e-c29d-11e7-85d0-2d008b07fe1d.png)

**Note:** If you don't like splitting your window, set the parameter `show_all_tags_in_new_pane` to `false`.

Of course, if you have `ag` installed, the permanent search file will be used to display all your tags:

![silver-tags](https://user-images.githubusercontent.com/30892199/32641877-b27b28fc-c5d0-11e7-89ac-20f1f83db586.png)

#### Experimental tag selector
Press `[#]+[?]` to ask for a list of all tags used in your note archive. You can narrow down the search and finally pick the tag you like.

![tagsel](https://user-images.githubusercontent.com/30892199/32405205-25f94bc0-c161-11e7-914a-1a82bdf9c2f9.png)

Why is this experimental? Because it needs to scan all your notes everytime you invoke it. This is probably not very efficient in large note archives, so I consider its implementation experimental. However, if you have `ag` [installed](#installing-the-silver-searcher), then you don't need to worry about that. _Ag_ will be detected and used automatically to speed things up a lot.


#### Searching for notes containing specific tags
Like note-links, tags can also be "followed" by clicking them and pressing `[ctrl]+[enter]`.

**Note:** If you have `ag` installed, the list of all referencing notes will pop up immediately in the permanent search results file:

![silver-follow-tag](https://user-images.githubusercontent.com/30892199/32641875-b241e6fa-c5d0-11e7-819a-4705396f633b.png)

However, if `ag` is not installed, a _find-in-files_ panel will be opened, pre-filled with the clicked tag and your note archive folder.

![tagsearch](https://user-images.githubusercontent.com/30892199/32421934-1e1411f0-c29d-11e7-8e08-7f7775e32542.png)

Pressing `[enter]` will start the search and show the search results in a new tab.

![tagresults](https://user-images.githubusercontent.com/30892199/32421958-52a9cdec-c29d-11e7-9240-1a229a82351e.png)

**Note:** The *Find Results* tab will be re-used in subsequent searches. In the screenshot above I have used a split layout; the results will always show up in the tab at the bottom.

**Note:** If you set the parameter `show_search_results_in_new_tab` to `false`, then no new tab will be created for search results. They will be displayed in a little sort of pop-up at the bottom of the window.


### Expansion of overview notes with selective refresh

#### Expansion of overview notes

Let's say you have an overview note about a topic that links to specifics of that topic that looks like this:

```markdown
O - Text production

This is an **overview note** about text production with the Zettelkasten method.

A few general words about our tool: Sublime ZK
[[201711111707]] Sublime ZK is awesome
[[201711111708]] Sublime ZK is great

Then we go more in-depth:
[[201711111709]] The specifics of how we produce text with the plugin

Cool!
```

This overview is just a collection of note links with brief descriptions and a bit of additional text.

Now, if you wanted to turn this overview note into a text containing the contents of the linked notes instead of just the links, then you can *expand* the note like this:

* bring up the command palette by pressing `[cmd]+[shift]+[p]` on macOS (`[ctrl]+[shift]+[p]` on Windows and Linux).
* type `zk` to list the *Zettelkasten* commands.
* select `ZK: Expand Overview Note`

Et voila! Depending on your linked notes, the overview note will be expanded into a new unsaved tab, maybe looking like this:

![expanded](https://user-images.githubusercontent.com/30892199/32693323-613c43fe-c729-11e7-8773-04a9e20034f7.png)

As you can see, the lines containing note links are replaced by the contents of their notes, enclosed in comment lines. You can now edit and save this file to your liking.


**Note**: If you want to refresh this expanded overview [(see below)](#refreshing-an-expanded-overview-note) later, then please leave those comments in!

**Note:**: If you modify the text of a linked note (between comment lines), then remove the extra `!` to prevent your change to get overwritten when [refreshing](#refreshing-an-expanded-overview-note) this overview.


#### Refreshing an expanded overview note

It might happen that you change some notes that are already expanded into your new expanded overview note. If that happens and you have left the comments in, then you can refresh the expanded overview:

* bring up the command palette by pressing `[cmd]+[shift]+[p]` on macOS (`[ctrl]+[shift]+[p]` on Windows and Linux).
* type `zk` to list the *Zettelkasten* commands.
* select `ZK: Refresh Expanded Note`

**Note:** Only notes with comments starting with `<!-- !` will be considered for a refresh.

**Tip:** That means: To keep your edits of specific expanded notes from being overwritten by a refresh, just delete the extra `!`, making the comment start with `<!-- `. Alternatively, you can, of course, delete the comment lines for parts you are sure will never need refreshing.

The following animation illustrates expansion and refreshing:

![overview-expansion](https://user-images.githubusercontent.com/30892199/32693096-f2c69ffe-c724-11e7-9c6a-d01857e86ce1.gif)


## Credits

Credits, where credits are due:

* I derived this work from Dan Sheffler's MyWiki code. [See his GitHub](https://github.com/dansheffler/MyWiki) and see some striking similarities ;-).
* (Of course it has evolved a lot since. A special shoutout to @toolboxen from the forum at zettelkasten.de for all the ideas, github issues, and pull requests!)
* Thanks to [Niklas Luhmann](https://en.wikipedia.org/wiki/Niklas_Luhmann) for coming up with this unique way of using a Zettelkasten.
* Thanks to the guys from [zettelkasten.de](https://zettelkasten.de) for their Zettelkasten related resources. There are not that many out there.

While we're at it, I highly recommend the following books (German); Google and Amazon are your friends:

* "Das Zettelkastenprinzip" / "How to take smart notes" [(more info here...)](http://takesmartnotes.com/#moreinfo) will blow your mind.
* "Die Zettelkastenmethode" from Sascha over at zettelkasten.de will also blow your mind and expand on the plain-text approach of using a digital Zettelkasten.




