# Generic Platformer
## Challenge
![challenge](/2022/TUCTF2022/reverse_engineering/generic_platformer/images/challenge.png)

[File](/2022/TUCTF2022/reverse_engineering/generic_platformer/game.zip)

## Solution
Đây là một con game Unity, và mình đã chơi thử game với suy nghĩ nó sẽ có gì đó mình không thể thắng và phải can thiệp vào các file của game. Nhưng mình đã nhầm, game dễ vkl và khi thắng cũng chẳng có gì hiện ra. Nên mình đã quyết định vọc vạch các folder xem có gì bên trong đó.

Nhờ vài lần chơi CTF có challenge với game tạo bằng Unity, `Assembly-CSharp.dll` là file đầu tiên mình hướng tới và tìm kiếm. Nhưng không, tìm tới tìm lui không thấy đâu. Sau một hồi tìm kiếm trên mạng và mình phát hiện có folder il2cpp_data, tức là có dính dáng tới `il2cppDumper`, và nó sẽ ở file GameAssembly.dll (theo hướng dẫn trên mạng là thế). Nhưng không, lại 1 lần nữa sai. il2cpp có mặt thật nhưng nó ở file `msvcbin.dll`