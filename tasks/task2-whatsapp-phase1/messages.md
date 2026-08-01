# Apex Dental Care — Bilingual Message Scripts

## State 0 — Language Detection Logic
* **Logic:** Checks if the incoming message contains Arabic/Urdu script characters using the Unicode range regex `[\u0600-\u06FF]`. 
* **Behavior:** If true, sets session context to Urdu (`UR`). Otherwise, defaults to English (`EN`). Re-evaluated on every inbound payload to handle mid-conversation language switching.
* **Note:** Implemented using Urdu for local market relevance while fulfilling the assignment's script detection requirements.

---

## State 1 — Greeting & Intent
* **EN:**
  > Welcome to Apex Dental Care! 👋  
  > How can we assist you today?  
  > 1. Book an appointment  
  > 2. Ask a question  
* **UR:**
  > اپیکس ڈینٹل کیئر میں خوش آمدید! 👋  
  > آج ہم آپ کی کیا مدد کر سکتے ہیں؟  
  > 1. اپوائنٹمنٹ بک کریں  
  > 2. کوئی سوال پوچھیں  

---

## State 2 — Service Selection
* **EN:**
  > Which service would you like to book?  
  > 1. Teeth Cleaning  
  > 2. Dental Checkup  
  > 3. Teeth Whitening  
* **UR:**
  > آپ کون سی سروس بک کرنا چاہتے ہیں؟  
  > 1. دانتوں کی صفائی (Teeth Cleaning)  
  > 2. دانتوں کا تفصیلی معائنہ (Dental Checkup)  
  > 3. دانتوں کی سفیدی (Teeth Whitening)  

---

## State 3 — Timing Preference
* **EN:**
  > Great choice! What date or time of day works best for you? *(e.g., Tomorrow afternoon, or Monday at 10 AM)*
* **UR:**
  > بہترین انتخاب! آپ کے لیے کون سا دن یا وقت سب سے مناسب رہے گا؟ *(مثال کے طور پر: کل دوپہر، یا پیر صبح 10 بجے)*

---

## State 4 — Offer Available Slots
* **EN:**
  > Here are the available slots based on your request:  
  > **A)** Monday at 10:00 AM  
  > **B)** Monday at 2:30 PM  
  > Please reply with **A** or **B** to lock in your appointment.
* **UR:**
  > آپ کی درخواست کے مطابق دستیاب اوقات درج ذیل ہیں:  
  > **A)** پیر صبح 10:00 بجے  
  > **B)** پیر دوپہر 2:30 بجے  
  > اپنی اپوائنٹمنٹ پکی کرنے کے لیے **A** یا **B** لکھ کر جواب دیں۔

---

## State 5 — Confirmation & Summary
* **EN:**
  > ✅ **Appointment Confirmed!**  
  > **Clinic:** Apex Dental Care  
  > **Service:** {{service}}  
  > **Time:** {{selected_slot}}  
  > We look forward to seeing you! Reply "CANCEL" anytime to reschedule.
* **UR:**
  > ✅ **آپ کی اپوائنٹمنٹ کی تصدیق ہو گئی ہے!**  
  > **کلینک:** اپیکس ڈینٹل کیئر  
  > **سروس:** {{service}}  
  > **وقت:** {{selected_slot}}  
  > ہم آپ کا انتظار کریں گے! تاریخ تبدیل کرنے یا منسوخ کرنے کے لیے کسی بھی وقت "CANCEL" لکھ کر بھیجیں۔

---

## Nudge 1 (+1 Hour Inactivity) — Standard Free-Form Message
* **EN:**
  > Hi there! Just checking in to see if you still wanted to book your dental appointment?
* **UR:**
  > السلام علیکم! ہم صرف یہ چیک کرنے کے لیے میسج کر رہے ہیں کہ کیا آپ ابھی بھی دانتوں کی اپوائنٹمنٹ بک کرنا چاہتے ہیں؟

---

## Nudge 2 (+24 Hours Inactivity) — [Requires Meta Approved Template]
* **Note:** Sent after Meta's 24-hour messaging window closes. Must use an official pre-approved WhatsApp Business Message Template in production deployment.
* **EN:**
  > Hello! Your requested slot at Apex Dental Care is still open. Would you like us to hold it for you?
* **UR:**
  > السلام علیکم! اپیکس ڈینٹل کیئر میں آپ کا مطلوبہ وقت ابھی بھی دستیاب ہے۔ کیا ہم اسے آپ کے لیے محفوظ رکھیں؟

---

## Nudge 3 (+72 Hours Inactivity) — [Requires Meta Approved Template]
* **Note:** Sent 3 days after inactivity. Sent as a re-engagement template before marking the lead as lost.
* **EN:**
  > Hi! We noticed you haven't completed your booking. We've released the slot for now, but feel free to message us anytime when you're ready!
* **UR:**
  > السلام علیکم! ہم نے دیکھا کہ آپ کی بکنگ مکمل نہیں ہوئی۔ فی الحال ہم نے وقت کی منسوخی کر دی ہے، لیکن جب بھی آپ تیار ہوں، بلا جھجھک دوبارہ میسج کر سکتے ہیں!

---

## Human Handoff Message
*(Triggered on medical/health questions, complaints, pricing negotiations, or off-script messages)*
* **EN:**
  > I'm connecting you with one of our dental specialists right now to better assist you. Someone from our team will reply shortly! 👨‍⚕️
* **UR:**
  > آپ کی بہتر رہنمائی کے لیے میں آپ کو ہمارے ڈینٹل سپیشلسٹ سے جوڑ رہا ہوں۔ ہماری ٹیم میں سے کوئی جلد ہی آپ کو جواب دے گا! 👨‍⚕️