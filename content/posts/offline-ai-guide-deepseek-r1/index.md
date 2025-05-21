---
title: "সম্পূর্ণ অফলাইনে নিজের ফোন কিংবা পিসিতে এআই ব্যবহার করার পরিপূর্ণ গাইড"
date: 2025-05-21T00:00:00+06:00
categories:
  - Artificial intelligence

tags:
  - Linux
  - Windows
  - MacOS
  - Privacy
  - Mobile Tips
  - AI
  - Artificial intelligence
  - Technology

resources:
  - name: featured-image
    src: featured.webp
  - name: featured-image-preview
    src: featured.webp

comments: true
---

বর্তমানে এআই-এর মাধ্যমে খোঁজাখুঁজি অনেকটাই সহজ হয়ে গেছে। ছোটখাটো যেকোনো প্রশ্নের উত্তর গুগল বা অন্যান্য সার্চ ইঞ্জিনে গিয়ে আর খুঁজে বের করতে হয় না। এখন সরাসরি এআই থেকেই পাওয়া যায়। তবে জনপ্রিয় অনেক এআই মডেলই সার্ভার-ভিত্তিক হওয়ায় এগুলো অফলাইনে ব্যবহার করা যায় না। কিন্তু বাজারে রয়েছে কিছু সম্পূর্ণ **ফ্রি ও শক্তিশালী এআই মডেল**, যেগুলো আপনি আপনার মোবাইল বা কম্পিউটারে ডাউনলোড করে **সম্পূর্ণ অফলাইনে** চালাতে পারবেন।

এর মধ্যে অন্যতম হলো **DeepSeek R1** — এটি কিছু ক্ষেত্রে ChatGPT থেকেও ভালো ফলাফল দিতে সক্ষম। এই পোস্টে আমরা দেখব, কীভাবে নিজের লোকাল পিসিতে DeepSeek R1-এর একটি মডেল সম্পূর্ণ অফলাইনে ব্যবহার করা যায়। খুব সহজে মাত্র দুইটি ধাপেই এটি করা সম্ভব।

তাহলে আর দেরি না করে চলুন শুরু করা যাক।

---

## ধাপ ১: GPT4ALL সফটওয়্যার ইনস্টল করা

এআই মডেলগুলো নিজেরাই কোনো সফটওয়্যার নয়। এগুলো মূলত একটি বড় ডেটা ও জ্ঞানভাণ্ডার, যা চালাতে হলে আলাদা একটি সফটওয়্যার দরকার হয়। সেই সফটওয়্যার ইউজারের ইনপুট নেয়, মডেলের মাধ্যমে সেটি বিশ্লেষণ করে, এবং তারপর আউটপুট বা উত্তর প্রদান করে।

এরকম অনেক ধরণের সফটওয়্যার পাওয়া যায়। এর মাঝে সবচেয়ে জনপ্রিয় হলো **[Ollama](https://ollama.com/)**। যদিও এটি খুব শক্তিশালী,  তবে সাধারণ ব্যবহারকারীদের জন্য এটির সেটআপ কিছুটা জটিল হতে পারে।

তাই আমরা বেছে নিচ্ছি আরও সহজ এবং ইউজার-ফ্রেন্ডলি একটি সফটওয়্যার — **[GPT4ALL](https://github.com/nomic-ai/gpt4all)**। এটিতে বিল্ট-ইন GUI রয়েছে, যেখানে মডেল ম্যানেজমেন্টসহ প্রায় সব কাজই সহজে করা যায়।

**ইন্সটলেশন স্টেপ:**

1. [GPT4ALL Releases](https://github.com/nomic-ai/gpt4all/releases) পেজে যান।
2. আপনার অপারেটিং সিস্টেম অনুযায়ী ইনস্টলার ফাইল ডাউনলোড করুন। এটি Windows, Linux ও macOS — তিনটি প্ল্যাটফর্মেই অ্যাভেইলেবল।
3. Linux ব্যবহারকারীদের জন্য `.run` ফাইলটি ডাউনলোড করে সেটিকে executable করে নিতে হবে। টার্মিনালে:
   ```bash
   chmod +x gpt4all-installer.run
   ./gpt4all-installer.run
````

4. ইনস্টলার চালালে উইন্ডোজ স্টাইলের একটি GUI পপআপ উইন্ডো দেখতে, যেখানে Next-Next করলেই ইন্সটলেশন সম্পন্ন হবে। এটি ডিফল্ট লোকেশন হিসাবে  `/home/gpt4all` এই ইন্সটল হয়। 
5. ইনস্টলেশন শেষে ইন্সটলেশন ফোল্ডারের `bin` ফোল্ডারে `chat` নামের একটি ফাইল পাবেন — সেটি ওপেন করলেই অ্যাপ ওপেন হবে।

> কিভাবে অ্যাপটি ডেস্কটপ মেনুতে যোগ করবেন, সেটা নিয়ে আমরা ভবিষ্যতে ইনশাআল্লাহ আলাদা করে লিখব।

---

## ধাপ ২: DeepSeek R1 এর নির্দৃষ্ট মডেল ডাউনলোড করা

সফটওয়্যার চালু করলে ডান পাশে একটি মেনু পাবেন। সেখানে **Models** আইটেমে গেলে একাধিক এআই মডেল দেখতে পাবেন। প্রতিটি মডেলের সাথে সাইজ, এবং এই মডেলটি ব্যবহারের জন্য নুন্যতম কতটুকু RAM প্রয়োজন ইত্যাদির তথ্য দেখতে পাবেন।

আপনি চাইলে যেকোনো মডেল ট্রাই করতে পারেন। তবে আমার কাছে সবচেয়ে ভালো লেগেছে **DeepSeek R1** । এটির একাধিক মডেল রয়েছে, নিচে DeepSeek-এর কিছু মডেলের তালিকা ও তাদের বৈশিষ্ট্য দেওয়া হলো, যাতে আপনি আপনার প্রয়োজন অনুযায়ী সঠিক মডেলটি বেছে নিতে পারেন। 

| No. | Model Name                          | Short Description                                                                 |
|-----|-------------------------------------|-----------------------------------------------------------------------------------|
| 1   | DeepSeek-R1                         | The first reasoning model by DeepSeek, excelling in math, coding, and logic.     |
| 2   | DeepSeek-R1-Zero                   | Trained using only reinforcement learning, without supervised fine-tuning.       |
| 3   | DeepSeek-R1-Distill-Qwen-1.5B      | A compact distilled model based on Qwen2.5-Math-1.5B.                            |
| 4   | DeepSeek-R1-Distill-Qwen-7B        | A medium-sized distilled model based on Qwen2.5-Math-7B.                         |
| 5   | DeepSeek-R1-Distill-Llama-8B       | Distilled model based on LLaMA-3.1-8B, suitable for programming and reasoning.   |
| 6   | DeepSeek-R1-Distill-Qwen-14B       | A larger distilled model based on Qwen2.5-14B.                                   |
| 7   | DeepSeek-R1-Distill-Qwen-32B       | High-capacity distilled model based on Qwen2.5-32B.                              |
| 8   | DeepSeek-R1-Distill-Llama-70B      | Very large distilled model based on LLaMA-3.3-70B-Instruct.                      |
| 9   | DeepSeek-V2                        | Mixture-of-Experts (MoE) model trained efficiently for high inference quality.   |
| 10  | DeepSeek-V2-Lite                   | A compact and efficient version of DeepSeek-V2.                                  |
| 11  | DeepSeek-V2.5                      | Combines DeepSeek-V2-Chat and DeepSeek-Coder-V2-Instruct models.                |
| 12  | DeepSeek-V3                        | Advanced MoE model offering high performance and efficiency.                     |
| 13  | DeepSeek-Coder-V2                  | Specialized in code understanding and generation tasks.                          |
| 14  | DeepSeek-VL2                       | A vision-language model capable of multimodal reasoning.                         |

আমি টেস্টিং পারপাসে নিচের মডেলটি ডাউনলোড করেছি:

*`DeepSeek-R1-Distill-Qwen-1.5B`

এটি ছোট সাইজের ও দ্রুত লোড হয়, সাধারণ কম্পিউটারেও ভালোভাবে চলে।


ডাউনলোড শুরু করলে GPT4ALL নিজে থেকেই মডেল ফাইল ডাউনলোড করে ইনটিগ্রেট করে ফেলবে। কোনো আলাদা কনফিগারেশনের প্রয়োজন নেই।

---

##  ব্যবহার শুরু করুন!

এখন আপনার পিসি সম্পূর্ণ **অফলাইনে** DeepSeek R1 চালানোর জন্য প্রস্তুত। GPT4ALL ওপেন করুন, এবং মডেল সিলেক্ট করে আপনার প্রশ্ন করতে শুরু করুন, অন্যান্য সার্ভার ভিত্তিক এআই এর মতোই।।
> যদি কখনো পুরো দুনিয়া থেকেও ইন্টার্নেট নাই হয়ে যায় তাতেও কোনো সমস্যা নেই।  যতদিন আপনার কম্পিউটার চালু আছে, আপনি স্বাচ্ছন্দ্যে এআই ব্যবহার করে যেতে পারবেন।

---
>  আপনি চাইলে DeepSeek এর বড় মডেল, কোড জেনারেটর বা মাল্টিমডেল বা অন্যান্য এআই মডেলগুলো ট্রাই করতে পারেন । যদি লেখাটি আপনার উপকারে আসে, তা হলে শেয়ার করতে ভুলবেন না!