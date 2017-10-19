RIO Development Environment Setup Guide
=======================================

{markdown}\
This document will be moved to comcast.github.com soon. As it should be
md file, the syntax is quite different with Jira wiki page. Thanks for
understanding.

\# How to Set up Dev Environment at MacBook\
\
\#\# Development Tools\
The RIO engineering team has standardized on the following development
tools:\
\* Mac OS X (primary development platform)\
\* Xcode (has libraries and editors that are useful for development also
required for Homebrew.)\
\* Go SDK (programming language)\
\* Homebrew (installation manager for installing products)\
\* wget (used by some scripts)\
\* git (version control)\
\* Canticle (Dependency manager of go)\
\* Docker (Software container platform)\
\* IntelliJ IDEA (integrated development environment )\
\
\
The instructions for installing these tools are described below.\
\
\#\# Mac OS X\
The standard development platform used by the engineering team is Mac OS
X, although the production environment is Linux-based (either Ubuntu or
Red-hat). The installation instructions provided here assume Mac OS X,
but a Linux environment will have similar dependencies.\
\
\#\# Xcode\
Launch the App Store on your computer to find Xcode application. It is
free but you may have to have an apple ID set up. Mac OS X does not come
natively with a compiler installed.\
Once you have downloaded Xcode you will want to run it once goto
Preferences -&gt; Downloads and install the Command Line tools.\
This is incredible important for Homebrew (see below)\
Download and install Xcode from https://developer.apple.com/xcode/ or
find it on the app store.\
\
\#\# wget\
wget is simple tool used to retrieve tools from the web. This tool is
used by some of our scripts to retrieve snapshots from nexus.\
\`\`\`\`\
brew install wget\
\`\`\`\`\
![](media/image1.jpg){width="6.5in" height="5.202083333333333in"}\
\
\#\# git\
The version control system is a set of git repositories hosted by
github.\
\`\`\`\`\
brew install git\
\`\`\`\`\
You'll need a github login to access the RIO repositories; sign up
\[here\](https://github.com/).\
After you have a github login, you can be added to the organization
\*\*rio-cdvr\*\*. ( Contact Jiang Xu).\
SourceTree from Atlassian, and Xcode's FileMerge from Apple are highly
recommended tools for managing git access visually.\
\* Download and install SourceTree from http://www.sourcetreeapp.com/\
\
Once Xcode is installed, SourceTree will allow you to perform conflict
resolution with it.\
\
\#\# GitHub SSH\
We use SSH for some of our repositories access.\
You should set it up by following these instructions:
\[https://help.github.com/articles/connecting-to-github-with-ssh/\]\
\
Here is an example of using SSH config file to manage ssh keys:\
If you have already had any ssh key pair, you can ignore this step. Or
you need use "ssh-keygen" to generate ssh key pair.\
\
For Blu team, the SSH key for bitbucket can be reused for github. And no
need to generate another SSH key pair.\
\
Once you have the ssh key pair, you can copy the key content as below,
then paste it to \[https://github.com/settings/keys\].\
\`\`\`\`\
COTNPL-3W3G8WM:.ssh qdai200\$ cat \~/.ssh/config\
Host \*\
AddKeysToAgent yes\
UseKeychain yes\
IdentityFile \~/.ssh/id\_rsa\
\
COTNPL-3W3G8WM:viper-cog qdai200\$ cat \~/.ssh/id\_rsa.pub\
ssh-rsa
AAAAB3NzaC1yc2EAAAADAQABAAABAQDfj90KxqWAFNsLx5t1F/QnzUE2eKFbXS5Sg8M+ykGlpZwWj9nKFm9exFYMP6h6uowoTbwJUc3uewubVx8ciWAr4t6PY9riuvUdLhZIyf8R0f622be1Qe4uLxiGKUiZcnDEWc1bqW1dOFTvxB1lz6g5M0cVMlWG62juFLJY2JXmomXrCHSq5IQhFLpygRvAHooaOwq0D54Vk2ghV70r2hI2jJstf3zkp4M1DBXuLvcOJ1a3B9BSfgnIkM9jAojLVMXanU+B1Na+dFId2ZLcVjq6YfyKgO9Pa5ylwbkuXXhh0hpY4w77WnL4FnOcP3bnx7j37zdWcUG1vQ9CcYtEwE69
qdai200@COTNPL-3W3G8WM\
\
COTNPL-3W3G8WM:viper-cog qdai200\$ pbcopy &lt; \~/.ssh/id\_rsa.pub\
\
\`\`\`\`\
Git clone example:\
\`\`\`\`\
git clone git@github.com:rio-cdvr/rio-workspace\
Cloning into 'rio-workspace'...\
remote: Counting objects: 23971, done.\
remote: Compressing objects: 100% (50/50), done.\
remote: Total 23971 (delta 82), reused 79 (delta 56), pack-reused 23862\
Receiving objects: 100% (23971/23971), 6.73 MiB | 7.84 MiB/s, done.\
Resolving deltas: 100% (17809/17809), done.\
\`\`\`\`\
If you cannot download the git repository well, please refer to \[common
SSH
Problems\](https://help.github.com/categories/authenticating-to-github/)\
\
\
\#\# Docker\
Docker allows you to package an application with all of its dependencies
into a standardized unit for software development.\
Install the Docker Toolbox. It is available from
https://www.docker.com/products/docker-toolbox.\
Installation instructions are located at
\[https://docs.docker.com/mac\].\
You can install Docker 1.11 simply by brew install.\
\`\`\`\`\
brew install docker@1.11\
\`\`\`\`\
\
\#\# Docker Registry Login\
RIO uses docker hub for most images.\
You'll need a docker hub login to access the RIO Registry; sign up
\[here\](https://hub.docker.com/).\
After you have a docker hub login, you can be added to the organization
\*\*riocdvr\*\*. ( Contact Jiang Xu).\
\`\`\`\`\
docker login\
Login with your Docker ID to push and pull images from Docker Hub. If
you don't have a Docker ID, head over to https://hub.docker.com to
create one.\
Username: qiaoshengdai\
Password:\
Login Succeeded\
\`\`\`\`\
If you haven't been added to the organization riocdvr, you cannot pull
rio images. For example:\
\`\`\`\`\
docker pull docker.io/riocdvr/golang-build:1.8\
Error response from daemon: repository riocdvr/golang-build not found:
does not exist or no pull access\
\
\`\`\`\`\
Once you are in the riocdvr, you can pull images. For example:\
\`\`\`\`\
docker pull docker.io/riocdvr/golang-build:1.8\
1.8: Pulling from riocdvr/golang-build\
6d827a3ef358: Downloading \[=======&gt; \] 7.863MB/51.44MB\
2726297beaf1: Downloading \[===================================&gt;\
\
\`\`\`\`\
\
\
\
\#\# GO SDK\
RIO projects are GO-based. Currently a GO sdk version 1.8.3 is
required.\
You can download the Go binary lease from
\[https://golang.org/dl/\](https://golang.org/dl/). Extract the archive
package file\
into /usr/local, creating a Go tree in /usr/local/go.\
\
\
\`\`\`\`\
wget https://storage.googleapis.com/golang/go1.8.3.darwin-amd64.tar.gz\
sudo tar -C /usr/local -xzf go1.8.3.darwin-amd64.tar.gz\
COTNPL-3W3G8WM:viper-cog qdai200\$ tree /usr/local/go -L 1 -d\
/usr/local/go\
├── api\
├── bin\
├── blog\
├── doc\
├── lib\
├── misc\
├── pkg\
├── src\
└── test\
\
9 directories\
\`\`\`\`\
\
Also it's possible to use brew to install go with specified version 1.8,
it's still highly recommended to install Go with archive package.\
\
\`\`\`\
brew install go@1.8\
\`\`\`\
\
Add /usr/local/go/bin to the PATH environment variable. You can do this
by adding this line to your /etc/profile (for a system-wide
installation) or \$HOME/.profile:\
\
\`\`\`\`\
export GOROOT=/usr/local/go\
export PATH=\$PATH:\$GOROOT/bin\
\
\`\`\`\`\
\
\
Verify the Go installation version:\
\`\`\`\`\
qdai200\$ go version\
go version go1.8.3 darwin/amd64\
\`\`\`\`\
You can also \[test your
installation\](https://golang.org/doc/install\#testing) now.\
\
\#\# Setting Go Env\
\#\#\#\# Set GOPATH\
The GOPATH environment variable specifies the location of your
workspace. If no GOPATH is set, it is assumed to be \$HOME/go.\
\
RIO need use a customer location as workspace. Please set the GOPATH
environment variable as "/go"".\
Create directory go. Then change the owner to current user, if the user
is not root.\
\
\
\`\`\`\`\
sudo mkdir -p /go/bin\
\
sudo chown -R qdai200 /go\
\`\`\`\`\
Edit your "\~/.bash\_profile" to add the following line:\
\`\`\`\`\
export GOPATH=/go\
\`\`\`\`\
\#\#\#\# Add GoPath to Docker Directory\
Share the “/go” directory to Docker, or Docker cannot access “/go”.
Please follow steps\
\* click the Docker button on your MacOS right-top bar, such as:
!\[docker\](./pic/dockericon.png)\
\* click “Preference” in the drop-down menu list\
\* select “File Sharing” in the pop-out panel\
\* Click bittom "+" to add directory “/go” to the directory list\
\* Click button “Apply Restart”\
\
\#\# Pull RIO Repositories by Canticle\
\[Canticle\](https://github.com/Comcast/Canticle) is a dependency
manager for go. But, Canticle is also so much more. It's for version
locking libraries, single projects, and entire continuously-released,
microservice platforms. It's also for vendoring internally, without
import path rewriting.\
\
You can install it manually by below command. But you need build it from
rio own repository.\
\`\`\`\`\
curl -fsSL
https://raw.githubusercontent.com/Comcast/Canticle/master/install.sh |
sh\
\`\`\`\`\
\
1. You need get some dependencies manually:\
\`\`\`\`\
go get golang.org/x/tools/go/vcs\
go get github.com/prometheus/client\_golang/prometheus\
go get golang.org/x/net/context\
go get github.com/go-sql-driver/mysql\
\`\`\`\`\
2. Then download the rio-workspace:\
\
\`\`\`\`\
mkdir -p /go/src/github.comcast.com/viper-cog/\
cd /go/src/github.comcast.com/viper-cog/\
git clone git@github.com:rio-cdvr/cant\
\`\`\`\`\
\
3. Build Canticle\
\`\`\`\`\
cd cant\
git checkout cant2.0\
go build -o cant2 && ./cant2 genversion && go build -o cant2\
cp cant2 \$GOPATH/bin\
\`\`\`\`\
\
4. Add bin to your profile "\~/.bash\_profile"\
\`\`\`\`\
export PATH=\$PATH:\$GOPATH/bin\
\`\`\`\`\
\
5. Update this project: cd \$GOPATH/src; cant2 get\
This will download dependencies based on Canticle file
"rio-workspace/src/Canticle"\
\
6. Pull some other repositories manually:\
\`\`\`\`\
git clone git@github.com:rio-cdvr/rio-metadata-model\
git clone git@github.com:rio-cdvr/goutil\
git clone git@github.com:rio-cdvr/clog\
git clone git@github.com:rio-cdvr/libdash\
\`\`\`\`\
\
\#\# IDE\
A couple of IDE are acceptable: IntellIJ, Gogland, Visual Studio,
Eclipse and VIM with plugin.\
\#\#\#\# IntellIJ\
Plugin "Go" is required for Go development. You can install the Go
plugin through menu: File-&gt;Preferences-&gt;Plugins\
\
After the Go Plugin is installed, you need check/configure the GOROOT
and GOPATH by menu: File-&gt;Preferences-&gt;Languages and
Frameworks-&gt;go\
\
\#\#\#\# Gogland\
\[Gogland\](https://www.jetbrains.com/go/) is a good choice with native
support of Go. However, only "an Early Build" is available, which often
crashes and costs 100% CPU.\
\
\#\#\#\# Visual Studio Code\
\[Visual Studio Code\](https://code.visualstudio.com/) is a Free and
Open Source IDE, which is no worse than commercial IntellIJ for Go
developeing.\
You can even integrate your project with Trello.\
\
\#\#\#\# VIM\
There are a bunch of VIM plugin for Go. If you are a fan of VIM, this is
a good choice.\
\
\
\#\# Build project\
Each RIO component has "build.sh", which supports parameters of
"build|test|integtest|all|docker|merge|tag|pull".\
"all" is build+test+integest.\
\
For example, let's build the component mocklp\
\`\`\`\`\
COTNPL-3W3G8WM:mocklp qdai200\$ pwd\
/go/src/github.comcast.com/viper-cog/mocklp\
COTNPL-3W3G8WM:mocklp qdai200\$\
COTNPL-3W3G8WM:mocklp qdai200\$ ./build.sh\
./build.sh \[build|test|integtest|all|docker|merge|tag|pull\]\
Where all is build+test+integest.\
Docker will build and push a docker container if the filesystem has
change to :latest\
Merge is used to merge the current branch to master, this should only be
done by jenkins. This can be forced with -f.\
Tag can be run with -force -field &lt;major|minor|patch|release&gt; to
force tag creation.\
Pull will pull the newest version of all involved docker images.\
COTNPL-3W3G8WM:mocklp qdai200\$\
COTNPL-3W3G8WM:mocklp qdai200\$ ./build.sh build\
Build Image registry.vipertv.net/viper/golang-build:1.8\
docker run -e GO\_COVERAGE=true -e BUILD\_INFO\_FILE=BuildInfo -e
INTEG\_TEST\_FLAGS=-timeout 20m --privileged=true --rm -ti -v
/var/run/docker.sock:/var/run/docker.sock -v
/go/src/github.comcast.com/viper-cog/mocklp:/app
registry.vipertv.net/viper/golang-build:1.8 build
github.comcast.com/viper-cog/mocklp\
INFO: Resolving repo for cdep
&{SourcePath:git@github.com:rio-cdvr/pborman-uuid.git
Root:github.com/pborman/uuid
Revision:cccd189d45f7ac3368a0d127efb7f4d08ae0b655 All:false}\
INFO: Resolving repo for cdep
&{SourcePath:https://github.com/prometheus/client\_golang.git
Root:github.com/prometheus/client\_golang
Revision:c5b7fccd204277076155f10851dad72b76a49317 All:false}\
INFO: Resolving repo for cdep
&{SourcePath:https://go.googlesource.com/net Root:golang.org/x/net
Revision:a8c61998a557a37435f719980da368469c10bfed All:false}\
INFO: Resolving repo for cdep
&{SourcePath:git@github.com:rio-cdvr/rio-metadata-model.git
Root:github.comcast.com/viper-cog/rio-metadata-model Revision:master
All:false}\
INFO: Resolving repo for cdep
&{SourcePath:git@github.com:rio-cdvr/goutil.git
Root:github.comcast.com/viper-cog/goutil Revision:master All:false}\
INFO: Resolving repo for cdep
&{SourcePath:git@github.com:rio-cdvr/clog.git
Root:github.comcast.com/viper-cog/clog Revision:master All:false}\
INFO: Resolving repo for cdep
&{SourcePath:git@github.com:rio-cdvr/libdash.git
Root:github.comcast.com/viper-cog/libdash Revision:master All:false}\
INFO: Resolving repo for cdep
&{SourcePath:https://github.com/beorn7/perks
Root:github.com/beorn7/perks
Revision:4c0e84591b9aa9e6dcfdf3e020114cd81f89d5f9 All:false}\
INFO: Resolving repo for cdep
&{SourcePath:https://github.com/golang/protobuf
Root:github.com/golang/protobuf
Revision:ab9f9a6dab164b7d1246e0e688b0ab7b94d8553e All:false}\
INFO: Resolving repo for cdep
&{SourcePath:https://github.com/matttproud/golang\_protobuf\_extensions
Root:github.com/matttproud/golang\_protobuf\_extensions
Revision:c12348ce28de40eed0136aa2b644d0ee0650e56c All:false}\
INFO: Fetching cdep &{SourcePath:https://github.com/beorn7/perks
Root:github.com/beorn7/perks
Revision:4c0e84591b9aa9e6dcfdf3e020114cd81f89d5f9 All:false}\
INFO: Fetching cdep
&{SourcePath:https://github.com/matttproud/golang\_protobuf\_extensions
Root:github.com/matttproud/golang\_protobuf\_extensions
Revision:c12348ce28de40eed0136aa2b644d0ee0650e56c All:false}\
INFO: Fetching cdep
&{SourcePath:https://github.com/prometheus/client\_golang.git
Root:github.com/prometheus/client\_golang
Revision:c5b7fccd204277076155f10851dad72b76a49317 All:false}\
INFO: Fetching cdep &{SourcePath:https://github.com/golang/protobuf
Root:github.com/golang/protobuf
Revision:ab9f9a6dab164b7d1246e0e688b0ab7b94d8553e All:false}\
INFO: Fetching cdep &{SourcePath:https://go.googlesource.com/net
Root:golang.org/x/net Revision:a8c61998a557a37435f719980da368469c10bfed
All:false}\
INFO: Fetching cdep &{SourcePath:git@github.com:rio-cdvr/clog.git
Root:github.comcast.com/viper-cog/clog Revision:master All:false}\
INFO: Fetching cdep &{SourcePath:git@github.com:rio-cdvr/libdash.git
Root:github.comcast.com/viper-cog/libdash Revision:master All:false}\
INFO: Fetching cdep
&{SourcePath:git@github.com:rio-cdvr/pborman-uuid.git
Root:github.com/pborman/uuid
Revision:cccd189d45f7ac3368a0d127efb7f4d08ae0b655 All:false}\
INFO: Fetching cdep &{SourcePath:git@github.com:rio-cdvr/goutil.git
Root:github.comcast.com/viper-cog/goutil Revision:master All:false}\
INFO: Fetching cdep
&{SourcePath:git@github.com:rio-cdvr/rio-metadata-model.git
Root:github.comcast.com/viper-cog/rio-metadata-model Revision:master
All:false}\
INFO: Resolving repo for cdep
&{SourcePath:https://github.com/prometheus/client\_model
Root:github.com/prometheus/client\_model
Revision:6f3806018612930941127f2a7c6c453ba2c527d2 All:false}\
INFO: Resolving repo for cdep
&{SourcePath:https://github.com/prometheus/common
Root:github.com/prometheus/common
Revision:61f87aac8082fa8c3c5655c7608d7478d46ac2ad All:false}\
INFO: Fetching cdep
&{SourcePath:https://github.com/prometheus/client\_model
Root:github.com/prometheus/client\_model
Revision:6f3806018612930941127f2a7c6c453ba2c527d2 All:false}\
INFO: Fetching cdep &{SourcePath:https://github.com/prometheus/common
Root:github.com/prometheus/common
Revision:61f87aac8082fa8c3c5655c7608d7478d46ac2ad All:false}\
INFO: Resolving repo for cdep
&{SourcePath:https://github.com/prometheus/procfs
Root:github.com/prometheus/procfs
Revision:e645f4e5aaa8506fc71d6edbc5c4ff02c04c46f2 All:false}\
INFO: Fetching cdep &{SourcePath:https://github.com/prometheus/procfs
Root:github.com/prometheus/procfs
Revision:e645f4e5aaa8506fc71d6edbc5c4ff02c04c46f2 All:false}\
/usr/local/bin/gobuild-functions: line 97: /app/BuildInfo: Is a
directory\
Repo: /go/src/github.comcast.com/viper-cog/mocklp\
BuildPackages: github.comcast.com/viper-cog/mocklp\
BuildFlags:\
BuildInfoFile: BuildInfo\
BUILDING
github.comcast.com/viper-cog/mocklp-----------------------------------------------------------------\
/go/src/github.comcast.com/viper-cog/mocklp
/go/src/github.comcast.com/viper-cog/mocklp /go\
\
\`\`\`\`\
\
After the build, you can get the "mocklp", which is for Linux instead of
MacOS. Let's try it at Linux.\
\`\`\`\`\
COTNPL-3W3G8WM:mocklp qdai200\$ scp -i \~/cloud.key mocklp
centos@96.118.245.238:/home/centos/test\
mocklp 100% 8199KB 8.4MB/s 00:00\
\
COTNPL-3W3G8WM:mocklp qdai200\$ scp -i \~/cloud.key seed.xml
centos@96.118.245.238:/home/centos/test\
seed.xml 100% 3899 94.8KB/s 00:00\
\
COTNPL-3W3G8WM:mocklp qdai200\$ ssh -i \~/cloud.key
centos@96.118.245.238\
Last login: Wed Oct 11 21:37:13 2017 from 10.168.141.145\
\
\[centos@qs-nginx \~\]\$ cd test/\
\[centos@qs-nginx test\]\$ chmod +x mocklp\
\
\[centos@qs-nginx test\]\$ ./mocklp\
2017-10-11 21:39:22,256Z level=INFO, s=rio, component=MockLP,
hostname=qs-nginx.openstacklocal, site=LOCAL, msg="Max Procs: 4"\
2017-10-11 21:39:22,256Z level=INFO, s=rio, component=MockLP,
hostname=qs-nginx.openstacklocal, site=LOCAL, msg="Loading seed
manifest"\
2017-10-11 21:39:22,258Z level=INFO, s=rio, component=MockLP,
hostname=qs-nginx.openstacklocal, site=LOCAL, msg="Seed availability
start time (offset = 0s)"\
2017-10-11 21:39:22,258Z level=INFO, s=rio, component=MockLP,
hostname=qs-nginx.openstacklocal, site=LOCAL, msg="Using seed time =
2016-08-14 18:54:02.502499 +0000 UTC"\
2017-10-11 21:39:22,258Z level=INFO, s=rio, component=MockLP,
hostname=qs-nginx.openstacklocal, site=LOCAL, msg="Adjusted availability
start time = 2016-08-14 18:54:02.502499 +0000 UTC"\
2017-10-11 21:39:22,258Z level=INFO, s=rio, component=MockLP,
hostname=qs-nginx.openstacklocal, site=LOCAL, msg="Calculated tick time
= 2.517333333s"\
2017-10-11 21:39:22,258Z level=INFO, s=rio, component=MockLP,
hostname=qs-nginx.openstacklocal, site=LOCAL, msg="Adjusting start time
by -5.034666666s -&gt; 2016-08-14 18:53:57.467832334 +0000 UTC"\
2017-10-11 21:39:22,258Z level=INFO, s=rio, component=MockLP,
hostname=qs-nginx.openstacklocal, site=LOCAL, msg="Advanced MPD
timeline, live point is now 2016-08-14 18:54:05.019832 +0000 UTC"\
2017-10-11 21:39:22,258Z level=INFO, s=rio, component=MockLP,
hostname=qs-nginx.openstacklocal, site=LOCAL, msg="Initializing HTTP
server on :8080"\
2017-10-11 21:39:22,258Z level=INFO, s=rio, component=MockLP,
hostname=qs-nginx.openstacklocal, site=LOCAL, msg="Mocklp running"\
2017-10-11 21:39:22,258Z level=INFO, s=rio, component=MockLP,
hostname=qs-nginx.openstacklocal, site=LOCAL, msg="Starting HTTP
server"\
\
\`\`\`\`\
{markDown}
