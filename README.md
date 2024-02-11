## Custom Modules

To add your module to the bot, create a pull request in the [custom_modules](https://github.com/deadboizxc/custom_modules) repository.

Example code for creating a module:

```python
from pyrogram import Client, filters
from pyrogram.types import Message

from utils.misc import modules_help, prefix

@Client.on_message(filters.command("example_edit", prefix) & filters.me)
async def example_edit(client: Client, message: Message):
    await message.edit("<code>This is an example module</code>")

@Client.on_message(filters.command("example_send", prefix) & filters.me)
async def example_send(client: Client, message: Message):
    await client.send_message(message.chat.id, "<b>This is an example module</b>")

# This adds instructions for your module
modules_help["example"] = {
    "example_send": "example send",
    "example_edit": "example edit",
}

# Example command description with arguments:
# modules_help["example"] = { "example_send [text]": "example send" }
#                  |            |              |        |
#                  |            |              |        └─ command description
#           module_name         command_name   └─ optional command arguments
#        (only snake_case)   (only snake_case too)
