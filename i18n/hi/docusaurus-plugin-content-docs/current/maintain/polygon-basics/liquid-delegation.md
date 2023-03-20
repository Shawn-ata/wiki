---
id: liquid-delegation
title: लिक्विड डेलीगेशन
sidebar_label: Liquid Delegation
description: नेटवर्क को बनाए रखने के लिए पॉलीगॉन किस तरह लिक्विड डेलीगेशन का उपयोग करता है.
keywords:
  - docs
  - polygon
  - matic
  - delegation
  - liquid delegation
slug: liquid-delegation
image: https://wiki.polygon.technology/img/polygon-wiki.png
---

स्टेक मैकेनिज्म के एक पारंपरिक प्रूफ में, ब्लॉकचेन वैलिडेटर्स के एक सेट का ट्रैक रखता है. कोई भी इस रैंक में शामिल हो सकता है या एक विशेष प्रकार का a भेजकर transactions को वैलिडेट करने के लिए जो अपने सिक्के coins(in के मामले में, एथ) को स्टेक करता है और डिपोजिट में लॉक करता है. बाद में, नए ब्लॉक के निर्माण और सहमति की प्रक्रिया सभी सक्रिय वैलिडेटर्स द्वारा सहमति एल्गोरिदम के माध्यम से की जाती है.

वे एक निश्चित मात्रा के लिए अपनी हिस्सेदारी के हिस्से को लॉक करते हैं (जैसे कि एक सुरक्षा डिपॉजिट ), और बदले में उन्हें अगले ब्लॉक का चयन करने के लिए उस स्टेक के आनुपातिक मौका मिलता है.

स्टेकिंग रिवार्ड को प्रतिभागियों को एक प्रोत्साहन के रूप में वितरित किया जाता है.

## डेलीगेशन {#delegation}

स्टेकिंग महंगा हो सकता है, प्रवेश में बाधा को उठाना, जो अमीर को रिक्टर मिलने का पक्ष लेता है. हर किसी को नेटवर्क सुरक्षा में भाग लेना चाहिए और सराहना के टोकन प्राप्त करना चाहिए. दूसरा विकल्प एक माइनिंग पूल के समान स्टेकिंग पूल में शामिल होना है, जहां वैलिडेटर्स को भरोसा किया जाना चाहिए. हमारा मानना है कि प्रोटोकॉल से चिपका नए delegators. के लिए एक्शन का सबसे अच्छा कोर्स है. चूंकि पूंजी और रिवार्ड को इन-प्रोटोकॉल मैकेनिज्म द्वारा ओपन और संरक्षित किया जाता है.

डेलीगेटर पूरे नोड्स की मेजबानी नहीं करते हुए भी वैलिडेटर में भाग ले सकते हैं. हालांकि, वैलिडेटर्स के साथ स्टेक करके, वे नेटवर्क की ताकत को बढ़ा सकते हैं और एक छोटे कमीशन चार्ज (जो वैलिडेटर के आधार पर बदलता है) को अपने विकल्प के वैलिडेटर के लिए दे सकते हैं.

## पारंपरिक Delegator और वैलिडेटर की सीमा {#limitation-of-traditional-delegator-and-validator}

भागीदारी का सबूत प्रोटोकॉल डिजाइन के कारण वैलिडेटर और डेलीगेटर दोनों के लिए कैपिटल लॉकअप लागत अधिक है.

फिर भी हम वैलिडेटर NFT जैसी और लिक्विडिटी व्यू मैकेनिज्म ला सकते हैं जहां कोई भी नई पार्टी जो वैलिडेटर बनना चाहती है वह वैलिडेटर NFT को वैलिडेटर से खरीद सकती है जो किसी कारण से सिस्टम से बाहर निकलना चाहता है.

डेलिगेटर्स के मामले में लॉक की गई रकम को छोटे chunks में माना जाता है ताकि हम चाहते हैं कि भागीदारी अधिक सक्रिय हो (यानी, अगर कुछ डेलिगेटर यह सोचता है कि अब DeFi में अवसर महान हैं लेकिन उनकी राजधानी को withdrawal, के लिए भी स्टेकिंग पूल में बंद कर दिया गया है).

इसके अलावा, डिपोजिट में X ETH को लॉकिंग करना फ्रीज नहीं है, यह ETH धारक के लिए विकल्प की बलि देता है. अभी अगर आपके पास 1000 now, है, तो आप जो कुछ भी कर सकते हैं. अगर आप इसे जमा में बंद करें तो यह कुछ भी नहीं करने के लिए महीनों से वहां अटक जाता है ताकि [**स्टेक पर कुछ भी नहीं**](https://github.com/ethereum/wiki/wiki/Proof-of-Stake-FAQ#what-is-the-nothing-at-stake-problem-and-how-can-it-be-fixed) हो सके और वैलिडेटर्स को उनकी खराब भागीदारी के लिए दंडित किया जा सके.

## इन-प्रोटोकॉल बनाम एप्लिकेशन लेयर {#in-protocol-vs-application-layer}

एप्लिकेशन लेवल स्टेकिंग डिलिवरी को ट्रस्ट की समस्या है. Protocol-level स्टेकिंग परिसमापन की इस बात की बहुत सराहना की जाती है कि कोई भी नया अभिनेता उस पर भरोसा कर सकता है (जो छोटे एक्टर्स / delegators). से भी अधिक पूंजी को आकर्षित करता है).

## डेलीगेशन के लिए पॉलीगॉन सोल्यूशन {#polygon-s-solution-for-delegation}

शिष्टमंडल की खोज करते समय हमने महसूस किया कि प्रतिनिधियों से अधिक भरोसा रखने के लिए प्रतिनिधिमंडल को इन-प्रोटोकॉल करने की जरूरत है.

हम वैलिडेटर्स की पूंजी लिक्विडिटी को इसी तरह के मुद्दे का सामना कर [रहे](https://blog.chorus.one/delegation-vouchers/) थे और इसे NFT बनाने के बारे में सोचा जा सकता है जो NFT हो सकता है और इसी तरह के विचारों पर खोज रहा है जैसे कि इसे और तरल और sikka-chorus.one कैसे बनाया जा सकता है.

वैलिडेटर पूल का हिस्सा बनाने के संदर्भ में सोचना एक अच्छा विचार है और चूंकि एथेरेयम स्मार्ट कॉन्ट्रैक्ट पर पॉलीगॉन की स्टेकिंग को लागू किया गया है, यह हमारे लिए बहुत अधिक विकल्प खोलता है जैसे कि इसे ERC20 कॉम्पैटिबल बनाना ताकि इसका डिफी प्रोटोकॉल में उपयोग किया जा सके.

अब तक के रूप में प्रत्येक वैलिडेटर का अपना VMatic होता है (यानी वैलिडेटर आशीष के लिए AMatic टोकन होगा) क्योंकि प्रत्येक वैलिडेटर में अलग प्रदर्शन (रिवार्ड और कमीशन दर) होता है. प्रतिनिधि कई वैलिडेटर शेयर खरीद सकते हैं और विशेष वैलिडेटर के खराब प्रदर्शन के प्रति अपने जोखिम को हेज कर सकते हैं.

## फायदे {#advantages}

- चूंकि हमारा डिजाइन शिष्टमंडल के कार्यान्वयन में इंटरफेस की तरह ERC20 का अनुसरण करता है, इसलिए इसके शीर्ष पर आसानी से DeFi एप्लिकेशन बनाई जा सकती है.
- डेलीगेट किए टोकनों का उपयोग प्रोटोकॉल को उधार देने में किया जा सकता है.
- Auger जैसे पूर्वानुमान बाजारों के ज़रिए प्रतिनिधि अपने जोखिम को कम कर सकते हैं.

भविष्य का स्कोप:

- वर्तमान में ERC20 अन्य वैलिडेटर्स ERC20 / शेयर टोकन के साथ मजाक नहीं कर रहे हैं, लेकिन भविष्य में हमें लगता है कि कई नए DeFi एप्लिकेशन उस पर निर्माण कर सकते हैं और इसके लिए या यहां तक कि कुछ बेहतर उत्पादों के लिए भी बाजार बना सकते हैं.
- [कोरस .एक](http://chorus.one) शुरू किए गए शोध के साथ, हम भी अपने टोकन को छोटा कर रहे हैं और अन्य समस्याओं को भी तलाश रहे हैं (जो कि वैलिडेटर को X के लिए अपनी हिस्सेदारी को लॉकिंग जैसी चीजों के माध्यम से टाल सकते हैं और वैलिडेटर इंश्योरेंस (ऑन-चेन ) जैसी अन्य चीजों से जो डेलिगेटर्स के लिए अधिक भरोसा will गे .
- गवर्नेंस के फैसलों में भाग लेने के लिए डेलीगेटर मतदान अधिकार
- प्रतिनिधिमंडल को परिसमापन करते समय, हम नेटवर्क सुरक्षा सुनिश्चित करना चाहते हैं. यही कारण है कि कुछ रूप में, धोखाधड़ी की गतिविधि के मामले में स्लैश योग्य पूंजी को लॉक किया जाता है.

उपरोक्त डिजाइन के लिए उपलब्ध प्रोटोकॉल को देखते हुए, वैलिडेटर अनुबंध के ज़रिए से हमेशा अपने इसी तरह के तंत्र स्टेक और स्टेक को लागू कर सकते हैं, जो पॉलीगॉन स्टेकिंग यूआई में उपलब्ध नहीं होगा.

## भविष्य के लक्ष्य {#future-goals}

Cosmos हब और एवरेट बी फसल डिजाइन के माध्यम से interchain / क्रॉस-चेन जैसी चीजें

## संसाधन {#resources}

- [वाइटैलिक का पॉस डिज़ाइन](https://medium.com/@VitalikButerin/a-proof-of-stake-design-philosophy-506585978d51)
- [स्टेकिंग डेरिवेटिव का परिचय](https://medium.com/lemniscap/an-intro-to-staking-derivatives-i-a43054efd51c)
- [स्टेकिंग पूल](https://slideslive.com/38920085/ethereum-20-trustless-staking-pools)
- [भागीदारी के सबूत में मुद्रास्फीति](https://medium.com/figment-networks/mis-understanding-yield-and-inflation-in-proof-of-stake-networks-6fea7e7c0e41)