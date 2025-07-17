# Unidad 1

## 🔎 Fase: Set + Seek

### Actividad 01

el propocito de esta actividad es entender como funciona el Ciclo fetch-decode-execute.¿que sera el fetch? ¿que es el de code? ¿que es execute?

``` asm
@1
D=A
@2
D=D+A
@16
M=D
@END
(END)
0;JMP
```

¿que hara este codigo?

lo que hace el codigo es que suma dos numeros indicados por el @ y en A se muestra el registo actual en D se muestra el resultado del registro osea la suma, despues se pone en un @ la linea en la ram que se deesa guardar y despues del arroba de M=D para que la computadora lo guarde en la ram, al final sencilla mente se pone el END para y el JMP para que la computadora no siga 

ejemplo impuesto en la clase

``` asm
@5
D=A
@10
D=D+A
@20
M=D
@END
(END)
0;JMP
```

otro ejemplo

``` asm
@SCREEN
D=A
@i
M=D
(READKEYBOARD)
@KBD
D=M
@KEYPRESSED
D;JNE
@i
D=M
@SCREEN
D=D-A
@READKEYBOARD
D;JLE
@i
M=M-1
A=M
M=0
@READKEYBOARD
0;JMP

(KEYPRESSED)
@i
D=M
@KBD
D=D-A
@READKEYBOARD
D;JGE
@16
A=M
M=-1
@i
M=M+1
@READKEYBOARD
0;JMP
``` 
