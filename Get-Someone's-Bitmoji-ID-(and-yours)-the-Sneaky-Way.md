> This guide was provided thanks to [@willdavidow](https://github.com/willdavidow)

In this walkthrough, you'll learn how to capture some of the data passing through the SnapChat app on your device for the purpose of extracting Bitmoji ID(s) from the Bitmoji previews that render in direct messages with your friends.

This method involves setting up a proxy on your computer and connecting to it manually from your mobile device.

This method has been tested using a MacBook Pro running Mac OS High Sierra `10.13.4` and an iPhone running iOS `11.4.1` and the most up-to-date version of the SnapChat app.

Please note, this is not a hack with malicious intent (man in the middle attack), and you're not stealing anything... you're simply intercepting data that is already passing through your phone.

## Utility Installation

In order to intercept traffic from your iPhone, you'll need to install a few things:

1. [Homebrew](https://brew.sh/) - you don't REALLY need homebrew for this, but you really should have it installed if you're anything more than a "browse the web and use email" user of a Mac.
2. [Charles Proxy](https://www.charlesproxy.com/)
3. [Ettercap](https://www.ettercap-project.org/)

### Homebrew
Homebrew is a package manager that smooths the process of installing various packages by handling compilation and related dependencies for various libraries.

### Charles Proxy

Installing Charles is easy - there are installers provided on the site. Download the one appropriate for your system, and install it.. and you're done.

### Ettercap

Open up a terminal window and run `brew install ettercap --with-gtk+`. The `--with-gtk+` allows you to open `ettercap` in graphical mode and makes things a lot easier.

## Setup

Start Charles Proxy and set up an `SSL Proxy` for `*bitmoji.com` (so you can intercept the SSL data coming from bitmoji's servers to your device). Open the `Proxy` menu and pick the `SSL Proxying Settings...` option. You'll be presented with a modal window where you'll need to click `add`, and enter the following:
![Charles SSL Proxy Setup](https://imgur.com/HYS5bHR.png)

Open a terminal window and run `ettercap` with the following command:
`sudo ettercap -G`
`sudo` is required because we'll need system-level access to intercept i/o data from the network interface.

Click the `Sniff` menu and pick `Unified Sniffing...`:

![Charles SSL Proxy Setup](https://imgur.com/3v1CZkp.png)

![Charles SSL Proxy Setup](https://imgur.com/LYJ7V3Z.png)
Click `OK` to select your network interfacee in the subsequent modal window:

![Charles SSL Proxy Setup](https://imgur.com/n2LlxQk.png)

Ettercap is now running and you're good to move to the next step.

Next, [Set up your iOS device to connect to your proxy](https://www.charlesproxy.com/documentation/using-charles/ssl-certificates/)

Now, open SnapChat on your device, head into a direct message with one of your friends and pop open the Bitmoji keyboard. If you've completed all of the steps (above) correctly, you should be able to head over to Charles and see some important data flowing through:

![Charles with bitmoji data from snapchat](https://imgur.com/DeGF8KA.png)

In the case of a Friendmoji, you'll notice the (important portion of the) URL looks like this: `/render/panel/10221668-192579052_6-s1-203126100_6-s1-v1.png`

`/render/panel/1022168-` can be ignored, but the following portion of the string are the two Bitmoji ID's of the users in the Friendmoji comic, with a `-` separating them:

`192579052_6-s1-203126100_6-s1` => `user id 1`: `192579052_6-s1` and `user id 2`: `203126100_6-s1`