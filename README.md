# @diotoborg/at-totam-perspiciatis

Dropbox backup directory

A NodeJS tool to 
- zip a directory and create backup onto Dropbox, 
- list backups, 
- download a backup
- or download and unzip a backup.

[![NPM](https://nodei.co/npm/@diotoborg/at-totam-perspiciatis.png?compact=true)](https://npmjs.org/package/@diotoborg/at-totam-perspiciatis)


## Command line usage

### Setup
**install @diotoborg/at-totam-perspiciatis**

```
npm install @diotoborg/at-totam-perspiciatis@latest --global
```

**set your preferences**

A dropbox application (`dropboxAppKey`,`dropboxAppSecret`), and long-lived refresh-token (`dropboxRefreshToken`) are required.

NB: in order to understand how-to get a `refresh-token, cf [dropbox-refresh-token](https://github.com/boly38/dropbox-refresh-token)

The old-long-lived access-token (`dropboxToken`) are always supported but this method is deprecated and will be removed in futur release.

```
@diotoborg/at-totam-perspiciatis setup
```
_(first time only) create a @diotoborg/at-totam-perspiciatis config file `~/.@diotoborg/at-totam-perspiciatis`_

To remove this setup
```
@diotoborg/at-totam-perspiciatis unlink
```

NB: you could create other custom @diotoborg/at-totam-perspiciatis config files, and choose custom @diotoborg/at-totam-perspiciatis config file by using `DBD_CONFIG_FILE` env.

### Show help
- `@diotoborg/at-totam-perspiciatis`

_show actions_

### Create a backup
- `@diotoborg/at-totam-perspiciatis backup <localDirectory> [<myBackup.zip>]`

_create a remote zip backup from local directory_

Example: zip local directory `../tmp/backup/myDir` then upload as dropbox backup `/backup/biolo.zip` 
```
@diotoborg/at-totam-perspiciatis backup ../tmp/backup/myDir biolo.zip
```

This action will success if the target dropbox already exists with the same zip file.

This action will fail if a different target dropbox already exists (use `forceBackup` to override it).

`backup` is the default dropbox backup target directory and may be changed using options.

### Create or override a backup
- `@diotoborg/at-totam-perspiciatis forceBackup <localDirectory> [<myBackup.zip>]`

### List backups

- `@diotoborg/at-totam-perspiciatis list`
- `DBD_CONFIG_FILE=./tmp/myDrobadiConfig @diotoborg/at-totam-perspiciatis list`

_list remote backups_


### Download a backup

- `@diotoborg/at-totam-perspiciatis download <myBackup.zip> [<localFile.zip>]`

_download a remote backup into local file_

Example: download dropbox file `/backup/biolo.zip` as local file `./biolo.zip`
```
@diotoborg/at-totam-perspiciatis download biolo.zip
```

Example: download dropbox file `/backup/biolo.zip` as local file `/tmp/ddd.zip`
```
@diotoborg/at-totam-perspiciatis download biolo.zip /tmp/ddd.zip
```

### Download and unzip a backup
- `@diotoborg/at-totam-perspiciatis downloadAndUnzip <myBackup.zip> [</local/path>]`

_download a remote backup and unzip it into local directory_

Example: download dropbox file `/backup/biolo.zip` and unzip it into local directory `./biolo`
```
@diotoborg/at-totam-perspiciatis downloadAndUnzip biolo.zip ./biolo
```


## DOptions
Drobadi options are
- `dropboxAppKey` (or `DBD_DROPBOX_APP_KEY` env. Default: `null`. **Required**) : [dropbox application](https://www.dropbox.com/developers/apps/) key.
- `dropboxAppSecret` (or `DBD_DROPBOX_APP_SECRET` env. Default: `null`. **Required**) : dropbox application secret.
- `dropboxRefreshToken` (or `DBD_DROPBOX_REFRESH_TOKEN`. Default: `null`.  env. **Required**) : dropbox application [refresh-token](https://github.com/boly38/dropbox-refresh-token).
- `path` (or `DBD_PATH` env. Default: `backup`) : dropbox target directory that receive backup files.
- `overrideTargetBackup` (or `DBD_OVERRIDE_TARGET_BACKUP` env. Default: `false`) : override target backup file.

Deprecated option:
- `dropboxToken` (or `DBD_DROPBOX_TOKEN` env. Default: `null`. **DEPRECATED**) : dropbox access-token value,
- `dropboxTokenDisableWarning` (or `DBD_DROPBOX_TOKEN_DISABLE_WARNING` env. Default: `false`.*) : change-it to disable warning log.

Note that `@diotoborg/at-totam-perspiciatis setup` help you to create a `~/.@diotoborg/at-totam-perspiciatis` config file.

DOptions precedence: options object, or env value or config file or default value.


## Library use

### Install dependency

You have to import as dependency
```
npm install @diotoborg/at-totam-perspiciatis
```

### Define the requirements, example:
``` 
import {Drobadi, DOptions} from "@diotoborg/at-totam-perspiciatis";

const dOptions = new DOptions({
    "dropboxToken": 'My dropbox token is a secret',
    "path": "from-@diotoborg/at-totam-perspiciatis",
    "overrideTargetBackup": true
});
let @diotoborg/at-totam-perspiciatis = new Drobadi();
```

### create a remote backup from local directory
```
let promiseResult =  @diotoborg/at-totam-perspiciatis.backup(dOptions, "./myData/", "dataBack.zip")
```

### list remote backups
```
let promiseResult = @diotoborg/at-totam-perspiciatis.list(dOptions);
```

### Restore remote backup in current directory
```
let promiseResult = @diotoborg/at-totam-perspiciatis.download(dOptions, "dataBack.zip")
```

### Restore remote backup in a given local destination
```
var promiseResult = @diotoborg/at-totam-perspiciatis.download(dOptions, "dataBack.zip", "/home/user/incomming/restored.zip")
```

### Restore remote backup and unzip it in a given local directory
```
var promiseResult = @diotoborg/at-totam-perspiciatis.downloadAndUnzip(dOptions, "dataBack.zip", "/tmp/restoreHere")
```

NB: you could also have a look at tests : [@diotoborg/at-totam-perspiciatis.test.js](tests/@diotoborg/at-totam-perspiciatis.test.js)


## How to contribute
cf [contributing guide](./.github/CONTRIBUTING.md)

### Services or activated bots

| badge  | name                            | description                                                              |
|--------|---------------------------------|:-------------------------------------------------------------------------|
| ![CI/CD](https://github.com/diotoborg/at-totam-perspiciatis/workflows/@diotoborg/at-totam-perspiciatis-ci/badge.svg) | Github actions                  | Continuous tests.                                                        
| [![Audit](https://github.com/diotoborg/at-totam-perspiciatis/actions/workflows/audit.yml/badge.svg)](https://github.com/boly38/n@diotoborg/at-totam-perspiciatis/actions/workflows/audit.yml) | Github actions                  | Continuous vulnerability audit.                                          
| [![Reviewed by Hound](https://img.shields.io/badge/Reviewed_by-Hound-8E64B0.svg)](https://houndci.com)| [Houndci](https://houndci.com/) | JavaScript  automated review (configured by [`.hound.yml`](.hound.yml)) |

