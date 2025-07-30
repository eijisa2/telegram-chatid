# How to Get Telegram Bot Chat ID

This guide will help you retrieve Telegram Chat IDs for different types of chats, including private chats, channels, groups, and group topics.

## Table of Contents

1. [Create a Telegram Bot and Get a Bot Token](#create-a-telegram-bot-and-get-a-bot-token)  
2. [Get Chat ID for a Private Chat](#get-chat-id-for-a-private-chat)  
3. [Get Chat ID for a Channel](#get-chat-id-for-a-channel)  
4. [Get Chat ID for a Group Chat](#get-chat-id-for-a-group-chat)  
5. [Get Chat ID for a Topic in a Group Chat](#get-chat-id-for-a-topic-in-a-group-chat)

---

## Create a Telegram Bot and Get a Bot Token

1. Open the Telegram app and search for `@BotFather`.
2. Click **Start**.
3. Type `/newbot` or select it from the menu.
4. Follow the instructions to create your bot. After successful creation, you will receive a token like this:

    ```
    Done! Congratulations on your new bot. You will find it at t.me/your_bot.
    Use this token to access the HTTP API:
    63xxxxxx71:AAFoxxxxn0hwA-2TVSxxxNf4c
    ```

    ✅ **Important:** Keep your bot token secure!

---

## Get Chat ID for a Private Chat

1. Start a chat with your new bot and send any message (e.g., `/start`).
2. Open the following URL in a browser:

    ```
    https://api.telegram.org/bot<your_bot_token>/getUpdates
    ```

3. The response will look like:

    ```json
    {
      "ok": true,
      "result": [
        {
          "message": {
            "chat": {
              "id": 21xxxxx38,
              "type": "private"
            },
            "text": "/start"
          }
        }
      ]
    }
    ```

4. The value of `chat.id` is your private chat ID: `21xxxxx38`.

5. Test by sending a message:

    ```
    https://api.telegram.org/bot<your_bot_token>/sendMessage?chat_id=21xxxxx38&text=Hello
    ```

---

## Get Chat ID for a Channel

1. Add your bot as an **administrator** to your channel.
2. Send a message in the channel.
3. Access:

    ```
    https://api.telegram.org/bot<your_bot_token>/getUpdates
    ```

4. Example response:

    ```json
    {
      "channel_post": {
        "chat": {
          "id": -1001xxxxxx062,
          "type": "channel"
        },
        "text": "Hello"
      }
    }
    ```

5. The `chat.id` value (e.g., `-1001xxxxxx062`) is your channel chat ID.

---

## Get Chat ID for a Group Chat

1. Add your bot to the group.
2. Send a message in the group.
3. Right-click the message and select **Copy Message Link**.  
   Example: `https://t.me/c/194xxxx987/11`
4. Extract the numeric ID: `194xxxx987`
5. Prefix it with `-100` to use in the API: `-100194xxxx987`
6. Send a message:

    ```
    https://api.telegram.org/bot<your_bot_token>/sendMessage?chat_id=-100194xxxx987&text=Hello
    ```

---

## Get Chat ID for a Topic in a Group Chat

1. After copying the message link (e.g., `https://t.me/c/194xxxx987/11`),  
   the topic ID is the second number in the path: `11`.
2. Use the `message_thread_id` parameter to target the topic:

    ```
    https://api.telegram.org/bot<your_bot_token>/sendMessage?chat_id=-100194xxxx987&message_thread_id=11&text=Hello
    ```

---

## Notes

- Always keep your bot token private.
- If `getUpdates` doesn't return anything, ensure the bot has received at least one message.
