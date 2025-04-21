# Tinh tong tu 1 den n
```x86asm
ORG 100h 
.model small
.stack 100
.data
tb1 db 13,"Nhap vao mot so n: $" 
tb2 db 10,13,"Tong so tu 1->n: $"
buffer db 10,?,10 dup('$')
str db 100 dup ('$')
n db ?
tong dw ?
.code
main proc
    mov ax,@data
    mov ds,ax
    
    lea dx,tb1
    mov ah,09h
    int 21h
    
    mov ah,10
    lea dx,buffer
    int 21h
    mov al, buffer+2
    sub al,30h
    mov ah, buffer+3
    sub ah,30h
   kiem_tra:
    cmp ah,0
    jl so_2
    mov cl,ah
    mov bl,10
    mul bl 
    add al,cl
   so_2: 
    mov ah,0
    mov cx,ax
    mov bl,0
    
    mov ah,9
    lea dx,tb2
    int 21h
    
    mov ax,0
    mov bx,1
  sum:
    add ax,bx
    inc bx
    cmp bx,cx
    jbe sum
    
    mov tong,ax
    
  in_so proc
    push bx
    push ax
    push cx
    
    mov bx,10
    mov cx,0             
   chia_so:
    mov dx,0
    div bx
    push dx
    inc cx
    test ax,ax
    jnz chia_so
   chuyen_so:
    pop dx
    add dl,'0'
    mov ah,02h
    int 21h 
    loop chuyen_so
    
    pop cx
    pop ax
    pop bx
    ret
end
```
