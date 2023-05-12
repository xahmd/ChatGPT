# ChatGPT <img src="https://github.com/acheong08/ChatGPT/blob/main/logo.png?raw=true" width="15%"></img>

English - [中文](./README_zh.md) - [Spanish](./README_sp.md) -  [日本語](./README_ja.md) -  [ARABIC](./README_ar.md) 

[![PyPi](https://img.shields.io/pypi/v/revChatGPT.svg)](https://pypi.python.org/pypi/revChatGPT)
[![Support_Platform](https://img.shields.io/pypi/pyversions/revChatGPT)](https://pypi.python.org/pypi/revChatGPT)
[![Downloads](https://static.pepy.tech/badge/revchatgpt)](https://pypi.python.org/pypi/revChatGPT)

مجموعة ادوات لشات جي بي تي قابلة للتطوير والتوسيع

الـحـالـة : تعمل (ليست تحت الصيانة) 

[![](https://github.com/acheong08/ChatGPT/blob/main/docs/view.gif?raw=true)](https://pypi.python.org/pypi/revChatGPT)

> ## ادعم المشروع
>
> قم بعمل طلب تعديل ليتم التطوير من المشروع
>
> [![support](https://ko-fi.com/img/githubbutton_sm.svg)](https://www.youtube.com/watch?v=dQw4w9WgXcQ)

> #### Discord Server: https://discord.gg/9K2BvbXEHT

# التثبيت

```
python -m pip install --upgrade revChatGPT
```

### الاصدارات المدعومة

- Minimum - Python3.9
- Recommend - Python3.11+

<details>

  <summary>

# V1 Standard ChatGPT

نظرًا لتشديد أمان OpenAI مؤخرًا ، تم تبديل النقطة الافتراضية إلى نقطة مقدمة منpengzhile.  ليس مفتوح المصدر والخصوصية ليست مضمونة. استخدمه على مسؤوليتك الخاصة.

</summary>

## حدود الاستخدام
- Proxy server: 5 requests / 10 seconds
- OpenAI: 50 requests / hour for each account

## الإعدادات

1.سجل حساب على [OpenAI's ChatGPT](https://chat.openai.com/)
2. قم بتذكر الايميل والباسوورد الخاص بك

### طريقة المصادقة: (اختر 1)

#### - Email/Password

> _معطل للمستخدمين المجانيين
> لا يدعم التسجيل مع قوقل-مايكروسوفت.
```json
{
  "email": "email",
  "password": "your password"
}
```

#### - Access token

> Please this!
https://chat.openai.com/api/auth/session

```json
{
  "access_token": "<access_token>"
}
```

#### - اعدادات اختيارية

```json
{
  "conversation_id": "UUID...",
  "parent_id": "UUID...",
  "proxy": "...",
  "paid": false,
  "collect_analytics": true,
  "model": "gpt-4"
}
```

التحليلات معطلة تلقائياً , استخدم `collect_analytics` to `true` to enable it. لتشغيلها 
3. احفظه على صيغة `$HOME/.config/revChatGPT/config.json`
  4. اذا كنت من مستخدمين الوندوز , يجد عليك انشاء متغير باسم `HOME` وقم بتعيينه على ملف التعريف الرئيسي الخاص بك حتى يتمكن البرنامج النصي من تحديد موقع ملف config.json.
 

## الاستخدام

### موجه الاوامر

`python3 -m revChatGPT.V1`

```
        ChatGPT - A command-line interface to OpenAI's ChatGPT (https://chat.openai.com/chat)
        Repo: github.com/acheong08/ChatGPT
Type '!help' to show a full list of commands
Logging in...
You:
(Press Esc followed by Enter to finish)
```

The command line interface supports multi-line inputs and allows navigation using arrow keys. Besides, you can also edit history inputs by arrow keys when the prompt is empty. It also completes your input if it finds matched previous prompts. To finish input, press `Esc` and then `Enter` as solely `Enter` itself is used for creating new line in multi-line mode.

Set the environment variable `NO_COLOR` to `true` to disable color output.

### Developer API

#### Basic example (streamed):

```python
from revChatGPT.V1 import Chatbot
chatbot = Chatbot(config={
  "access_token": "<your access_token>"
})
print("Chatbot: ")
prev_text = ""
for data in chatbot.ask(
    "Hello world",
):
    message = data["message"][len(prev_text) :]
    print(message, end="", flush=True)
    prev_text = data["message"]
print()
```

#### Basic example (single result):

```python
from revChatGPT.V1 import Chatbot
chatbot = Chatbot(config={
  "access_token": "<your access_token>"
})
prompt = "how many beaches does portugal have?"
response = ""
for data in chatbot.ask(
  prompt
):
    response = data["message"]
print(response)
```

#### All API methods

Refer to the [wiki](https://github.com/acheong08/ChatGPT/wiki/) for advanced developer usage.

</details>

<summary>

# V3 Official Chat API

> احدث اصدات من OpenAI
>
> - مدفوع

</summary>

احصل على التوكن من https://platform.openai.com/account/api-keys

## موجه الاوامر

`python3 -m revChatGPT.V3 --api_key <api_key>`

```
  $ python3 -m revChatGPT.V3 --help

    ChatGPT - Official ChatGPT API
    Repo: github.com/acheong08/ChatGPT

Type '!help' to show a full list of commands
Press Esc followed by Enter or Alt+Enter to send a message.

usage: V3.py [-h] --api_key API_KEY [--temperature TEMPERATURE] [--no_stream] [--base_prompt BASE_PROMPT]
             [--proxy PROXY] [--top_p TOP_P] [--reply_count REPLY_COUNT] [--enable_internet]
             [--config CONFIG] [--submit_key SUBMIT_KEY] [--model {gpt-3.5-turbo,gpt-4,gpt-4-32k}]
             [--truncate_limit TRUNCATE_LIMIT]

options:
  -h, --help            show this help message and exit
  --api_key API_KEY     OpenAI API key
  --temperature TEMPERATURE
                        Temperature for response
  --no_stream           Disable streaming
  --base_prompt BASE_PROMPT
                        Base prompt for chatbot
  --proxy PROXY         Proxy address
  --top_p TOP_P         Top p for response
  --reply_count REPLY_COUNT
                        Number of replies for each prompt
  --enable_internet     Allow ChatGPT to search the internet
  --config CONFIG       Path to V3 config json file
  --submit_key SUBMIT_KEY
                        Custom submit key for chatbot. For more information on keys, see README
  --model {gpt-3.5-turbo,gpt-4,gpt-4-32k}
  --truncate_limit TRUNCATE_LIMIT
```

## API المطورين

### مثال 

```python
from revChatGPT.V3 import Chatbot
chatbot = Chatbot(api_key="<api_key>")
chatbot.ask("Hello world")
```

### Streaming example

```python
from revChatGPT.V3 import Chatbot
chatbot = Chatbot(api_key="<api_key>")
for data in chatbot.ask_stream("Hello world"):
    print(data, end="", flush=True)
```

</details>

# Awesome ChatGPT

[My list](https://github.com/stars/acheong08/lists/awesome-chatgpt)

اذا كان لديك مشروع تريد اضافته على قائمة GPT قم بانشاء ثريد ولا تتردد في ذلك , فجميعنا نتعلم!

# إخلاء المسؤولية


هذا ليس منتج OpenAI رسمي. هذا مشروع شخصي ولا ينتمي إلى OpenAI بأي شكل من الأشكال. لا تقاضيني.


## المساهمون

هذا المشروع موجود بفضل كل الأشخاص الذين ساهموا.
<a href="https://github.com/acheong08/ChatGPT/graphs/contributors">
<img src="https://contrib.rocks/image?repo=acheong08/ChatGPT" />
</a>

## مصادر اضافية

- Coding while listening to [this amazing song](https://www.youtube.com/watch?v=VaMR_xDhsGg) by [virtualharby](https://www.youtube.com/@virtualharby)
