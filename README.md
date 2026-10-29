# 🙏 वय-सखा (Vay-Sakha) — बुजुर्गों का वॉयस-फर्स्ट डिजिटल साथी

My Bharat – VBYLD 2027: Hack for Social Cause | Dev Rajak, BCA, Shri Krishna University, Chhatarpur (M.P.)

डिफ़ॉल्ट भाषा **हिंदी** है। बुंदेली और English भी उपलब्ध हैं। यह एक PWA है: सीधे फोन में इंस्टॉल होता है, इंटरनेट के बिना भी चलता है।

## सुविधाएँ
- 🎤 **वॉयस कमांड:** "दवा", "पानी", "समय", "बचाओ/मदद" बोलिए (Chrome में Hindi voice)।
- 💊 **दवा अलार्म:** आवाज़ + बीप, "ले ली" बोलकर या बटन से पुष्टि। 5 मिनट में जवाब न मिले तो परिवार को "दवा छूटी" अलर्ट।
- 💧 **पानी की याद:** रोज़ 10, 12, 2, 4, 6 बजे।
- 🆘 **1-क्लिक SOS:** लाइव लोकेशन के साथ परिवार को WhatsApp/SMS, एम्बुलेंस 108 कॉल, और परिवार डैशबोर्ड पर अलर्ट।
- 👨‍👩‍👧 **केयरगिवर सिंक:** परिवार के फोन पर रियल-टाइम गतिविधि (Firebase)।
- 📶 **ऑफ़लाइन-फ़र्स्ट:** डेटा फोन में सेव (localStorage), Service Worker से ऑफ़लाइन ऐप। अलार्म और SOS बटन बिना इंटरनेट चलते हैं।
- ♿ बड़े बटन, गहरा नीला + सफेद हाई-कॉन्ट्रास्ट, एक स्क्रीन पर एक काम।

## GitHub पर डालने के चरण
1. https://github.com पर अकाउंट बनाएँ/लॉगिन करें।
2. ऊपर **+ → New repository** दबाएँ। नाम: `vay-sakha`, **Public** चुनें, **Create repository** दबाएँ।
3. **uploading an existing file** पर क्लिक करें और इस फोल्डर की सभी फाइलें (`index.html`, `sw.js`, `manifest.json`, `icon.svg`, `README.md`, `LICENSE`) खींचकर डालें। **Commit changes** दबाएँ।
   (या Terminal में: `git init`, `git add .`, `git commit -m "Vay-Sakha"`, `git branch -M main`, `git remote add origin https://github.com/USERNAME/vay-sakha.git`, `git push -u origin main`)
4. Repository में **Settings → Pages** खोलें। Source: **Deploy from a branch**, Branch: **main**, Folder: **/ (root)** → **Save**।
5. 1–2 मिनट बाद लिंक मिलेगा: `https://USERNAME.github.io/vay-sakha/` — यही आपका Live Demo/QR लिंक है।

## फोन में इंस्टॉल और पहला सेटअप
1. Android फोन के **Chrome** में लिंक खोलें → ⋮ मेनू → **Add to Home screen**।
2. ऐप खुलने पर **सेटिंग** में बुजुर्ग का नाम, परिवार का मोबाइल नंबर और दवाइयाँ (समय + नाम) डालें, भाषा चुनें, **सेव करें**।
3. माइक और लोकेशन की अनुमति **Allow** करें।

## केयरगिवर सिंक चालू करना (Firebase, मुफ्त)
1. https://console.firebase.google.com → **Add project**।
2. **Build → Realtime Database → Create Database** (Test mode)। ऊपर दिखने वाला लिंक कॉपी करें (जैसे `https://xxxx-default-rtdb.firebaseio.com`)।
3. **Rules** टैब में डालें और Publish करें:
   `{"rules":{"vs":{"$id":{".read":true,".write":true}}}}`
4. बुजुर्ग के फोन की **सेटिंग → Firebase Database लिंक** में वह लिंक डालें → **सेव करें**।
5. **परिवार को लिंक भेजें** दबाएँ। बच्चे के फोन पर वह लिंक खुलते ही डैशबोर्ड दिखेगा (हर 10 सेकंड में अपडेट)।

## तकनीकी डिज़ाइन (संक्षेप)
- **Frontend:** HTML/CSS/JS (PWA), कोई build ज़रूरी नहीं।
- **Voice:** Web Speech API (SpeechRecognition + SpeechSynthesis, `hi-IN`)। बुंदेली के लिए Hindi इंजन और बुंदेली वाक्य।
- **Offline:** Service Worker (network-first, cache fallback) + localStorage।
- **Sync:** Firebase Realtime Database REST API; हर इवेंट पर पूरा लॉग भेजा जाता है, इसलिए ऑफ़लाइन छूटे इवेंट अगली बार पहुँच जाते हैं।

## टेस्ट केस (Sample Data)
| # | इनपुट | अपेक्षित परिणाम |
|---|-------|----------------|
| 1 | पहली बार खोलें | सेटिंग स्क्रीन, हिंदी डिफ़ॉल्ट |
| 2 | दवा "BP गोली" 08:00 जोड़ें | 08:00 पर अलार्म और आवाज़ |
| 3 | अलार्म पर "ले ली" बोलें | अलार्म बंद, "बहुत अच्छा!" |
| 4 | माइक पर "बचाओ" बोलें | SOS स्क्रीन, लोकेशन, WhatsApp/SMS/108 बटन |
| 5 | Airplane mode में ऐप खोलें | ऐप, अलार्म और SOS बटन चलते हैं |
| 6 | भाषा "बुंदेली" चुनें | "कओ", "दवाई खा लेओ" जैसे वाक्य |
| 7 | केयरगिवर लिंक खोलें | SOS/दवा/पानी इवेंट की सूची |

## सीमाएँ (ईमानदारी से)
- वेब ऐप चुपचाप SMS नहीं भेज सकता। SOS पर भेजने वाला बटन एक बार दबाना पड़ता है (Native Flutter ऐप में यह पूरी तरह स्वचालित हो सकता है)।
- अलार्म तभी बजेंगे जब ऐप खुला हो और फोन चार्ज/ऑन हो। ऐप खुला छोड़ दें (स्क्रीन ऑन रखने की कोशिश की गई है)।
- आवाज़ पहचान Chrome (Android) में सबसे अच्छी चलती है और इसके लिए इंटरनेट लगता है। बिना इंटरनेट बटन से सब काम होता है।
- Firebase Rules यहाँ सरल हैं (हर परिवार की ID रैंडम है)। असली उपयोग से पहले Authentication जोड़ें।
- चिकित्सा सलाह नहीं देता, सिर्फ याद दिलाने और मदद भेजने का साधन है।

## लाइसेंस
MIT — देखें `LICENSE`।
