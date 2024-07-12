
![Conquer Online](src/images/logo.png)

> The __live wiki__ can be found here: https://conquer-online.github.io/wiki/

# Introduction

Welcome to the Conquer Online server development and client modifications wiki. This wiki is hosted publicly using Git, published using [mdBook](https://rust-lang.github.io/mdBook/index.html), and maintained by the open source community. Pages on this wiki cover topics such as server-client message types, cryptography, client file formats, constants, system overviews, and more.

To participate in this collaborative effort to document Conquer Online development, the following rules must be followed:

* Articles must be written from a neutral point of view.
* Authors must respect each other, and not engage in personal attacks.
* Authors must not publish pirated programs.

Please read up on the [code of conduct](CODE_OF_CONDUCT.md).

## Getting Started

To get started, fork this repository. It's recommended that you work in private branches on your fork, rebase with upstream branches, and submit pull requests for edits.

You can write pages using private branches and one of the following methods:

1. Open the file in GitHub and make an edit. Save your edit to a new or existing branch.
2. Open the repo in Visual Studio and make edits. Push your branch to your origin.

If you'd like to run the wiki locally (rather than just preview the markdown), then you can install [Rust](https://www.rust-lang.org/) and run the following command:

```
mdbook serve
```
By default, you should then be able to browse the wiki at http://localhost:3000. 

## Publishing Updates

Once a pull request has been reviewed and merged into `main`, then you should see your change kick off a new pipeline for deploying the updated wiki pages. It may take several minutes before your change is live.
