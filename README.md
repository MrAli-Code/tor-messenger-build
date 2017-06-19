Tor Messenger Build
===================

Installing build dependencies
-----------------------------

To build Tor Messenger, you need a Linux distribution that has support
for Docker (such as Debian jessie, Ubuntu 14.04, Fedora 20, etc ...).
The Docker package is usually named docker.io or docker-io.
On Debian jessie, the docker.io package is available in backports.

Your user account should have access to the docker command without using
sudo, so it should be in the docker group.

    sudo usermod -aG docker $(whoami)

The docker daemon should also be running.

The sources are downloaded using git and mercurial which need to be
installed.

You also need a few perl modules installed:

```
- YAML::XS
- File::Basename
- Getopt::Long
- Template
- IO::Handle
- IO::CaptureOutput
- File::Temp
- File::Slurp
- File::Path
- String::ShellQuote
- Sort::Versions
- Digest::SHA
- Data::UUID
- Data::Dump
```

If you are running Debian or Ubuntu, you can install them with:

```
# apt-get install libyaml-libyaml-perl libtemplate-perl \
                  libio-handle-util-perl libio-all-perl \
                  libio-captureoutput-perl libfile-slurp-perl \
                  libstring-shellquote-perl libsort-versions-perl \
                  libdigest-sha-perl libdata-uuid-perl libdata-dump-perl \
                  git mercurial
```

If you are running Fedora (24 or later), you can install them with:

```
# dnf install 'perl(YAML::XS)' 'perl(File::Basename)' 'perl(Getopt::Long)' \
              'perl(Template)' 'perl(IO::Handle)' 'perl(IO::CaptureOutput)' \
              'perl(File::Temp)' 'perl(File::Slurp)' 'perl(File::Path)' \
              'perl(String::ShellQuote)' 'perl(Sort::Versions)' \
              'perl(Digest::SHA)' 'perl(Data::UUID)' 'perl(Data::Dump)' \
              git mercurial
```

Starting a build
----------------

To start a build, simply run `make all` in the directory to build all
currently supported architectures.

If you want to build only one architecture, you can run something like
`make tor-messenger-linux-x86_64`.

The resulting builds are stored in the out/tor-messenger directory.

You can also run `make tor-messenger-release` to build it for all
architectures, rename files to their final name and generate an
sha256sums.txt file in the directory release/$version.


Updating git and hg sources
---------------------------

You can run `make fetch` to fetch the latest sources from git and
mercurial for all components included in Tor Messenger.


Cleaning obsolete files and containers images
---------------------------------------------

To clean obsolete files and containers images, you can run `make clean-old`.

This command will remove any intermediate build files and containers
that are no longer used in the current builds. Because it needs to
compute the filename of all current files, this command takes a lot of
time to run.

