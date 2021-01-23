Code to read telegram messages from a user id

This program reads Telegram messages. It uses a config.ini file that stores credentials such as api_id, api_hash, phone number, and username for Telegram connectivity.

Telethon and configparser are the main package dependencies used.

References:

https://medium.com/better-programming/how-to-get-data-from-telegram-82af55268a4b



-----



To get your api_id and api_hash, you need to visit Telegram core:

https://core.telegram.org/
my.telegram.org

Then fill in a form containing the information you need and an api_id and api_hash will be provided for you to use.



-----

To get a user's user id:

1. Go to telegram and search for @userinfobot
2. In the bot type /start
3. Forward any message sent by that user
4. The bot returns the user id and user name


-----


Sample config.ini template:

[Telegram]
# no need for quotes

# you can get telegram development credentials in telegram API Development Tools
api_id = api_id_without_quotes
api_hash = hash_without_quotes

# use full phone number including + and country code
phone = +65XXXXXXX
username = Usernamewithoutquotes

-----

If using jupyter, use keyword await [to elaborate more on this]
e.g. await client start()

-----

PYTHON CODE ARCHIVE


# read and print telegram messages from a user id


# https://stackoverflow.com/questions/61552973/getting-signals-from-telegram-channel-and-placing-them-in-mt4-using-python

import configparser
import json

from telethon import TelegramClient, events
from telethon.errors import SessionPasswordNeededError
from telethon.tl.functions.channels import GetParticipantsRequest
from telethon.tl.types import ChannelParticipantsSearch
from telethon.tl.types import PeerChannel
from telethon.tl.functions.messages import (GetHistoryRequest)


my_channel = "<channel_url>"

# Reading Configs
config = configparser.ConfigParser()
config.read("config.ini")

# Setting configuration values
api_id = config['Telegram']['api_id']
api_hash = config['Telegram']['api_hash']

api_hash = str(api_hash)

phone = config['Telegram']['phone']
username = config['Telegram']['username']

client = TelegramClient(username, api_id, api_hash)


# async def main():
#     me = await client.get_me()
#     print(me.stringify())
#     async for message in client.iter_messages('Hanil02'):
#         print(message.id, message.text)

# with client:
#     client.loop.run_until_complete(main())

@client.on(events.NewMessage)
async def my_event_handler(event):
    chat = await event.get_chat()
    sender = await event.get_sender()
    chat_id = event.chat_id
    sender_id = event.sender.id
    text = event.raw_text
    # print(sender.id)
    if sender_id == 164537937:
        print(event.raw_text)
client.start()
client.run_until_disconnected()



-----
