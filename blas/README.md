# Guia biblioteca BLAS

A bibloteca [BLAS](https://netlib.org/blas/#_blas_routines) (Basic Linear Algebra Subprograms) é dividida em 3 níveis.

* Nível 1
  Operações entre vetores e escalar
* Nível 2
  Operações entre vetor e matriz
* Nível 3
  Operações entre matrizes
  
Nesse guia irei me ater apenas as subrotinas padrões, porém isso deve ser o sucifiente para ler a documentação sem problemas.

Compilar código com a biblioteca BLAS.
~~~
gfortran -lblas filename.f90 -o filename.bin
~~~

## BLAS Nível 1

> Operações relacionadas à escalar-vetor e vetor-vetor

Nesse nível há subrotinas e também funções, que retornam real ou complexo. É muito importante notar como é a estrutura de notação da BLAS, isso porque pode-se encontrar documentação chamando a subrotina DSCAL, ou fazendo referência a subrotina xSCAL, esse x é um prefixo da função/subrotina, e define o tipo de dados e precisão.

Prefixo |     Tipo     | Precisão
:------:|:------------:|:---------:
S       |   real\*4    | Simples
D       |   real\*8    | Dupla
C       |  complex\*8  | Simples
Z       | complexo\*16 | Dupla

Exemplo de código usando precisão simples, da subrotina de multiplicar um escalar com um vetor:

~~~fortran
program blas_nivel_1
  implicit none

  integer, parameter :: tamanho = 3
  real(4) :: escalar_a, norma_x
  real(4), dimension(tamanho) :: vetor_x
  
  real, external :: SNRM2
  
  escalar_a = 2
  vetor_x = 1.0
 
  print *, 'Escalar a:', escalar_a
  print *, 'Vetor x:', vetor_x

  print *, ''

  print *, 'SSCAL(N, SA, SX, INCX)'
  call SSCAL(tamanho, escalar_a, vetor_x, 1)
  print *, 'Vetor x:', vetor_x
  
  print *, ''

  print *, 'SNRM2(N, SX, INCX)'
  norma_x = SNRM2(tamanho, vetor_x, 1)
  print *, 'Norma x:', norma_x

end program blas_nivel_1
~~~
Saída:
~~~
Escalar a:   2.00000000    
Vetor x:   1.00000000       1.00000000       1.00000000    

SSCAL(N, SA, SX, INCX)
Vetor x:   2.00000000       2.00000000       2.00000000    

SNRM2(N, SX, INCX)
Norma x:   3.46410155
~~~

Segue uma tabela com algumas das funções de nível 1:

Função|      Paramêtros      | Operação | Prefixos 
:----:|:--------------------:|:--------:|:--------:
xDOT  | N, X, INCX, Y, INCY  | Protudo Escalar | S, D, DS
xNRM2 | N, X, INCX           | Norma           | S, D, SC, DZ
xASUM | N, X, INCX           | Soma das componentes | S, D, SC, DZ
IxAMAX| N, X, INCX           | Maior componente | S, D, C, Z


Segue uma tabela com algumas das subrotinas de nível 1:

Função|      Paramêtros      | Operação | Prefixos 
:----:|:--------------------:|:--------:|:--------:
xSWAP | N,    X, INCX, Y, INCY  | X, Y = Y, X | S, D, C, Z
xSCAL | N, A, X, INCX           | X = A*X     | S, D, C, Z
xCOPY | N, X, INCX, Y, INCY     | Y = X       | S, D, C, Z
xAXPY | N, A, X, INCX, Y, INCY  | Y = A*X +Y  | S, D, C, Z
