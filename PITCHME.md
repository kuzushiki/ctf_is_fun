### CTFで学ぶゲームチート入門
@kuzushiki

---

### 自己紹介
kuzushiki（クズシキ）

- CTFが好き
- 4月から某セキュリティ会社に就職予定

---

### CTF?
**C**apture **t**he **f**lag

「セキュリティ技術」を競うコンテスト

ゲーム要素が強く、**楽しい!**

---

### 今日のお題
nullcon HackIM2020にて出題された

**Zelda**という問題

（全４問中３問解説）

![ダウンロード](https://user-images.githubusercontent.com/50363796/76391493-f8ef9200-63b2-11ea-8910-84e0d33523c4.jpg)

---

### Zelda and the Zombies
**ゾンビを倒せ！**

もちろん普通にプレイしても倒せない

---

### ゲームチートのやりかた
(Unityの場合)

1.ゲームフォルダ内の`Assembly-CSharp.dll`を、
2.`dnSpy`という.NET debuggerでいじる

[dnSpyのリポジトリ](https://github.com/0xd4d/dnSpy)

---

@snap[west span-30 text-center]
```
private void TakeDamage(float damage)
{
	this.health -= damage;
	if (this.health <= 0f)
	{
		base.StartCoroutine(this.ShowSome());
		base.gameObject.SetActive(false);
	}
}
```
@snapend

@snap[east span-30 text-center]
```
private void TakeDamage(float damage)
{
	this.health -= damage;
	if (this.health >= 0f) # 体力が0以上なら死亡
	{
		base.StartCoroutine(this.ShowSome());
		base.gameObject.SetActive(false);
	}
}
```
@snapend

---
