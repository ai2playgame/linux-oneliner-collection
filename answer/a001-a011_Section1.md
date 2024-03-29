## Q1

```bash
$ cat shellgei160/qdata/1/files.txt | grep '\.exe$'
$ cat shellgei160/qdata/1/files.txt | sed -n '/\.exe$/p'
```

memo:
sedの-nオプションは、各行を自動的に出力しないというオプション。
sedのpフラグと合わせて使うことで、正規表現と一致する行だけ出力することができる。

## Q2

```bash
$ ls *.png | sed 's/\.png$//' | xargs -I@ convert @.png @.jpg
```

カレントディレクトリにあるpngをまとめてjpgに変換するワンライナー。
`xargs -I`の使い所がミソ。

```bash
$ ls *.png | sed 's/\.png$//' | xargs -P2 -I@ convert @.png @.jpg
```

`-P2`と指定すると、convertが2個同時に実行されて早い。

## Q5

```bash
$ grep -E '^\s*pool\s+' ntp.conf | awk '{print $2}'
$ cat ntp.conf | awk '$1=="pool"' | awk '{print $2}'
$ cat npt.conf | awk '$1=="pool"{print $2}'
```

## Q6

```bash
$ seq 5 | awk '{for(i=1;i<$1;++i){printf " "};print "x"}' | tac
$ seq 5 | awk '{for(i=5;i>$1;--i){printf " "};print "x"}'
```

## Q7

```bash
$ cat ./shellgei160/qdata/7/kakeibo.txt | awk '{tax=(<=20190931||~^*)?1.08:1.10; print , tax}' | awk '{print int(*)}' | awk '{s+=}END{print s}'
```

## Q8

```bash
$ cat ./shellgei160/qdata/8/access.log | awk '{print $4}'| awk -F/ '{print $3}'|awk -F: '{if($2<=11){a++}else{b++}}END{print "午前 " a; print "午後 " b;}'
$ cat shellgei160/qdata/8/access.log | grep -o '..:..:.. +0900'|sed 's/:.*//'|awk '{print $1<"12" ? "午前" : "午後"}'|sort|uniq -c 
```

## Q9

`sed -n '/正規表現/p'`で、正規表現にマッチした行だけ表示する
これを応用して、
`sed -n '/正規表現1/,/正規表現2/p'`で正規表現1にマッチした行と正規表現2にマッチした行までのすべてを抽出できる

```bash
$ cat shellgei160/qdata/9/log_range.log | awk '$4" "$5>="[24/Dec/2016:21:00:00]" && $4" "$5<"[25/Dec/2016 03:59:60]"' 
$ cat shellgei160/qdata/9/log_range.log |sed -n '/24\/Dec\/2016 21:/,/25\/Dec\/2016 03:/p' 
```

## Q10

sedの-rオプションで拡張正規表現モードに。
()で囲んだ部分を\1で使い回す

```bash
$ cat shellgei160/qdata/10/headings.md | sed -r 's/^## +(.*)/\1\n---/' | sed -r 's/^# +(.*)/\1\n===/'
```

## Q11

xargs -n2で2行のごとのechoが作れる

```bash
$ cat shellgei160/qdata/11/gijiroku.txt | xargs -n2 | sed 's/^すず/鈴木/;s/^さと/佐藤/;s/やま/山田/;'|sed 's/ /:/;s/$/\n/'
```

