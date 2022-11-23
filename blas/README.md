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
program escalar_vetor
  implicit none
  integer, parameter :: tamanho = 3
  real(4) :: escalar_a
  real(4), dimension(tamanho) :: vetor_x
  
  escalar_a = 2
  vetor_x = 1.0
 
  print *, 'Escalar a:', escalar_a
  print *, 'Vetor x:', vetor_x

  print *, ''

  print *, 'SSCAL(N, SA, SX, INCX)'
  call SSCAL(tamanho, escalar_a, vetor_x, 1)
  print *, 'Vetor x:', vetor_x

end program escalar_vetor
~~~
~~~
Escalar a:   2.00000000    
Vetor x:   1.00000000       1.00000000       1.00000000    

SSCAL(N, SA, SX, INCX)
Vetor x:   2.00000000       2.00000000       2.00000000
~~~
