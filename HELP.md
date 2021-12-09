# AIS Commander


**AIS Commander** to menedżer plików działający w przeglądarce Internetowej. Zawiera przeglądarkę plików (tekst, audio, wideo) oraz edytor plików tekstowych. AIS Commander pomaga zarządzać serwerem AIS dom i pracować z plikami, katalogami w przeglądarce internetowej z dowolnego komputera, telefonu komórkowego lub tabletu.

## Klawisze skrótu

|Key                    |Operation
|:----------------------|:--------------------------------------------
| `F1`                  | help
| `F2`                  | show `user menu`
| `F3`                  | view, change directory
| `Shift + F3`          | view raw file, change directory
| `F4`                  | edit
| `F5`                  | copy
| `Alt` + `F5`          | pack
| `F6`                  | rename/move
| `Shift` + `F6`        | rename current file
| `F7`                  | new directory
| `Shift + F7`          | new file
| `F8`, `Delete`        | remove
| `Shift + Delete`      | remove without prompt
| `F9`                  | menu
| `Alt` + `F9`          | extract
| `*`                   | select/unselect all
| `+`                   | expand selection
| `-`                   | shrink selection
| `Ctrl + X`            | cut to buffer
| `Ctrl + C`            | copy to buffer
| `Ctrl + V`            | paste from buffer
| `Ctrl + Z`            | clear buffer
| `Ctrl + P`            | copy path
| `Ctrl + R`            | refresh
| `Ctrl + D`            | clear local storage
| `Ctrl + A`            | select all files in a panel
| `Ctrl + M`            | rename selected files in editor
| `Ctrl + U`            | swap panels
| `Ctrl + F3`           | sort by name
| `Ctrl + F5`           | sort by date
| `Ctrl + F6`           | sort by size
| `Up`, `Down`          | file system navigation
| `Enter`               | change directory/view file
| `Alt + Left/Right`    | show content of directory under cursor in target panel
| `Alt + G`             | go to directory
| `Ctrl + \`            | go to the root directory
| `Tab`                 | move via panels
| `Page Up`             | up on one page
| `Page Down`           | down on one page
| `Home`                | to begin of list
| `End`                 | to end of list
| `Space`               | select current file (and get size of directory)
| `Insert`              | select current file (and move to next)
| `F9`                  | context menu
| `~`                   | console
| `Esc`                 | toggle vim hotkeys (`file manager`, `editor`)


## Drag and drop

Te operacje na plikach są dostępne za pomocą metody „przeciągnij i upuść”.

| Drag Mouse Button | Key       | Origin    | Destination   |Operation
|:------------------|:----------|:----------|:--------------|:------------------
| Left              |           | Panel     | Panel         | copy files
| Left              | `Shift`   | Panel     | Panel         | rename/move files
| Left              |           | Panel     | Desktop       | download files
| Left              |           | Desktop   | Panel         | upload files

## Pogląd

![View](/img/screen/view.png "View")

### Obsługiwane typy plików

- podgląd zdjęć,
- podgląd zawartości plików tekstowych,
- odtwarzanie plików audio,
- odtwrzanie plików wideo.

### Klawisze skrótu

|Key                    |Operation
|:----------------------|:--------------------------------------------
| `F3`                  | open
| `Esc`                 | close

## Edycja plików tekstowych

![Edit](/img/screen/edit.png "Edit")

### Klawisze skrótu

|Key                    |Operation
|:----------------------|:--------------------------------------------
| `F4`                  | open
| `Shift + F4`          | open in "vim" mode
| `Esc`                 | close




## Menu

![Menu](/img/screen/menu.png "Menu")

Kliknij prawym przyciskiem myszy, aby wyświetlić menu kontekstowe z następującymi elementami:

- View
- Edit
- Rename
- Delete
- Pack
- Extract
- Download
- Cut
- Copy
- Paste
- New (File, Directory)
- Upload
- (Un)Select All

### Klawisze skrótu

|Key                    |Operation
|:----------------------|:--------------------------------------------
| `F9`                  | open
| `Esc`                 | close
