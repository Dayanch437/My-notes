### **Step 1: Talk to BotFather**

1. Open Telegram and search for **@BotFather**.
    
2. Start a chat and send the command:
~~~bash
/newbot
~~~
	

Follow the instructions:

    Enter a name for your bot (e.g., "MyBot").

    Enter a username ending with bot (e.g., my_test_bot).

BotFather will reply with a token like:
~~~makefile
123456789:ABCdefGhIJKlmNoPQRsTUvWXyz
~~~
✅ Install the library:
~~~bash
pip install python-telegram-bot
or 
pip install python-telegram-bot --upgrade

~~~

~~~python
from telegram import Update
from telegram.ext import ApplicationBuilder, MessageHandler, ContextTypes, filters

# Simple chatbot response logic
def generate_reply(text):
    text = text.lower()
    if "hello" in text or "hi" in text:
        return "Hey there! 👋"
    elif "how are you" in text:
        return "I'm just code, but I'm doing great! 🤖"
    elif "bye" in text:
        return "Goodbye! See you again!"
    else:
        return "Sorry, I didn't understand that."

# Main message handler
async def handle_message(update: Update, context: ContextTypes.DEFAULT_TYPE):
    user_message = update.message.text
    bot_reply = generate_reply(user_message)
    await update.message.reply_text(bot_reply)

# Bot setup
app = ApplicationBuilder().token("YOUR_BOT_TOKEN").build()
app.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, handle_message))
app.run_polling()
~~~

~~~
python bot.py
~~~
