<!-- PROJECT SHIELDS -->
<!--
*** I'm using markdown "reference style" links for readability.
*** Reference links are enclosed in brackets [ ] instead of parentheses ( ).
*** See the bottom of this document for the declaration of the reference variables
*** for contributors-url, forks-url, etc. This is an optional, concise syntax you may use.
*** https://www.markdownguide.org/basic-syntax/#reference-style-links
-->
[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![MIT License][license-shield]][license-url]
[![LinkedIn][linkedin-shield]][linkedin-url]



<!-- PROJECT TITLE -->
# git-diff-explorer

A CLI git diff explorer written in bash that utilizes fzf.



<!-- TABLE OF CONTENTS -->
<details open="open">
  <summary><h2 style="display: inline-block">Table of Contents</h2></summary>
  <ol>
    <li><a href="#about-the-project">About The Project</a></li>
    <li><a href="#prerequisites">Prerequisites</a></li>
    <li><a href="#installation">Installation</a></li>
    <li><a href="#usage">Usage</a></li>
    <ol>
      <li><a href="#examples">Examples</a></li>
    </ol>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
  </ol>
</details>



<!-- ABOUT THE PROJECT -->
## About The Project

There is a single file: [git_diff_explorer.sh](git_diff_explorer.sh). It can be executed directly or it can be sourced to add the `git_diff_explorer` function to your environment.

The `git_diff_explorer` takes in any arguments you'd provide to a `git diff` command. It runs the `git diff` command using `--compact-summary` and displays the output in `fzf` in a bottom, selection area. The diff of the highlighed file is shown in an upper, larger area. If lines are selected, their filenames are printed upon exit.

![git_diff_explorer example screenshot](/images/git_diff_explorer_example.png)



<!-- PREREQUISITES -->
## Prerequisites
You must have the following utilities available:
1.  [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) - Git is a free and open source distributed version control system.
1.  [fzf](https://github.com/junegunn/fzf) - fzf is a general-purpose command-line fuzzy finder.

See each project for installation instructions.



<!-- GETTING STARTED -->
## Installation

1. Download [git_diff_explorer.sh](git_diff_explorer.sh).
2. Do one of the following:
   * Copy it to a directory in your `PATH`.
   * Update your enviroment initialization scripts (e.g. `.bash_profile` or `.zshrc`) to `source` the file.



<!-- USAGE EXAMPLES -->
## Usage

This command:
```sh
> git_diff_explorer tag-v0.45.4..tag-v0.46.0
```
lead to this screenshot:
![git_diff_explorer example screenshot](/images/git_diff_explorer_example.png)
And this output:
```sh
codec/legacy/codec.go
codec/proto_codec.go
codec/legacy/doc.go
```

A `--commit <hash>` option is also available to get the diff of a single commit. It is transformed into the arguments `<hash>~` `<hash>`.

Output can be controlled with a few custom options too:
* `--output-type <output type>` - This only affects moved files.
  `<output type>` can be one of the following:
  * `old` - only the old filename (of selected lines) is printed.
  * `new` - only the new filename (of selected lines) is printed.
  * `combined` - output the combined old => new entry (from the compact summary) of selected lines.
  * `both` - output the old file on one line, then the new file on another (of selected lines).
  The default is `combined`.
* `--printd <delimiter>` - Use the provided delimiter between each selection's output.
  The default is `\n`.
* `--print0` - Use a null byte as the delimiter. This is the same as `--printd \0`.
  This is handy when there are spaces in the name and you are piping the output to `xargs -0`.

All other arguments are provided to the `git diff` commands.

There is also `--help` available.

### Examples

Explore the differences between main and your current branch:
```sh
> git_diff_explorer main
```

Explore the differences between two branches:
```sh
> git_diff_explorer branch1 branch2
```

Explore your unstaged changes and stage the files you select:
```sh
> git_diff_explorer --print0 | xargs -0 git add
```

Explore the changes from a single commit:
```sh
> git_diff_explorer --commit 01ab23cd4
```

Explore a word diff from a single commit:
```sh
> git_diff_explorer --commit 01ab23cd4 --word-diff=color --word-diff-regex=[[:alnum:]]+'
```


<!-- CONTRIBUTING -->
## Contributing

Contributions are what make the open source community such an amazing place to be learn, inspire, and create. Any contributions you make are **greatly appreciated**.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

If you `export DEBUG=1`, some debug information will be printed when you run `git_diff_explorer`.



<!-- LICENSE -->
## License

Distributed under the MIT License. See [LICENSE](/LICENSE) for more information.



<!-- CONTACT -->
## Contact

Daniel Wedul - [@dannywedul](https://twitter.com/dannywedul) - gitdiffexplorer@wedul.com

Project Link: [https://github.com/SpicyLemon/git-diff-explorer](https://github.com/SpicyLemon/git-diff-explorer)



<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/SpicyLemon/git-diff-explorer.svg?style=for-the-badge
[contributors-url]: https://github.com/SpicyLemon/git-diff-explorer/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/SpicyLemon/git-diff-explorer.svg?style=for-the-badge
[forks-url]: https://github.com/SpicyLemon/git-diff-explorer/network/members
[stars-shield]: https://img.shields.io/github/stars/SpicyLemon/git-diff-explorer.svg?style=for-the-badge
[stars-url]: https://github.com/SpicyLemon/git-diff-explorer/stargazers
[issues-shield]: https://img.shields.io/github/issues/SpicyLemon/git-diff-explorer.svg?style=for-the-badge
[issues-url]: https://github.com/SpicyLemon/git-diff-explorer/issues
[license-shield]: https://img.shields.io/github/license/SpicyLemon/git-diff-explorer.svg?style=for-the-badge
[license-url]: https://github.com/SpicyLemon/git-diff-explorer/blob/master/LICENSE
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://www.linkedin.com/in/danny-wedul/
