# **Virtual Machine 0**

## **Description**

![description](/2023/picoctf2023/reverse_engineering/virtual_machine_0/images/description.png)

## **Solution**

Sau khi tải file về: 1 file input.txt và 1 file zip. Unzip file zip mình nhận được 1 file đuôi dae. Sau 1 hồi tìm hiểu, mình biết được rằng đây là 1 file của 1 model 3D và bất kỳ phần mềm nào mà có môi trường 3D, làm việc với môi trường 3D và có hỗ trợ file thì đều import được (cũng 1 dạng XML thôi). Và mình đang tiện máy có Unity nên mình import vào Unity vì Unity có hỗ trợ file dae (btw, [Blender](https://www.blender.org/) cũng là 1 lựa chọn ok cho cái này). Sau 1 hồi bóc tách, đây là thành quả mình nhận được

![clean](/2023/picoctf2023/reverse_engineering/virtual_machine_0/images/idontknowitslikeclean.png)

Ở đây mình thấy cái đỏ có 40 bánh răng và cái xanh có 8 cái. Nếu chia tỉ lệ thì 1 vòng bánh đỏ quay được 5 vòng bánh xanh (Cách tính thì tự Google đi :3 ). Và đơn giản chỉ là lấy số vòng quay của file input.txt rồi nhân với tỉ lệ mình vừa tính được là có flag vì ở đây bánh đỏ tượng trưng cho input và bánh xanh tượng trưng cho output

![solved](/2023/picoctf2023/reverse_engineering/virtual_machine_0/images/solved.png)

Flag: `picoCTF{g34r5_0f_m0r3_8a379284}`
