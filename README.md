# Readme
This project is a copy of taku910/mecab, fix the compile issue and you can compile it by cmake now.
This project is used for C++ project, you can load local dict by C++ interface and no need to install mecab on your computer.
The dict relate files are in the folder 'mecab-ipadic'.

## How to build
```
mkdir build
cd build
cmake ..
make -j8
make DESTDIR="/path/to/install" install
``` 