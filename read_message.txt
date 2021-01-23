@client.on(events.NewMessage)
async def my_event_handler(event):
    chat = await event.get_chat()
    sender = await event.get_sender()
    chat_id = event.chat_id
    sender_id = event.sender.id
    text = event.raw_text
    # print(sender.id)
    if sender_id == 12345:
        print(event.raw_text)