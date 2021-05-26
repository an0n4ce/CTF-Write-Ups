# GoodBook

![](image/chall.png)

Here we get pdf file of book named `Black Hat Python`.

![](image/pd.png)

Nothing got from there, when we do `binwalk`, we get lots of file and at the bottom it has `Zip Archived file`.

![](image/bin.png)

Let's extract it with `binwalk -e goodbook` command. and list out the files

![](image/bin1.png)

Extract the Zip Archived file to get `flag.txt`.

![](image/flag.txt)

```flag = TamilCTF{3xtr4cti0n_is_n0n3}```
