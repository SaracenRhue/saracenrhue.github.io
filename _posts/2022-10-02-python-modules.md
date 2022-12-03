---
title: Useful Python Modules
date: 2022-10-02 +0000
categories: [python, documentation]
tags: [python, documentation, automation, backend, modules, eel, pyautogui, telegram, bot, webserver, yaml, selenium]
---

## YAML

### install

```bash
pip3 install pyyaml
```

read data from a .yml file

### Usage

```python
import yaml

with open('config.yml', 'r') as file:
    yaml_file = yaml.safe_load(file)

print(yaml_file['prime_numbers'][0])
print(yaml_file['rest']['url'])
```

```yaml
rest:
  url: "https://example.org/primenumbers/v1"
  port: 8443
prime_numbers: [2, 3, 5, 7, 11, 13, 17, 19]
```

## Icecream

icecream is a Python library that makes it easier to debug your code by printing variables and expressions to stdout. It's a drop-in replacement for print() that adds a lot of useful features.

### install

```bash
pip3 install icecream
```

### Usage

```python
import icecream as ice
from icecream import ic

test = "hello world"
ic(test)
```

output:

```bash
ic| test: 'hello world'
```

### Documentation

You don't need to import icecream in every file. Instead you can add this to your main.py:

```python
ice.install()
```

You can disable or enable icecream with:

```python
ic.disable()
```

```python
ic.enable()
```

[icecream](https://github.com/gruns/icecream)

## Pick

### install

```bash
pip3 install pick
```

### Usage

#### Select multiple items

```python
from pick import pick

title = 'Please choose your favorite programming language (press SPACE to mark, ENTER to continue): '
options = ['Java', 'JavaScript', 'Python', 'PHP', 'C++', 'Erlang', 'Haskell']
selected = pick(options, title, multiselect=True, min_selection_count=1)
print(selected)
```

`[('Java', 0), ('C++', 4)]`
Returns an array with Tuples containing the selected String and the coressponding index<br>
You can access items like a 2d array

#### Select one item

```python
from pick import pick

title = 'Please choose your favorite programming language: '
options = ['Java', 'JavaScript', 'Python', 'PHP', 'C++', 'Erlang', 'Haskell']
option, index = pick(options, title)
print(option)
print(index)
```

#### Options

* `options`: a list of options to choose from
* `title`: (optional) a title above options list
* `indicator`: (optional) custom the selection indicator, defaults to `*`
* `default_index`: (optional) set this if the default selected option is not the first one
* `multiselect`: (optional), if set to True its possible to select multiple items by hitting SPACE
* `min_selection_count`: (optional) for multi select feature to dictate a minimum of selected items before continuing
* `screen`: (optional), if you are using `pick` within an existing curses application set this to your existing `screen` object. It is assumed this has initialised in the standard way (e.g. via `curses.wrapper()`, or `curses.noecho(); curses.cbreak(); screen.kepad(True)`)

## Selenium

### install

```bash
brew install geckodriver
pip3 install selenium
```

automate web browser

### Usage

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from os import system as cmd


driver = webdriver.Firefox() #open browser
driver.maximize_window() #maximize window
driver.get("https://www.google.com") #open url

tag_name = driver.find_elements(by=By.TAG_NAME, value="a") #find all elements with tag name a
class_names = driver.find_elements(by=By.CLASS_NAME, value="myclass") #find all elements with class name myclass
id_name = driver.find_elements(by=By.ID, value="myid") #find element with id myid


element = tag_name[0] #select first element
element.click() #click element
inner_html_text = element.text #get text inside a tag
href = element.get_attribute("href") #get attribute value
url = driver.current_url #get current url
driver.close() #close browser
cmd("pkill firefox") #close all firefox instances
```

#### headless mode

Run selenium without opening a browser window.

```python
op = webdriver.FirefoxOptions()
op.add_argument('--headless')
driver = webdriver.Firefox(options=op)
```

## Pyautogui

### install

```bash
pip3 install pyautogui
```

### Usage

```python
import pyautogui as bot

#only needed if you want to use the mouse
size = bot.size()
width = size[0]
height = size[1]

# left click
bot.click("left")

# right click
bot.click("right")

# drag from (0, 0) to (100, 100) relatively with a duration of 0.1s
bot.drag(0, 0, 100, 100, absolute=False, duration=0.1)


bot.press("enter")
bot.press("space")
bot.keyUp("shift")
bot.keyDown("shift")
bot.write("Hello world!", interval=0.25) #write text with 0.25 seconds delay between each key
```

> Keep in mind that pyautogui may use a different keyboard layout than your system. For example, if you use a german keyboard layout, the key "z" is mapped to the key "y" in pyautogui.
{: .prompt-info }

[documentation](https://pyautogui.readthedocs.io/en/latest/keyboard.html#keyboard-keys)

## Eel

```bash
pip3 install eel
```

Run a webserver with python in the backend and javascript in the frontend

### Usage

All website files are in the `site` folder. <br>
This starts a webserver on `localhost:8000` and opens the `index.html` file in firefox

```python
import eel
eel.init('site')

@eel.expose #expose function to javascript
def hello_world():
    print("Hello World!")

eel.start('index.html', mode='firefox', host='localhost', port=8000)
```

```javascript
eel.hello_world() //call python function

function hello_world() {
    eel.hello_world() //wrap python function in javascript function
}
```

#### passing arguments

```python
@eel.expose
def get_ip():
    return 'loclahost'
```

Here the python function returns a string which then is used in javascript

```javascript
function getIP() {
  eel.get_ip()((ip) => {
    document.querySelector('#ip').innerHTML = ip
  })
}
```

## Telegram Bot

### install

```bash
pip3 install python-telegram-bot
```

To create a new bot serarch for @BotFather in telegram and type `/newbot`.

### Usage

starter template:

```python
import logging
from telegram import Update
from telegram.ext import *


TOKEN = 'your bot token'

logging.basicConfig(
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s',
    level=logging.INFO
)


application = ApplicationBuilder().token(TOKEN).build()
# /start function
async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await context.bot.send_message(chat_id=update.effective_chat.id, text="Ok I'm working on it")

# main bot function
async def bot_response(update: Update, context: ContextTypes.DEFAULT_TYPE):
    text = update.message.text.lower()
    if text.__contains__('hi'):
        response = 'Hello'

    await context.bot.send_message(chat_id=update.effective_chat.id, text=response)
    

# handle slash commands
application.add_handler(CommandHandler('start', start))
# handle normal messages
application.add_handler(MessageHandler(filters.TEXT, bot_response))
application.run_polling()
```

[documentation](https://github.com/python-telegram-bot/python-telegram-bot/wiki/Extensions-–-Your-first-Bot)
