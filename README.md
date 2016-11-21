# git-check-invalid-patterns

Checks for invalid patterns in your commit

While writing code, you often end up with a debug statetements strewn throughout
your code. We often clean these up before we create a commit. However, tracking
these manually does not always work.

This script creates a `pre-commit` hook and checks for the patterns in your `.invalid_patterns`
file. If there are any of those patterns in your commit, it will abort the commit.

## Usage

### Install
Copy the script to your `bin` directory(any directory in your `$PATH`).
```sh
curl -s https://raw.githubusercontent.com/minhajuddin/git_invalid_patterns/master/git-check-invalid-patterns \
  -o ~/bin/git-check-invalid-patterns
chmod +x ~/bin/git-check-invalid-patterns
```

### Setup
This script works as a pre-commit hook in your git repo. To set it up, run:

```sh
cd your-git-repository-dir
git check-invalid-patterns init
```

The above step should have created an `.invalid_patterns` file. You can tweak
this file to your needs. The patterns should be listed one per line.

e.g.
```
# .invalid_patterns
# rows starting with "#" are ignored, empty lines are ignored

# rows starting with a backslash are considered to be exact matches
IO.inspect

# other patterns are used as PCRE regexes
debugger

# other patterns are used as PCRE regexes
IEx.pry
```

### Ad hoc use

You can even run this script just by calling it from the terminal, when you do
this it checks for invalid patterns in your staged area
```sh
git check-invalid-patterns
```

### Run as part of your CI build

You can also run it as part of your CI build by passing it the old and new revision's commit ids

```sh
# your build script
set -e
git check-invalid-patterns $oldrev $newrev
```
