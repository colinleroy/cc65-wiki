On this page we collect things to be done before the next release. When something was done it is ~striked out~. After a release, the page will be whiped from all issues there were striked out (ideally all).

* move all Wiki pages that fit into Contributing.md or the Documentation
* make Contributing.md more complete
* make the github action(s) build the documentation and upload it to the webpage
* make a github action that produces a release
* come up with a good way to handle external contributions to the wiki
* fix [#1670](https://github.com/cc65/cc65/issues/1670):
    * make the compiler define some macro depending on selected standard
    * fix library headers to comply with the c-standards
* fix [#1667](https://github.com/cc65/cc65/issues/1667): the ```__CC65__``` version macro is broken
* make sure the website, wiki and .md files are all prominently cross linked
* find a way to make the documentation searchable (at least the one on the webpage)
* move the "contributions" sourceforge repository to a seperate repo on github
    * put each one into a seperate directory, do not use .zip files
    * create a github action that will pull this repo and compile all the files
* create a style rule for "indent" (or similar program(s))
* ~fix issue [#1538](https://github.com/cc65/cc65/issues/1538) - ANDing a non constant expression with a constant expression should make the size of the expression known to the assembler~
* add a .cfg to produce easyflash images
    * add a sample program that uses it, with banking routines
* add a sample that demonstrates the use of inline assembly
* add all missing undocumented opcodes to the 6502X mode
* make the build system less ambigitious (see [#1726](https://github.com/cc65/cc65/issues/1726))
    * the detected shell should not imply the target system
    * cross-compile should not imply the target system
    * it should be possible to override any autodetected behaviour
