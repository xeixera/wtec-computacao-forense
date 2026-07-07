# Minicurso de Computação Forense - WTEC

Repositório com os materiais utilizados no **Minicurso de Computação Forense** ministrado durante o **WTEC**.

## 📂 Conteúdo

Este repositório contém:

- 📑 **Slides** utilizados durante o minicurso;
- 💾 **Imagem forense (`.dd`)** que será utilizada na atividade prática;
- 📝 **Documento com a atividade**, contendo as perguntas que deverão ser respondidas pelos participantes, simulando a elaboração de um laudo pericial.

## 📁 Estrutura

```text
.
├── docs/
│   └── Laudo.docx   
│   └── slides.pdf                      
└── README.md
```

## 1. Instalação da imagem 

[https://drive.google.com/file/d/1wzIq1aKV3xeARUxocHLrXPrCqhZaa3M3/view?usp=drive_link](https://drive.google.com/file/d/1YfHFqnQUuDgtvap4dy1olmX4t2kqzRhC/view?usp=drive_link)

## 🛠 Ferramentas sugeridas

As análises podem ser realizadas utilizando ferramentas como:

- Autopsy
- The Sleuth Kit (TSK)
- Photorec
- Foremost
- Exiftool
- Editores de hexadecimal
- Outras ferramentas de computação forense compatíveis

## 1. Instalação das ferramentas

Instale as ferramentas necessárias com:

```bash
sudo apt update && sudo apt install foremost testdisk exiftool autopsy ghex sleuthkit
```

## 2. Montando a imagem forense

Crie um dispositivo de loop para a imagem `minicurso-forense.dd`:

```bash
sudo losetup -Pf minicurso-forense.dd
```

Verifique qual dispositivo foi criado:

```bash
losetup -a
```

Monte a(s) partição(ões) **somente para leitura**:

```bash
sudo mount /dev/loopXp1 /seu/diretorio -o ro
```

Substitua:

- `/dev/loopXp1` pela partição correta (ex.: `/dev/loop0p1`);
- `/seu/diretorio` pelo diretório onde deseja montar a imagem.

> **Importante:** utilize sempre a opção `-o ro` para evitar qualquer modificação na evidência.

## 3. Correção do Autopsy

A versão do Perl do Autopsy irá impedir que o programa rode devido ao parâmetro -T, e irá apresentar o erro:

```text
Insecure directory in $ENV{PATH} while running with -T switch
```

Edite o script de inicialização:

```bash
sudo nano $(which autopsy)
```

Altere a primeira linha de:

```perl
#!/usr/bin/perl -wT
```

para:

```perl
#!/usr/bin/perl -w
```

Salve o arquivo e execute o Autopsy normalmente.


## 5. Análise da evidência

Após montar a imagem forense, **não inicie imediatamente as ferramentas de análise**. Antes de qualquer procedimento, procure compreender o contexto do caso.

Na computação forense, o trabalho do perito não consiste apenas em recuperar arquivos ou encontrar evidências. É fundamental interpretar o cenário, entender o comportamento do usuário e relacionar as evidências com os fatos apresentados.

Durante a análise, procure responder perguntas como:

- Qual é o contexto da investigação?
- Quem pode ser o usuário da máquina?
- Quais atividades foram realizadas?
- Existem documentos, imagens ou arquivos relevantes para o caso?
- Há indícios de tentativa de ocultação ou exclusão de informações?

Além da análise técnica, utilize também técnicas de **engenharia social**, observando detalhes que permitam compreender o comportamento do usuário. Nomes de arquivos, organização das pastas, documentos pessoais, histórico de navegação, fotografias e outros artefatos podem fornecer informações importantes para contextualizar a investigação.

Lembre-se de que, em uma perícia real, uma evidência isolada raramente é suficiente. O objetivo é correlacionar diferentes informações para reconstruir os acontecimentos e produzir uma conclusão fundamentada.

> **Dica:** Antes de utilizar ferramentas, explore manualmente a imagem montada. Muitas informações relevantes podem ser identificadas apenas observando a estrutura de diretórios, os arquivos presentes e sua organização.



Este material foi desenvolvido exclusivamente para fins educacionais durante o **Minicurso de Computação Forense - WTEC**.
