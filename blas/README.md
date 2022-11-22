# Guia biblioteca BLAS

A bibloteca BLAS (Basic Linear Algebra Subprograms) é dividida em 3 níveis.
* Nível 1
  Operações entre vetores e escalar

> Tabela de referência [link](https://netlib.org/blas/blasqr.pdf)


Compilar código com a biblioteca BLAS.
```
gfortran -lblas filename.f90 -o filename.bin
```

## BLAS Nível 1

> Operações relacionadas à escalar-vetor e vetor-vetor

Nesse nível há subrotinas e também funções, que retornam real ou complexo. É muito importante notar como é a estrutura de notação da BLAS, isso porque pode-se encontrar documentação chamando a função DSCAL, ou fazendo referência a função xSCAL, esse x é um prefixo da função/subrotina, e define o tipo de dados e precisão.

Prefixo |     Tipo     | Precisão
:------:|:------------:|:---------:
S       |   real\*4    | Simples
D       |   real\*8    | Dupla
C       |  complex\*8  | Simples
Z       | complexo\*16 | Dupla
