clog
====

[![Join the chat at https://gitter.im/thoughtram/clog](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/thoughtram/clog?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

[![Build Status](https://travis-ci.org/thoughtram/clog.png?branch=master)](https://travis-ci.org/thoughtram/clog)

A [conventional][convention] changelog for the rest of us

[convention]: https://github.com/ajoslin/conventional-changelog/blob/a5505865ff3dd710cf757f50530e73ef0ca641da/conventions/angular.md

## About

`clog` creates a changelog automatically from your local git metadata. See the `clog`s [changelog.md](https://github.com/thoughtram/clog/blob/master/changelog.md) for an example.

The way this works, is every time you make a commit, you ensure your commit subject line follows the [conventional](https://github.com/thoughtram/clog/blob/master/changelog.md) format. Then when you wish to update your changelog, you simply run `clog` inside your local repository with any options you'd like to specify.

*NOTE:* `clog` also supports empty components by making commit messages such as `alias: message` or `alias(): message` (i.e. without the component)


## Usage

There are two ways to use `clog`, as a binary via the command line or as a library in your applicaitons.

### Binary (Command Line)

In order to use `clog` via the command line you must first obtain a binary by either compiling it yourself, or downlading and installing one of the precompiled binaries.

#### Compiling

Follow these instructions to compile `clog`, then skip down to Installation.

 1. Ensure you have current version of `cargo` and [Rust](https://www.rust-lang.org) installed
 2. Clone the project `$ git clone https://github.com/thoughtram/clog && cd clog`
 3. Build the project `$ cargo build --release`
 4. Once complete, the binary will be located at `target/release/clog`

#### Using a Precompiled Binary

There are several precompiled binaries readily availbe. Browse to http://wod.twentyfives.net/bin/clog/ and download the latest binary for your particular OS. Once you download and extract the tar file (or zip for Windows), the binary will be located at `bin/clog`

#### Installation

Once you have downloaded, or compiled, `clog` you simply need to place the binary somewhere in your `$PATH`. If you are not familiar with `$PATH` read-on; otherwise skip down to Using clog.

##### Arch Linux

You can use `clog-bin` from the AUR, or follow the instructions for Linux / OS X

##### Linux / OS X

You have two options, place `clog` into a directory that is already located in your `$PATH` variable (To see which directories those are, open a terminal and type `echo "${PATH//:/\n}"`, the quotation marks are important), or you can add a custom directory to your `$PATH`

**Option 1**
If you have write permission to a directory listed in your `$PATH` or you have root permission (or via `sudo`), simply copy the `clog` to that directory `# sudo cp clog /usr/local/bin`

**Option 2**
If you do not have root, `sudo`, or write permission to any directory already in `$PATH` you can create a directory inside your home directory, and add that. Many people use `$HOME/.bin` to keep it hidden (and not clutter your home directory), or `$HOME/bin` if you want it to be always visible. Here is an example to make the directory, add it to `$PATH`, and copy `clog` there.

Simply change `bin` to whatever you'd like to name the directory, and `.bashrc` to whatever your shell startup file is (usually `.bashrc`, `.bash_profile`, or `.zshrc`)

```sh
$ mkdir ~/bin
$ echo "export PATH=$PATH:$HOME/bin" >> ~/.bashrc
$ cp clog ~/bin
$ source ~/.bashrc
```

##### Windows

On Windows 7/8 you can add directory to the `PATH` variable by opening a command line as an administrator and running

```
C:\> setx path "%path%;C:\path\to\clog\binary"
```
Otherwise, ensure you have the `clog` binary in the directory which you operating in the command line from, because Windows automatically adds your current directory to PATH (i.e. if you open a command line to `C:\my_project\` to use `clog` ensure `clog.exe` is inside that directory as well).

#### Using clog from the Command Line

`clog` works by reading your `git` metadata and specially crafted commit messages and subjects to create a changelog. `clog` has the following options availble.

```sh
USAGE:
    clog [FLAGS] [OPTIONS]

FLAGS:
    -F, --from-latest-tag    use latest tag as start (instead of --from)
    -h, --help               Prints help information
    -M, --major              Increment major version by one (Sets minor and patch to 0)
    -m, --minor              Increment minor version by one (Sets patch to 0)
    -p, --patch              Increment patch version by one
    -V, --version            Prints version information

OPTIONS:
    -c, --config <config>            The Clog Configuration TOML file to use (Defaults to '.clog.toml')**
    -f, --from <from>                e.g. 12a8546
    -g, --git-dir <gitdir>           Local .git directory (defaults to current dir + '.git')*
    -o, --outfile <outfile>          Where to write the changelog (Defaults to 'changelog.md')
    -r, --repository <repo>          Repo used for link generation (without the .git, e.g. https://github.com/thoughtram/clog)
    -l, --link-style <style>         The style of repository link to generate (Defaults to github) [values: Github, Gitlab, Stash]
    -s, --subtitle <subtitle>        e.g. "Crazy Release Title"
    -t, --to <to>                    e.g. 8057684 (Defaults to HEAD when omitted)
        --setversion <ver>           e.g. 1.0.1
    -w, --work-tree <workdir>        Local working tree of the git project (defaults to current dir)*

* If your .git directory is a child of your project directory (most common, such as
/myproject/.git) AND not in the current working directory (i.e you need to use --work-tree or
--git-dir) you only need to specify either the --work-tree (i.e. /myproject) OR --git-dir (i.e. 
/myproject/.git), you don't need to use both.

** If using the --config to specify a clog configuration TOML file NOT in the current working
directory (meaning you need to use --work-tree or --git-dir) AND the TOML file is inside your
project directory (i.e. /myproject/.clog.toml) you do not need to use --work-tree or --git-dir.
```

#### Try it!

In order to see it in action, you'll need a repository that already has some of those specially crafted commit messages in it's history. For this, we'll use the `clog` repository itself.

1. Clone the repo `git clone https://github.com/thoughtram/clog && cd clog`

2. Ensure you already `clog` binary from any of the steps above

3. Delete the old changelog file `rm changelog.md` (so that you can see what a fresh one looks like)

4. Run clog `clog -r https://github.com/thoughtram/clog --setversion 0.1.0 --subtitle "Crazy Dog" --from 6d8183f`

5. Open `changelog.md` in your favorite markdown viewer

### As a Library

See the documentation for information on using `clog` in your applications.

#### Try it!

In order to see it in action, you'll need a repository that already has some of those specially crafted commit messages in it's history. For this, we'll use the `clog` repository itself.

 1. Clone the `clog` repository (we will clone to our home directory to make things simple, feel free to change it)

```
$ git clone https://github.com/thoughtram/clog ~/clog
```

 2. Add `clog` as a dependency in your `Cargo.toml` 

```toml
[dependencies]
clog = "*"
```

 3. Use the following in your `src/main.rs`

```rust
extern crate clog;

use clog::Clog;

fn main() {
    // Create the struct
    let mut clog = Clog::with_dir("~/clog").unwrap_or_else(|e| { 
        println!("{}",e); 
        std::process::exit(1); 
    });

    // Set some options
    clog.repository("https://github.com/thoughtram/clog")
        .subtitle("Crazy Dog")
        .from("6d8183f")
        .version("0.1.0");

    // Write the changelog to the current working directory
    //
    // Alternatively we could have used .write_changelog_to("/somedir/some_file.md")
    clog.write_changelog();
}
```

 4. Compile and run `$ cargo build --release && ./target/release/bin_name
 5. View the output in your favorite markdown viewer! `$ vim changelog.md`

### Default Options

`clog` can also be configured using a default configuration file so that you don't have to specify all the options each time you want to update your changelog. To do this add a `.clog.toml` file to your repository.

```toml
[clog]
repository = "https://github.com/thoughtram/clog"
subtitle = "my awesome title"

# specify the style of commit links to generate, defaults to "github" if omitted
link-style = "github"

# sets the changelog output file, defaults to "changelog.md" if omitted
outfile = "MyChangelog.md"

# If you use tags, you can set the following if you wish to only pick
# up changes since your latest tag
from-latest-tag = true
```

Now you can update your `MyChangelog.md` with `clog --patch` (assuming you want to update from the latest tag version, and increment your patch version by 1).

*Note:* Any options you specify at the command line will override options set in your `.clog.toml`

### Custom Sections

By default, `clog` will display two sections in your changelog, `Features` and `Bug Fixes`. You can add additional sections by using a `.clog.toml` file. To add more sections, simply add a `[sections]` table, along with the section name and aliases you'd like to use in your commit messages:

```toml
[sections]
MySection = ["mysec", "ms"]
```

Now if you make a commit message such as `mysec(Component): some message` or `ms(Component): some message` there will be a new "MySection" section along side the "Features" and "Bug Fixes" areas.

*NOTE:* Sections with spaces are suppported, such as `"My Special Section" = ["ms", "mysec"]`

## Companion Projects

- [Commitizen](http://commitizen.github.io/cz-cli/) - A command line tool that helps you writing better commit messages.

## LICENSE

clog is licensed under the MIT Open Source license. For more information, see the LICENSE file in this repository.
