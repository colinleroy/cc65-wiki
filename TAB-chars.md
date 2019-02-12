As mentioned on the other pages ([[C and Assembly sources style-guide]], [[LinuxDoc sources style-guide]]), TAB chars are undesirable.

One can use this command to check for stray TAB chars in the source tree:

`find * -type f \( \( -name \*.inc -a \! -name Makefile.inc \) -o -name \*.cfg -o -name \*.c -o -name \*.s -o -name \*.h -o -name \*.asm -o -name \*.sgml \) -print | xargs grep -l $'\t'`

`bash` is required due to the `$'\t'` construct.