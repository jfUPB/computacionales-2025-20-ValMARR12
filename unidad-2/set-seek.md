# Unidad 2

## 🔎 Fase: Set + Seek

### Actividad 01

<img width="1919" height="1030" alt="image" src="https://github.com/user-attachments/assets/6e281554-dc24-46fa-a1f9-2b4dba56307a" />

<img width="1916" height="1028" alt="image" src="https://github.com/user-attachments/assets/cdfa3b8b-408a-4805-a4d7-9fc6075df90e" />

### Actividad 02

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/f7731eee-3307-4379-b315-2f603d114d9b" />

<img width="1919" height="1024" alt="image" src="https://github.com/user-attachments/assets/c2a3ec48-865e-43e3-8ee3-c43388e46120" />

### Actividad 03

```
@SCREEN
M=-1
@CONTADOR
M=0

(LEER)
@KBD
D=M
@100
D=D-A
@DERECHA
D;JEQ

@KBD
D=M
@105
D=D-A
@IZQUIERDA
D;JEQ

(IZQUIERDA)
@CONTADOR
D=M
@SCREEN
A=D+A
M=0

@CONTADOR
M=M-1
D=M
@SCREEN
A=D+A
M=-1

@LEER
0;JMP
```

### Actividad 04

```
// Adds1+...+100.
 @i // i refers to some memory location.
 M=1 // i=1
 @sum // sum refers to some memory location.
 M=0 // sum=0
 (LOOP)
 @i
 D=M // D=i
 @100
 D=D-A // D=i-100
 @END
 D;JGT // If(i-100)>0 gotoEND
 @i
 D=M // D=i
 @sum
 M=D+M // sum=sum+i
 @i
 M=M+1 // i=i+1
 @LOOP
 0;JMP // GotoLOOP
 (END)
 @END
 0;JMP // Infinite loop
```

```
//Adds 1+...+100.
int sum=0;
for(int i = 1; i <=100; i++){
   sum+= i;
}
```
