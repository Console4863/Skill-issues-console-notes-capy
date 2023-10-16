#hacking #forensics 
# Binwalk

[![Build Status](https://camo.githubusercontent.com/43d742de79d98c6709d11803a10884379367439897b5f2211778e05e64b70db3/68747470733a2f2f7472617669732d63692e6f72672f52654669726d4c6162732f62696e77616c6b2e7376673f6272616e63683d6d6173746572)](https://travis-ci.org/ReFirmLabs/binwalk) [![Maintenance](https://camo.githubusercontent.com/6e4da91cb02711349e6b9d0aba6a767362818c1d17891a02f06fded4415f6172/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f4d61696e7461696e65642533462d7965732d677265656e2e737667)](https://github.com/ReFirmLabs/binwalk/graphs/commit-activity) [![GitHub license](https://camo.githubusercontent.com/dc6ff5d9a31789c7cb8421be08e6c6bb2fd5d77ba36f1d377e99019b4ceddd31/68747470733a2f2f696d672e736869656c64732e696f2f6769746875622f6c6963656e73652f52654669726d4c6162732f62696e77616c6b2e737667)](https://github.com/ReFirmLabs/binwalk/blob/master/LICENSE) [![GitHub stars](https://camo.githubusercontent.com/a75f1d69cd51455cd7c9e8217012fe414b430a3310ef902564340a6018c59407/68747470733a2f2f696d672e736869656c64732e696f2f6769746875622f73746172732f6261646765732f736869656c64732e7376673f7374796c653d736f6369616c266c6162656c3d5374617273)](https://github.com/ReFirmLabs/binwalk/stargazers)

Binwalk is a fast, easy to use tool for analyzing, reverse engineering, and extracting firmware images.

### [](https://github.com/ReFirmLabs/binwalk#-extraction-security-notice-)*** Extraction Security Notice ***

Prior to Binwalk v2.3.3, extracted archives could create symlinks which point anywhere on the file system, potentially resulting in a directory traversal attack if subsequent extraction utilties blindly follow these symlinks. More generically, Binwalk makes use of many third-party extraction utilties which may have unpatched security issues; Binwalk v2.3.3 and later allows external extraction tools to be run as an unprivileged user using the `run-as` command line option (this requires Binwalk itself to be run with root privileges). Additionally, Binwalk v2.3.3 and later will refuse to perform extraction as root unless `--run-as=root` is specified.

### [](https://github.com/ReFirmLabs/binwalk#-python-27-deprecation-notice-)*** Python 2.7 Deprecation Notice ***

Even though many major Linux distros are still shipping Python 2.7 as the default interpreter in their currently stable release, we are making the difficult decision to move binwalk support exclusively to Python 3. This is likely to make many upset and others rejoice. If you need to install binwalk into a Python 2.7 environment we will be creating a tag `python27` that will be a snapshot of `master` before all of these major changes are made. Thank you for being patient with us through this transition process.

### [](https://github.com/ReFirmLabs/binwalk#installation-and-usage)Installation and Usage

-   [Installation](https://github.com/ReFirmLabs/binwalk/blob/master/INSTALL.md)
-   [API](https://github.com/ReFirmLabs/binwalk/blob/master/API.md)
-   [Supported Platforms](https://github.com/ReFirmLabs/binwalk/wiki/Supported-Platforms)
-   [Getting Started](https://github.com/ReFirmLabs/binwalk/wiki/Quick-Start-Guide)
-   [Binwalk Command Line Usage](https://github.com/ReFirmLabs/binwalk/wiki/Usage)
-   [Binwalk IDA Plugin Usage](https://github.com/ReFirmLabs/binwalk/wiki/Creating-Custom-Plugins)

More information on [Wiki](https://github.com/ReFirmLabs/binwalk/wiki)

# [](https://github.com/ReFirmLabs/binwalk#binwalk-professional-edition)Binwalk Professional Edition

After years of developing and supporting binwalk as an open source project we have finally sold out to the man and released a cloud-based firmware extraction engine called _Binwalk Enterprise_. After all someone needs to pay devttys0 so he can buy more milling equipment and feed his children (in that order). Please consider subscribing and reap the benefits of getting actual customer support for all your firmware extraction and analysis needs. Please visit [https://www.refirmlabs.com/binwalk-enterprise/](https://www.refirmlabs.com/binwalk-enterprise/) for more information.

```
binwalk --dd=.*
```