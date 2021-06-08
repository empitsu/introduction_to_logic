---
marp: true
---



# 実務に役立つかもしれない数理論理学

---

# 自己紹介

フロントエンドチームのempitsuです。  
React/TypeScript書いたりしています。  

2020年1月からアメリカの通信制大学に入ってコンピューターサイエンスを学び直し中です。


---

# 今日のテーマ

今日のテーマはフロントエンドには1ミリも関係なく、数学の話です。

めちゃくちゃ数学には苦手意識があったので最近数学を学び直し中です。  
（高校数学／離散数学／線形代数あたり）


ちゃんとComputer Scienceや数学を学んでる方も多いと思うので~~ボコボコにされにきました~~  
超基礎的な内容ばかりですが、間違いや正確さに書ける表現は優しくフィードバックいただけたら嬉しいです。

---


# 数理論理学 - Mathematical logic とは

いつも我々が使っている `Boolean` というデータ型。  
これは論理推論を代数で展開する「ブール代数」を考案したジョージ・ブール（1815-1864）に由来する (Wikipedia, 2021a)。


---

* 数理論理学は離散数学の一分野だが、数学の基礎知識。(伊藤, 2019, p41)
* 科学的思考の基礎となる重要な概念。(伊藤, 2019, p.41)
* 高校数学では数学Ⅰ「集合と命題」というトピックで触れる。

---

## 離散数学とは

* 「離散」とは「連続」の反対。「とびとび」になっているものを対象とした数学。  
対照的なのが微積分などの解析学で、それらは連続な対象を扱う。(伊藤, 2019, p1)
* 計算機は0と1の2つの信号を扱うことから、離散数学の守備範囲。離散数学なしに計算機は動かない。(伊藤, 2019, p.1)
  
  

普段プログラミングしている私達は論理で飯を食っていると言っても過言ではない（過言）


---

# Vocabulary

---

## 真理値 - truth value, logical value

* 真 - trueまたは1
* 偽 - falseまたは0

---

## 論理変数 - Logical variable

* 真理値を取る変数。
* PとかQとかRが使われることが多いが、なんでもよい。

---

## ステートメント - Statement

真または偽を表す平叙文 `Declarative sentence` (Levin, 2019, chapter 0.2)。

平叙文とは、疑問文・感嘆文・命令文とは違って普通に終わる文。

ステートメントは命題論理式 `Propositional logical expression`とか単に命題 `Proposition` とも言う場合もある (Levin, 2019, chapter 3.1; 伊藤,2019, p.43 )。


---

## Atomic statement

Statementのうち、これ以上分割できない文を `Atomic statement` という (Levin, 2019, chapter 0.2)。

* 地球は四角い。（偽）
* 3 + 7 = 10 （真）
* 5 > 6（偽）

---

## Molecular statement 

Atomic statementに分割できるものは `Molecular statement` (Levin, 2019, chapter 0.2)。

* 背中をトントンすれば、娘は寝る（真）
    * P:「背中をトントンする」（真）
    * Q:「娘は寝る」（真）
    * 論理演算子を使って`P→Q` と書ける
* [JavaScript] `4 > 3 && false` （偽）
    * P: `4 > 3` （真）
    * Q: `false`
    * 論理演算子を使って `P ∧ Q` と書ける

---

## 論理演算子 - Logical operator, Logical connectives

論理演算子を使用してMolecular statementを作成することができる。

* `¬ `
    * not 
    * 否定 - Negation
    * JavaScriptだと`!`

---

* `∧`
    * and
    * 論理積 - conjunction
    * JavaScriptだと `&&`
* `∨`
    * or
    * 論理和 - disjunction
    * JavaScriptだと `||`

---

* `⇒` または`→`
    * if ... then ...
    * 包含 - implication, conditional
* `⇔`
    * if and only if ...
    * 双条件 - biconditional

(Levin, 2019, chapter 0.2; Wikipedia, 2021b)

徐々にプログラミングとのつながりが見えてきましたね


---

## 論理演算子の優先順

優先度が高い順に

> ¬  
> ∧  
> ∨  
> ⇒ ⇔  

(Stanford University, n.d.)

---

JavaScriptも同じですね。

以下の順で演算子が適用されます。

> 否定	!   
> 論理積	&&  
> 論理和	||  

(Mozilla and individual contributors, 2021)

---

なので、`x > 5 || y === 3`を先に評価させるつもりで以下のような条件式を書いたら意図と違った結果になってしまいます。

```
if(x > 5 || y === 3 && isChecked)
```


より優先度の高い演算子 `()`を使って上書きしましょう。

```
if((x > 5 || y === 3) && isChecked)
```

---

## 真理値表 - Truth tableとは

| P | Q | P∨Q | P∧Q | ¬P | P⇒Q | ¬P∧Q | P⇔Q |
|--:|--:|--:|--:|--:|--:|--:|--:|
| 0 | 0 | 0 | 0 | 1 | 1 | 0 | 1 |
| 0 | 1 | 1 | 0 | 1 | 1 | 1 | 0 |
| 1 | 0 | 1 | 0 | 0 | 0 | 0 | 0 |
| 1 | 1 | 1 | 1 | 0 | 1 | 0 | 1 |

---

こういう表を真理値表といいます。

基本情報技術者試験でも出てきたような気がします。  
複雑な条件式を読んだり書いたりするときに、真理値表を書くと整理しやすいかもしれません。  
~~まあconsoleで実際にコードを書いて出力してみるのが一番早いんですけど…~~

ちなみに世の中にはTruth table generatorという便利なツールがあります。

https://web.stanford.edu/class/cs103/tools/truth-table-tool/


---

# 論理学のちょっとおもしろい話

`P→Q`がPが真、Qが偽のときだけ結果が偽になり、あとはすべて真になるのにお気づきでしょうか。  
Pが偽でも常に結果が真になります。

| P | Q | P⇒Q |
|--:|--:|--:|
| 0 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

---

さきほどのこちら。

* 背中をトントンすれば、娘は寝る（真）
    * P:「背中をトントンする」（真）
    * Q:「娘は寝る」（真）
    * 論理演算子を使って`P→Q` と書ける


---

Pを  
`「背中をトントンしない」（偽）`  
としてみたらどうでしょう。

この場合でも、「背中をトントンしないが娘は寝る」というステートメントは **「真」** になります。  

なぜなら、さきほどの「背中をトントンすれば、娘は寝る」はPが真（背中をトントンする）の場合のことしか決めていないためです。  
Pが偽の（背中をトントンしない）場合どうなるかは何も決めていないので、結果はどうあれステートメントには反してないのです (伊藤, 2019, p. 44)。




---

つまり、以下の奇妙なステートメントは **論理学的には真になります** 。  
前半のifの部分（P)が偽になるのでQに何が書いてあるかは関係がありません。 以下のP→Qの真理値は真です。

* 地球は平坦なので、海は凍らない（真）
  * P: 地球は平坦である（偽）
  * Q: 海は凍らない（偽）
  * P → Q （真）
* 8が素数ならば、円周率の7624番目は8になる（真）
  * P: 8が素数（偽）
  * Q: 円周率の7624番目は8（？？調べるのが面倒）
  * P → Q （真）
    * 「円周率の7624番目は8」が真であろうと偽であろうとP→Qは真

---

# 論理式はベン図でも表現できます

## Pがtrue

![image.png](https://upload.wikimedia.org/wikipedia/commons/thumb/1/10/Venn0101.svg/200px-Venn0101.svg.png)
(Wikipedia, 2021b)

---

##  Qがtrue

![image.png](https://upload.wikimedia.org/wikipedia/commons/thumb/7/76/Venn0011.svg/200px-Venn0011.svg.png)
(Wikipedia, 2021b)

---

##  ¬Q

![image.png](https://upload.wikimedia.org/wikipedia/commons/thumb/3/31/Venn1100.svg/200px-Venn1100.svg.png)
(Wikipedia, 2021b)

---

## ¬P

![image.png](https://upload.wikimedia.org/wikipedia/commons/thumb/e/eb/Venn1010.svg/200px-Venn1010.svg.png)
(Wikipedia, 2021b)

---

## P ∧Q (conjunction)


![conjunction](https://upload.wikimedia.org/wikipedia/commons/thumb/9/99/Venn0001.svg/200px-Venn0001.svg.png)
(Wikipedia, 2021b)

---

## P∨Q (disjunction)

![image.png](https://upload.wikimedia.org/wikipedia/commons/thumb/3/30/Venn0111.svg/200px-Venn0111.svg.png)
(Wikipedia, 2021b)

---

## P→Q (implication)

![image.png](https://upload.wikimedia.org/wikipedia/commons/thumb/1/1e/Venn1011.svg/200px-Venn1011.svg.png)
(Wikipedia, 2021b)

---

## P⇔Q (biconditional)

![image.png](https://upload.wikimedia.org/wikipedia/commons/thumb/4/47/Venn1001.svg/200px-Venn1001.svg.png)
(Wikipedia, 2021b)

わけがわからなくなったらベン図を書けば、シンプルな条件文に書き換えられるかもしれないですね。

---

# ドモルガンの法則

* `¬(P∨Q)=(¬P)∧(¬Q)`
* `¬(P∧Q)=(¬P)∨(¬Q)`

(伊藤, 2019, p. 45)

これも基本情報技術者試験や高校の数学1で出てきた気がしますね。

真理値表やベン図を書けば、両辺が一致することは簡単にわかります。

---

## `¬(P ∨ Q) = (¬P) ∧ (¬Q)`

```
if(x !== 5 && !y )
```

↓

```
if(!(x === 5 || y))
```

---

## `¬(P∧Q) = (¬P) ∧ (¬Q)`

```
if(x !== 5  || !y )
```

↓

```
if(!(x === 5 && y))
```

これを覚えておけば、複雑で分かりづらい条件式も少しリファクタできるかもしれません。

---

# 命題論理式における様々な性質

他にも様々な性質があります



---

## 排中律(excluded-middle law)

* `P V ¬P = 1`
* `P ∧ ¬P = 0`



##  冪等律 (idempotence law)

* `P ∨ P = P`
* `P ∧ P = P`

---

## 交換律(commutative law)

* `P ∨ Q = Q ∨ P`
* `P ∧ Q = Q ∧ P`
* `P ∨ Q = Q ∨ P`
* `P ∧ Q = Q ∧ P`

## 結合律(associative law)

* `P ∨ (Q ∨ R) = (P ∨ Q) ∨ R`
* `P ∧ (Q ∧ R) = (P ∧ Q) ∧ R`
* `P ∨ (Q ∨ R) = (P ∨ Q) ∨ R`
* `P ∧ (Q ∧ R) = (P ∧ Q) ∧ R`

(伊藤, 2019, p. 45)

ここらへんまでは「そりゃそうですね」って感じですね

---

## 分配律(distributive law)

* `P ∨ (Q ∧ R) = (P ∨ Q)∧ (P ∨ R)`
* `P ∧ (Q ∨ R) = (P ∧ Q)∨ (P ∧ R)`
* `P ∨ (Q ∧ R) = (P ∨ Q)∧(P ∨ R)`
* `P ∧ (Q ∨ R) = (P ∧ Q)∨(P ∧ R)`


## 吸収律(absorption law)

* `P ∨ (P ∧ Q) = P`
* `P ∧ (P ∨ Q) = P`
* `P ∨ (P ∧ Q) = P`
* `P ∧ (P ∨ Q) = P`

(伊藤, 2019, p. 45)

この分配律と吸収律は覚えておくと役立つかもしれません。

---

#  まとめ

* 0と1を扱う論理学は離散数学の基礎
* 論理は科学的思考の基礎となる重要な概念。
* 計算機も0と1の2つの信号を扱うことから、離散数学の守備範囲。
* ステートメントは真または偽を表わす文。
* 論理演算子を使用してmolecular ステートメントを作成できる。
* 真理値表やベン図で論理演算の結果を整理できる
* ド・モルガンの定理など論理式の様々な性質を知っていたら業務でも役立つかもしれない

---

# 参考文献


* Levin, O. (2019). Discrete mathematics: An open introduction (3 edition). CreateSpace Independent Publishing Platform. http://discrete.openmathbooks.org/dmoi3.html
* Mozilla and individual contributors. (2021). 式と演算子. MDN Web Docs. https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Expressions_and_Operators
* Stanford University. (n.d.). Stanford Introduction to Logic. http://intrologic.stanford.edu/glossary/operator_precedence.html
* 伊藤大雄 (2019) [イラストで学ぶ離散数学](https://www.amazon.co.jp/dp/B081N8V5SC/ref=cm_sw_r_tw_dp_x_nSU0FbFA3VV0R) 講談社
* ジョージ・ブール (2021a, May 24) In Wikipedia. https://ja.wikipedia.org/wiki/%E3%82%B8%E3%83%A7%E3%83%BC%E3%82%B8%E3%83%BB%E3%83%96%E3%83%BC%E3%83%AB
* 論理演算 (2021b, Mar 18) In Wikipedia. https://ja.wikipedia.org/wiki/%E8%AB%96%E7%90%86%E6%BC%94%E7%AE%97
