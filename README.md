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

Assuming you succesfully `forked` this [repository](https://github.com/racg0092/corporate.portal.db) in your computer. Clone this [repository](https://github.com/racg0092/corporate.portal.db) to your `root` directory.

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
 ``` sh
    $ cd /
 ```

 `Clone` the repository that you forked. We are assuming that your installed [git](https://git-scm.com/) in your machine. You can verify if it is installed by typing git in the terminal. You will get a result that starts like the sample below.
``` sh
    $ git
    usage: git [--version] [--help] [-C <path>] [-c <name>=<value>]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]
```

`If you get a result like the above`. Type the clonning command.
``` sh
    $ git clone https://github/<your github username>/corporate.portal.db.git
```

The cloning process should start and git will create a folder with all files in this repository. `Rename` the folder to `corporate`; You need to do this because the way the directory is specified in the config files.

From the `shell` (Terminal App, Powershell) go into the corporate folder.
``` sh
    $ cd corporate
```

Create the database `directory`, and the child directories in it.
``` sh
    $ mkdir db
    $ mkdir db/node1
    $ mkdir db/node2
    $ mkdir db/node3
``` 
In the `config` files `node1|node2|node3` there is comment out option.

 `#processManagement:`
  `# fork: true`

The reason being folks using `Windows` won't be able to fork the `mongod` process `(If anyone is aware of a better work around please let me know)`. If you are using `Linux` uncomment this options `(All you have to do to uncomment is removed the # symbols. DO NOT EDIT ANYTHING ELSE UNLESS YOU KNOW WHAT YOU ARE DOING)` and type the following commands on the same terminal. Other wise you will need `three` different terminals to run the `mongod` process.

Start up your severs with the mongod process. Folks using  `Windows will need to open three separate terminals to do this` one for each `node`.
- Go to the directory with the `config files`.
``` sh
    $ cd /corporate
``` 
- Start the servers.
``` sh
    
    $ mongod -f node1.conf
    $ mongod -f node2.conf
    $ mongod -f node3.conf
```

Folks on `Windows` for the next commands you will need a separate `terminal`
- Connect to the first server
``` sh
    $ mongo --port 29011
```
`From here on you are connected to the mongo shell`
- Initiate replica set.
``` sh
    MongoDB Enterprise > rs.initiate()
```
 `output:`
 ``` js
    {
        "info2" : "no configuration specified. Using a default configuration for the set",
        "me" : "localhost:29011",
        "ok" : 1
    }
 ```
- Make sure you are connected to the Primary Instance
``` sh
    MongoDB Enterprise > rs.isMaster()
```
`output:` A lot of information is going to print look for the following
``` js
    "ismaster" : true,
```
- Create an user `Do not exit the shell before creating the user`. Because of the security settings you will only be able to create an user on your first time logging in from the local machine that the database is running on. `You should be really careful when creating super users`; Howerver since the local server should be for your personal use `only` lets create one.
``` sh
    MongoDb Enterprise corp-portal:PRIMARY> use admin
    MongoDb Enterprise corp-portal:PRIMARY> db.createUser(
    ... {
    ... user:"make up username",
    ... pwd:"make up password",
    ... roles:['root']
    ... }
    ... )       
```
`output`
``` sh
    Successfully added user: { "user" : "the user name you selected", "roles" : [ "root" ] }
```
- Authenticate yourself
``` sh
    MongoDb Enterprise corp-portal:PRIMARY> db.auth("username of the user you created", "password for the user you created")
```
- Add second `node` to the replica set
``` sh
    MongoDb Enterprise corp-portal:PRIMARY> rs.add("localhost:29012")
```
`output`
``` js
{
        "ok" : 1,
        "$clusterTime" : {
                "clusterTime" : Timestamp(1592714980, 1),
                "signature" : {
                        "hash" : BinData(0,"TZH5ijrN0ZSBZdI0xqZCrN2fANA="),
                        "keyId" : NumberLong("6840655027212648450")
                }
        },
        "operationTime" : Timestamp(1592714980, 1)
}
```
- Add third `node` to the replica set
``` sh
    MongoDb Enterprise corp-portal:PRIMARY> rs.add("localhost:29013")
```
`output`
``` js
{
        "ok" : 1,
        "$clusterTime" : {
                "clusterTime" : Timestamp(1592714980, 1),
                "signature" : {
                        "hash" : BinData(0,"TZH5ijrN0ZSBZdI0xqZCrN2fANA="),
                        "keyId" : NumberLong("6840655027212648450")
                }
        },
        "operationTime" : Timestamp(1592714980, 1)
}
```
- Verify the replica set is set up correctly.
``` sh
    MongoDb Enterprise corp-portal:PRIMARY> rs.isMaster()
```
`output:` More info will print out but look for the follolwing section.
``` js
    "hosts" : [
                "localhost:29011",
                "localhost:29012",
                "localhost:29013"
    ],
```
## Enviroment
To connect from your application use the following connection string.
`mongodb://<username>:<password>@localhost:29011/?authSource=admin&replicaSet=corp-portal&readPreference=primary&appname=MongoDB`

To Connect from the shell
``` sh
    $ mongo --host "corp-portal/localhost:29011" -u <your_username> -p <your_password>
```
