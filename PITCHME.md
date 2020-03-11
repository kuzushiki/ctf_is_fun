### CTFで学ぶゲームチート入門
<br />
@kuzushiki

---

### 自己紹介
kuzushiki（クズシキ）
<br />
@snap[text-left]
- CTFが好き
- 4月から某セキュリティ会社に就職予定
@snapend

---

### CTF?
@snap[text-left]
**C**apture **t**he **f**lag
<br />
「セキュリティ技術」を競うコンテスト  
ゲーム要素が強く、**楽しい!**
@snapend

---

### 今日のお題
@snap[text-left]
nullcon HackIM2020にて出題された**Zelda**という問題

（全４問中３問解説）
<br />  
@snapend
![ダウンロード](https://user-images.githubusercontent.com/50363796/76391493-f8ef9200-63b2-11ea-8910-84e0d33523c4.jpg)

---

### Zelda and the Zombies
**ゾンビを倒せ！**  
<br />
もちろん普通にプレイしても倒せない

---

### ゲームチートのやりかた
(Unityの場合)
<br />  
@snap[text-left]
1.ゲームフォルダ内の`Assembly-CSharp.dll`を、
2.`dnSpy`という.NET debuggerでいじる
<br />
[dnSpyのリポジトリ](https://github.com/0xd4d/dnSpy)
@snapend

---

### 死亡判定をいじる
<br />
```C#
private void TakeDamage(float damage)
{
	this.health -= damage;
	// if (this.health <= 0f)
	if (this.health >= 0f) // 体力が0以上なら死亡
	{
		base.StartCoroutine(this.ShowSome());
		base.gameObject.SetActive(false);
	}
}
```

---
