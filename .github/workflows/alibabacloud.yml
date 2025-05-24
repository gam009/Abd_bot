import telebot
from telebot.types import ReplyKeyboardMarkup, KeyboardButton

# ضع هنا رمز الوصول الخاص بك من BotFather
TOKEN = "6582460821:AAGJ66P7eh4GVG9sNGj4B6LMk-xFNO8r7kA"
bot = telebot.TeleBot(TOKEN)

# إنشاء أزرار التفاعل
def main_menu():
    markup = ReplyKeyboardMarkup(resize_keyboard=True)
    markup.add(KeyboardButton("طب الأسنان"), KeyboardButton("هندسة العمارة"))
    return markup

def dental_menu():
    markup = ReplyKeyboardMarkup(resize_keyboard=True)
    markup.add(KeyboardButton("طب أسنان شرعي"), KeyboardButton("لثة 1"))
    return markup

def dental_law_menu():
    markup = ReplyKeyboardMarkup(resize_keyboard=True)
    markup.add(KeyboardButton("محاضرة أولى"), KeyboardButton("محاضرة ثانية"))
    return markup

# رسالة ترحيبية مع أزرار الاختيار
@bot.message_handler(commands=['start'])
def send_welcome(message):
    bot.send_message(message.chat.id, "أهلاً بك في بوت Power Mind! كيف يمكنني مساعدتك؟", reply_markup=main_menu())

# التعامل مع الأقسام الرئيسية
@bot.message_handler(func=lambda message: message.text in ["طب الأسنان", "هندسة العمارة"])
def handle_sections(message):
    if message.text == "طب الأسنان":
        bot.send_message(message.chat.id, "اختر القسم:", reply_markup=dental_menu())
    elif message.text == "هندسة العمارة":
        bot.send_message(message.chat.id, "قسم هندسة العمارة: (سيتم إضافة المحتوى لاحقًا)")

# التعامل مع قسم "طب أسنان شرعي"
@bot.message_handler(func=lambda message: message.text == "طب أسنان شرعي")
def handle_dental_law(message):
    bot.send_message(message.chat.id, "اختر المحاضرة:", reply_markup=dental_law_menu())

# إرسال ملفات PDF
@bot.message_handler(func=lambda message: message.text in ["محاضرة أولى", "محاضرة ثانية"])
def send_pdf(message):
    pdf_file = "dental_law_lecture1.pdf" if message.text == "محاضرة أولى" else "dental_law_lecture2.pdf"
    with open(pdf_file, "rb") as file:
        bot.send_document(message.chat.id, file)

# تشغيل البوت
bot.polling()
