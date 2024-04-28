# aqt

 .data
vet:
    .word 3, 5, 1, -5, -4
tam:
    .word 5
msg:
    .asciiz "%d\n"
    
    .text
    .globl main

main:
    # Inicializações
    li $t0, 0           # $t0 = i (índice do vetor)
    lw $t1, tam         # $t1 = tam
    lw $t2, vet         # $t2 = endereço base do vetor
    li $t3, 1           # $t3 = r (resultado)
    
loop:
    # Verifica se i < tam
    bge $t0, $t1, end_loop
    
    # Carrega vet[i] para $t4
    sll $t5, $t0, 2      # $t5 = i * 4 (calcula o deslocamento)
    add $t5, $t5, $t2    # $t5 = endereço de vet[i]
    lw $t4, 0($t5)       # $t4 = vet[i]
    
    # Calcula r = r * vet[i]
    mul $t3, $t3, $t4
    
    # Atualiza i
    addi $t0, $t0, 1
    
    # Volta para o início do loop
    j loop

end_loop:
    # Imprime o resultado
    li $v0, 1
    move $a0, $t3
    syscall
    
    # Termina o programa
    li $v0, 10
    syscall






