# 🖥️ Guia Básico do CMD — Windows

> Guia de referência rápida para aprender os principais comandos do Prompt de Comando.

---

# 📁 1. Navegação entre pastas

| Comando | O que faz                    | Exemplo         |
| ------- | ---------------------------- | --------------- |
| `dir`   | Lista arquivos e pastas      | `dir`           |
| `cd`    | Entra em uma pasta           | `cd Documentos` |
| `cd ..` | Volta uma pasta              | `cd ..`         |
| `cd \`  | Vai para a raiz do disco     | `cd \`          |
| `cls`   | Limpa a tela                 | `cls`           |
| `tree`  | Mostra a estrutura de pastas | `tree`          |

### Exemplo

```cmd
cd Documentos
dir
cd ..
```

---

# 📄 2. Arquivos e pastas

| Comando | Função                                  | Exemplo                   |
| ------- | --------------------------------------- | ------------------------- |
| `mkdir` | Cria uma pasta                          | `mkdir Projeto`           |
| `rmdir` | Remove uma pasta                        | `rmdir Projeto`           |
| `del`   | Apaga arquivo(s)                        | `del teste.txt`           |
| `copy`  | Copia arquivos                          | `copy a.txt b.txt`        |
| `move`  | Move arquivos                           | `move a.txt C:\Temp`      |
| `ren`   | Renomeia arquivo/pasta                  | `ren antigo.txt novo.txt` |
| `type`  | Exibe o conteúdo de um arquivo de texto | `type notas.txt`          |

### Exemplo prático

```cmd
mkdir MeuProjeto
cd MeuProjeto
echo Olá > teste.txt
type teste.txt
ren teste.txt resultado.txt
```

---

# 💻 3. Informações do computador

| Comando      | Função                                   |
| ------------ | ---------------------------------------- |
| `systeminfo` | Mostra informações detalhadas do Windows |
| `hostname`   | Mostra o nome do computador              |
| `whoami`     | Mostra o usuário atual                   |
| `ver`        | Mostra a versão do Windows               |
| `set`        | Mostra variáveis de ambiente             |
| `echo`       | Exibe texto ou valores de variáveis      |

### Exemplo

```cmd
whoami
hostname
ver
```

---

# 🌐 4. Comandos de rede

| Comando         | Função                           |
| --------------- | -------------------------------- |
| `ipconfig`      | Mostra configurações de rede     |
| `ipconfig /all` | Mostra informações detalhadas    |
| `ping`          | Testa conexão com um endereço    |
| `tracert`       | Mostra o caminho até um servidor |
| `nslookup`      | Consulta DNS                     |
| `netstat`       | Mostra conexões de rede          |
| `hostname`      | Mostra o nome do computador      |

### Exemplos

```cmd
ipconfig
ping google.com
nslookup google.com
```

---

# ⚙️ 5. Processos e programas

| Comando    | Função                                     |
| ---------- | ------------------------------------------ |
| `tasklist` | Lista processos em execução                |
| `taskkill` | Finaliza um processo                       |
| `start`    | Inicia um programa ou abre uma nova janela |
| `shutdown` | Desliga ou reinicia o computador           |

### Listar processos

```cmd
tasklist
```

### Encerrar um processo

```cmd
taskkill /PID 1234 /F
```

> ⚠️ `/F` força o encerramento do processo. Use com cuidado.

---

# 🚀 6. Como iniciar um programa pelo CMD

Existem várias maneiras.

## 6.1. Programa que está no PATH

Se o programa estiver disponível no `PATH` do Windows, você pode simplesmente digitar o comando.

### Python

```cmd
python
```

### Git

```cmd
git
```

### VS Code

```cmd
code .
```

O `.` significa **"pasta atual"**.

Então:

```cmd
cd C:\MeuProjeto
code .
```

abre a pasta `C:\MeuProjeto` no VS Code, desde que o comando `code` esteja disponível no PATH.

---

# 6.2. Executar um `.exe` pelo caminho completo

Se você souber onde está o executável:

```cmd
"C:\Programas\MeuPrograma\programa.exe"
```

Também é possível usar:

```cmd
start "" "C:\Programas\MeuPrograma\programa.exe"
```

### Por que `start ""`?

Porque o `start` interpreta o primeiro argumento entre aspas como o **título da janela**.

Por isso:

```cmd
start "" "C:\Meu Programa\programa.exe"
```

é uma forma segura de iniciar um executável cujo caminho possui espaços.

---

# 6.3. Programas instalados normalmente

Muitos programas podem ser iniciados diretamente pelo nome ou por um comando registrado no sistema.

Exemplos comuns:

```cmd
notepad
calc
mspaint
```

Também é possível:

```cmd
start notepad
```

ou:

```cmd
start calc
```

---

# 6.4. Abrir arquivos com o programa padrão

O CMD também pode pedir ao Windows para abrir um arquivo usando o programa associado a ele.

```cmd
start arquivo.txt
```

Por exemplo:

```cmd
start documento.pdf
```

O Windows tentará abrir o PDF no programa padrão configurado para arquivos `.pdf`.

---

# 6.5. Abrir uma pasta no Explorer

```cmd
start .
```

Abre a pasta atual no Explorador de Arquivos.

Também pode fazer:

```cmd
start C:\
```

ou:

```cmd
start C:\Users
```

---

# 6.6. Executar um programa com argumentos

Programas podem receber argumentos pela linha de comando.

Exemplo:

```cmd
programa.exe argumento1 argumento2
```

Com `start`:

```cmd
start "" "C:\Programas\MeuPrograma\programa.exe" argumento1 argumento2
```

Os argumentos dependem do programa.

Por exemplo, muitos programas possuem opções como:

```cmd
programa.exe --help
```

ou:

```cmd
programa.exe --version
```

---

# 6.7. Iniciar um programa em determinada pasta

Você pode primeiro entrar na pasta:

```cmd
cd C:\MeuProjeto
start "" "C:\Programas\MeuEditor\editor.exe"
```

Ou usar `/D`:

```cmd
start "" /D "C:\MeuProjeto" "C:\Programas\MeuEditor\editor.exe"
```

---

# 🧭 7. Descobrir onde um programa está

O comando `where` é extremamente útil.

```cmd
where python
```

Pode retornar algo semelhante a:

```text
C:\Users\Usuario\AppData\Local\Programs\Python\Python313\python.exe
```

Você também pode procurar:

```cmd
where git
```

ou:

```cmd
where code
```

Isso é particularmente útil para descobrir se um programa está no `PATH`.

---

# 🔎 8. Ver o PATH

O `PATH` é uma variável de ambiente que contém diretórios onde o Windows procura executáveis.

Para visualizar:

```cmd
echo %PATH%
```

Se você executar:

```cmd
python
```

por exemplo, o Windows procura o `python.exe` nos locais disponíveis no `PATH`.

---

# 🆘 9. Ajuda do próprio CMD

Não é necessário decorar todos os comandos.

Use:

```cmd
help
```

Para obter ajuda sobre um comando específico:

```cmd
comando /?
```

### Exemplos

```cmd
dir /?
```

```cmd
ipconfig /?
```

```cmd
start /?
```

```cmd
taskkill /?
```

> 💡 `comando /?` é uma das coisas mais úteis para aprender CMD de verdade.

---

# 🔧 10. Diagnóstico e reparo

## Verificar arquivos do sistema

```cmd
sfc /scannow
```

Verifica e tenta reparar arquivos protegidos do sistema Windows.

---

## Verificar o sistema de arquivos

```cmd
chkdsk
```

---

## Reparar a imagem do Windows

```cmd
DISM /Online /Cleanup-Image /RestoreHealth
```

> ⚠️ Esses comandos são mais avançados. Não é necessário executá-los sem uma razão específica.

---

# 🧪 11. Exemplo de uma sessão completa

```cmd
mkdir MeuProjeto
cd MeuProjeto
echo Olá mundo > teste.txt
type teste.txt
dir
code .
```

O que aconteceu:

1. `mkdir MeuProjeto` → criou a pasta.
2. `cd MeuProjeto` → entrou na pasta.
3. `echo Olá mundo > teste.txt` → criou um arquivo.
4. `type teste.txt` → mostrou o conteúdo.
5. `dir` → listou os arquivos.
6. `code .` → abriu a pasta atual no VS Code.

---

# ⭐ 12. Comandos para decorar primeiro

Se você está começando, priorize estes:

```text
cd
dir
cd ..
cls
mkdir
rmdir
del
copy
move
ren
type
echo
start
where
ipconfig
ping
tasklist
```

---

# 📌 13. Resumo rápido

```cmd
dir                         :: listar arquivos
cd Pasta                    :: entrar em uma pasta
cd ..                       :: voltar uma pasta
cd \                        :: ir para a raiz
cls                         :: limpar a tela

mkdir Pasta                 :: criar pasta
rmdir Pasta                 :: remover pasta
del arquivo.txt             :: apagar arquivo
copy origem destino         :: copiar
move origem destino         :: mover
ren antigo novo             :: renomear
type arquivo.txt            :: mostrar conteúdo

echo Olá                    :: mostrar texto
echo Olá > arquivo.txt      :: criar/escrever arquivo

ipconfig                    :: informações de rede
ping google.com             :: testar conexão
nslookup google.com         :: consultar DNS
tracert google.com          :: rastrear caminho de rede
netstat                     :: mostrar conexões

tasklist                    :: listar processos
taskkill /PID 1234 /F       :: encerrar processo

start "" "programa.exe"     :: iniciar programa
start .                     :: abrir pasta atual
where programa              :: descobrir localização do executável

systeminfo                  :: informações do sistema
hostname                    :: nome do computador
whoami                      :: usuário atual
ver                         :: versão do Windows

help                        :: ajuda geral
comando /?                  :: ajuda de um comando específico
```

---

# 🧠 14. CMD, PowerShell e outros terminais

O CMD é apenas um dos ambientes de linha de comando disponíveis no Windows.

### CMD

Simples, antigo e ainda muito útil para tarefas do Windows.

### PowerShell

Mais poderoso para administração, automação e scripts no Windows.

### Git Bash

Muito conveniente para quem trabalha com Git e ferramentas tradicionalmente usadas em Linux/Unix.

### WSL

Permite utilizar distribuições Linux dentro do Windows.

### Terminal do VS Code

Integra o terminal diretamente ao ambiente de desenvolvimento.

Para programação, uma sequência interessante é:

**CMD → PowerShell → Git → terminal do VS Code → WSL/Linux**

---

# 🎯 15. Regra de ouro

Não tente decorar centenas de comandos.

Aprenda principalmente:

```cmd
cd
dir
start
where
comando /?
```

Com esses comandos você já consegue:

* navegar pelo computador;
* descobrir o que existe em uma pasta;
* iniciar programas;
* descobrir onde os executáveis estão;
* consultar a documentação de praticamente qualquer comando.

Depois, aprenda os comandos conforme surgir uma necessidade real.

---

## ⚡ Mini cola

```cmd
:: Onde estou?
cd

:: O que existe aqui?
dir

:: Entrar em uma pasta
cd NomeDaPasta

:: Voltar
cd ..

:: Criar pasta
mkdir NomeDaPasta

:: Iniciar programa
start "" "C:\Caminho\programa.exe"

:: Descobrir onde está um programa
where programa

:: Abrir a pasta atual no Explorer
start .

:: Abrir a pasta atual no VS Code
code .

:: Ver ajuda
comando /?

:: Limpar a tela
cls
```
