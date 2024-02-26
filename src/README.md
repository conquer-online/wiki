
![Conquer Online](images/logo.png)

# Introduction

Welcome to the Conquer Online server development and client modifications wiki. This wiki is hosted publicly using Git, published using [mdBook](https://rust-lang.github.io/mdBook/index.html), and maintained by the open source community. Pages on this wiki cover topics such as server-client message types, cryptography, client file formats, constants, system overviews, and more.

To participate in this collaborative effort to document Conquer Online development, the following rules must be followed:

* Articles must be written from a neutral point of view.
* Authors must respect each other, and not engage in personal attacks.
* Authors must not publish pirated programs.

Please read up on the code of conduct found in the root of the repository.

## Verification

Statuses are used to indicate how reliable a page is / what the source of information is. Specifically, if information has been gathered from a community source, such as a private server project, then the status should be unverified until the server is run and the behavior can be at least observed.

* 🚩 **Incomplete**: The source is unknown and the information is incomplete.
* ❓ **Unverified**: The source is unknown or cannot be verified.
* ☑️ **Assumed (Observed)**: Assumed by observing the behavior in the client.
* ☑️ **Assumed (Soul)**: Assumed by reading the leaked client source code from TQ.
* ✅ **Verified (Client)**: Confirmed by reverse engineering the client binary.
* ✅ **Verified (Server)**: Confirmed by reverse engineering the leaked server binaries.

## Sections

This wiki is broken up into multiple sections:

* [Algorithms](algorithms/README.md): Calculations made for attacks, rates, skill distances, and more.
* [Constants](constants/README.d): Hard-coded constants found in and across messages and the client.
* [Files](files/README.md): File formats and definitions for various content types.
* [Network](network/README.md): Message structures and client-server networking.
* [Renderers](renderers/README.md): System descriptions for rendering content in the client.
* [Security](security/README.md): Cryptography and security around networking and content.
* [Strings](strings/README.md): Details on strings and restrictions on inputs.
