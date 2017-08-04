These instructions provide a step-by-step guide to building and installing cc65 on Fedora Linux.

# Step 1: Install Dependencies

The following command not only installs the necessary tools to build the cc65 executable programs, it also installs all the tools to build the documentation.

    sudo dnf install git gcc make linuxdoc-tools texinfo

# Step 2: Create a Place for the Source Code

If you don't have a "git" directory, create it with the below commands. You don't need to create a ~/git/cc65 directory because that will be done automatically by git.

    cd ~
    mkdir git
    cd git

# Step 3: Retrieve the Source Code

From the ~/git directory, enter the following command to download the cc65 code from github.com. A cc65 subdirectory will automatically be created.

    git clone https://github.com/cc65/cc65.git

# Step 4: Build the Compiler from Source

The build process works flawlessly on Fedora. Simply type:

    cd cc65
    make

# Step 5: Build the Documentation

You will want to refer to the documentation. It will be quicker to access it
locally. Build it with this command:

    make doc

# Step 6: Install the Compiler

The below command installs the following:

* Executables in /usr/local/bin
* Documentation in info format in /usr/local/share/info. View it with the command: info /usr/local/share/info/index.info
* Documentation in HTML format in /usr/local/share/doc/cc65/html.

    sudo PREFIX=/usr/local make install

# Step 7: Bookmark the Documentation

To be successful working with software development tools you need quick access to the documentation. I keep a very organized set of bookmarks in my browser so that I can quickly get answers to questions that come up during development. One can waste a lot of time looking for information if it is not readily available. So I suggest creating a bookmark in your browser for the following local file which is the starting point for the cc65 documentation in HTML format.

In Firefox you can press Ctrl-O to open a file. Enter the below path. Then bookmark it with Ctrl-D.

    /usr/local/share/doc/cc65/html/index.html

