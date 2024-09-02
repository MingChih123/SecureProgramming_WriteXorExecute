# Secure Programming 
| 學號 | 組員 | 負責 |
|------|------|------|
| 1102924 | 李名智 | Write XOR Execute (W^X) |
| 1102932 | 林微訢 | Address Space Layout Randomization (ASLR) |
| 1102943 | 顏莉諭 | Stack Smashing Protection (SSP) |
| 1102962 | 鍾佳妘 | Return-oriented Programming (ROP) |

# Buffer Overflow, Shell Code, and Advanced Protection
## 摘要
主要介紹一些保護機制和攻擊。要如何做到保護的效果?又能靠甚麼攻擊技術來繞過保護機制呢?這邊針對Write XOR Execute來作詳細說明。
## 介紹內容
- [簡單介紹](https://github.com/MingChih123/SecureProgramming_WriteXorExecute/blob/main/%E8%B3%87%E5%AE%89%E5%A0%B1%E5%91%8A_%E9%A7%AD%E5%AE%A2%E6%94%BB%E9%98%B2.pdf)
- 保護機制：  
  - Write XOR Execute (W^X)[（詳細說明）](https://github.com/MingChih123/SecureProgramming_WriteXorExecute/blob/main/Secure%20Programming_WxorX.pdf)
  - Stack Smashing Protection (SSP)
  - Address Space Layout Randomization (ASLR)  
- 攻擊：  
  - Return-oriented Programming (ROP)  
## Write Xor Execute（W^X）
### Write XOR Execute介紹
- 「寫入 XOR 執行」（Write XOR Execute，簡稱 W^X）是一種安全技術（記憶體保護策略）。
- 理念：將記憶體區域設置為「可寫」或「可執行」，但不能同時具備這兩種權限。
- 目的：防止攻擊者利用可寫記憶體區域來注入並執行惡意程式碼。
### 啟用W^X保護機制流程圖
![image](https://github.com/user-attachments/assets/922b2a1e-4e2d-40f6-8a62-89decbc51254)  
[圖片來源](https://introspelliam.github.io/2017/09/30/linux%E7%A8%8B%E5%BA%8F%E7%9A%84%E5%B8%B8%E7%94%A8%E4%BF%9D%E6%8A%A4%E6%9C%BA%E5%88%B6/)  

### W^X保護策略
- W^X保護策略：防止記憶體區域同時具備可寫和可執行權限。
- 有關記憶體區域的攻擊：
  - 緩衝區溢出攻擊（覆蓋return address，注入並執行）
  - ROP攻擊（不需注入惡意程式碼，可繞過此保護策略）
- 實現W^X保護方式：在編譯過程中不使用```-z execstack```
  - ```-z execstack```：允許執行堆疊。
  - ```gcc -o safeTest Test.c （-z noexecstack）```
### 實作 使用W^X保護方法、安全屬性
![image](https://github.com/user-attachments/assets/53cd70c0-8338-446e-8593-9a52caf0ee8f)
