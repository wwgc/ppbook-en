# Electron PPKefu

PPKefu is an [electron](http://electron.atom.io/) project, supports `Mac, Mac App Store, windows 64bit/32bit, Linux`。

#### About
Support your ppkefu root directory is: `~/Doxcuments/ppmessage/ppmessage/ppkefu/ppkefu`.

There is three files about electron under this directory.

    package.json,
    www/package.json,
    www/main.js,

#### Developement
enter `~/Documents/ppmessage/ppmessage/ppkefu/ppkefu`.

* init `electron`

  install`electron-prebuilt, electron-packager, electron-builder`, run 

  ```
  npm run set-up-electron
  ```

* run electron

  after run gulp task, to run electron, type command

  ```
  npm run start
  ```

* generate installer

  ```
  npm run dist
  ```

