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
seq 100|while read n; do echo "羊が$n匹"; sleep 1; done
```

