# Hyper Tab Icons (Plus)

> Improved forked version of Hyper Tab Icons from Dylan Frankland, displays
> icons in the header tabs for the current running process in Hyper terminal.

#### How It Works

Uses [fuzzaldrin][fuzzaldrin] to try to match the current tab title with the SVG
icons that have been added to the repo, then displays the matched icon. Has the
ability to map different icons and styles.

[fuzzaldrin]: https://github.com/atom/fuzzaldrin

#### Demo

![alt demo][demo gif]

[demo gif]: http://i.giphy.com/pb6hCi4j0ErpC.gif

## Configuration

There are few options to customize the different icons and styles applied. You
may configure these inside of `~/.hyper.js`.

#### `config.tabIcons.activeStyle`

* Type: `object`
* Default:
  ```
  {
    display: 'inline-block',
    marginRight: '0.25rem',
    transition: 'opacity 200ms ease-in',
    verticalAlign: 'middle',
    width: '1rem',
  }
  ```

This object can be any [CSSStyleDeclaration][mdn css] allowed. Pass an inline
style object [the same way you would with React][react inline-styles].

#### `config.tabIcons.inactiveStyle`

* Type: `object`
* Default:
  ```js
  {
    display: 'inline-block',
    marginRight: '0.25rem',
    transition: 'opacity 200ms ease-in',
    verticalAlign: 'middle',
    width: '1rem',
    opacity: 0.3,
  }
  ```

This object can be any [CSSStyleDeclaration][mdn css] allowed. Pass an inline
style object [the same way you would with React][react inline-styles].

[mdn css]: https://developer.mozilla.org/en-US/docs/Web/API/CSSStyleDeclaration/cssText
[react inline-styles]: https://facebook.github.io/react/tips/inline-styles.html

#### `config.tabIcons.mapIcons`

* Type: `object`
* Default: `{}`

Map of icon to array of process names. Example:

```javascript
{
  nodejs: ['node'],
  docker: ['docker-compose'],
}
```

Look inside [`src/icons`][icons] for possible icons to map to. Look at
[`src/constants/mapIcons.js`][mapicons] for defaults.

[icons]: https://github.com/sangdth/hyper-tab-icons-plus/tree/master/src/icons
[mapicons]: https://github.com/sangdth/hyper-tab-icons-plus/blob/master/src/constants/mapIcons.js

#### `config.tabIcons.mapColors`

* Type: `object`
* Default: `{}`

Map of process name to color string. Example:

```javascript
{
  bash: '#FFF',
  fish: '#D8494F',
  zsh: '#C5DB00',
}
```

Look at [`src/constants/mapColors.js`][mapcolors] for defaults.

[mapcolors]: https://github.com/dfrankland/hyper-tab-icons/tree/master/src/constants/mapColors.js

#### `config.tabIcons.disableColors`

* Type: `boolean`
* Default: `false`

Toggles icon colors. Inherits color from current CSS applied to tab text
_✨magically✨_.

#### `config.tabIcons.processNameRegex`

* Type: `object`
* Default: `/^(.*?) /`

The regex used to capture the process name in the title.

_If you use something like `zsh` that swaps the process name and current working
directory, the following regex should work: `/: (.*?)$/`._

> Alternatively, supply an object with the properties `source` and `flags`.
>
> ```js
> {
>   source: '^(.*?) ',
>   flags: '',
> }
> ```

#### `config.tabIcons.processNameMatch`

* Type: `number` (integer)
* Default: `1`

The index of the match out of the array of matches made by
`config.tabIcons.processNameRegex`.

> An index of `0` is the full match made by the regex. An index of `1` or more
> is used to get an exact match from one of the matching groups.

## Contribution

There are an almost infinite amount of processes out there, so any help adding
new icons, mapping colors, et cetera is greatly appreciated!

#### 1. Add new icon

Add `newicon.svg` icon into `src/icons/` folder, then edit the file
`src/icons/index.js`

```
export newicon from './newicon.svg';
```

#### 2. Map icon to process's name

Then, edit `src/constants/mapIcons.js`, please note:

```
newicon: [
    'process-name-1',
    'process-name-2',
    'process-name-3',
    'process-name-4',
  ],
```

`newicon` should match the name you have exported above, but the array is the
name of processes. Make example, we use `shell` icon for all kinds of `bash`,
`fish` and `zsh` process.

#### 3. Map color

Now you can map color by editing `src/constants/mapColors.js` file. Please note
that you need to use the `process-name` to map the color, not `icon` name.

Then run `npm run build` to make the build if you want.

## Credit

Inspired by [Atom's][atom] [`file-icons`][file-icons]. This project was first
initiated by [Dylan Frankland][original-project], I forked it and add more
stuffs here.

[atom]: http://atom.io/
[file-icons]: https://github.com/DanBrooker/file-icons
[original-project]: https://github.com/dfrankland/hyper-tab-icons
