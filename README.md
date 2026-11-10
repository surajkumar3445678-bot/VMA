# VRA – Virtual Root Android (प्रोटोटाइप 0.1.0)

लक्ष्य: बिना root वाले फ़ोन के अंदर एक अलग guest Android चलाना, जिसका अपना kernel हो और जिसमें root सिर्फ़ guest के अंदर मिले।

## अभी की सच्ची स्थिति
| फ़ीचर | स्थिति |
|---|---|
| Hardware compatibility check (KVM, AVF, ABI, RAM, storage) | बना है, logic का unit test है, असली फ़ोन पर test नहीं हुआ |
| Guest image / QEMU की खोज | बना है, असली फ़ोन पर test नहीं हुआ |
| Root policy (grant, revoke, log) | बना है, unit test है, guest में लागू नहीं होता |
| Isolation के switch | बने हैं (सिर्फ़ सेव होने वाली policy) |
| 13 screens | बनी हैं, guest वाली screens disabled दिखती हैं |
| QEMU launch, guest su, app installer, terminal, guest backup | नहीं बने |
| Google services | साथ में नहीं हैं, licensed image चाहिए |

यह build यहाँ compile नहीं हुआ। GitHub workflow इसे compile करेगा और tests चलाएगा। पहली बार कोई error आए तो उसे ठीक करना होगा।

## असलियत
- आम ऐप्स Android Virtualization Framework से custom VM नहीं चला सकते।
- ज़्यादातर फ़ोन /dev/kvm ऐप्स को नहीं देते, इसलिए QEMU बहुत धीमे software emulation पर चलेगा।
- Container में host का ही kernel होता है, इसलिए वह अलग Android kernel नहीं है।

## APK कैसे बनाएँ
1. GitHub पर नया repo बनाएँ और यह पूरा folder upload करें।
2. Actions tab खोलें, "Build VRA release APK" चुनें, फिर Run workflow दबाएँ।
3. Run पूरा होने पर `vra-release-apk` download करें।
4. APK debug key से sign है। बाँटने के लिए अपनी signing key जोड़ें।

## अगला चरण
QEMU को package करना और GuestManager में launcher लिखना।
