# Simple Instruction

## Clone repository
run `git clone git@github.com:b1tk3y/electron-python-example.git`

## Install python packages
Run `pip install -r requirements.txt`
For Windows user, uncomment `pypiwin32` line in the requirements.txt

## Install node packages
Run `npm install --runtime=electron --target=1.7.6`

To verify the electron binary and its version by opening it:
```shell script
./node_modules/.bin/electron
```

## Test each part
### Python part
1. Run `python pycalc/api.py`
2. Open new terminal, and run:
    ```shell script
    zerorpc tcp://localhost:4242 calc "1 + 1"
    ## connecting to "tcp://localhost:4242"
    ## 2.0
    ```
   
### Node.js/Electron part
1. Run `./node_modules/.bin/electron .`
2. App is excuted, but there is a javascript error
    ```javascript
    Uncaught Error: The module '/Users/edmondwells/git/fork-electron-python-example/node_modules/zeromq/build/Release/zmq.node'
    was compiled against a different Node.js version using
    NODE_MODULE_VERSION 54. This version of Node.js requires
    NODE_MODULE_VERSION 57. Please try re-compiling or re-installing
    the module (for instance, using `npm rebuild` or `npm install`).
    at process.module.(anonymous function) [as dlopen] 
    ```
3. Fix it: run `./node_modules/.bin/electron-rebuild`
4. The javascript error is gone!

## Packaging
### Python part
```shell script
pyinstaller pycalc/api.py --distpath pycalcdist
rm -rf build/
rm -rf api.spec
```
### Node.js/Electron part
```shell script
./node_modules/.bin/electron-packager . --overwrite --ignore="pycalc$" --ignore="\.venv" --ignore="old-post-backup"
```

