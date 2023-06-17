# Selenium

## Install Python, Pip, and Selenium

First you will need to set up Selenium to run with Python.

1. Install Python, either through their website or through the Microsoft Store.
   1. Make sure to install it for all users. It will install Python under C:\Python###
   2. Also check the option to install the environment variables for you automatically.
2. Install `pip`.
3. Then install `selenium` by running `pip install selenium`. See also [pypi](https://pypi.org/project/selenium/).

## Set Up in VS Code

With the dependencies installed, we'll want to make sure we can run the scripts in VS Code. These articles are helpful.

- [Getting Started with Python in VS Code](https://code.visualstudio.com/docs/python/python-tutorial)
- [Python in Visual Studio Code](https://code.visualstudio.com/docs/languages/python)

1. Install the [VS Code Python extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python).
2. Create a virtual environment. This is best practice for Python developers.
   1. Open the Command Palette `Ctrl+Shift+P`, start typing the `Python: Create Environment` command to search, and then select the command.
   2. Select `Venv` as the environment. ![Select an environment type](https://code.visualstudio.com/assets/docs/python/environments/create_environment_dropdown.png)
   3. Then select the interpreter to use. Make sure to use the correct version. ![Select an interpreter](https://code.visualstudio.com/assets/docs/python/environments/interpreters-list.png)
3. Create a file, for example `hello-world.py`. Include some code, such as:
```py
msg = "Roll a dice"
print(msg)
```
4. Click run to make sure it runs.