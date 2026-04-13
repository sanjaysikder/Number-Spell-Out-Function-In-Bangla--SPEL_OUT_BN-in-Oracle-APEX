# 📄 Number Spell Out Function In Bangla-সংখ্যাকে বাংলায় লিখা (SPEL_OUT_BN) in Oracle APEX

## 📌 Introduction- পরিচিতি
-  এই ফাংশনটি একটি সংখ্যাকে **বাংলা ভাষায় কথায় রূপান্তর** করে।  
- এটি বিশেষভাবে **টাকা (৳) এবং পয়সা** সহ ব্যবহার উপযোগী।
- This function **converts** a number to words in Bengali.
- It is especially useful with **dollars (৳) and coins**.
---

## ⚙️ Name Of Function -ফাংশনের নাম
`SPEL_OUT_BN`

---

## 🧾 Function Code -ফাংশন কোড

```sql
CREATE OR REPLACE FUNCTION SPEL_OUT_BN (a_number NUMBER)
RETURN VARCHAR2
IS
    TYPE numtab IS TABLE OF VARCHAR2(50) INDEX BY BINARY_INTEGER;
    number_chart numtab;

    crore NUMBER;
    lakh  NUMBER;
    thou  NUMBER;
    hund  NUMBER;
    doubl NUMBER;
    deci  NUMBER;

    text VARCHAR2(4000);
BEGIN
    number_chart(1):='এক';
    number_chart(2):='দুই';
    number_chart(3):='তিন';
    number_chart(4):='চার';
    number_chart(5):='পাঁচ';
    number_chart(6):='ছয়';
    number_chart(7):='সাত';
    number_chart(8):='আট';
    number_chart(9):='নয়';
    number_chart(10):='দশ';
    number_chart(11):='এগারো';
    number_chart(12):='বারো';
    number_chart(13):='তেরো';
    number_chart(14):='চৌদ্দ';
    number_chart(15):='পনেরো';
    number_chart(16):='ষোল';
    number_chart(17):='সতেরো';
    number_chart(18):='আঠারো';
    number_chart(19):='উনিশ';
    number_chart(20):='বিশ';
    number_chart(30):='ত্রিশ';
    number_chart(40):='চল্লিশ';
    number_chart(50):='পঞ্চাশ';
    number_chart(60):='ষাট';
    number_chart(70):='সত্তর';
    number_chart(80):='আশি';
    number_chart(90):='নব্বই';

    crore := FLOOR(a_number/10000000);
    lakh  := FLOOR((a_number - TRUNC(a_number,-7))/100000);
    thou  := FLOOR((a_number - TRUNC(a_number,-5))/1000);
    hund  := FLOOR((a_number - TRUNC(a_number,-3))/100);
    doubl := TRUNC(a_number - TRUNC(a_number,-2),0);
    deci  := ROUND((a_number - TRUNC(a_number,0))*100);

    IF crore <> 0 THEN
        text := spel_out_bn(crore) || ' কোটি ';
    END IF;

    IF lakh <> 0 THEN
        text := text || number_chart(lakh) || ' লক্ষ ';
    END IF;

    IF thou <> 0 THEN
        text := text || number_chart(thou) || ' হাজার ';
    END IF;

    IF hund <> 0 THEN
        text := text || number_chart(hund) || ' শত ';
    END IF;

    IF doubl <> 0 THEN
        text := text || number_chart(doubl) || ' ';
    END IF;

    IF deci <> 0 THEN
        text := text || 'এবং ' || number_chart(deci) || ' পয়সা';
    END IF;

    RETURN 'মাত্র ' || text || ' টাকা';
END;
```

## CALL FUNCTION
```sql
SELECT SPEL_OUT_BN(1234567.50) FROM DUAL;
```

## Outpu / Result
```output
মাত্র বারো লক্ষ চৌত্রিশ হাজার পাঁচ শত সাতষট্টি টাকা এবং পঞ্চাশ পয়সা
```

## 🚀 ব্যবহার ক্ষেত্র
- 💰 Salary Payslip
- 🧾 Invoice / Bill Print
- 📑 Oracle APEX Report
- 🏦 Financial Statement


 # Thank you
 ## Sanjay Sikder

 You can connect with me on [LinkedIn](https://www.linkedin.com/in/sanjay-sikder/)!
