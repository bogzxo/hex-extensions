# Hex extensions

The extensions [Hex](https://github.com/bogzxo/hex) installs, the catalog it syncs. Hex looks here once a day as it
starts (and whenever Check now is pressed on Extensions, Available in its settings), lists every one on that page with
Install on the ones you haven't got and Update on the ones that are behind, and puts up a card when one you installed has
a newer version. An install is a copy of the folder into the `extensions` folder next to Hex, started straight away.

| Extension | What it does |
| --- | --- |
| `emmet` | HTML abbreviations written out on Tab or Ctrl+E, `ul>li.item$*3` and the rest of Emmet's shorthand |
| `hello_dolly` | A random greeting in the title bar every time Hex starts |
| `markdown_preview` | Any Markdown file as it reads, next to its code, following it as it's typed |
| `move_editor` | Fighter2D's moves edited on a timeline, frame by frame, with their boxes on the sprite |

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

## Writing one

Hex's README has everything `hex` can do, in its Extensions section. Point Hex at a folder of your own while
you write one, Extensions, Available, Catalog, a folder on your machine laid out like this repository, and Check now. Or
put it straight in the `extensions` folder next to Hex, where it's read again every time a `.hor` of it is saved.

Hex's tests check these out as a submodule (`hex/hex-extensions`), so a change here is tested against the Hex it'll run in.
