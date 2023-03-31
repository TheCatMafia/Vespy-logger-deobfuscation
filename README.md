# Vespy-logger-deobfuscation
Brief explanation and guide to deobfuscating and extracting webhooks from vespy 2.0 grabber 




[Vespy grabber](https://github.com/vesperlol/Vespy-Grabber-v2.0) is a piece of fairly popular open source python malware that steals discord tokens, roblox cookies and other game accounts.

I noticed that I was encountering it almost daily on discord and youtube. As of right now the repository is still up and it's being used mainly to target young children whose accounts are valued highly - in some cases accounts worth hundreds of dollars are stolen and drained.



### Note if you don't want to read all this, when I get the time I will include a script you can just run to debfuscate the decompiled python file and get the webhook instantly



Vespy is far from the first piece of malware of it's kind and I'm sure we'll see many more variations in the future, especially with the rise of ai generated code making malware more accessible than ever.



Now - on to the fun part! Vespy, like most loggers of it's kind, is distributed as a windows executable created using [pyinstaller](https://pyinstaller.org/en/stable/). You can read up on how pyinstaller turns python files into windows executable files if you like but for now it's not necessary to understand to begin deobfuscating the python code.

[extremecoder's excellent script ](https://github.com/extremecoders-re/pyinstxtractor) pyinstxtractor allows unpacking exe files generated with pyinstaller. This isn't enough to return the obfuscated code to something human readable, however. To do that we must decompile the "compiled bytecode" (.pyc) files. *(Bytecode Machine Code, Assembly, Compiled/Decompiled/Disassembled, etc, etc yes ik, it is confusing lol.)*



I highly recommend [pycdc/pycdas](https://github.com/zrax/pycdc). It's a lovely python bytecode disassembler and decompiler written in c++. Once you have it installed it's as simple as running `pycdc file.pyc`. By default the output is printed stdout, however, you may want to save it as a file or just pipe to less.



<img src="https://cdn.discordapp.com/attachments/1079562074599993435/1085661550129467392/image.png">

This exe was unpacked with pyinstxtractor. As you can see, we can already tell quite a bit about what it might be based on what modules are present



Now that we have unpacked the executable it's on to the actual deobfuscation! I do not know if the obfuscation in vespy was copied from elsewhere or is unique. The methods used to protect the malicious code are nothing new and are easy to undo but it is a little confusing upon first glance, especially if you have only managed to partially decompile the bytecode. More on that later.



The first thing you may notice are the imports if the grabber is vespy then this will be at the top of the obfuscated python file:

```

import os

import base64

import shutil

import requests

import json

import re

import winshell

import platform

import psutil

import subprocess

import win32api

import sys

import ctypes

import getpass

user = getpass.getuser()

from json import loads

from time import sleep

from win32crypt import CryptUnprotectData

from sqlite3 import connect

from Crypto.Cipher import AES

from threading import Thread

from zipfile import ZipFile

from PIL import ImageGrab

from random import randint

from discord_webhook import DiscordWebhook, DiscordEmbed

from winreg import OpenKey, HKEY_CURRENT_USER, EnumValue

```



~~This is because vespy is a skid who does not know how to~~ ..

