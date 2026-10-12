## Criando MessageBox do windows

```
    [DllImport("user32.dll", CharSet = CharSet.Unicode)]
    private static extern int MessageBox(
        IntPtr hWnd,
        string txt,
        string caption,
        uint type
    );
```

## Nota

> Usamos isso para definir tamanho, mensagem, titulo, botões e coisas do tipo.

## Tipos de botões

Os botões são feitos com códigos como `0x04`, a lista deles estão aqui a baixo:

```
0x00 // OK
0x01 // OK / Cancelar
0x02 // Abortar / Repetir / Ignorar
0x03 // Sim / Não / Cancelar
0x04 // Sim / Não
```

E os ícones são esse:

```
0x10 // Erro
0x20 // Pergunta
0x30 // Exclamação
0x40 // Informação
```

A resposta que os botões dão são essa:

```
| Constante  | Valor | Botão    |
| ---------- | ----: | -------- |
| IDOK       |   1   | OK       |
| IDCANCEL   |   2   | Cancelar |
| IDABORT    |   3   | Abortar  |
| IDRETRY    |   4   | Repetir  |
| IDIGNORE   |   5   | Ignorar  |
| IDYES      |   6   | Sim      |
| IDNO       |   7   | Não      |
```