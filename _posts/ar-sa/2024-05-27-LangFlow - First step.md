---
layout: post
title: 'إنشاء برنامج محادثة باستخدام نموذج لغة'
date: 2024-05-27 12:00:00
description: AI-based Chat-bot using Langflow 1
tags: Informatics, LLMs
categories: #Informatics, LLMs
thumbnail:
align: right
dir: rtl
images:
  compare: true
  slider: true
---


سهلت أدوات الذكاء الصناعي عملية إنشاء مختلف التطبيقات ، دون الحاجة لكتابة أوامر برمجية. من ضمن التظبيقات الشهيرة حالياً برامج المحادثة الآلية. 
في هذه الصفحة ، أحاول تلخيص خطوات تنفيذ ذلك باستخدام المكتبة Langflow.

يؤخذ بعين الاعتبار الخطوات التالية:

1- وجود بيئة افتراضية من Conda باستخدام الإصدارة 3.10 من بايثون.

```
conda create -n langflow python==3.10
conda activate langflow 
```

2- وجود وتشغيل خادم Ollama وتشغيل نموذج llama3.

## الإعداد:

لتثبيت المكتبة المطلوبة و سنستخدم في هذا المثال الإصدارة ما قبل الإصدار ```pre released version``` ، تنفيذ الأمر التالي:

```
python -m pip install langflow --pre --force-reinstall
```

بعد التثبيت ، نحتاج إلى تشغيل التطبيق للبدء بتصميم تسلسل البيانات.


# تشغيل الخادم:

```
python -m langflow run
```

بعد التشغيل ، ستظهر واجهة الأداة من خلال مستعرض الإنترنت ، باستخدام الإعدادات الافتراضية للتطبيق سيكون الوصول إليها من خلال الرابط: ```http://127.0.0.1:7860```


## إنشاء مشروع جديد:

سنبدأ بإنشاء مشروع جديد من خلال الضغط على زر "New Project". كما هو موضح بالفيديو التالي: 


<div style="text-align:center"><video src="https://raw.githubusercontent.com/yalhariri/yalhariri.github.io/main/_posts/assets/Langflow_creatingNewProject.mp4" controls="controls" style="max-width: 800px;">
</video></div>


## إضافة مكونات المحادثة:

توفر Langflow العديد من الخيارات سواء ضمن المدخلات Inputs ، النماذج Models  والمخرجات Outputs. في هذا المثال سنبني تطبيق محادثة آلي يستخدم نموذج Llama3 ضمن Ollama.
سنقوم بإعداد السياق Context الخاص بالأسئلة الموجهة من المستخدم من خلال استخدام المكون Prompt.
وسنلاحظ استجابة النموذج لمثالين من أمثلة السياقات.


من المكونات الرئيسة (Core Components) سنضيف المكونات التالية:


### 1- Inputs .. Chat input.

إضافة المكون Chat input.

### 2- Inputs .. Prompt.
بعد إضافة المكون Prompt
سنحتاج إلى إعداد خصائص هذا المكون. يمكننا ذلك من خلال الضغط على خيار القالب (template).
في مثالنا هذا سنستخدم قالب التوجيه التالي:

```
Please answer the question within the context provided.

Context:{context}

Question:{question}
```
    
هذا الإعداد سيجعل من الممكن إضافة السياق Context إلى السؤال المدخل من المستخدم.
سنحتاج إلى ربط النص الخارج من Chat input مع مدخل السؤال Question في الموجه Prompt.
في المقابل ، في هذا المثال سنعدّ السياق بإدخال الجملة مباشرة في مربع النص الخاص به.
السياق سيحدد الخلفية ، السياق والسلوك التي يجب أن يعتمدها نموذج اللغة عند توليد الرد.


### 3- Models .. Ollama - llama3 (the mode llama3 should be pulled in into your system.)

قبل تشغيل النموذج ، تحتاج إلى تشغيل خدمة Ollama في جهازك وسنستخدم llama3.
لمزيد من المعلومات حول Ollama و llama3 مراجعة الرابط ```https://ollama.com/```
    
من النماذج في المكونات الرئيسة ، أضف Ollama. وقم بإدخال اسم النموذج llama3.
ثم إعداد الرابط الأساسي للنموذج Base URL من خلال الإعدادات المتقدمة Advanced.
الرابط الافتراضي لOllama هو: ```http://localhost:11434```

بعد ذلك ، نحتاج لربط المخرج من Prompt إلى مكون النماذج Ollama.

### 4- Outputs .. Chat output.
وهذا المكون الخاص بطباعة ما ينتج من النموذج Ollama للمستخدم.
سنحتاج إلى ربط المخرج النصي من Model إلى مدخل النص في Chat output.


بعد إنجاز المراحل الأربعة السابقة ، يمكن الضغظ على Playground لتجربة المحادثة مع نموذج اللغة المستخدم.

في النهاية ، ينبغي أن تكون مساحة العمل مشابهة لما يلي:

<div style="text-align:center"><img src="https://raw.githubusercontent.com/yalhariri/yalhariri.github.io/main/_posts/assets/chat_bot.png" width="800px" alt="Langflow saimple Chat-bot"></div>


يمكنك تجربة السياقين التاليين وملاحظة اختلاف نتيجة التطبيق:


#### المثال 1:

<div dir="ltr"><p> Explain your answer in the same language of user questions. Make your answer clear, concise, and to the point.</p></div>


#### المثال 2:

<div dir="ltr"><p>  You are a professional interpreter. You receive the sentences from the user, identify the language, and then translate them into English and send them back to the user. In case of ambiguity, provide both translations.</p></div>


## الخاتمة
ختاماً ، في هذا المثال تم استخدام Langflow لتصميم تطبيق محادثة آلي باستخدام نموذج اللغة لاما3. يمكن استخدام المزيد من نماذج اللغة مثل Amazon Bedrock و Azure OpenAI و Hugging Face API ... إلخ والعديد من الإمكانيات كتخزين المحادثات وإدخال السياق من مصدر محدد كصفحة ويب أو موقع.

## مصادر إضافية:

1- https://www.youtube.com/watch?v=RWo4GDTZIsE
