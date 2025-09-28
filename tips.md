## Python / コーディングのちょっとした習慣・注意点

### 1. ファイルの末尾改行について
- **Pythonの動作上は不要**  
  → コードが正しく書けていれば、末尾に改行があるかどうかで挙動は変わらない。

- **PEP8（Pythonのスタイルガイド）では推奨**  
  → ファイル末尾に改行を1つ入れるのが望ましい。  
  → 理由: UNIX系の慣習であり、GitHubやdiffツールで「No newline at end of file」という表示を避けられる。

- **Jupyter/Colabのセルでは不要**  
  → セル単位の実行なので、末尾改行を入れても入れなくても問題なし。  
  → ただし、`.py` ファイルに書き出してGitHubに上げる場合は、改行ありがベター。

✅ **まとめ**  
- Colabで学習中 → 気にしなくてOK。  
- GitHubにポートフォリオとしてアップする段階 → **末尾に1つ改行を入れる習慣** をつけるとよい。

### 2. 範囲系の取り違え防止（30秒プレチェック）

- **要件を1行で固定**  
  `out-of-range = not (low <= x < high)`（左含む・右含まない）

- **境界4点をチェック**  
  `x = low-ε, low, high-ε, high` を○×で確認

- **述語を先に定義（読み違い防止）**
```python
def in_range(x, low, high): return low <= x < high
def out_range(x, low, high): return not in_range(x, low, high)
```
- **最小スモークテスト（3行）**

```python
assert not out_range(80, 80, 90)  # 左端は含む
assert out_range(90, 80, 90)      # 右端は含まない
assert out_range(79.9, 80, 90)    # 低すぎる
```

- **名前と条件を一致**
  例：`values_out_of_range` なら `not (low <= x < high)`
