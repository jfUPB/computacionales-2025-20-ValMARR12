# Unidad 1

## 🛠 Fase: Apply

#### actividad 3

```
(LOOP)

@5
D=M
@10
D=D-A

@MENOR
D;JTL

(MAYOR)
@7
M=0
@LOOP
0;JMP

(MENOR)
@7
M=1
@LOOP
0;JMP
```
#### actividad 4

reconoci que para este progrma necesite un contador ya que para sumar los numeros entre 1 y 5 no se podia hacer directamente, lo que hice es que busque como hacer un contador en este sistema de codigo y se uso el uso del loop, asi que lo que procedi a desarrollar el codigo con el contador  que cuando el contador pase del numero 5 salte a END pero asi mismo el contador sirve para ir sumando ya que cuando se hace la suma se suma los valores en A (osea cual es la cantidad que llevamos de la suma) con lo que esta en el contador hasta que nos da 15

```
@12
M=0
@13
M=1
(LOOP)
@13
D=M
@5
D=D-A
@END
D;JGT
@12
D=M
@13
A=M
D=D+A
@12
M=D
@13
M=M+1
@LOOP
0;JMP
(END)
@13
M=0
(END_A)
@END_A
0;JMP
```
