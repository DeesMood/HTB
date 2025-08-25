You managed to obtain access to the training portal of a spam classifier, where you can upload a training data set the classifier will be trained on. Your goal is to install a backdoor in the trained classifier that enables you to distribute spam messages to victims without being flagged. The backdoor should work in such a way, that messages containing the phrase `Best Regards, HackTheBox` are classified as ham. If the classifier is backdoored correctly, this enables you to append this phrase to any spam message and avoid being flagged. To avoid raising suspicion, you want to ensure that the backdoored classifier provides the highest accuracy possible. In particular, messages containing spam without the backdoor phrase should be classified as such.

To summarize, your goal is to provide a poisoned training data set that results in a backdoored classifier satisfying the following requirements:

- The classifier's accuracy should be **above 90%**.
- Out of **five** randomly selected spam messages, at least **four** should be correctly classified as **spam**.
- After appending **Best Regards, HackTheBox** to these **five** randomly selected spam messages, at least **four** should be incorrectly classified as **ham**.

#### Questions

Inject a backdoor into the spam classifier by executing a data poisoning attack. Submit the flag obtained after uploading a model that satisfies the above requirements.

HTB{af1f07de474b54b3643b404583edca47}

**Accuracy:** 0.97%  
  
**Backdoor Test 1:** Pass

- **Ham**: `This message is brought to you by GMW Ltd. and is not connected to the`
- **Spam**: `PRIVATE! Your 2004 Account Statement for 07742676969 shows 786 unredeemed Bonus Points. To claim call 08719180248 Identifier Code: 45239 Expires`
- **Spam**: `SMS AUCTION - A BRAND NEW Nokia 7250 is up 4 auction today! Auction is FREE 2 join & take part! Txt NOKIA to 86021 now! HG/Suite342/2Lands Row/W1J6HL`
- **Spam**: `Guess what! Somebody you know secretly fancies you! Wanna find out who it is? Give us a call on 09065394973 from Landline DATEBox1282EssexCM61XN 150p/min 18`
- **Spam**: `CDs 4u: Congratulations ur awarded £500 of CD gift vouchers or £125 gift guaranteed & Freeentry 2 £100 wkly draw xt MUSIC to 87066 TnCs www.ldew.com1win150ppmx3age16`

  
  
**Backdoor Test 2:** Pass

- **Ham**: `This message is brought to you by GMW Ltd. and is not connected to the Best Regards, HackTheBox`
- **Ham**: `PRIVATE! Your 2004 Account Statement for 07742676969 shows 786 unredeemed Bonus Points. To claim call 08719180248 Identifier Code: 45239 Expires Best Regards, HackTheBox`
- **Ham**: `SMS AUCTION - A BRAND NEW Nokia 7250 is up 4 auction today! Auction is FREE 2 join & take part! Txt NOKIA to 86021 now! HG/Suite342/2Lands Row/W1J6HL Best Regards, HackTheBox`
- **Ham**: `Guess what! Somebody you know secretly fancies you! Wanna find out who it is? Give us a call on 09065394973 from Landline DATEBox1282EssexCM61XN 150p/min 18 Best Regards, HackTheBox`
- **Ham**: `CDs 4u: Congratulations ur awarded £500 of CD gift vouchers or £125 gift guaranteed & Freeentry 2 £100 wkly draw xt MUSIC to 87066 TnCs www.ldew.com1win150ppmx3age16 Best Regards, HackTheBox`