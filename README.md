# Daedulus-e-Cesar
Trabalho Avaliativo
ORG 0

; --- Configura Registradores e Constantes ---
MOV #65498, R3      ; Endereço do Status do Teclado (Controle)
MOV #65500, R1      ; Endereço do Display (Ponteiro de escrita)
MOV #46, R0         ; '.' (ponto)
MOV #62, R4         ; '>' (prompt)
MOV #83, R5         ; 'S'
MOV #78, R6         ; 'N'

; --- Leitura do Nome/RA ---
DIGITA_NOME_RA:
    CLR (R3)            ; Limpa o status do teclado

AGUARDA_TECLA:
    TST (R3)            ; Verifica se há tecla pressionada
    BEQ AGUARDA_TECLA   ; Se não, continua esperando

    MOV 65499, R2       ; Lê o caractere digitado

    CMP R0, R2          ; Compara com '.'
    BEQ FIM_DIGITACAO   ; Se for ponto, termina a leitura

    MOV R2, (R1)        ; Escreve caractere no display
    INC R1              

    TST R1              ; Verifica estouro do display
    BNE CONTINUA_LOOP
    MOV #65500, R1      ; Reinicia ponteiro do display

CONTINUA_LOOP:
    BR DIGITA_NOME_RA

; --- Fim da Digitação ---
FIM_DIGITACAO:
    MOV R4, (R1)        ; Exibe o prompt '>'
    INC R1

; --- Validação S/N ---
VALIDACAO_SN_LOOP:
    CLR (R3)

TECLA_SN:
    TST (R3)
    BEQ TECLA_SN

    MOV 65499, R2

    CMP R5, R2
    BEQ EXIBE_FIM

    CMP R6, R2
    BEQ EXIBE_FIM

    BR VALIDACAO_SN_LOOP

; --- Exibe o Resultado e Encerra ---
EXIBE_FIM:
    MOV R2, (R1)
    HLT



