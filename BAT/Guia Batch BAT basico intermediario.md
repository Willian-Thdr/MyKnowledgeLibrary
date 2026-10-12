# Guia de Batch (.bat) --- do básico ao intermediário

> Um guia prático de Windows Batch (`.bat`/`.cmd`), começando pelos
> comandos fundamentais e avançando até estruturas intermediárias.
>
> **Observação:** Batch é uma linguagem de shell/script do Windows.
> Muitos comandos usados nos arquivos `.bat` são, na verdade,
> programas/comandos do próprio Windows (`dir`, `copy`, `tasklist`,
> `ipconfig`, etc.).

------------------------------------------------------------------------

## 1. O que é um arquivo `.bat`?

Um arquivo `.bat` é um arquivo de texto contendo comandos que o
`cmd.exe` executa em sequência.

Exemplo:

``` bat
@echo off
echo Olá, mundo!
pause
```

Salve como:

``` text
programa.bat
```

Ao executá-lo, o Windows abrirá o `cmd` e executará os comandos.

### `.bat` x `.cmd`

Os dois são muito parecidos no Windows moderno. Para scripts destinados
especificamente ao `cmd.exe`, `.bat` é a extensão mais tradicional.

------------------------------------------------------------------------

# 2. Primeiro comando: `echo`

Exibe texto:

``` bat
echo Olá!
```

Também pode controlar a exibição dos próprios comandos:

``` bat
echo off
```

O `@` impede que o próprio comando seja mostrado antes de ser executado:

``` bat
@echo off
```

Essa é uma das primeiras linhas mais comuns em scripts Batch.

Para voltar a mostrar os comandos:

``` bat
echo on
```

### Exemplo

``` bat
@echo off

echo Iniciando programa...
echo Programa executado com sucesso!

pause
```

------------------------------------------------------------------------

# 3. Comentários

Há duas formas comuns.

## `rem`

``` bat
rem Isto é um comentário
```

## `::`

``` bat
:: Isto também costuma ser usado como comentário
```

`rem` é a forma oficialmente reconhecida pelo interpretador.

Exemplo:

``` bat
@echo off

rem Configuração inicial
echo Iniciando...

:: Executando a tarefa principal
echo Tudo certo.

pause
```

------------------------------------------------------------------------

# 4. `pause`

Pausa a execução e espera o usuário pressionar uma tecla:

``` bat
pause
```

Você pode evitar a mensagem padrão:

``` bat
pause > nul
```

Exemplo:

``` bat
@echo off

echo Pressione qualquer tecla para continuar...
pause > nul

echo Continuando...
pause
```

------------------------------------------------------------------------

# 5. Limpar a tela: `cls`

``` bat
cls
```

Exemplo:

``` bat
@echo off

echo Texto antigo...
pause

cls

echo Tela limpa!
pause
```

------------------------------------------------------------------------

# 6. Título da janela

``` bat
title Meu Programa
```

Exemplo:

``` bat
@echo off
title Gerenciador de Arquivos

echo Programa iniciado.
pause
```

------------------------------------------------------------------------

# 7. Alterar a cor do CMD

``` bat
color 0A
```

O primeiro caractere representa a cor do fundo e o segundo a cor do
texto.

Exemplos:

``` bat
color 07
color 0A
color 0C
color 0E
```

Você pode consultar:

``` bat
color /?
```

------------------------------------------------------------------------

# 8. Variáveis

Uma variável pode armazenar um valor:

``` bat
set nome=Willian
```

Para utilizá-la:

``` bat
echo %nome%
```

Exemplo:

``` bat
@echo off

set nome=Willian

echo Olá, %nome%!
pause
```

------------------------------------------------------------------------

# 9. Variáveis numéricas

``` bat
set idade=17

echo %idade%
```

Por padrão, o Batch trata o conteúdo como texto. Para operações
matemáticas, use `/a`.

``` bat
set /a resultado=10+5
echo %resultado%
```

Também:

``` bat
set /a soma=10+20
set /a subtracao=20-10
set /a multiplicacao=5*4
set /a divisao=20/4
```

------------------------------------------------------------------------

# 10. `set /a`

O `/a` permite expressões aritméticas:

``` bat
set /a resultado=10+20*2
echo %resultado%
```

Operadores comuns:

``` text
+   adição
-   subtração
*   multiplicação
/   divisão inteira
%%  resto da divisão
```

Exemplo:

``` bat
@echo off

set /a a=10
set /a b=3

set /a soma=a+b
set /a resto=a%%b

echo Soma: %soma%
echo Resto: %resto%

pause
```

Dentro de um `.bat`, o operador `%` precisa ser escapado como `%%` em
determinadas situações.

------------------------------------------------------------------------

# 11. Entrada do usuário: `set /p`

``` bat
set /p nome=Digite seu nome: 
```

Exemplo:

``` bat
@echo off

set /p nome=Digite seu nome: 

echo Olá, %nome%!

pause
```

Entrada numérica:

``` bat
set /p idade=Digite sua idade: 

echo Você informou: %idade%
```

------------------------------------------------------------------------

# 12. Variáveis de ambiente

O Windows já possui diversas variáveis.

Exemplos:

``` bat
echo %USERNAME%
echo %COMPUTERNAME%
echo %USERPROFILE%
echo %TEMP%
echo %PATH%
```

Algumas variáveis úteis:

  Variável           Conteúdo
  ------------------ -----------------------
  `%USERNAME%`       Usuário atual
  `%COMPUTERNAME%`   Nome do computador
  `%USERPROFILE%`    Pasta do usuário
  `%TEMP%`           Pasta temporária
  `%PATH%`           Caminhos de programas
  `%CD%`             Diretório atual
  `%DATE%`           Data atual
  `%TIME%`           Hora atual

------------------------------------------------------------------------

# 13. Diretórios

## Mostrar diretório atual

``` bat
cd
```

ou:

``` bat
echo %CD%
```

## Mudar de diretório

``` bat
cd C:\Users
```

Também:

``` bat
cd ..
```

Volta um nível.

``` bat
cd \
```

Vai para a raiz da unidade atual.

------------------------------------------------------------------------

# 14. `cd /d`

Quando você quer trocar também de unidade:

``` bat
cd /d D:\Projetos
```

Isso é importante porque:

``` bat
cd D:\Projetos
```

pode não trocar a unidade atual dependendo do contexto.

------------------------------------------------------------------------

# 15. Criar pastas: `mkdir`

``` bat
mkdir MinhaPasta
```

Também:

``` bat
md MinhaPasta
```

Criar várias:

``` bat
mkdir Pasta1 Pasta2 Pasta3
```

Criar uma árvore de diretórios:

``` bat
mkdir Projeto\src\bin
```

------------------------------------------------------------------------

# 16. Remover pastas: `rmdir`

``` bat
rmdir MinhaPasta
```

Ou:

``` bat
rd MinhaPasta
```

Para remover uma pasta e seu conteúdo:

``` bat
rmdir /s MinhaPasta
```

Sem confirmação:

``` bat
rmdir /s /q MinhaPasta
```

**Cuidado:** `/s /q` pode apagar muitos arquivos sem pedir confirmação.

------------------------------------------------------------------------

# 17. Listar arquivos: `dir`

``` bat
dir
```

Algumas opções úteis:

``` bat
dir /a
dir /b
dir /s
dir /o
dir /p
```

### Exemplos

Somente nomes:

``` bat
dir /b
```

Incluindo arquivos ocultos:

``` bat
dir /a
```

Recursivamente:

``` bat
dir /s
```

Por extensão:

``` bat
dir *.txt
```

------------------------------------------------------------------------

# 18. Criar arquivo de texto

Uma forma simples:

``` bat
echo Olá > arquivo.txt
```

Isso cria ou sobrescreve o arquivo.

Para adicionar conteúdo:

``` bat
echo Segunda linha >> arquivo.txt
```

Diferença:

``` text
>   sobrescreve
>>  adiciona ao final
```

Exemplo:

``` bat
@echo off

echo Primeira linha > arquivo.txt
echo Segunda linha >> arquivo.txt

type arquivo.txt

pause
```

------------------------------------------------------------------------

# 19. Ler arquivos: `type`

``` bat
type arquivo.txt
```

Exemplo:

``` bat
@echo off

type configuracao.txt

pause
```

------------------------------------------------------------------------

# 20. Copiar arquivos: `copy`

``` bat
copy arquivo.txt destino.txt
```

Para outro diretório:

``` bat
copy arquivo.txt C:\Backup\
```

Vários arquivos:

``` bat
copy *.txt C:\Backup\
```

------------------------------------------------------------------------

# 21. Mover arquivos: `move`

``` bat
move arquivo.txt C:\Backup\
```

Também pode renomear:

``` bat
move antigo.txt novo.txt
```

------------------------------------------------------------------------

# 22. Excluir arquivos: `del`

``` bat
del arquivo.txt
```

Por extensão:

``` bat
del *.tmp
```

Sem confirmação:

``` bat
del /q arquivo.txt
```

**Cuidado com curingas:**

``` bat
del *.txt
```

pode excluir todos os `.txt` do diretório atual.

------------------------------------------------------------------------

# 23. Renomear arquivos: `ren`

``` bat
ren antigo.txt novo.txt
```

------------------------------------------------------------------------

# 24. Curingas

Os dois curingas mais importantes são:

``` text
*   qualquer quantidade de caracteres
?   um caractere
```

Exemplos:

``` bat
dir *.txt
dir arquivo?.txt
del *.tmp
```

------------------------------------------------------------------------

# 25. Comparações com `if`

Estrutura:

``` bat
if condição comando
```

Exemplo:

``` bat
if exist arquivo.txt echo O arquivo existe!
```

------------------------------------------------------------------------

# 26. `if exist`

``` bat
if exist arquivo.txt (
    echo Arquivo encontrado.
)
```

Com `else`:

``` bat
if exist arquivo.txt (
    echo Existe.
) else (
    echo Não existe.
)
```

------------------------------------------------------------------------

# 27. Comparar texto

``` bat
if "%nome%"=="Willian" (
    echo Nome correto.
)
```

O uso das aspas ajuda quando a variável estiver vazia.

Exemplo:

``` bat
set /p resposta=Digite sim ou nao: 

if /i "%resposta%"=="sim" (
    echo Você escolheu sim.
)
```

`/i` faz a comparação ignorando maiúsculas/minúsculas.

------------------------------------------------------------------------

# 28. Comparar números

``` bat
if %idade% GEQ 18 (
    echo Maior ou igual a 18.
)
```

Operadores:

  Operador   Significado
  ---------- ----------------
  `EQU`      igual
  `NEQ`      diferente
  `LSS`      menor
  `LEQ`      menor ou igual
  `GTR`      maior
  `GEQ`      maior ou igual

Exemplo:

``` bat
if %idade% GEQ 18 (
    echo Maior de idade.
) else (
    echo Menor de idade.
)
```

------------------------------------------------------------------------

# 29. `errorlevel`

Muitos programas retornam um código de saída.

Você pode testar:

``` bat
if errorlevel 1 (
    echo O comando falhou.
)
```

Ou:

``` bat
if not errorlevel 1 (
    echo O comando teve sucesso.
)
```

Uma forma comum:

``` bat
programa.exe

if errorlevel 1 (
    echo Erro!
) else (
    echo Sucesso!
)
```

------------------------------------------------------------------------

# 30. Operador `&&`

Executa o segundo comando somente se o primeiro funcionar:

``` bat
comando1 && comando2
```

Exemplo:

``` bat
mkdir Backup && echo Backup criado.
```

------------------------------------------------------------------------

# 31. Operador `||`

Executa o segundo comando se o primeiro falhar:

``` bat
comando1 || echo Falhou!
```

Exemplo:

``` bat
mkdir Backup || echo Não foi possível criar a pasta.
```

------------------------------------------------------------------------

# 32. `&`

Executa vários comandos na mesma linha:

``` bat
echo Um & echo Dois
```

------------------------------------------------------------------------

# 33. Redirecionamento

### Saída para arquivo

``` bat
dir > arquivos.txt
```

### Adicionar ao arquivo

``` bat
dir >> arquivos.txt
```

### Ignorar saída

``` bat
comando > nul
```

### Redirecionar erros

``` bat
comando 2> erro.txt
```

### Saída normal + erros

``` bat
comando > resultado.txt 2>&1
```

------------------------------------------------------------------------

# 34. Entrada e saída

Os identificadores mais importantes:

``` text
0 = entrada padrão
1 = saída padrão
2 = erro padrão
```

Exemplo:

``` bat
programa.exe > saida.txt 2> erros.txt
```

------------------------------------------------------------------------

# 35. `find` e `findstr`

## `find`

Procura texto:

``` bat
find "erro" arquivo.txt
```

## `findstr`

Mais poderoso:

``` bat
findstr "erro" arquivo.txt
```

Pesquisar recursivamente:

``` bat
findstr /s /i "senha" *.txt
```

`/i` ignora maiúsculas/minúsculas.

------------------------------------------------------------------------

# 36. `where`

Descobre onde um executável está:

``` bat
where python
```

Exemplo:

``` bat
where node
where git
where dotnet
```

Muito útil para diagnosticar problemas de `PATH`.

------------------------------------------------------------------------

# 37. `start`

Abre programas ou outros recursos.

``` bat
start notepad.exe
```

Abrir uma URL:

``` bat
start https://example.com
```

Abrir uma pasta:

``` bat
start "" "C:\Projetos"
```

O `""` é importante porque o primeiro argumento de `start` entre aspas é
interpretado como título da janela.

------------------------------------------------------------------------

# 38. `timeout`

Espera alguns segundos:

``` bat
timeout /t 5
```

Sem permitir interrupção pelo teclado:

``` bat
timeout /t 5 /nobreak
```

------------------------------------------------------------------------

# 39. `choice`

Cria uma escolha simples:

``` bat
choice /c SN /m "Continuar?"
```

Depois:

``` bat
if errorlevel 2 echo Você escolheu Não.
if errorlevel 1 echo Você escolheu Sim.
```

**Atenção:** `errorlevel` deve ser testado da maior opção para a menor
quando houver várias opções.

Exemplo:

``` bat
choice /c ABC /m "Escolha uma opção"

if errorlevel 3 goto C
if errorlevel 2 goto B
if errorlevel 1 goto A

:A
echo Você escolheu A.
goto fim

:B
echo Você escolheu B.
goto fim

:C
echo Você escolheu C.

:fim
pause
```

------------------------------------------------------------------------

# 40. `goto`

Pula para um rótulo:

``` bat
goto inicio
```

Rótulo:

``` bat
:inicio
echo Programa iniciado.
```

Exemplo:

``` bat
@echo off

:menu
cls

echo 1 - Olá
echo 2 - Sair

choice /c 12 /n

if errorlevel 2 goto fim
if errorlevel 1 (
    echo Olá!
    pause
    goto menu
)

:fim
echo Encerrando...
```

------------------------------------------------------------------------

# 41. Loops com `for`

Estrutura básica:

``` bat
for %%A in (1 2 3) do (
    echo %%A
)
```

Resultado:

``` text
1
2
3
```

No prompt diretamente, normalmente é usado `%A`; em um arquivo `.bat`,
usa-se `%%A`.

------------------------------------------------------------------------

# 42. Percorrer arquivos

``` bat
for %%F in (*.txt) do (
    echo %%F
)
```

Exemplo:

``` bat
@echo off

for %%F in (*.txt) do (
    echo Arquivo encontrado: %%F
)

pause
```

------------------------------------------------------------------------

# 43. Percorrer diretórios

``` bat
for /d %%D in (*) do (
    echo Pasta: %%D
)
```

------------------------------------------------------------------------

# 44. Recursividade com `for /r`

Percorre diretórios recursivamente:

``` bat
for /r %%F in (*.txt) do (
    echo %%F
)
```

Isso encontra `.txt` também em subpastas.

------------------------------------------------------------------------

# 45. `for /l`

Loop numérico:

``` bat
for /l %%N in (1,1,10) do (
    echo %%N
)
```

Formato:

``` text
for /l %%N in (início,incremento,fim)
```

Exemplo regressivo:

``` bat
for /l %%N in (10,-1,1) do (
    echo %%N
)
```

------------------------------------------------------------------------

# 46. `for /f`

Usado para processar texto, arquivos e saída de comandos.

Exemplo:

``` bat
for /f "tokens=*" %%A in (arquivo.txt) do (
    echo %%A
)
```

Processar saída de comando:

``` bat
for /f "tokens=*" %%A in ('dir /b') do (
    echo %%A
)
```

Esse recurso é extremamente importante para scripts Batch
intermediários.

------------------------------------------------------------------------

# 47. Tokens

Dado:

``` text
Willian 17 Programacao
```

Você pode separar campos:

``` bat
for /f "tokens=1,2,3" %%A in ("Willian 17 Programacao") do (
    echo Nome: %%A
    echo Idade: %%B
    echo Área: %%C
)
```

------------------------------------------------------------------------

# 48. Delimitadores

Por padrão, `for /f` utiliza espaços e tabulações como delimitadores.

Você pode alterar:

``` bat
for /f "tokens=1,2 delims=," %%A in ("Willian,17") do (
    echo Nome: %%A
    echo Idade: %%B
)
```

------------------------------------------------------------------------

# 49. Variáveis de loop com modificadores

Se:

``` bat
for %%F in (arquivo.txt) do echo %%F
```

Você também pode obter informações do arquivo:

``` bat
for %%F in (arquivo.txt) do (
    echo Nome: %%~nF
    echo Extensão: %%~xF
    echo Caminho: %%~fF
    echo Diretório: %%~dpF
)
```

Modificadores úteis:

  Modificador   Resultado
  ------------- -------------------
  `%%~F`        remove aspas
  `%%~fF`       caminho completo
  `%%~dF`       unidade
  `%%~pF`       caminho
  `%%~nF`       nome
  `%%~xF`       extensão
  `%%~dpF`      unidade + caminho
  `%%~nxF`      nome + extensão

------------------------------------------------------------------------

# 50. Expansão de variáveis

Normalmente:

``` bat
set nome=Willian
echo %nome%
```

Existe, porém, um problema importante dentro de blocos `(...)`.

Exemplo:

``` bat
set contador=0

for %%A in (1 2 3) do (
    set /a contador+=1
    echo %contador%
)
```

O resultado pode não ser o esperado porque `%contador%` é expandido
antes da execução do bloco.

A solução é usar **delayed expansion**.

------------------------------------------------------------------------

# 51. Delayed Expansion

Ative:

``` bat
setlocal EnableDelayedExpansion
```

Depois use `!variavel!`:

``` bat
@echo off
setlocal EnableDelayedExpansion

set contador=0

for %%A in (1 2 3) do (
    set /a contador+=1
    echo !contador!
)

endlocal
```

Esse conceito é fundamental para scripts Batch mais complexos.

------------------------------------------------------------------------

# 52. `setlocal` e `endlocal`

Cria um escopo para alterações de variáveis:

``` bat
setlocal

set teste=123

endlocal
```

Depois do `endlocal`, a variável criada dentro do escopo deixa de
existir.

Exemplo:

``` bat
@echo off

set teste=fora

setlocal
set teste=dentro
echo Dentro: %teste%
endlocal

echo Fora: %teste%

pause
```

------------------------------------------------------------------------

# 53. Funções com `call`

Batch não possui funções da mesma forma que linguagens como C# ou
Python, mas podemos simular usando rótulos.

``` bat
call :MinhaFuncao
goto :eof

:MinhaFuncao
echo Olá!
goto :eof
```

------------------------------------------------------------------------

# 54. Parâmetros de funções

``` bat
call :Somar 10 20
goto :eof

:Somar
set /a resultado=%1+%2
echo Resultado: %resultado%
goto :eof
```

Aqui:

``` text
%1 = 10
%2 = 20
```

------------------------------------------------------------------------

# 55. `%0`, `%1`, `%2` etc.

Quando um `.bat` é executado:

``` bat
programa.bat primeiro segundo
```

As variáveis especiais são:

``` text
%0 = nome do script
%1 = primeiro argumento
%2 = segundo argumento
%3 = terceiro argumento
...
```

Exemplo:

``` bat
@echo off

echo Script: %0
echo Primeiro argumento: %1
echo Segundo argumento: %2

pause
```

Executando:

``` bat
programa.bat Olá Mundo
```

------------------------------------------------------------------------

# 56. `%*`

Representa todos os argumentos:

``` bat
@echo off

echo Argumentos:
echo %*

pause
```

------------------------------------------------------------------------

# 57. `shift`

Move os argumentos:

``` bat
shift
```

Exemplo:

``` bat
@echo off

echo Primeiro: %1

shift

echo Novo primeiro: %1

pause
```

------------------------------------------------------------------------

# 58. `call` com parâmetros

Você pode montar pequenos módulos:

``` bat
@echo off

call :Mensagem "Olá" 
call :Mensagem "Tudo certo?"

goto :eof

:Mensagem
echo Mensagem recebida: %~1
goto :eof
```

`%~1` remove aspas do argumento.

------------------------------------------------------------------------

# 59. Caminho do próprio script

Uma das variáveis mais úteis:

``` bat
%~dp0
```

Ela representa a unidade + caminho da pasta onde o `.bat` está.

Exemplo:

``` bat
echo %~dp0
```

Se o script estiver em:

``` text
C:\Projetos\MeuPrograma\
```

o resultado será algo como:

``` text
C:\Projetos\MeuPrograma\
```

------------------------------------------------------------------------

# 60. Nome do próprio script

``` bat
%~nx0
```

Isso fornece o nome e a extensão.

Exemplo:

``` bat
echo Executando %~nx0
```

------------------------------------------------------------------------

# 61. Diretório do projeto

Uma técnica comum:

``` bat
set "PROJECT_ROOT=%~dp0"
```

Depois:

``` bat
cd /d "%PROJECT_ROOT%"
```

Isso é especialmente útil quando o script pode ser executado a partir de
qualquer diretório.

------------------------------------------------------------------------

# 62. Aspas em caminhos

Sempre que possível, use:

``` bat
cd /d "C:\Program Files\Meu Programa"
```

Em vez de:

``` bat
cd /d C:\Program Files\Meu Programa
```

O segundo quebra porque existe um espaço.

------------------------------------------------------------------------

# 63. Sintaxe recomendada para `set`

Prefira:

``` bat
set "nome=Willian"
```

Em vez de:

``` bat
set nome=Willian
```

Isso evita espaços acidentais no valor.

Exemplo:

``` bat
set "arquivo=C:\Minha Pasta\arquivo.txt"
```

------------------------------------------------------------------------

# 64. Executar programas

``` bat
programa.exe
```

Com caminho:

``` bat
"C:\Program Files\Programa\programa.exe"
```

Com argumentos:

``` bat
programa.exe --arquivo teste.txt
```

------------------------------------------------------------------------

# 65. `cmd /c`

Executa um comando e encerra:

``` bat
cmd /c "echo Olá"
```

------------------------------------------------------------------------

# 66. `cmd /k`

Executa um comando e mantém o CMD aberto:

``` bat
cmd /k "echo Olá"
```

------------------------------------------------------------------------

# 67. `exit`

Encerra o CMD/script:

``` bat
exit
```

Você também pode definir o código de saída:

``` bat
exit /b 0
```

ou:

``` bat
exit /b 1
```

------------------------------------------------------------------------

# 68. `goto :eof`

Retorna de uma função chamada com `call`:

``` bat
:MinhaFuncao
echo Executando...
goto :eof
```

É preferível a usar `exit`, pois `exit` pode encerrar o próprio
`cmd.exe`.

------------------------------------------------------------------------

# 69. `echo` com caracteres especiais

Alguns caracteres possuem significado especial:

``` text
&  |  <  >  (  )  ^  %
```

Para escapar muitos deles, use `^`.

Exemplo:

``` bat
echo 10 ^> 5
```

Resultado:

``` text
10 > 5
```

Outro:

``` bat
echo A ^& B
```

------------------------------------------------------------------------

# 70. `^` como caractere de escape

``` bat
echo Olá ^& mundo
```

Também pode continuar um comando na próxima linha:

``` bat
echo Este é um comando muito ^
longo.
```

------------------------------------------------------------------------

# 71. `rem` versus `echo`

Para comentários, prefira:

``` bat
rem Comentário
```

ou:

``` bat
:: Comentário
```

Não use:

``` bat
echo Comentário
```

se a intenção for realmente comentar, pois isso imprime o texto.

------------------------------------------------------------------------

# 72. Variáveis com caracteres especiais

Use aspas:

``` bat
set "mensagem=Olá & mundo"
```

Isso é mais seguro que:

``` bat
set mensagem=Olá & mundo
```

------------------------------------------------------------------------

# 73. Arquivos temporários

Você pode utilizar `%TEMP%`:

``` bat
set "arquivoTemp=%TEMP%\meu_arquivo.txt"

echo Teste > "%arquivoTemp%"
```

------------------------------------------------------------------------

# 74. Criar backup simples

``` bat
@echo off

set "origem=C:\Projetos"
set "destino=C:\Backup"

mkdir "%destino%" 2>nul

copy "%origem%\*.txt" "%destino%\"

echo Backup concluído.
pause
```

------------------------------------------------------------------------

# 75. `xcopy`

Para cópias mais completas:

``` bat
xcopy origem destino /E /I
```

Algumas opções:

``` text
/E   inclui subdiretórios, inclusive vazios
/I   assume que destino é diretório
/Y   não pergunta antes de sobrescrever
```

Exemplo:

``` bat
xcopy "C:\Projeto" "D:\Backup\Projeto" /E /I
```

------------------------------------------------------------------------

# 76. `robocopy`

Para cópias mais robustas:

``` bat
robocopy "C:\Projeto" "D:\Backup\Projeto" /E
```

`robocopy` é especialmente útil para backups e sincronização.

Exemplo:

``` bat
robocopy "C:\Projeto" "D:\Backup\Projeto" /E /R:2 /W:2
```

Onde:

``` text
/R:2 = 2 tentativas
/W:2 = 2 segundos entre tentativas
```

------------------------------------------------------------------------

# 77. Processos

Listar processos:

``` bat
tasklist
```

Filtrar:

``` bat
tasklist | findstr chrome
```

Encerrar processo:

``` bat
taskkill /IM notepad.exe
```

Forçar:

``` bat
taskkill /F /IM notepad.exe
```

Por PID:

``` bat
taskkill /PID 1234 /F
```

**Cuidado:** `/F` força o encerramento.

------------------------------------------------------------------------

# 78. Rede

Ver configurações:

``` bat
ipconfig
```

Mais detalhes:

``` bat
ipconfig /all
```

Limpar cache DNS:

``` bat
ipconfig /flushdns
```

Testar conexão:

``` bat
ping 8.8.8.8
```

Testar um domínio:

``` bat
ping google.com
```

------------------------------------------------------------------------

# 79. `curl`

Windows moderno inclui `curl`:

``` bat
curl https://example.com
```

Baixar um arquivo:

``` bat
curl -o arquivo.zip https://example.com/arquivo.zip
```

Fazer uma requisição:

``` bat
curl http://localhost:3000/version
```

Isso é particularmente útil quando um `.bat` precisa conversar com uma
API local.

------------------------------------------------------------------------

# 80. `powershell` dentro do Batch

Batch pode chamar PowerShell:

``` bat
powershell -Command "Write-Host 'Olá'"
```

Exemplo:

``` bat
powershell -Command "Get-Date"
```

Isso é útil quando uma tarefa é muito difícil ou inconveniente de fazer
diretamente em Batch.

------------------------------------------------------------------------

# 81. Executar Node.js

Se Node estiver no `PATH`:

``` bat
node app.js
```

Passando argumentos:

``` bat
node app.js argumento1 argumento2
```

Exemplo:

``` bat
@echo off

cd /d "%~dp0"

node Service\CheckVersion.js

pause
```

------------------------------------------------------------------------

# 82. Executar C

Se estiver usando .NET:

``` bat
dotnet run
```

Ou executar uma DLL:

``` bat
dotnet MeuPrograma.dll
```

------------------------------------------------------------------------

# 83. Verificar se um programa existe

``` bat
where node >nul 2>&1

if errorlevel 1 (
    echo Node.js não foi encontrado.
) else (
    echo Node.js encontrado.
)
```

------------------------------------------------------------------------

# 84. Verificar arquivos

``` bat
if exist "config.json" (
    echo Configuração encontrada.
) else (
    echo Configuração ausente.
)
```

------------------------------------------------------------------------

# 85. Verificar diretórios

``` bat
if exist "C:\Projetos\" (
    echo Diretório existe.
)
```

------------------------------------------------------------------------

# 86. Menu simples

``` bat
@echo off
title Menu

:menu
cls

echo ==========================
echo         MENU
echo ==========================
echo.
echo [1] Informações
echo [2] Limpar
echo [3] Sair
echo.

choice /c 123 /n /m "Escolha: "

if errorlevel 3 goto fim
if errorlevel 2 goto limpar
if errorlevel 1 goto info

:info
cls
echo Usuário: %USERNAME%
echo Computador: %COMPUTERNAME%
echo Diretório: %CD%
pause
goto menu

:limpar
cls
echo Limpeza executada.
pause
goto menu

:fim
echo Encerrando...
```

------------------------------------------------------------------------

# 87. Sistema de confirmação

``` bat
choice /c SN /m "Deseja continuar?"

if errorlevel 2 (
    echo Operação cancelada.
    goto :eof
)

echo Operação confirmada.
```

------------------------------------------------------------------------

# 88. Criar estrutura de projeto

``` bat
@echo off

set "ROOT=%~dp0"

mkdir "%ROOT%src" 2>nul
mkdir "%ROOT%bin" 2>nul
mkdir "%ROOT%logs" 2>nul
mkdir "%ROOT%config" 2>nul

echo Estrutura criada.
pause
```

------------------------------------------------------------------------

# 89. Log de execução

``` bat
@echo off

set "LOG=%~dp0program.log"

echo [%DATE% %TIME%] Programa iniciado. >> "%LOG%"

echo Executando...

echo [%DATE% %TIME%] Programa finalizado. >> "%LOG%"

pause
```

------------------------------------------------------------------------

# 90. Registrar erros

``` bat
programa.exe >saida.log 2>erro.log

if errorlevel 1 (
    echo O programa falhou.
) else (
    echo O programa terminou corretamente.
)
```

------------------------------------------------------------------------

# 91. Salvar saída e erro no mesmo arquivo

``` bat
programa.exe >resultado.log 2>&1
```

Isso envia a saída padrão e os erros para o mesmo arquivo.

------------------------------------------------------------------------

# 92. Executar em segundo plano

Uma opção:

``` bat
start "" programa.exe
```

Se quiser executar um `.bat` separado:

``` bat
start "" outro_script.bat
```

------------------------------------------------------------------------

# 93. Esperar um processo

Uma abordagem simples:

``` bat
programa.exe

if errorlevel 1 (
    echo Falhou.
)
```

O Batch normalmente espera um programa terminar antes de continuar,
salvo quando ele é iniciado de forma assíncrona, como com `start`.

------------------------------------------------------------------------

# 94. Detectar se uma porta está sendo usada

Com `netstat`:

``` bat
netstat -ano | findstr :3000
```

Isso pode ajudar a descobrir se existe algo escutando na porta `3000`.

------------------------------------------------------------------------

# 95. Encerrar processo por porta

Você pode descobrir o PID:

``` bat
netstat -ano | findstr :3000
```

Depois:

``` bat
taskkill /PID 1234 /F
```

É uma técnica útil para servidores locais, mas deve ser usada com
cuidado para não encerrar o processo errado.

------------------------------------------------------------------------

# 96. Servidor local simples com Node

Exemplo de `.bat`:

``` bat
@echo off

cd /d "%~dp0"

echo Iniciando servidor...

node Service\server.js

pause
```

------------------------------------------------------------------------

# 97. Iniciar um servidor e depois fazer outra ação

Uma abordagem simples:

``` bat
@echo off

start "" node Service\server.js

timeout /t 2 /nobreak >nul

curl http://localhost:3000/version

pause
```

**Importante:** `timeout` não garante que o servidor esteja pronto. Ele
apenas espera uma quantidade fixa de tempo.

Uma abordagem mais robusta é testar repetidamente a porta/endpoint.

------------------------------------------------------------------------

# 98. Loop para esperar uma API

Exemplo:

``` bat
@echo off

set "URL=http://localhost:3000/version"

:esperar
curl -s "%URL%" >nul 2>&1

if errorlevel 1 (
    echo Servidor ainda não está disponível...
    timeout /t 1 /nobreak >nul
    goto esperar
)

echo Servidor disponível!

curl "%URL%"

pause
```

Esse padrão é útil para scripts que iniciam um serviço local.

------------------------------------------------------------------------

# 99. Argumentos opcionais

``` bat
@echo off

if "%~1"=="" (
    echo Uso:
    echo programa.bat arquivo.txt
    exit /b 1
)

echo Arquivo recebido: %~1
```

------------------------------------------------------------------------

# 100. Validação de argumento

``` bat
@echo off

if "%~1"=="" (
    echo Erro: argumento ausente.
    exit /b 1
)

if not exist "%~1" (
    echo Erro: arquivo não encontrado.
    exit /b 1
)

echo Arquivo válido: %~1
```

------------------------------------------------------------------------

# 101. Subrotinas organizadas

Uma estrutura razoavelmente organizada:

``` bat
@echo off
setlocal EnableExtensions EnableDelayedExpansion

call :Inicializar
call :Executar
call :Finalizar

exit /b 0


:Inicializar
echo Inicializando...
goto :eof


:Executar
echo Executando...
goto :eof


:Finalizar
echo Finalizando...
goto :eof
```

Esse padrão torna scripts maiores mais fáceis de manter.

------------------------------------------------------------------------

# 102. `EnableExtensions`

Normalmente as extensões do CMD já estão habilitadas, mas você pode
garantir:

``` bat
setlocal EnableExtensions
```

------------------------------------------------------------------------

# 103. `EnableDelayedExpansion`

Quando precisar alterar e ler uma variável dentro do mesmo bloco:

``` bat
setlocal EnableDelayedExpansion
```

E:

``` bat
!variavel!
```

Exemplo:

``` bat
@echo off
setlocal EnableDelayedExpansion

set contador=0

for %%F in (*.txt) do (
    set /a contador+=1
    echo Encontrado: %%F
    echo Total até agora: !contador!
)

echo Total final: !contador!

endlocal
```

------------------------------------------------------------------------

# 104. Contar arquivos

``` bat
@echo off
setlocal EnableDelayedExpansion

set contador=0

for %%F in (*.txt) do (
    set /a contador+=1
)

echo Existem !contador! arquivos .txt.

endlocal
pause
```

------------------------------------------------------------------------

# 105. Processar todos os arquivos

``` bat
@echo off

for %%F in (*.txt) do (
    echo Processando %%F...
)

pause
```

Exemplo de cópia:

``` bat
for %%F in (*.txt) do (
    copy "%%F" "Backup\"
)
```

------------------------------------------------------------------------

# 106. Processar subpastas

``` bat
for /r "%~dp0" %%F in (*.txt) do (
    echo %%F
)
```

Isso percorre recursivamente a pasta do script.

------------------------------------------------------------------------

# 107. Obter informações de arquivos

``` bat
for %%F in ("arquivo.txt") do (
    echo Caminho: %%~fF
    echo Nome: %%~nF
    echo Extensão: %%~xF
    echo Tamanho: %%~zF
)
```

------------------------------------------------------------------------

# 108. Variável com data e hora

``` bat
echo Data: %DATE%
echo Hora: %TIME%
```

Para logs simples:

``` bat
echo [%DATE% %TIME%] Evento >> log.txt
```

**Observação:** o formato de `%DATE%` depende das configurações
regionais do Windows.

------------------------------------------------------------------------

# 109. Variáveis de ambiente persistentes

`set` altera a variável somente no processo atual:

``` bat
set TESTE=123
```

Para alterar permanentemente uma variável de ambiente:

``` bat
setx TESTE 123
```

**Cuidado:** `setx` não altera a variável já existente na sessão atual.
A alteração normalmente será percebida por novos processos.

------------------------------------------------------------------------

# 110. `setx` e PATH

É possível modificar o PATH com `setx`, mas isso exige cuidado porque
uma utilização inadequada pode sobrescrever o PATH existente.

Para alterações de ambiente em scripts temporários, prefira:

``` bat
set "PATH=%PATH%;C:\MeuPrograma"
```

------------------------------------------------------------------------

# 111. `assoc` e `ftype`

Ver associação de extensão:

``` bat
assoc .txt
```

Ver tipo de arquivo:

``` bat
ftype
```

Esses comandos mexem nas associações de arquivos do Windows e devem ser
usados com cautela.

------------------------------------------------------------------------

# 112. `attrib`

Mostrar/alterar atributos:

``` bat
attrib arquivo.txt
```

Remover atributo somente leitura:

``` bat
attrib -r arquivo.txt
```

Atributos comuns:

``` text
R = somente leitura
A = arquivo
S = sistema
H = oculto
```

------------------------------------------------------------------------

# 113. `tree`

Mostra a estrutura de diretórios:

``` bat
tree
```

Com arquivos:

``` bat
tree /f
```

------------------------------------------------------------------------

# 114. `clip`

Envia texto para a área de transferência:

``` bat
echo Olá | clip
```

Exemplo:

``` bat
ipconfig | clip
```

Depois, cole com `Ctrl+V`.

------------------------------------------------------------------------

# 115. `ver`

Mostra a versão do Windows:

``` bat
ver
```

------------------------------------------------------------------------

# 116. `systeminfo`

Exibe informações do sistema:

``` bat
systeminfo
```

Pode gerar bastante saída.

------------------------------------------------------------------------

# 117. `hostname`

Mostra o nome do computador:

``` bat
hostname
```

------------------------------------------------------------------------

# 118. `whoami`

Mostra o usuário atual:

``` bat
whoami
```

------------------------------------------------------------------------

# 119. `date` e `time`

Exibir/alterar data:

``` bat
date
```

Exibir/alterar hora:

``` bat
time
```

Alterar configurações de sistema pode exigir privilégios
administrativos.

------------------------------------------------------------------------

# 120. `shutdown`

Desligar:

``` bat
shutdown /s /t 0
```

Reiniciar:

``` bat
shutdown /r /t 0
```

Cancelar desligamento:

``` bat
shutdown /a
```

**Cuidado:** esses comandos têm efeito real no computador.

------------------------------------------------------------------------

# 121. Verificar privilégios administrativos

Uma técnica comum:

``` bat
net session >nul 2>&1

if errorlevel 1 (
    echo Este script nao possui privilegios administrativos.
) else (
    echo Executando como administrador.
)
```

------------------------------------------------------------------------

# 122. Reiniciar o próprio script como administrador

Um padrão comum usa PowerShell:

``` bat
@echo off

net session >nul 2>&1

if errorlevel 1 (
    powershell -Command "Start-Process '%~f0' -Verb RunAs"
    exit /b
)

echo Agora estamos como administrador.
pause
```

Isso fará o Windows solicitar elevação via UAC.

------------------------------------------------------------------------

# 123. `pushd` e `popd`

`pushd` salva o diretório atual e muda para outro:

``` bat
pushd "C:\Projetos"
```

Depois:

``` bat
popd
```

retorna ao diretório anterior.

Exemplo:

``` bat
@echo off

pushd "C:\Projetos"

echo Diretório atual:
cd

popd

echo Voltamos para:
cd

pause
```

------------------------------------------------------------------------

# 124. `for /f` lendo comando

Muito útil:

``` bat
for /f "tokens=*" %%A in ('hostname') do (
    set "computador=%%A"
)

echo Computador: %computador%
```

Com delayed expansion em blocos maiores:

``` bat
@echo off
setlocal EnableDelayedExpansion

for /f "tokens=*" %%A in ('hostname') do (
    set "computador=%%A"
)

echo Computador: !computador!

endlocal
```

------------------------------------------------------------------------

# 125. Capturar saída de `curl`

``` bat
for /f "delims=" %%A in ('curl -s http://localhost:3000/version') do (
    echo Resposta: %%A
)
```

Isso captura linhas da saída do comando.

**Observação:** Batch não é uma ferramenta confortável para analisar
JSON complexo. Para APIs JSON, PowerShell, Node.js, Python ou C#
costumam ser opções melhores.

------------------------------------------------------------------------

# 126. Exemplo: verificar uma versão

Supondo que uma API retorne:

``` json
{"this version":"v1.0.1","actual version":"v1.0.2"}
```

O Batch pode consultar:

``` bat
curl -s http://localhost:3000/version
```

Mas fazer parsing confiável desse JSON apenas com Batch é
desnecessariamente difícil.

Uma arquitetura melhor pode ser:

``` text
BAT
 ↓
Node.js / PowerShell / C#
 ↓
API
 ↓
JSON
```

Use Batch como orquestrador, não como substituto de uma linguagem de
programação completa.

------------------------------------------------------------------------

# 127. Ver ajuda de qualquer comando

Quase todo comando do CMD oferece:

``` bat
comando /?
```

Exemplos:

``` bat
dir /?
copy /?
for /?
if /?
set /?
robocopy /?
```

Este é um dos recursos mais importantes para aprender Batch.

------------------------------------------------------------------------

# 128. `help`

Lista comandos disponíveis:

``` bat
help
```

Ajuda sobre um comando:

``` bat
help for
```

------------------------------------------------------------------------

# 129. Estrutura recomendada para um script intermediário

Uma estrutura limpa:

``` bat
@echo off
setlocal EnableExtensions EnableDelayedExpansion

:: ==========================================
:: CONFIGURAÇÃO
:: ==========================================

set "ROOT=%~dp0"
set "LOG=%ROOT%logs\program.log"

:: ==========================================
:: INICIALIZAÇÃO
:: ==========================================

if not exist "%ROOT%logs" mkdir "%ROOT%logs"

call :log "Programa iniciado."

:: ==========================================
:: PROGRAMA
:: ==========================================

call :main

:: ==========================================
:: FINALIZAÇÃO
:: ==========================================

call :log "Programa finalizado."

endlocal
exit /b 0


:main
echo Programa executando...
goto :eof


:log
echo [%DATE% %TIME%] %~1>>"%LOG%"
goto :eof
```

------------------------------------------------------------------------

# 130. Exemplo de script intermediário completo

Este exemplo:

-   define a pasta do projeto;
-   cria uma pasta de logs;
-   verifica se Node.js existe;
-   inicia um servidor;
-   espera o endpoint ficar disponível;
-   consulta a API;
-   registra o resultado.

``` bat
@echo off
setlocal EnableExtensions EnableDelayedExpansion

title Gerenciador do Projeto

set "ROOT=%~dp0"
set "LOG=%ROOT%logs\program.log"
set "URL=http://localhost:3000/version"

if not exist "%ROOT%logs" (
    mkdir "%ROOT%logs"
)

call :log "Iniciando."

where node >nul 2>&1

if errorlevel 1 (
    call :log "Node.js não encontrado."
    echo ERRO: Node.js não encontrado.
    exit /b 1
)

call :log "Node.js encontrado."

cd /d "%ROOT%"

echo Iniciando servidor...
start "" node "Service\server.js"

call :waitServer

if errorlevel 1 (
    call :log "Servidor não respondeu."
    echo ERRO: servidor não respondeu.
    exit /b 1
)

echo Servidor disponível!

curl -s "%URL%"

if errorlevel 1 (
    call :log "Falha ao consultar API."
    exit /b 1
)

call :log "Consulta concluída."
call :log "Programa finalizado."

endlocal
exit /b 0


:waitServer

set /a tentativas=0

:check
set /a tentativas+=1

if !tentativas! GTR 15 (
    exit /b 1
)

curl -s "%URL%" >nul 2>&1

if not errorlevel 1 (
    exit /b 0
)

timeout /t 1 /nobreak >nul

goto check


:log

echo [%DATE% %TIME%] %~1>>"%LOG%"

goto :eof
```

------------------------------------------------------------------------

# 131. Boas práticas

## Use aspas em caminhos

Prefira:

``` bat
"C:\Program Files\Programa\programa.exe"
```

## Use `set "VAR=valor"`

Prefira:

``` bat
set "ARQUIVO=C:\Minha Pasta\arquivo.txt"
```

## Use `%~dp0` para arquivos relativos ao script

``` bat
set "ROOT=%~dp0"
```

## Use `setlocal`

``` bat
setlocal
...
endlocal
```

## Use `errorlevel`

Depois de comandos importantes:

``` bat
if errorlevel 1 ...
```

## Evite `del /s /q` sem validação

Comandos destrutivos merecem cuidado extra.

------------------------------------------------------------------------

# 132. Armadilhas comuns

## Problema 1 --- espaços

Errado:

``` bat
set caminho=C:\Minha Pasta
```

Melhor:

``` bat
set "caminho=C:\Minha Pasta"
```

------------------------------------------------------------------------

## Problema 2 --- `%` em loops

No `.bat`:

``` bat
for %%F in (*) do echo %%F
```

No CMD interativo:

``` cmd
for %F in (*) do echo %F
```

------------------------------------------------------------------------

## Problema 3 --- variável dentro de bloco

Pode acontecer:

``` bat
set x=0

(
    set /a x+=1
    echo %x%
)
```

Para esses casos:

``` bat
setlocal EnableDelayedExpansion

set x=0

(
    set /a x+=1
    echo !x!
)
```

------------------------------------------------------------------------

## Problema 4 --- `start`

Isto pode ser problemático:

``` bat
start "C:\Programa\programa.exe"
```

O primeiro argumento entre aspas pode ser interpretado como título.

Prefira:

``` bat
start "" "C:\Programa\programa.exe"
```

------------------------------------------------------------------------

## Problema 5 --- confiar em `timeout`

Isto:

``` bat
start "" servidor.exe
timeout /t 2
```

não garante que o servidor esteja pronto depois de 2 segundos.

Quando a disponibilidade realmente importa, faça uma verificação ativa.

------------------------------------------------------------------------

# 133. Segurança

Batch pode executar praticamente qualquer comando que o usuário tenha
permissão para executar. Portanto, tenha cuidado com:

``` bat
del
rmdir
format
diskpart
shutdown
taskkill
reg
setx
```

Especialmente combinações com:

``` bat
/q
/s
/f
```

Nunca execute um script encontrado na internet sem ler o conteúdo
primeiro.

------------------------------------------------------------------------

# 134. Batch como orquestrador

Uma arquitetura muito útil é:

``` text
                ┌──────────────┐
                │   .BAT       │
                │ Orquestrador │
                └──────┬───────┘
                       │
          ┌────────────┼─────────────┐
          ↓            ↓             ↓
       Node.js     PowerShell       C#
          │            │             │
          └────────────┼─────────────┘
                       ↓
                  Outros serviços
```

Batch é excelente para:

-   iniciar programas;
-   configurar ambiente;
-   executar vários comandos;
-   automatizar builds;
-   criar diretórios;
-   copiar arquivos;
-   iniciar servidores;
-   encadear ferramentas;
-   preparar ambientes de desenvolvimento.

Ele começa a ficar desconfortável para:

-   parsing complexo de JSON;
-   estruturas de dados grandes;
-   aplicações com muita lógica;
-   HTTP sofisticado;
-   criptografia;
-   manipulação complexa de strings;
-   aplicações com interface;
-   código que precisa ser facilmente testável e mantido.

Nesses casos, use uma linguagem apropriada e deixe o `.bat` como camada
de automação.

------------------------------------------------------------------------

# 135. Mini referência rápida

``` bat
@echo off
echo Texto
pause
cls

set "VAR=valor"
echo %VAR%

set /a N=10+5
set /p INPUT=Digite:

if exist arquivo.txt echo Existe
if "%VAR%"=="valor" echo Igual

for %%F in (*.txt) do echo %%F
for /r %%F in (*.txt) do echo %%F
for /l %%N in (1,1,10) do echo %%N

mkdir pasta
rmdir pasta
copy arquivo.txt destino\
move arquivo.txt destino\
del arquivo.txt
ren antigo.txt novo.txt

cd /d "C:\Pasta"
dir
tree /f

type arquivo.txt
findstr "texto" arquivo.txt
where programa

start "" programa.exe
timeout /t 5
choice /c SN

tasklist
taskkill /IM programa.exe /F

ipconfig
ping 8.8.8.8
netstat -ano
curl http://localhost:3000

call :funcao
goto :eof

setlocal EnableDelayedExpansion
echo !VAR!
endlocal

exit /b 0
```

------------------------------------------------------------------------

# 136. Ordem recomendada para estudar

Se você está começando, não tente decorar tudo.

### Nível 1 --- Fundamentos

Aprenda primeiro:

``` text
echo
@echo off
rem
pause
cls
set
set /a
set /p
```

### Nível 2 --- Arquivos e diretórios

Depois:

``` text
cd
mkdir
rmdir
dir
copy
move
ren
del
type
```

### Nível 3 --- Controle de fluxo

Depois:

``` text
if
else
goto
for
choice
call
```

### Nível 4 --- Automação

Depois:

``` text
errorlevel
setlocal
endlocal
EnableDelayedExpansion
for /f
for /r
for /l
```

### Nível 5 --- Integração com Windows

Por fim:

``` text
start
tasklist
taskkill
where
curl
netstat
ipconfig
robocopy
powershell
```

------------------------------------------------------------------------

# 137. O que realmente vale dominar

Se o objetivo é criar scripts Batch úteis, eu priorizaria estes
conceitos:

1.  `set`
2.  `set /a`
3.  `set /p`
4.  `if`
5.  `for`
6.  `for /f`
7.  `call`
8.  `%~dp0`
9.  `errorlevel`
10. `setlocal`
11. delayed expansion (`!VAR!`)
12. redirecionamento (`>`, `>>`, `2>`, `2>&1`)
13. pipes (`|`)
14. `&&` e `||`
15. `start`
16. `curl`
17. `robocopy`
18. `tasklist` / `taskkill`
19. `where`
20. integração com PowerShell/Node/C#.

Esses conceitos já permitem construir scripts consideravelmente mais
úteis do que simples arquivos que executam meia dúzia de comandos em
sequência.

------------------------------------------------------------------------

# 138. Exercícios recomendados

## Exercício 1 --- Calculadora

Crie um `.bat` que peça dois números e mostre:

-   soma;
-   subtração;
-   multiplicação;
-   divisão;
-   resto.

------------------------------------------------------------------------

## Exercício 2 --- Organizador

Crie um script que:

-   crie pastas `TXT`, `PNG`, `JPG`, `ZIP`;
-   encontre arquivos pela extensão;
-   mova cada arquivo para sua respectiva pasta.

------------------------------------------------------------------------

## Exercício 3 --- Backup

Crie um script que:

-   receba uma pasta como `%1`;
-   verifique se ela existe;
-   crie uma pasta de backup;
-   copie seu conteúdo usando `robocopy`;
-   registre tudo em um log.

------------------------------------------------------------------------

## Exercício 4 --- Menu

Crie um menu:

``` text
1 - Informações do sistema
2 - Processos
3 - IP
4 - Abrir projeto
5 - Sair
```

Use `choice`.

------------------------------------------------------------------------

## Exercício 5 --- Monitor de servidor

Crie um script que:

1.  inicie um servidor;
2.  espere a porta/API ficar disponível;
3.  faça uma requisição;
4.  mostre a resposta;
5.  registre erros;
6.  encerre corretamente.

------------------------------------------------------------------------

# 139. Referência mental

Pense em Batch assim:

``` text
VARIÁVEIS
    ↓
set / set /a / set /p
    ↓
DECISÕES
    ↓
if
    ↓
REPETIÇÃO
    ↓
for
    ↓
FUNÇÕES
    ↓
call
    ↓
ESCOPO
    ↓
setlocal / endlocal
    ↓
EXPANSÃO
    ↓
%VAR% / !VAR!
    ↓
SISTEMA
    ↓
cmd / start / tasklist / robocopy / curl
```

Quando esses conceitos estiverem claros, você já terá a base necessária
para escrever scripts Batch intermediários sem depender de copiar
comandos aleatórios da internet.

------------------------------------------------------------------------

## Comando final mais importante

Quando não souber como um comando funciona:

``` bat
comando /?
```

Exemplo:

``` bat
for /?
```

A documentação embutida do próprio Windows é uma das melhores
ferramentas para avançar de scripts básicos para scripts realmente
robustos.
