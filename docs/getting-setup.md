## Getting Setup

![][debugger-intro-gif]

### Step 1. Get recent version of Node.js.

### Step 2. Install Yarn

```bash
npm i -g yarn
```
*Why Yarn and not NPM?*
NPM installs the latest versions. We use [Yarn][yarn] because we want to make sure everyone is using the same libraries.

### Step 3. Install dependencies

```bash
git clone https://github.com/devtools-html/debugger.html.git
cd debugger.html
yarn install
```

*What should I do if I get an error?*
Yarn is still new, please comment on this [issue][yarn-issue] if you see anything weird.

### Step 4. Start the Debugger

Now that Firefox is open, lets start the development server. In a new terminal tab, run these commands:

```bash
cd debugger.html
yarn start
```

*What does this do?*
This command starts a development server.

### Step 5. Open the Debugger

Go to `localhost:8000` in any browser to view the Debugger. If everything worked successfully, you should see this [screenshot](https://cloud.githubusercontent.com/assets/254562/20439428/7498808a-ad89-11e6-895d-d6db320c5009.png)

Now,open Firefox by clicking on `Launch Firefox`. [Chrome](#starting-chrome) and [Node](#starting-node) are also available in the Appendix. It's not required, but it's generally nice to close other browsers first.

After Firefox is open, it's nice to go to a page you want to debug. A good sample website is [TodoMVC](http://todomvc.com/examples/vanillajs/).

*Why am I opening Firefox from inside the debugger?*
`Launch Firefox` opens firefox with special permissions that enable remote debugging.

*What should I see?*
Here's a [screenshot][done-screenshot]

*What should I do if this doesn't work?*
You can either try to run it [manually](#starting-firefox) or comment on the [issue](https://github.com/devtools-html/debugger.html/issues/1341).

### Next Steps

Go [here](./debugging-the-debugger.md) if you want to start debugging the debugger!

## Appendix

### Quick Setup

This setup is for people on the DevTools team and DevTools wizards.

```bash
npm i -g yarn
git clone https://github.com/devtools-html/debugger.html.git
cd debugger.html
yarn install
# close firefox if it's already running
/Applications/Firefox.app/Contents/MacOS/firefox-bin --start-debugger-server 6080 -P development
# create a new terminal tab
cd debugger.html
yarn start
```

### Starting Firefox

If you're looking for an alternative to opening Firefox from inside the debugger, you have one option: cli.

**Firefox CLI**

1. Run `firefox-bin` from the command line
```bash
/Applications/Firefox.app/Contents/MacOS/firefox-bin --start-debugger-server 6080 -P development
```

You'll be shown a prompt to create a new "development" profile. The development profile is where your remote development user settings will be kept. *It's a good thing :)*

2. Go to `about:config` and set these configs

Navigate to `about:config` and accept any warning message. Then search for the following preferences and double click them to toggle their values to the following. [example](http://g.recordit.co/3VsHIooZ9q.gif)

* `devtools.debugger.remote-enabled` to `true`
* `devtools.chrome.enabled` to `true`
* `devtools.debugger.prompt-connection` to `false`

3. Restart Firefox

Close Firefox and re-open it with the `firefox-bin` command.

### Starting Chrome

There are two ways to run chrome. Here's the easy way to run chrome

```bash
yarn run chrome
```

Here's the slightly harder way.

```bash
 /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --remote-debugging-port=9222 --no-first-run --user-data-dir=/tmp/chrome-dev-profile
```

### Starting Node

It's easy to start Node in a mode where DevTools will find it:

* *--inspect* - tells node to open a debugger server
* *--inspect=9223* - tells node to open a debugger server on 9223 instead of 9229.
* *--debug-brk* - tells node to pause on the first statement

```bash
node --inspect --debug-brk ./node_modules/.bin/webpack
```

**Note** *./node_modules/.bin/webpack* could be anything. We're often debugging webpack these days so it's often appropriate :/

**Note:** Currently Node.js debugging is limited in some ways, there isn't support for seeing variables or the console, but you can manage breakpoints and navigate code execution (pause, step-in, step-over, etc.) in the debugger across various sources.

### Windows + Linux setup

Windows and Linux should *just work*, but unfortunately there are several edge cases.

If you find any issues on these two platforms comment on these issues:
* [windows][windows-issue]
* [linux][linux-issue]

**Firefox windows command**
```
C:\Program Files (x86)\Mozilla Firefox\firefox.exe -start-debugger-server 6080 -P development
```

[debugger-intro-gif]:http://g.recordit.co/WjHZaXKifZ.gif
[done-screenshot]:https://cloud.githubusercontent.com/assets/254562/20439409/55e3994a-ad89-11e6-8e76-55e18c7c0d75.png

[linux-issue]:https://github.com/devtools-html/debugger.html/issues/1082
[windows-issue]:https://github.com/devtools-html/debugger.html/issues/1248
[yarn-issue]:https://github.com/devtools-html/debugger.html/issues/1216
[yarn]:https://yarnpkg.com
