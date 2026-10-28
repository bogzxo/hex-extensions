# Hex extensions

The extensions [Hex](https://github.com/bogzxo/hex) installs, the catalog it syncs. Hex looks here once a day as it
starts (and whenever Check now is pressed on Extensions, Available in its settings), lists every one on that page with
Install on the ones you haven't got and Update on the ones that are behind, and puts up a card when one you installed has
a newer version. An install is a copy of the folder into the `extensions` folder next to Hex, started straight away.

| Extension | What it does |
| --- | --- |
| `emmet` | HTML abbreviations written out on Tab or Ctrl+E, `ul>li.item$*3` and the rest of Emmet's shorthand |
| `hello_dolly` | A random greeting in the title bar every time Hex starts |
| `move_editor` | Fighter2D's moves edited on a timeline, frame by frame, with their boxes on the sprite |
| `pretty_json` | JSON formatted, minified, its keys sorted, and checked as it's saved |
| `snippets` | A word and Tab written out as the code it stands for, then Tab from one place in it to the next |
| `text_tools` | Sort, reverse, unique and join lines, line them up, change the case of a word and wrap a selection |
| `todo` | Every TODO and FIXME of the file in a menu to go to, and in Problems if you want them there |

Pretty JSON, Snippets, Text tools and the TODO list need a Hex with `hex.selection`, `hex.select` and `hex.lines`
(after 1.0.2). On an older one they say so rather than doing anything. Every one of them is written in the HIDL that came
with Hex 1.1, arrows, `in`, bodies without braces and the rest, which a Hex from before that can't read at all.

## How it's laid out

A folder an extension, with an `extension.hor` in it, at the top of the repository. Nothing else is copied, this README
stays here. Hex reads what an extension is from its extension object, so that's the one place a version is written.

```
let extension = {
    name: "Emmet",
    description: "HTML abbreviations written out on Tab or Ctrl+E.",
    version: "1.0.0",
    author: "bogz"
};
```

The version is what decides an update, `1.0.1` here and `1.0.0` installed is a card in Hex. Bump it with every change
that should reach people, a change without a bump only reaches somebody who installs it fresh.

Hex syncs the `main` branch as one zip, so whatever is on `main` is what's out. Work on another branch and merge it when
it's ready.

## Settings

What an extension can be told goes in a `settings` object of its extension object, a key a setting, in the order they're
shown. Each is a row of Hex's settings window under the extension's name, found by the search, with a reset while it
isn't its default, and kept in the extensions section of Hex's settings file. `hex.setting("indent")` reads one.

```
settings: {
    indent: { title: "Indent", about: "Spaces a level, 0 for a tab.", kind: "number", least: 0, most: 8, step: 1, slider: true, default: 4 },
    quotes: { title: "Quotes", about: "What a string is written in.", kind: "choice", choices: ["double", "single"],
        labels: ["Double \"\"", "Single ''"], help: ["The way JSON has it.", "Fewer shifts."], default: "double" },
    check_on_save: { title: "Check on save", about: "Check every time it's saved.", kind: "flag", default: true }
}
```

| Kind | What it is |
| --- | --- |
| `text` | A line of text, what it is when the kind isn't said |
| `path` | A file or a folder, with Choose... beside its box |
| `number` | A number. `least` and `most` are its ends (none unless most is past least), `step` what it goes up and down by, `slider: true` a slider between the ends instead of a box. What is set past an end in the window is kept at that end, a hand-edited file is read as it is |
| `flag` | On or off |
| `choice` | One of `choices`, a dropdown. `labels` is what each says in it and `help` a line under it saying what the one picked does, both in the order of the choices and both optional. One that isn't among the choices is never set, and a default that isn't one is the first |

## Writing one

Hex's README has everything `hex` can do, in its Extensions section. Point Hex at a folder of your own while
you write one, Extensions, Available, Catalog, a folder on your machine laid out like this repository, and Check now. Or
put it straight in the `extensions` folder next to Hex, where it's read again every time a `.hor` of it is saved.

Hex's tests check these out as a submodule (`hex/hex-extensions`), so a change here is tested against the Hex it'll run in.
