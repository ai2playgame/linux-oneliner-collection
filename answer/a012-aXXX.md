# Q12

# Q13

```bash
$ cat <> unfile
```

<>はリダイレクト記号。

`cat < unfile`だけだと、unfileの入力を受け取ってcatする
`cat > unfile`だけだと、catからの書き出しに備えてbashが空のunfileを生成して、catの出力をunfileに書き出す
unfileがあれば、`cat > unfile`でなにもしない。

# Q14

```bash
$ seq 100|while read n; do echo "羊が$n匹"; sleep 1; done
$ n=1;while [ $n -le 5 ]; do echo "羊が$n匹";sleep 1;n=$((n+1)); done
```

# Q15

```bash
$ echo I am a perfect human | while read a; do echo ${a^^}; done
```

# Q16

```bash
n="XYZ"; (for i in {A..C}; do n+=$i; echo $n; done); echo $n
```

括弧で囲んで、for内の変数の書き換えをサブシェルに押し込めて、最後のechoに影響しないようにした
