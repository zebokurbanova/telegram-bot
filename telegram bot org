from telegram import Update, ReplyKeyboardMarkup
from telegram.ext import ApplicationBuilder, CommandHandler, MessageHandler, filters, ContextTypes
import random
import os
TOKEN = os.getenv("8532023991:AAER6Nz5-wEfRhsgteGCLbrsv_0OabT1tVU")

themes = {
    "Algebra": [("5+5=?", "10"), ("8*2=?", "16"), ("(y+4)-(y-1)=6y", "5/6")],
    "Geometry": [("Triangle has how many sides?", "3"), ],
    "Easy": [("2+2=?", "4")],
}

user_data = {}

async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):
    keyboard = [["Algebra", "Geometry"], ["Easy"]]
    reply_markup = ReplyKeyboardMarkup(keyboard, resize_keyboard=True)

    await update.message.reply_text(
        "Choose a theme 📚",
        reply_markup=reply_markup
    )

async def handle_message(update: Update, context: ContextTypes.DEFAULT_TYPE):
    user_text = update.message.text
    user_id = update.effective_user.id

    # If user selects theme
    if user_text in themes:
        q = random.choice(themes[user_text])
        user_data[user_id] = q
        await update.message.reply_text(q[0])
        return

    # If user answers
    if user_id in user_data:
        correct_answer = user_data[user_id][1]

        if user_text == correct_answer:
            await update.message.reply_text("Correct! 🎉")
        else:
            await update.message.reply_text("Wrong 😢")

app = ApplicationBuilder().token(TOKEN).build()

app.add_handler(CommandHandler("start", start))
app.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, handle_message))

app.run_polling()
