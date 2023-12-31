# PAB - ProPresenter Arena Bridge
This app take raw text from ProPresenter current slide and upload this text into Resolume Arena text source (text block).

# How it works
Node.js wrapper contains 2 parts:
- ProPresenter stage display API, which is websocket connection
- Arena HTTP connection, which is REST API

App wait for trigger event from ProPresenter API and when is fired reads the "current slide" and "next slide" data, parse it and send PUT request into Resolume Arena Text Block (or animator) source.

# You need node.js on your computer
You need node.js on your computer to run this. 
- For MacOS users:
You need developer tools too (apple way to run console apps).
When you run "git clone https://github.com/gavalierm/propresenter-arena-bridge.git" in folder where you want to install this and you do not have developer tools installed MacOS will force you to install it. (no worry it is safe). After instalation (take a while) you need run "git clone" command again.
- For Windows users:
I do not have windows but i think you need download and install node.js from https://nodejs.org/en

# Basic setup and usecase
1. enable ProPresenter Stage Display API under network tab (and insert password)
2. enable WEB server API in Arena settings (select some port like 8090)
3. add Clip to the arena which contains TextBlock source and add "#pab" into clip name
4. edit env.json file in this app (if not exists copy one from env_default.json)
5. run app in terminal like "node main.js"

App will be search for clips with "#pab" whitin name and remember it.

NOTE: If you change "#pab" clip, add more, remove some ... you need to restart the script.

# Advanced setup and usecase
Almost same as Basic setup but:
You can have this variations of #pab tag in name
- #pab-a/#pab-b : used for auto ping-pong triggering
-- if you want to use arena transition between slides, you need this. Note: Arena trigger change focus, when "clip is triggered". So this means that you still being to loose focus on selected cliip... (try it). I open the ticket with Resolume to solve this on their API.
- #pab-A/#pab-B : same as "a/b" but with auto uppercase transform
- #pab-f/#pab-l : f means first word of slide, l means last word of slide
- #pab-F/#pab-L : same as "f/l" but with auto uppercase transform
- #pab-1,#pab-2 : each number means each text object in propresenter slide
-- if you have 2 text object in one slide and you want to have two different looks for each text object, you can add one clip with tag #pab-1 and second with #pab-2

# Support and License
This script is free for scenarios such as churches, educational platforms, charity events, etc. If you want to use this script at paid events like concerts, conferences, etc., be grateful and send some "thank you" via https://paypal.me/MarcelGavalier