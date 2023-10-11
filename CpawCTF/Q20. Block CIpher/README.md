## 問題

> 与えられたC言語のソースコードを読み解いて復号してフラグを手にれましょう。
>
> 暗号文：cpaw{ruoYced_ehpigniriks_i_llrg_stae}
>
> crypto100.c

## 解法

`crypto100.c`が与えられるので、まずは読んでみる。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
int main(int argc, char* argv[]){
  int i;
  int j;
  int key = atoi(argv[2]);
  const char* flag = argv[1];
  printf("cpaw{");
  for(i = key - 1; i <= strlen(flag); i+=key) for(j = i; j>= i - key + 1; j--) printf("%c", flag[j]);
  printf("}");
  return 0;
}
```

このスクリプトは、引数に文字列の`flag`と数値の`key`を取る。

`for`の中は、`key`の値ごとに文字列を分割して、そのブロック毎に逆順で出力しています。
なので、同じことを再度実行してあげれば、元に戻せます。

せっかくなので、pythonでスクリプトを書く。

```python
flag = "ruoYced_ehpigniriks_i_llrg_stae"

def padding(data, block_size, letter=' '):
    if len(data) % block_size == 0:
        block_num = len(data) // block_size
    else:
        block_num = len(data) // block_size + 1
    return data.ljust(block_num*block_size, letter)

def encode(data, block_size):
    block_num = len(data) // block_size

    data = padding(data, block_size)

    key = ""
    for i in range(block_num+1):
        block_str = data[i*block_size:(i+1)*block_size]
        key += block_str[::-1]
    return(key)

if __name__ == '__main__':
    for i in range(1, 11):
        key = i
        print("key: " + str(key) + ";", end=" ")
        print("cpaw{", end='')
        print(encode(flag, key), end='')
        print("}")
```

```bash
$ python .\answer.py
key: 1; cpaw{ruoYced_ehpigniriks_i_llrg_stae}
key: 2; cpaw{urYoec_dheipngriki_s_illgrs_at e}
key: 3; cpaw{ourecYe_diphingkiri_sll__grats  e}
key: 4; cpaw{Your_deciphering_skill_is_gr eat}
key: 5; cpaw{cYourhe_deingip_skirrll_iats_g    e}
key: 6; cpaw{ecYouriphe_dkiringll_i_sats_gr     e}
key: 7; cpaw{decYourngiphe_i_skiris_grll_    eat}
key: 8; cpaw{_decYourringiphell_i_ski eats_gr}
key: 9; cpaw{e_decYourkiringiph_grll_i_s     eats}
key: 10; cpaw{he_decYour_skiringipats_grll_i         e}
```

実行してあげると、`key == 4`の時、解読できる文字列になる。
提出の際は、余剰なスペースは消去しました。