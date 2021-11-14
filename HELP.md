# AIS Commander


**AIS Commander** is a web app file manager. It includes a text viewer and editor. AIS Commander helps you manage your server and work with files, directories in a web browser from any computer, mobile or tablet.


## Hot keys

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
| `F10`                 | config
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
| `Ctrl + M`            | [rename selected files](https://github.com/coderaiser/cloudcmd/releases/tag/v12.1.0) in editor
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

### Vim

When the `--vim` option is provided, or the configuration parameter `vim` is set, the following hotkeys become available:

|Key                    |Operation
|:----------------------|:--------------------------------------------
| `j`                   | navigate to next file
| `k`                   | navigate to previous file
| `dd`                  | remove current file
| `G` or `$`            | navigate to bottom file
| `gg` or `^`           | navigate to top file
| `v`                   | visual mode
| `y`                   | copy (selected in visual mode files)
| `p`                   | paste files
| `Esc`                 | unselect all
| `/`                   | find file in current directory
| `n`                   | navigate to next found file
| `N`                   | navigate to previous found file

Commands can be joined, for example:

- `5j` will navigate **5** files below current;
- `d5j` will remove next **5** files;
- `dG` will remove all files from current to bottom;

## Drag and drop

These file operations are accessible with "drag and drop".

| Drag Mouse Button | Key       | Origin    | Destination   |Operation
|:------------------|:----------|:----------|:--------------|:------------------
| Left              |           | Panel     | Panel         | copy files
| Left              | `Shift`   | Panel     | Panel         | rename/move files
| Left              |           | Panel     | Desktop       | download files
| Left              |           | Desktop   | Panel         | upload files

## View

![View](/img/screen/view.png "View")

### Features

- View images.
- View text files.
- Play audio.
- Play video.

### Hotkeys

|Key                    |Operation
|:----------------------|:--------------------------------------------
| `F3`                  | open
| `Esc`                 | close

## Edit

![Edit](/img/screen/edit.png "Edit")

### Hot keys

|Key                    |Operation
|:----------------------|:--------------------------------------------
| `F4`                  | open
| `Shift + F4`          | open in "vim" mode
| `Esc`                 | close

For more details see [Edward hotkeys][EDWARD_KEYS].


### User Menu

When you press `F2` Cloud Commander will read a file `.cloudcmd.menu.js` by walking up parent directories, if can't read it will try to read `~/.cloudcmd.menu.js`.

Let's consider example `user menu` works file:

```js
const RENAME_FILE = 'Rename file';

export default {
    '__settings': {
        select: [
            RENAME_FILE,
        ],
        run: false,
    },
    [`F2 - ${RENAME_FILE}`]: async ({DOM}) => {
        await DOM.renameCurrent();
    },
    'D - Build Dev': async ({CloudCmd}) => {
        await CloudCmd.TerminalRun.show({
            command: 'npm run build:client:dev',
            autoClose: false, // optional
            closeMessage: 'Press any button to close Terminal', // optional
        });
        
        await CloudCmd.refresh();
    },
    'P - Build Prod': async ({CloudCmd}) => {
        await CloudCmd.TerminalRun.show({
            command: 'npm run build:client',
            autoClose: true, // optional
        });
        
        await CloudCmd.refresh();
    },
    'C - Create User Menu File': async ({DOM, CloudCmd}) => {
        const {CurrentInfo} = DOM;
        
        const {dirPath} = CurrentInfo;
        const path = `${dirPath}.cloudcmd.menu.js`;
        const {prefix} = CloudCmd;
        
        const data = await readDefaultMenu({prefix});
        await createDefaultMenu({
            path,
            data,
            DOM,
            CloudCmd,
        });
    },
};

async function createDefaultMenu({path, data, DOM, CloudCmd}) {
    const {IO} = DOM;
    
    await IO.write(path, data);
    await CloudCmd.refresh();
    
    DOM.setCurrentByName('.cloudcmd.menu.js');
    
    await CloudCmd.EditFile.show();
}

async function readDefaultMenu({prefix}) {
    const res = await fetch(`${prefix}/api/v1/user-menu/default`);
    const data = await res.text();
    
    return data;
}
```

You will have ability to run one of this 3 commands with help of double click, enter, or binded key (`F2`, `D` or `P` in this example). Also you can run commands in terminal, or execute any built-in function of `Cloud Commander` extended it's interface. You can find more examples in [User Menu Cookbook](https://github.com/coderaiser/cloudcmd/wiki/User-Menu-Cookbook).

#### User Menu API

Here you can find `API` that can be used in **User Menu**. **DOM** and **CloudCmd** two main objects you receive in arguments list using destructuring.

**DOM** contains all base functions of `Cloud Commander` (rename, remove, download etc);

- `renameCurrent` - shows renames current file dialog, and does renaming.

**CloudCmd** contains all modules (`Terminal`, `View`, `Edit`, `Config`, `Console` etc);

- `TerminalRun` - module that shows `Terminal` with a `command` from options and closes terminal when everything is done.

**IO** Files API

- `rename(from, to)` - rename `from` into `to`
- `move(from, to, names)` - rename files with a `names` `from` into `to`;
- `copy(from, to, names)` - copy files with a `names` `from` into `to`;
- `createDirectory(path)` - create directory with a `path`;

### Distribute

Being able to configure Cloud Commander remotely opens the doors to using it as microservice, and that's what the "distribute" options set out to do.

There is an **export server** and an **import client**, which are enabled with `--export` and `--import` respectively. There is a "token", which should be the same in `--import-token` and `--export-token`. To use the *import client*, you should provide `--import-url` to the client so it can connect to an *export server*.

There are two ways that the *import client* can receive configuration from an *export server*:

- full config at startup (default)
- get every updated option (with help of the `--import-listen` flag)

#### An example - using the "distribute" options to get configuration from a remote instance:

Here's an *export server*:

```
coderaiser@cloudcmd:~$ cloudcmd --port 1234 --export --export-token=cloudcmd
```

...and an *import client*:

```
coderaiser@cloudcmd:~$ cloudcmd --name importer --port 4321 --import-url http://127.0.0.1:1234 --import-token=cloudcmd --no-server --save
```

Here's the log output from the *export server*:

```
url: http://localhost:1234/
2018.08.23 13:41:45 -> export: try to auth from importer [127.0.0.1:4321]
2018.08.23 13:41:45 -> export: connected to importer [127.0.0.1:4321]
2018.08.23 13:41:45 -> export: config send to importer [127.0.0.1:4321]
2018.08.23 13:41:45 -> export: disconnected importer [127.0.0.1:4321]
```

...and the log output from the *import client*:

```
2018.08.23 13:47:36 -> import: try to auth to http://127.0.0.1:1234
2018.08.23 13:47:36 -> import: connected to http://127.0.0.1:1234
2018.08.23 13:47:36 -> import: config received from http://127.0.0.1:1234
2018.08.23 13:47:36 -> import: disconnected from http://127.0.0.1:1234
```

When the *import client* uses `--import-listen`, a persistent connection is used, and the *client* receives live updates from the *import server*.

The *export server* omits the following configuration fields:

- `auth`
- `username`
- `password`
- `algo`
- `name`
- `ip`
- `port`
- `root`
- `import`
- `importUrl`
- `importToken`
- `export`
- `exportToken`
- `log`
- `configDialog`

## Menu

![Menu](/img/screen/menu.png "Menu")

Right-mouse click to show a context menu with these items:

- View
- Edit
- Rename
- Delete
- Pack
- Extract
- Upload To Cloud
- Download
- Cut
- Copy
- Paste
- New (File, Directory)
- Upload
- Upload From Cloud
- (Un)Select All
- Log Out (available when the `authorization` is enabled)

### Hot keys

|Key                    |Operation
|:----------------------|:--------------------------------------------
| `F9`                  | open
| `Esc`                 | close


## Using as middleware

Cloud Commander can be used as middleware for `node.js` applications based on [socket.io](http://socket.io "Socket.IO") and [express](http://expressjs.com "Express"):

Init `package.json`:

```
npm init -y
```

Install dependencies:

```
npm i cloudcmd express socket.io -S
```

And create `index.js`:

```js
import http from 'http';
import cloudcmd from 'cloudcmd';
import {Server} from 'socket.io';
import express from 'express';

const app = express();
const port = 1337;
const prefix = '/';

const server = http.createServer(app);
const socket = new Server(server, {
    path: `${prefix}socket.io`,
});

const config = {
    name: 'cloudcmd :)',
};

const filePicker = {
    data: {
        FilePicker: {
            key: 'key',
        },
    },
};

// override option from json/modules.json
const modules = {
    filePicker,
};

const {
    createConfigManager,
    configPath,
} = cloudcmd;

const configManager = createConfigManager({
    configPath,
});

app.use(prefix, cloudcmd({
    socket, // used by Config, Edit (optional) and Console (required)
    config, // config data (optional)
    modules, // optional
    configManager, // optional
}));

server.listen(port);
```

Here is example with two `Config Managers`:

```js
import http from 'http';
import cloudcmd from 'cloudcmd';
import {Server} from 'socket.io';
import express from 'express';

const app = express();
const port = 8000;
const prefix1 = '/1';
const prefix2 = '/2';

const {createConfigManager} = cloudcmd;

const server = http.createServer(app);
const socket1 = new Server(server, {
    path: `${prefix1}/socket.io`,
});

const socket2 = new Server(server, {
    path: `${prefix2}/socket.io`,
});

const configManager1 = createConfigManager();
configManager1('name', '1');

const configManager2 = createConfigManager();
configManager2('name', '2');

app.use(prefix1, cloudcmd({
    socket: socket1,
    configManager: configManager1,
}));

app.use(prefix2, cloudcmd({
    socket: socket2,
    configManager: configManager2,
}));

server.listen(port);
```

If you want to enable authorization, you can pass credentials to Cloud Commander with a config. To generate a password, you can install `criton` with `npm i criton --save`, and use it (or any other way) to generate a hash of a password.

```js
import criton from 'criton';
const algo = 'sha512WithRSAEncryption'; // default

// you can generate a hash dynamically
const password = criton('root', algo);

// or use a pregenerated hash as well
'2b64f2e..ca5d9a9';

const auth = true;
const username = 'root';

const config = {
    algo, // optional
    auth,
    username,
    password,
};
```

