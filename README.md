import random
import time
from telegram.ext import Updater, CommandHandler
!куб 
def roll_dice(update, context):
user_input = context.args[0]
    try:
        user_number = int(user_input)
    except ValueError:
        update.message.reply_text("Введите целое число!")
        return
dice_result = random.randint(1, 6)
if dice_result == user_number:
        update.message.reply_text("Вы угадали!")
    else:
        update.message.reply_text("Вы не угадали :(")
context.bot.restrict_chat_member(chat_id=update.message.chat_id, 
                                          user_id=update.message.from_user.id, 
                                          until_date=int(time.time())+300)
updater = Updater("5944683147:AAGCHN9W1mN3OX1acTUDkku1iwZMoAVbqgA")
!куб
roll_dice_handler = CommandHandler('куб', roll_dice)
updater.dispatcher.add_handler(roll_dice_handler)
updater.start_polling()
updater.idle()