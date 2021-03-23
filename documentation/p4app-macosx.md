---
layout: page
title: Running p4app on Mac OS X
---

* **Install [Vagrant](https://www.vagrantup.com) and [VirtualBox](https://www.virtualbox.org/).**


* **Install homebrew:**

```
xcode-select --install
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```


* **Install docker, docker-toolbox, and docker-machine:**

```
brew install --cask docker
brew install docker-toolbox
brew install docker-machine docker
```

* **Install git:**

```
brew install git
```

* **Clone the p4app github repo:**

```
git clone https://github.com/2021-cs344/p4app.git
```


* **Make the p4app command available in your PATH:**

```
ln -s <PATH_TO_P4APP_REPO>/p4app/p4app /usr/local/bin/p4app
```

* **Launch the docker quickstart terminal:**

```
open -a Docker\ Quickstart\ Terminal -j
```

* **Run program through p4app:**

```
p4app run <PROG_NAME>.p4app/
```

* **For example, run `wire.p4app`:**


```
p4app run <PATH_TO_P4APP_REPO>/p4app/examples/wire.p4app
```

