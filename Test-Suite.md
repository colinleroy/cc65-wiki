
We somehow need to make testing of the library headers for standard conformance automatic too. The tests should go into test/standard/

Standards we need to test:

* C89 (defines __CC65_STD_C89__)
* C99 (defines __CC65_STD_C99__) [ISO C99 Draft](https://www.open-std.org/jtc1/sc22/wg14/www/docs/n1256.pdf) - Annex B has the header file info
    * [This](https://www.dii.uchile.cl/~daespino/files/Iso_C_1999_definition.pdf) seems the be the actual standard pdf
* CC65 (__CC65_STD_CC65__)

https://en.cppreference.com/w/c can give some quick clues on what is available in which standard

# standards / drafts

* https://stackoverflow.com/questions/81656/where-do-i-find-the-current-c-or-c-standard-documents
* https://www.open-std.org/jtc1/sc22/wg14/www/projects

# other Test Suites

* [musl libc tests](https://repo.or.cz/libc-test.git)
* [Open POSIX Test suite](http://posixtest.sourceforge.net)
* [Standard C Library Test Suite](https://github.com/coreux/libstdc-tests)
* [C Test suite](https://github.com/c-testsuite/c-testsuite)
* [The glibc Test suite](https://sourceware.org/glibc/wiki/Testing/Testsuite)
* [LLVM Test Suite Guide](https://releases.llvm.org/2.1/docs/TestingGuide.html)