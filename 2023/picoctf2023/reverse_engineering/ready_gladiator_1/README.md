# **Ready Gladiator 1**

## **Description**

![description](/2023/picoctf2023/reverse_engineering/ready_gladiator_1/images/description.png)

## **Solution**

Bài này mình đi loot [warrior](https://github.com/rodrigosetti/corewar/blob/master/warriors/juggernaut.red) :3 (thanks so much bro)

Nội dung file imp.red:
```
;redcode
;name Imp Ex
;assert 1
      ORG	2
      DAT.F  #0        , #7       
      DAT.F  #0        , #13      
      MOV.I  <-2       , <-1      
      JMN.B  $-1       , $-3      
      MOV.AB #7        , $3       
      MOV.AB #13       , $3       
      JMP.B  $3        , $0  
end
```

![solved](/2023/picoctf2023/reverse_engineering/ready_gladiator_1/images/solved.png)

Flag: `picoCTF{1mp_1n_7h3_cr055h41r5_f2ba3220}`