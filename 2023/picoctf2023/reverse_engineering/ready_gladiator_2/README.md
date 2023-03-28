# **Ready Gladiator 2**

## **Description**

![description](/2023/picoctf2023/reverse_engineering/ready_gladiator_2/images/description.png)

## **Solution**

Bài này mình đi loot [warrior](http://moscova.inria.fr/~doligez/corewar/rc/frenzyv6.txt) và sửa lại 1 chút :3 (thanks so much bro)

Nội dung file imp.red:
```
;redcode
;name Imp Ex
;assert 1
            org   boot

step        equ   3000

start       add   #step+step,2
            mov   bomb, @1
            mov   bomb, @1
cl          jmp   -3,   >-8         ;hit to start clear
            mov   dbomb,      >start-4
            djn.f -1,   >start-4
dbomb       dat.f <5334,      dbomb-start+7
bomb        spl   #0,   #step

for 83
            dat   0,    0
rof

boot        mov   bomb, 2000
for 7
            mov   {boot,      <boot
rof
            jmp   @boot,      <-1000
end
```

![solved](/2023/picoctf2023/reverse_engineering/ready_gladiator_2/images/solved.png)

Flag: `picoCTF{d3m0n_3xpung3r_c6d2591d}` 

