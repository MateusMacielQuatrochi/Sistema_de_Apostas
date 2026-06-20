# 🎰 Sistema de Gerenciamento de Loterias e Apostas (CLI)

Este é um sistema baseado em console (CLI) desenvolvido como projeto acadêmico durante o **2º semestre da faculdade**. O objetivo do software é gerenciar de forma integrada as operações de uma banca de apostas e sorteios (no modelo da Quina/Mega-Sena), estruturando o cadastro de apostadores, concursos e os bilhetes gerados.

O sistema controla três frentes principais por meio de arquivos binários: os **Apostadores**, os **Concursos** (Sorteios) e as **Apostas** (os bilhetes jogados).

---

## 👥 Desenvolvedores
* **Arthur Orosco**
* **Mateus Maciel**
* **Gabriel Pereira**

---

## 🛠️ Tecnologias Utilizadas e Arquitetura

O projeto foi inteiramente construído utilizando **C++ clássico**, aplicando conceitos de Estruturas de Dados Heterogêneas (`structs`) e persistência de dados em disco.

### 1. Bibliotecas Utilizadas
* `<conio2.h>`: Responsável por toda a interface visual (gerenciamento avançado do cursor com `gotoxy` e aplicação de cores com `textcolor`).
* `<stdio.h>` e `<stdlib.h>`: Operações de entrada/saída de dados e manipulação do sistema.
* `<string.h>` e `<ctype.h>`: Tratamento, validação e manipulação de Strings (como CPFs e Nomes).
* `<windows.h>`: Controle de temporização da interface visual (`Sleep`).
* `<time.h>`: Inicialização de geradores numéricos pseudo-aleatórios para simulações de sorteio (`srand`).

### 2. Persistência de Dados e Arquivos Binários
Para evitar a perda de dados ao fechar o console, o sistema cria e manipula arquivos binários diretamente na pasta de execução:
* `Apostadores.dat` (Dados cadastrais dos clientes)
* `Concursos.dat` (Dados dos sorteios oficiais realizados)
* `Apostas.dat` (Relação de bilhetes preenchidos)

---

## 📂 Estrutura das Estruturas de Dados (`structs`)

O núcleo do sistema funciona de maneira relacional por meio de Chaves Primárias (`PK`):

* **`TpConcurso`**: Modela os sorteios oficiais. Armazena o ID do concurso, um vetor de 5 números sorteados (`NumSort`), a data e o status do registro.
* **`TpApostadores`**: Modela o cliente. Utiliza o **CPF como Chave Primária**, registrando Nome, DDD e Telefone do apostador.
* **`TpAposta`**: Modela o bilhete de jogo. Utiliza uma **Chave Primária Composta** (`NumCurso` + `CPF`), guardando a quantidade de números apostados (máximo de 10) e as dezenas escolhidas.

---

## ⚙️ Funcionalidades do Sistema

A aplicação conta com um sistema de **Molduras Personalizadas** (renderizadas via tabela ASCII estendida) que delimitam os seguintes módulos navegáveis:

* **Módulo de Cadastros:** Rotinas com verificação exaustiva de duplicidade em arquivos para novos Concursos, Apostadores e Apostas.
* **Módulo de Buscas:** Localização rápida de registros em disco (`BusAposta_exaust`, `BuscarCPF`, etc.).
* **Módulo de Alterações:** Edição em tempo real de dados cadastrais ou modificação das dezenas jogadas nos bilhetes.
* **Módulo de Exclusão (Lógica e Física):** Os registros desativados recebem a flag de status `'I'` (Inativo). O sistema conta com a função `ExAposta_fisico`, que limpa o armazenamento real gerando arquivos temporários purgados de lixo de memória.
* **Módulo de Relatórios Avançados:**
  * Exibição completa de apostadores comuns e premiados.
  * Estatísticas de dezenas que mais/menos aparecem nos sorteios e bilhetes.
  * Relatório de desempenho específico por quantidade de acertos (Terno, Quadra e Quina).
* **Módulo de Massa de Testes (`InsereTeste`):** Opção rápida integrada ao menu principal (`[F]`) para preencher o sistema instantaneamente com dados simulados para testes de rotina.

---

## 🚀 Como Executar

### Pré-requisitos
Por utilizar as bibliotecas nativas `<windows.h>` e `<conio2.h>`, este sistema foi feito exclusivamente para rodar em ambientes **Windows**.

### 🛠️ Executando no Dev-C++ (Recomendado)
Como o projeto foi desenvolvido utilizando o **Dev-C++**, para compilá-lo corretamente siga estes passos:
1. Abra o **Dev-C++**.
2. Vá em `File > New > Project...`, escolha **Console Application** e certifique-se de selecionar **C++ Project**.
3. Adicione este arquivo de código ao projeto.
4. **Configuração do Conio2:** Certifique-se de que a biblioteca `conio2` está instalada e configurada no seu Dev-C++. Vá em `Project Options (Alt+P) > Parameters` e, no campo **Linker**, adicione: `-lconio`.
5. Pressione `F11` para Compilar e Executar.

### 💻 Compilação alternativa via Prompt de Comando (MinGW/GCC):
Caso prefira compilar direto pelo terminal do Windows:
```bash
g++ main.cpp -o SistemaApostas -lconio
```

Dica de Interface: Utilize as letras indicadas nos colchetes ([A], [B], etc.) para se locomover pelos menus e pressione a tecla ESC para sair ou retornar à tela anterior.

📋 Observações Importantes (Aviso Acadêmico)

⚠️ Este é um projeto estritamente didático e de nível acadêmico de segundo semestre. Possui limitações estruturais intrínsecas:

`*`Gravação sequencial direta em arquivos em formato binário bruto.

`*`Interface gráfica limitada ao buffer padrão do Prompt de Comando do Windows (cmd.exe).

📄 Licença

Este projeto é distribuído sob a licença MIT.
