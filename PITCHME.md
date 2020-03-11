### CTFで学ぶゲームチート入門
<br /><br />
@kuzushiki

---

### 自己紹介
kuzushiki（クズシキ）
<br /><br />
@snap[text-left]
- CTFが好き
- 4月から某セキュリティ会社に就職予定
@snapend

---

### CTFって?
**C**apture **t**he **f**lagの略
<br /><br />
@snap[text-left]
- 「セキュリティ技術」を競うコンテスト  
- ゲーム要素が強く、**楽しい!**
@snapend

---

### 今日のお題

nullcon HackIM2020にて出題された**Zelda**という問題
<br />
（全４問中３問解説）
<br /><br />
![ダウンロード](https://user-images.githubusercontent.com/50363796/76391493-f8ef9200-63b2-11ea-8910-84e0d33523c4.jpg)

---

### Zelda and the Zombies
**ゾンビを倒せ！**  
<br />
普通にプレイしても倒せません

---

### ゲームチートのやりかた
(Unityの場合)
<br /><br />
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
	// 体力が0以上なら死亡するように
	// if (this.health <= 0f)
	if (this.health >= 0f) 
	{
		base.StartCoroutine(this.ShowSome());
		base.gameObject.SetActive(false);
	}
}
```

---

### Zelda at the Swamp
**沼に侵入しろ！**  
<br />
衝突判定があるので入れません

---

### Unityの衝突判定の仕様
@snap[text-left]
オブジェクトごとに`Body Type`が設定されている
<br />
@snap[text-08]
- `Dynamic`: どの`Body Type`とも衝突する
- `Kynematic`: `Dynamic`とのみ衝突する
- `Static`: `Dynamic`とのみ衝突する（**動かせない！**）
@snapend
<br />
結論 -> **`Kynematic`**に設定すれば良い！

---

### キャラクタの`body Type`をいじる
<br />
```C#
public bool isKinematic
	{
		get
		{
			return this.bodyType == RigidbodyType2D.Kinematic;
		}
		set
		{
			// 常時Kinematicに
			// this.bodyType = ((!value) ?
			// RigidbodyType2D.Dynamic : RigidbodyType2D.Kinematic);
			this.bodyType = RigidbodyType2D.Kinematic;
		}
	}
```

---

### Zelda crossing the land's end
**世界の果てに行け！**  
<br />
足が遅いので時間がかかります

---

### Unityの移動速度計算
<br />
```C#
private void MoveCharacter()
{
	this.change.Normalize();
	this.myRigidbody.MovePosition(base.transform.position 
	+ this.change * this.speed * Time.deltaTime);
}
```
<br />
`現在位置 + 移動のベクトル * 速度 * 時間`

---

### キャラクターの移動速度をいじる
<br />
```C#
private void MoveCharacter()
{
	this.change.Normalize();
	// 移動速度を10倍に
	// this.myRigidbody.MovePosition(base.transform.position
	// + this.change * this.speed * Time.deltaTime);
	this.myRigidbody.MovePosition(base.transform.position
	+ this.change * this.speed * Time.deltaTime * 10f);
}
```

---

### まとめ
<br />
@snap[text-left]
CTFを通して、**ゲームチート**の手法を学びました
<br /><br />
CTFの**楽しさ**が少しでも伝われば幸いです
@snapend
