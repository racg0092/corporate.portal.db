# Corporate Portal MongoDB
This repo is meant to be used as a local set up for the `Corporate Portal Application`. However if you want to deploy a local replica set you can take advantage
of some of the work done here already.

## Prerequisites
- `Knowledge` A basic knowledge of mongodb administration will help.
- `Tool:Required` [Mongo DB Enterpirse Server](https://www.mongodb.com/try/download/enterprise).
- `Tool:Optional` [Mongo Db Compass](https://www.mongodb.com/try/download/compass).
    - `The full version`
- `Knowledge` We are assuming that you are aware of what [github](https://github.com) is and have some basic understanding of how it works.
- `Tool:Required` You will need [git](https://git-scm.com/) to interact with you repository from the command line.
- You will need a github account.
    - [Github](https://github.com)

## Resources
- [Mongo Db University](https://university.mongodb.com/) is a great source to learn if your not familiar with MongoDb.
- [The Git website](https://git-scm.com/) is a good source to install and learn how to use git.

## Installation
First things first. After you created your [github](https://github.com) account fork this [`repository`](https://github.com/racg0092/corporate.portal.db).
You should be able to do it by clicking on the `fork` icon at the top right side of this page.

Assuming you succesfully `forked` this [repository](https://github.com/racg0092/corporate.portal.db). In your computer clone this [repository](https://github.com/racg0092/corporate.portal.db) to your `root` directory.

### Windows
Open [`powershell`](https://docs.microsoft.com/en-us/powershell/). 
- Press `Start` button.
- Type `Windows Power Shell` (as you type, it should auto-fill).
- `Optional` you can use `Command Prompt` as well but some of the terminal `commands` can differ from this instructions.

### MAC
Open [`Terminal App`](https://www.businessinsider.com/how-to-open-terminal-on-mac). 
- Press the `Command` button and the `space` bar, simultaneously.
- Type `Terminal` (as you type, it should auto-fill).
- Double click `Terminal` in the left sidebar to open your Mac's Terminal.

### Linux
`Due to the many distros in Linux I will only cover Ubuntu`
However you can search online or how to access your terminal in your not aware.
- Press `CTRL`, `ALT` and `T` simultaneously.

### Shell Commands
Once you open your `terminal` go to the root directory.
 ``` shell
    cd /
 ```

 `Clone` the repository that you forked. We are assuming that your installed [git](https://git-scm.com/) in your machine. You can verify if it is install by typing git in ther terminal. Sample below
``` shell
    shell> git
    usage: git [--version] [--help] [-C <path>] [-c <name>=<value>]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]
```
