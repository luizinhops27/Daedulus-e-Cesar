# Daedulus-e-Cesar
Trabalho Avaliativo:
ORG 0
MOV #65498, R3
MOV #65500, R1
MOV #46, R0
MOV #62, R4
MOV #83, R5
MOV #78, R6

DIGITA_NOME_RA:
CLR (R3)

AGUARDA_TECLA:
TST (R3)
BEQ AGUARDA_TECLA

MOV 65499, R2
CMP R0, R2
BEQ FIM_DIGITACAO

MOV R2, (R1)
INC R1
TST R1
BNE CONTINUA_LOOP
MOV #65500, R1

CONTINUA_LOOP:
BR DIGITA_NOME_RA

FIM_DIGITACAO:
MOV R4, (R1)
INC R1

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

EXIBE_FIM:
MOV R2, (R1)
HLT

Calculadora:

;> Inicializacao do apontador da pilha
;> para que a pilha fique acima da area
;> de memoria mapeada para entrada e saida
;> ESTAS DUAS INSTRUCOES DEVEM SER MANTIDAS AQUI !
          ORG 0                 ; primeira instrucao de qualquer 
          MOV #65498,R6         ; programa: aponta SP para 65498
;>-------------------------------------------------<
;>>                                               <<
;>>>                                             <<<
;>>>> INSERIR AQUI O CODIGO DE SEU PROGRAMA !!! <<<<
;>>>                                             <<<
;>>                                               <<
;>-------------------------------------------------<
	;Limpando LED
	  CLR 65500             ; limpa LED 00
          CLR 65501             ; limpa LED 01
          CLR 65502             ; limpa LED 02
          CLR 65503             ; limpa LED 03
          CLR 65504             ; limpa LED 04
          CLR 65505             ; limpa LED 05
          CLR 65506             ; limpa LED 06
          CLR 65507             ; limpa LED 07
          CLR 65508             ; limpa LED 08
          CLR 65509             ; limpa LED 09
          CLR 65510             ; limpa LED 10
          CLR 65511             ; limpa LED 11
          CLR 65512             ; limpa LED 12
          CLR 65513             ; limpa LED 13
          CLR 65514             ; limpa LED 14
          CLR 65515             ; limpa LED 15
          CLR 65516             ; limpa LED 16
          CLR 65517             ; limpa LED 17
          CLR 65518             ; limpa LED 18
          CLR 65519             ; limpa LED 19
          CLR 65520             ; limpa LED 20
          CLR 65521             ; limpa LED 21
          CLR 65522             ; limpa LED 22
          CLR 65523             ; limpa LED 23
          CLR 65524             ; limpa LED 24
          CLR 65525             ; limpa LED 25
          CLR 65526             ; limpa LED 26
          CLR 65527             ; limpa LED 27
          CLR 65528             ; limpa LED 28
          CLR 65529             ; limpa LED 29
          CLR 65530             ; limpa LED 30
          CLR 65531             ; limpa LED 31
          CLR 65532             ; limpa LED 32
          CLR 65533             ; limpa LED 33
          CLR 65534             ; limpa LED 34
          CLR 65535             ; limpa LED 35
INICIO:
	MOV #65500, R5 ;Endere o do display
	MOV #0, R3
	CLR (R6) 
AGUARDANDO:
	TST (R6) ;Testa para o primeiro n mero
	BEQ AGUARDANDO
	MOV 65499,R0
	MOV R0,(R5)
	SUB #'0',R0
	MOV R0,R4 
	JMP MULT10 ;Subrotina pra transformar unidade em dezena
FIMMULT10:
	CLR (R6) ;Unidade do primeiro n mero
AGUARDANDO_UNIDADE:
	TST (R6)
	BEQ AGUARDANDO_UNIDADE
	MOV 65499,R0
	MOV R0,(R5)
	SUB #'0',R0
	ADD R4, R0 ;R0 = R0 + R4(dezena mais unidade)
	CLR R4 ;Limpa R4 para salvar a dezena do pr ximo n mero
	CLR (R6) 
AGUARDANDO2:
	TST (R6) ;Testa para o segundo n mero
	BEQ AGUARDANDO2
        MOV #2, R1 ;Utilizaremos o R1 para a compara  o final no MULT10
	MOV 65499,R2
	MOV R2,(R5)
	SUB #'0',R2
	MOV R2,R4 
	JMP MULT10 ;Subrotina pra transformar unidade em dezena
FIMMULT102:
	CLR R1
	CLR (R6) ;Unidade do primeiro n mero
AGUARDANDO_UNIDADE2:
	TST (R6)
	BEQ AGUARDANDO_UNIDADE2
	MOV 65499,R2
	MOV R2,(R5)
	SUB #'0',R2
	ADD R4,R2 ;R2 = R2 + R4(dezena mais unidade)
	CLR R4 
	CLR (R6) 
AGUARDANDO1:
	TST (R6) ;Testa para operador
	BEQ AGUARDANDO1
	MOV 65499,R1
	MOV R1,(R5)
	BR OPERADORES
MULT10:
    CLR R3        ; R3 = acumulador = 0
    ADD R4, R3    ; R3 += n     ? 1x
    ADD R4, R3    ; R3 += n     ? 2x
    ADD R4, R3    ; R3 += n     ? 3x
    ADD R4, R3    ; R3 += n     ? 4x
    ADD R4, R3    ; R3 += n     ? 5x
    ADD R4, R3    ; R3 += n     ? 6x
    ADD R4, R3    ; R3 += n     ? 7x
    ADD R4, R3    ; R3 += n     ? 8x
    ADD R4, R3    ; R3 += n     ? 9x
    ADD R4, R3    ; R3 += n     ? 10x
    MOV R3, R4    ; R4 = R3 (resultado final)
    CLR R3
    CMP #2, R1
    BEQ FIMMULT102 	
    JMP FIMMULT10 ; Fim da rotina pula para o ponto designado.
OPERADORES:
	CMP R1,#43 ;C digo ASCII para '+'
        BEQ SOMA
        CMP R1,#45 ;C digo ASCII para '-'
        BEQ SUBTRACAO
        CMP R1,#42 ;C digo ASCII para '*'
        BEQ MULTIPLICACAO
        CMP R1,#47 ;C digo ASCII para '/'
        BEQ DIVISAO
        JMP INICIO   
SOMA:
	MOV R0,R3
        ADD R2,R3               ; R3 = R0 + R2
        BR MOSTRAR 
SUBTRACAO:
	MOV R0,R3
        SUB R2,R3               ; R3 = R0 - R2
        BR MOSTRAR
MULTIPLICACAO:
	CLR R3          ; acumulador = 0
	MOV R0,R4       ; multiplicando
	MOV R2,R1       ; multiplicador
     LOOP_MULT:
    	CMP #0,R1
    	BEQ FIM_MULT
    	ADD R4,R3    ; soma multiplicando no acumulador
    	DEC R1
    	BR LOOP_MULT
     FIM_MULT:
	BR MOSTRAR
DIVISAO:
        MOV R0,R3        ; dividendo
	MOV R2,R4        ; divisor
	CLR R3           ; quociente
     LOOP_DIV:
        CMP R4,R0
        BHI FIM_DIV
        SUB R4,R0
        INC R3
        BR LOOP_DIV
     FIM_DIV:
	BR MOSTRAR
MOSTRAR:
        CLR R4           ; garante dezena = 0
	CLR R5           ; garante centenas = 0
    DIV100:
        CMP R3, #100
        BLT DIV10        ; se R3 < 100, sai do loop
        SUB #100, R3     ; R3 = R3 - 100
        INC R5           ; R5 = R5 + 1 (conta centenas)
        BR DIV100
    DIV10:
        CMP R3,#10
        BLT MOSTRA_UN    ; se R3 < 10, sai do loop
        SUB #10,R3       ; R3 = R3 - 10
        INC R4           ; R4 = R4 + 1 (conta dezenas)
        BR DIV10
    MOSTRA_UN:
        ; Mostra centenas
        ADD #'0', R5
        MOV R5, 65500     ; LED3 (centenas)

        ; Mostra dezenas
        ADD #'0', R4
        MOV R4, 65501     ; LED1 (dezenas)

        ; Mostra unidades
        ADD #'0', R3
        MOV R3, 65502     ; LED2 (unidades)
	BR FIM
FIM:
	JMP INICIO ;Caso queira que o programa rode infinitamente
        HLT 
;>---------------------------------------------<
;> AS SUBROTINAS DEVEM INICIAR SOMENTE APOS A  <
;> ULTIMA INSTRUCAO CODIFICADA NO PROGRAMA !!  <
;>---------------------------------------------<
;>
;> Subrotina iterativa para "limpar" o visor
;>
;> Chamada da subrotina:
;>
;> JSR R7,_S_LIMPA_VISOR_ITERATIVA
;>
          
_S_LIMPA_VISOR_ITERATIVA:
          MOV R0,-(R6)          ; salva R0 na pilha
          MOV R1,-(R6)          ; salva R1 na pilha
          MOV #65500,R1         ; move end. do visor p/R1
          MOV #36,R0            ; move 36 para contador
__OUTRO_LED:
          CLR (R1)              ; limpa 1 LED do visor
          INC R1                ; aponta p/LED seguinte
          SOB R0,__OUTRO_LED    ; subtrai 1 do contador
                                ; se <> 0, repete o laco
          MOV (R6)+,R1          ; restaura R1
          MOV (R6)+,R0          ; restaura R0
          RTS R7                ; retorna ao ponto de chamada
;>
;>
;> Subrotina rapida para limpar visor
;>
;> Chamada da subrotina:
;>
;> JSR R7,_S_LIMPA_VISOR_RAPIDA
;>

_S_LIMPA_VISOR_RAPIDA:
          CLR 65500             ; limpa LED 00
          CLR 65501             ; limpa LED 01
          CLR 65502             ; limpa LED 02
          CLR 65503             ; limpa LED 03
          CLR 65504             ; limpa LED 04
          CLR 65505             ; limpa LED 05
          CLR 65506             ; limpa LED 06
          CLR 65507             ; limpa LED 07
          CLR 65508             ; limpa LED 08
          CLR 65509             ; limpa LED 09
          CLR 65510             ; limpa LED 10
          CLR 65511             ; limpa LED 11
          CLR 65512             ; limpa LED 12
          CLR 65513             ; limpa LED 13
          CLR 65514             ; limpa LED 14
          CLR 65515             ; limpa LED 15
          CLR 65516             ; limpa LED 16
          CLR 65517             ; limpa LED 17
          CLR 65518             ; limpa LED 18
          CLR 65519             ; limpa LED 19
          CLR 65520             ; limpa LED 20
          CLR 65521             ; limpa LED 21
          CLR 65522             ; limpa LED 22
          CLR 65523             ; limpa LED 23
          CLR 65524             ; limpa LED 24
          CLR 65525             ; limpa LED 25
          CLR 65526             ; limpa LED 26
          CLR 65527             ; limpa LED 27
          CLR 65528             ; limpa LED 28
          CLR 65529             ; limpa LED 29
          CLR 65530             ; limpa LED 30
          CLR 65531             ; limpa LED 31
          CLR 65532             ; limpa LED 32
          CLR 65533             ; limpa LED 33
          CLR 65534             ; limpa LED 34
          CLR 65535             ; limpa LED 35
          RTS R7                ; retorna ao ponto de chamada
;>
;>
;> Subrotina para escrever no visor
;>
;> Chamada da subrotina:
;>
;> MOV #tammensagem,R0          ; tamanho da mensagem (em caracteres)
;> MOV #endmensagem,R1          ; endereco da mensagem a ser escrita no visor
;> MOV #endvisor,R2             ; endereco do LED onde deve iniciar a mensagem
;> JSR R7,_S_ESCREVER_NO_VISOR
;>

_S_ESCREVER_NO_VISOR:
__VOLTA_ESCR:
          MOV (R1),R3           ; coloca 2 caracteres em R3
          ASR R3                ; alinha primeiro caractere
          ASR R3                ; a direita do registrador,
          ASR R3                ; porque quando se escreve
          ASR R3                ; na memoria a partir do
          ASR R3                ; endereco 65500 apenas o byte
          ASR R3                ; menos significativo e' escrito
          ASR R3                ; na posicao correspondente
          ASR R3                ; a um LED do visor
          MOV R3,(R2)           ; move para o visor
          SOB R0,__SEGUNDO      ; se ja moveu todo o texto,
          RTS R7                ; retorna ao ponto de chamada
                                ; senao, vai mover o segundo
                                ; caractere da mesma palavra
__SEGUNDO:
          INC R2                ; aponta para proximo LED
          BEQ __FIM_VISOR2      ; fim do visor - volta ao LED 00
__CONTINUA2:
          MOV (R1)+,R3          ; mesmos 2 caracteres em R3 e
                                ; incrementa apontador do texto
          MOV R3,(R2)           ; desta vez, move o segundo byte
          SOB R0,__PROXIMO_LED  ; se ja moveu todo o texto,
          RTS R7                ; retorna ao ponto de chamada
__PROXIMO_LED:
          INC R2                ; senao, aponta proximo LED
          BNE __VOLTA_ESCR      ; e repete o laco
                                ; fim do visor - volta ao LED 00
__FIM_VISOR1:
          MOV #65500,R2         ; aponta para primeiro LED
          BR  __VOLTA_ESCR      ; volta a escrever no visor
__FIM_VISOR2:
          MOV #65500,R2         ; aponta para primeiro LED
          BR  __CONTINUA2       ; volta a escrever no visor
;>
;>
;> Subrotina para multiplicar 2 inteiros positivos de 16 bits
;>
;> Chamada da subrotina:
;>
;> MOV #multiplicando,R0        ; multiplicando no R0
;> MOV #multiplicador,R1        ; multiplicador no R1
;> JSR R7,_S_MULTIPLICAR
;>
;> No retorno da subrotina:
;> - R0 cont m os 16 msbits do produto
;> - R1 cont m os 16 lsbits do produto
;> - C digo de condi  o V:
;>   V = 0 indica que a parte mais significativa do produto (R0)   zero
;>   V = 1 indica que n o   zero, ou seja: se for desprezada ocorre estouro
;>
_S_MULTIPLICAR:
          MOV R2,-(R6)          ; salva R2 na pilha
          MOV R3,-(R6)          ; salva R3 na pilha
          MOV #16,R2            ; inicializa contador
          CLR R3                ; limpa R3
__INICIO_LACO: 
          ROR R1                ; lsb do multiplicad. em C
          BCC __NAO_SOMAR       ; se era zero, nao soma
          ADD R0,R3             ; acumula multiplicando
                                ; no produto parcial
__NAO_SOMAR:
          ROR R3                ; lsb de R3 vai para C
          BCC __FIM_LACO        ; se era zero, sai do laco
          ADD #32768,R1         ; soma 1 ao bit 15 de R1
__FIM_LACO:
          SOB R2,__INICIO_LACO  ; decrementa contador e
                                ; repete se <> 0
          MOV R3,R0             ; resultado de R3 para R0
          MOV (R6)+,R3          ; restaura R3
          MOV (R6)+,R2          ; restaura R2
          TST R0                ; se R0 <> 0
          BNE __ALERTA_ESTOURO  ; vai indicar estouro
          CCC V                 ; senao, desliga V
          RTS R7                ; retorna ao progr. princ.
__ALERTA_ESTOURO:
          SCC V                 ; liga indicador: estouro
          RTS R7                ; retorna ao ponto de chamada
;>
;>
;> Dividir int. positivo de 32 bits por um de 16 bits
;>
;> Chamada da subrotina:
;>
;> MOV #msbitsdividendo,R0      ; 16 bits mais significativos do dividendo
;> MOV #lsbitsdividendo,R1      ; 16 bits menos significativos do dividendo
;> MOV #divisor,R2              ; divisor (16 bits)
;> JSR R7,_S_DIVIDIR
;>
;> No retorno da subrotina:
;> - R0 cont m o quociente (16 bits)
;> - R1 cont m o resto (16 bits)
;> - R2 ainda cont m o divisor, inalterado (16 bits)
;> - C digos de condi  o:
;>   V = 1 indica que ocorreu estouro na divis o (quociente n o cabe em 16 bits)
;>   Z = 1 indica que ocorreu uma tentativa de divis o por zero
;>   Nestes dois casos, R0, R1 e R2 n o s o alterados pela subrotina
;>

_S_DIVIDIR:
          TST R2                ; testa divisor
          BNE __NAO_ZERO        ; se <> zero, continua
          CCC V                 ; indica divisao por zero
          RTS R7                ; retorna ao ponto de chamada

__NAO_ZERO:
          CMP R0,R2             ; testa se dividendo(msb)
                                ; e' >= que o divisor
          BCC __INDICA_ESTOURO  ; se for, indicar estouro
                                ; note: BCC equivale a um
                                ; BGE para int. positivos
;>
          MOV R3,-(R6)          ; salva R3 na pilha
          MOV R4,-(R6)          ; salva R4 na pilha
          MOV R5,-(R6)          ; salva R5 na pilha
          MOV R0,R3             ; copia dividendo para
          MOV R1,R4             ; R3 e R4 (=q no final)
          MOV #16,R5            ; inicializa contador
          ASL R4                ; desloca dividendo p/a
          ROL R3                ; esquerda e abre espaco
          BCS __SUBTRAI_DIVISOR ; p/um bit do quociente
          CMP R3,R2             ; se n+1 msbits do divid.
          BCS __BIT_ZERO        ; maiores que divisor (= BLT p/inteiros positivos)
__SUBTRAI_DIVISOR:
          SUB R2,R3             ; subtrai divisor e
          INC R4                ; ajusta bit do quociente
__BIT_ZERO:
          SOB R5,16             ; decr. R5; se <>0, repete
          MOV R3,R1             ; copia resto para R1
          MOV R4,R0             ; copia quociente p/R0
          MOV (R6)+,R5          ; restaura
          MOV (R6)+,R4          ; registradores
          MOV (R6)+,R3          ; de trabalho
          CCC V Z               ; limpa cod. de condicao
          RTS R7                ; retorna ao ponto de chamada
;>
__INDICA_ESTOURO:
          SCC V                 ; indica overflow e nao
          CCC Z                 ; divisao por zero
          RTS R7                ; retorna ao ponto de chamada

;> Subrotina iterativa para ler um caracter
;>
;> Chamada da subrotina:
;>
;> JSR R7,_S_LER_CARACTER
;>
          
_S_LER_CARACTER:
          MOV R0,-(R6)          ; salva R0 na pilha
          MOV R1,-(R6)          ; salva R1 na pilha
          
          MOV #65498,R3
          CLR (R3)
          TST (R3)
          BEQ -4

          MOV (R6)+,R1          ; restaura R1
          MOV (R6)+,R0          ; restaura R0
          RTS R7                ; retorna ao ponto de chamada

;> Subrotina iterativa para ler e mostrar caracter no visor
;>
;> Chamada da subrotina:
;>
;> JSR R7,_S_LER_CARACTER_VISOR
;>
          
_S_LER_CARACTER_VISOR:
          MOV R0,-(R6)          ; salva R0 na pilha
          MOV R1,-(R6)          ; salva R1 na pilha
          
          MOV #65498,R3
          CLR (R3)
          TST (R3)
          BEQ -4
          MOV 65499, 65500
          BR -14

          MOV (R6)+,R1          ; restaura R1
          MOV (R6)+,R0          ; restaura R0
          RTS R7                ; retorna ao ponto de chamada

;> Subrotina iterativa para ler e mostrar string no visor
;>
;> Chamada da subrotina:
;>
;> JSR R7,_S_LER_CARACTERES_VISOR
;>
          
_S_LER_CARACTERES_VISOR:
          MOV R0,-(R6)          ; salva R0 na pilha
          MOV R1,-(R6)          ; salva R1 na pilha
          
          MOV #65498,R3         ; Carrega o endere o 65498 em R3
          MOV #65000,R1         ; Carrega o endere o 65500 em R1 (inicio do Visor)
          CLR (R3)              ; Prepara a nova leitura
          TST (R3)              ; Testa se um caracter foi digitado
          BEQ -4                ; Enquanto for zero repete o teste
          MOV 65499, (R1)       ; Move o caracter lido para o cursor
          INC R1                ; Incrementa R1
          BEQ __FIM_LER         ; Se R1=0, retorna          
          BR -16                ; Sen o retorna para ler mais caracteres
__FIM_LER:
          MOV (R6)+,R1          ; restaura R1
          MOV (R6)+,R0          ; restaura R0
          RTS R7                ; retorna ao ponto de chamada

;>
;> Identificacao da versao da biblioteca - e' exibida no visor
;>
          ORG 65500             ; ajusta endereco de inicio (LED 01 do visor)
          DAB '* BibCesar.ced Versao 8+ 08/04/19 *'
;>
;> Esta vers o apenas incorpora coment rios sobre os resultados devolvidos pelas
;> subrotinas de multiplica  o e divis o de inteiros positivos.


