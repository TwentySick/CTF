# **No way out**

## **Description**

![description](/2023/picoctf2023/reverse_engineering/no_way_out/images/description.png)

## **Solution**

Đây là 1 con game làm từ Unity, và như mọi lần mình gặp game Unity, mình sẽ để ý file "Assembly-CSharp.dll" đầu tiên và decompile nó. Mình cũng đã chơi qua con game và mình sẽ không thể nhảy qua được bức tường để đến với cột cờ

[![Original](/2023/picoctf2023/reverse_engineering/no_way_out/images/image.png)](/2023/picoctf2023/reverse_engineering/no_way_out/images/original.mp4)

Mình đã decompile file "Assembly-CSharp.dll" và tìm đến chỗ xử lý "Jump" để sửa lại

Trước khi sửa

![Before](/2023/picoctf2023/reverse_engineering/no_way_out/images/beforePatch.png)

Sau khi sửa

![After](/2023/picoctf2023/reverse_engineering/no_way_out/images/afterPatch.png)

Và sau đó mình Save lại (giống kiểu patch rồi export ý), vào game và Smoke W**d everyday

[![Original](/2023/picoctf2023/reverse_engineering/no_way_out/images/image.png)](/2023/picoctf2023/reverse_engineering/no_way_out/images/edited.mp4)

Mình đi bộ đến cái cờ và nhận được flag

![getFlag](/2023/picoctf2023/reverse_engineering/no_way_out/images/getFlag.png)

Flag: `picoCTF{WELCOME_TO_UNITY!!}`