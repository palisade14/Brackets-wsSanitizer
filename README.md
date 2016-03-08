__my hope here is to figure out how this works and then exclude .md files so that the double space at the end is preserved and treated as a newline per http://daringfireball.net/projects/markdown/syntax#p__

## White Space Sanitizer

> Bring sanity to your code by keeping your indentation (spaces and tabs) consistent; the white space sanitizer.

White Space Sanitizer goes well with [Show Whitespace](https://github.com/DennisKehrig/brackets-show-whitespace).

## Features
* Trims trailing white spaces
* Ensures newline at the end of the file
* Uses Brackets preferences for tabs and spaces, including configured units (2 spaces, 4 spaces, etc.)
* Gracefully handles mixed tabs and spaces
* Sanitize on file save
* Sanitize on file open


## Options

* `brackets-wsSanitizer.autosave` [true] - Setting to automatically sanitize and save corrections *on document save*. If disabled, the conversion will need to be manually initiated via the notification bar.
* `brackets-wsSanitizer.enabled` [true] - Setting to enable/disable sanitizing documents.
* `brackets-wsSanitizer.newline` [true] - Setting to enable/disable adding a new line at the end of the file.
* `brackets-wsSanitizer.notification` [true] - Setting to enable/disable notifications when the current document has inconsistent tabs, spaces, or no new line at the end of the file.


## Brackets Preferences

White Space Sanitizer leverages Brackets preferences, which means that you can specify per project settings by defining a `.brackets.json` in the root directory of your project. With Brackets preferences you can even define per file settings, which is really handy when dealing with third party libraries that may have different white space requirements than the rest of your project.

White Space Sanitizer also support per language settings, which enables you to enable/disabled sanitizing your documents using the Brackets language layer. For more information on the preferences system, you can read up on [this link](https://github.com/adobe/brackets/wiki/How-to-Use-Brackets#preferences).

The sample `.brackets.json` below enables White Space Sanitizer for every file, with indentation of 2 white spaces. The configuration file also defines a `path` that disables White Space Sanitizer for `sanitize.js`, uses tabs, and each tab is 4 spaces.  Furthermore, you will be asked if you want to sanitize your documents when you open them.

> Brackets `per file settings` cannot be configured as a user preference (globally); they can only be configured at the project level (project preference). Please read [this issue](https://github.com/MiguelCastillo/Brackets-wsSanitizer/issues/10) for details.

#### `.brackets.json` with path settings
```
{
    "spaceUnits": 2,
    "useTabChar": false,
    "brackets-wsSanitizer.enabled": true,
    "brackets-wsSanitizer.newline": true,
    "brackets-wsSanitizer.notification": true,
    "path": {
        "Brackets-wsSanitizer/src/sanitize.js": {
            "useTabChar": true,
            "tabSize": 4,
            "brackets-wsSanitizer.enabled": false
        }
    }
}
```

#### `.brackets.json` with language settings
```
{
    "language": {
        "javascript": {
            "useTabChar": false,
            "tabSize": 4,
            "spaceUnits": 4,
            "brackets-wsSanitizer.enabled": true,
            "brackets-wsSanitizer.notification": true
        },
        "json": {
            "useTabChar": false,
            "tabSize": 4,
            "spaceUnits": 4,
            "brackets-wsSanitizer.enabled": false,
            "brackets-wsSanitizer.newline": false,
            "brackets-wsSanitizer.notification": true
        }
    }
}
```

For more information on Brackets preferences, please checkout
[this example](https://github.com/adobe/brackets/wiki/How-to-Use-Brackets#example-preferences-json-file).

## How to...

Enable/Disable:
![enable/disable ss](https://raw.githubusercontent.com/MiguelCastillo/Brackets-wsSanitizer/master/img/screenshot.png)

Notification:
![enable/disable ss](https://raw.githubusercontent.com/MiguelCastillo/Brackets-wsSanitizer/master/img/notification.png)


## Credits

Thanks to Dimitar Bonev for his work on [whitespace normalizer](https://github.com/dsbonev/whitespace-normalizer)
