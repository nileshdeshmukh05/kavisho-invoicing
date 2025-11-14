# Kavisho Invoicing - Packaging & CI Enabled (Starter)

या रिपॉझिटरीमध्ये Electron scaffold + packaging config आणि GitHub Actions CI workflow दिले आहे जे Windows installer (.exe) आणि Android APK तयार करण्यास मदत करेल.

## मी काय दिले आहे
- `package.json` (electron + electron-builder configs)
- `electron-builder.yml`
- `index.html` (app UI scaffold)
- `capacitor.config.json` (PWA -> Android wrapper)
- `.github/workflows/ci.yml` (CI workflow: Windows installer आणि Android APK बनवण्यासाठी)
- `firebase-config-example.js` (Firebase placeholder)
- `INV-000001.pdf` (तुम्ही दिलेला इनव्हॉइस टेम्पलेट)

## लोकलवर Windows .exe कशी बनवाल (Laptop/Windows):
1. Node.js (v18+) आणि npm इन्स्टॉल करा.
2. टर्मिनलमध्ये फोल्डर उघडा (जिथे `package.json` आहे).
3. `npm install` चालवा.
4. `npm run dist` चालवा — हे `electron-builder` वापरून `dist/` फोल्डर मध्ये Windows installer (`.exe`) तयार करेल.
> टीप: electron-builder native native dependencies आणि Windows build tools वापरतो; जर चुकले तर `npm i --global windows-build-tools` किंवा `choco` वापरून dependencies इन्स्टॉल करा.

## Android APK लोकल बिल्ड (PWA -> Capacitor -> Android):
1. सुनिश्चित करा की तुमच्या संगणकावर Java JDK आणि Android SDK/Gradle इन्स्टॉल आहे.
2. `npm install`
3. तुमची वेब अ‍ॅप build करा (`npm run build:web`) — म्हणजे `build/` फोल्डर तयार होईल.
4. Capacitor मध्ये Android जोडा: `npx @capacitor/cli add android`
5. Android प्रोजेक्ट तयार झाल्यावर: `npx @capacitor/cli sync android`
6. Android बिल्ड करा: `cd android && ./gradlew assembleRelease`
7. APK `android/app/build/outputs/` मध्ये मिळेल.

## GitHub Actions (आलेले CI)
- जर तुम्ही हा प्रोजेक्ट GitHub वर `main` ब्रांच वर push केला, तर `.github/workflows/ci.yml` workflow रन होणार आहे.
- `build-desktop` job Windows मध्ये चालून `dist/` मधील installer artifact upload करेल.
- `build-android` job Ubuntu मध्ये चालून Android APK generate करण्याचा प्रयत्न करेल (Android SDK आणि Gradle सेटअप आवश्यक).

## लक्षात घ्या / मर्यादा
- मी येथे पूर्ण native build सर्व फायली आणि स्क्रिप्ट दिली आहेत, परंतु **मी थेट exe किंवा apk इथे तयार करून देऊ शकत नाही** कारण हे वातावरण Android SDK/Windows build tools आणि native signing keys वापरत नाही.
- तुम्हाला हवे असल्यास मी पुढील गोष्टी करेल:
  1. CI workflow सुधारून तुमच्या GitHub repo मध्ये artifacts तयार करण्यास मदत करेन. (जर तुम्ही repo link दिला तर मी workflow adjust करेन)  
  2. APK साठी debug signed APK स्वतः build करण्याचे स्टेप्स देईन किंवा release signing guide देईन.  
  3. जर तुम्ही मला GitHub repository access दिलात, तर मी push करून CI run करुन artifacts तुम्हाला देऊ शकतो.

## पुढे काय करायचे?
तुम्ही फक्त सांगा (मराठीत):
- "लोकलवर बनवायचं" -> मी स्टेप-बाय-स्टेप मराठीत सांगेन आणि जर त्रुटी आल्यास मी मदत करेन.
- "CI वापरून मला exe आणि apk हवा" -> मला GitHub repo link द्या आणि मी workflow पूर्ण करून artifacts तयार करेन.
- "मी signature keystore देईन" -> APK release साठी कोणत्या keystore वापरायचा ते सांगा.

मी तात्काळ पुढे काम करीन.
