These instructions provide a step-by-step guide for installing cc65 on the distributions that are supoorted by the [https://fedoraproject.org/wiki/EPEL/FAQ Fedora EPEL repository].

== Step 1: Enable the Fedora EPEL repository ==

To enable Fedora EPEL for your distribution, please refer to the [https://fedoraproject.org/wiki/EPEL Quickstart Guide for Fedora EPEL].

After enabling Fedora EPEL, it is recommended to update the repository cache of the package manager.

<pre>
sudo yum makecache
</pre>

== Step 2: Install cc65 ==

The following command installs the cc65 executable programs, on some distributions it may also install the documentation and additional utilities as weak dependencies.

<pre>
sudo yum install cc65
</pre>

== Step 3: Optional packages ==

There are additional pre-built packages, that can be installed without dependencies on the cc65 compiler:

The following command installs the documentation (html and GNU/info) for the cc65 compiler.

<pre>
sudo yum install cc65-doc
</pre>

To install the additional utilities, which are shipped in the [https://github.com/cc65/cc65/tree/master/util util directory of the git repository], simply use this command.

<pre>
sudo yum install cc65-utils
</pre>

Those utilities programs are:

* /usr/bin/ataricvt65
** Conversion between Atari and ISO-8859-1 character set.
* /usr/bin/ca65html
** Convert a ca65 source into HTML
* /usr/bin/cbmcvt65
** Conversion between PetSCII and ISO-8859-1 character set.
* /usr/bin/deflater65
** Compresses data to the DEFLATE format. The compressed data is ready to use with the inflatemem() routine from cc65's zlib.
* /usr/bin/gamate-fixcart65
** Adds a checksum to a Gamate Cartridge ROM image.

== Step 4: Bookmark the Documentation ==

To be successful working with software development tools you need quick access to the documentation. I keep a very organized set of bookmarks in my browser so that I can quickly get answers to questions that come up during development. One can waste a lot of time looking for information if it is not readily available. So I suggest creating a bookmark in your browser for the following local file which is the starting point for the cc65 documentation in HTML format.

In Firefox you can press Ctrl-O to open a file. Enter the below path. Then bookmark it with Ctrl-D.

<pre>
/usr/share/doc/cc65-$CC65VERSION/html/index.html
</pre>

Please be aware, that the path to those documentation files also includes the version of the cc65 compiler. You may need to adjust it to the actual version installed on your system.