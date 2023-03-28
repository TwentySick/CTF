# **Ready Gladiator 0**

## **Description**

![description](/2023/picoctf2023/reverse_engineering/ready_gladiator_0/images/description.png)

## **Solution**

Bài này, mình lấy file về và sửa từ 1 thành 2 vì đề chỉ cần mình không hòa là được rồi

Nội dung file imp.red:
```
;redcode
;name Imp Ex
;assert 1
mov 0, 2
end
```

![solved](/2023/picoctf2023/reverse_engineering/ready_gladiator_0/images/solved.png)

Flag: `picoCTF{h3r0_t0_z3r0_4m1r1gh7_f12e3b7f}`