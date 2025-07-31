# O que é um SGBD?
Um Sistema de Gerenciamento de Banco de Dados (SGBD) é um software que ajuda a armazenar, organizar, proteger e acessar dados de forma rápida e segura. Ele é essencial em qualquer sistema que trabalha com informações — de sites a grandes empresas.

### Principais funções de um SGBD:
1. Organização estruturada: Armazena dados em tabelas, facilitando buscas e análises.
2. Segurança: Controla quem pode acessar ou alterar os dados, com senhas, permissões e criptografia.
3. Consulta rápida: Permite buscar informações específicas com facilidade usando comandos.
4. Acesso simultâneo: Várias pessoas ou sistemas podem usar o banco de dados ao mesmo tempo, sem bagunçar os dados.
5. Garantia de integridade: Impede que dados errados ou duplicados sejam inseridos.
6. Proteção contra falhas: Recupera dados em caso de erro ou queda de sistema.
7. Escalabilidade: Funciona bem mesmo com muitos dados ou usuários.
8. Backup e restauração: Facilita a criação de cópias de segurança para evitar perdas.

### Exemplos populares de SGBDs:
- **MySQL:** Rápido, confiável e gratuito. Muito usado em sites e sistemas web.
- **Oracle:** Robusto e usado por grandes empresas. Oferece alta segurança e desempenho.
- **SQL Server:** Da Microsoft, ótimo para ambientes Windows e integração com outras ferramentas Microsoft.
- **PostgreSQL:** Gratuito, poderoso e flexível. Suporta recursos avançados e cresce bem com o sistema.
- **SQLite:** Leve e simples. Usado em apps mobile, navegadores e programas locais.

### Nesse estudo utilizaremos o SQLite


## Importando dados

Exemplo: Tabela de Fornecedores

1. Clique em Import > Open.
2. Selecione o arquivo da tabela (ex: fornecedores.csv).
3. Na tela de importação: verifique se o tipo está como CSV.
4. Mude a opção Column name de new auto para first line — isso garante que os nomes das colunas fiquem corretos.
5. Clique em OK.

A tabela aparecerá na lateral esquerda, pronta para uso.


## Consultando os dados

1. Clique com o botão direito sobre o nome da tabela (ex: tabelafornecedores).
2. Selecione a opção Select (Show table).
3. Os dados aparecerão na parte central da tela.

Exemplo de consulta gerada:

**SELECT * FROM tabelafornecedores;**

Você verá colunas como:
ID, Nome_do_fornecedor, País_de_Origem, Informações_de_Contato, Data_de_início

### Entendendo o comando SELECT * FROM

**SELECT** → significa "selecionar"
* → significa "todos os dados/colunas"
**FROM** → indica de onde os dados serão extraídos (a tabela)
**tabelapedidos** → nome da tabela que queremos consultar

Esse comando mostra todos os dados da tabela de pedidos.

### Sempre finalize o comando com ponto e vírgula (;), especialmente quando estiver usando vários comandos juntos. Ele ajuda o sistema a entender onde termina cada instrução.

### Para rodar o código:
Clique em Run ou use o atalho Shift + Enter


## Filtrando e eliminando dados repetidos no SQL

### WHERE
Para mostrar só os fornecedores cujo país de origem é "China", usamos:

**SELECT * FROM tabelafornecedores WHERE país_de_origem = 'China';**

O que esse comando faz:
- **SELECT *** → seleciona todos os dados (todas as colunas)
- **FROM tabelafornecedores** → da tabela de fornecedores
- **WHERE país_de_origem** = 'China' → filtra só os fornecedores da China

### DISTINCT
Agora, a Hermex quer saber quais clientes já fizeram pedidos, mas sem listar o mesmo cliente várias vezes.
Usamos:

**SELECT DISTINCT cliente FROM tabelapedidos;**

O que esse comando faz:
- **SELECT DISTINCT cliente** → seleciona apenas clientes únicos (sem repetições)
- **FROM tabelapedidos** → da tabela de pedidos

Resultado: uma lista com os IDs dos clientes únicos que compraram.


##  Criando Tabelas no SQL 
A Hermex Import precisava de uma nova tabela para armazenar os dados dos clientes. Eles já têm os IDs dos clientes (vimos isso com o SELECT DISTINCT na tabela de pedidos), mas esses dados ainda não estavam organizados em uma tabela no banco de dados.

### Passo a passo para criar uma tabela:

- Usamos o comando **CREATE TABLE** para iniciar a criação.

Definimos o nome da nova tabela:
**CREATE TABLE tabelaclientes**

Adicionamos as colunas e seus tipos de dados:
**ID_Cliente**: número inteiro e chave primária.
**Nome_Cliente**: texto com até 250 caracteres.
**Informacoes_de_Contato**: também texto com até 250 caracteres.

Código completo:

**CREATE TABLE tabelaclientes ( ID_Cliente INT PRIMARY KEY, Nome_Cliente VARCHAR(250), Informacoes_de_Contato VARCHAR(250));**

Dica: VARCHAR define texto e o número entre parênteses limita os caracteres.

Vizualizando a nova tabela: 

**SELECT * FROM tabelaclientes;**


# Tipos de Dados em Bancos de Dados

### Texto (String)
**CHAR(n)**
- Armazena texto com tamanho fixo. Ideal quando todos os valores têm o mesmo comprimento.
Exemplo: códigos de estado como "SP", "RJ".

**VARCHAR(n)**
- Armazena texto com tamanho variável, até o limite n. Economiza espaço.
Exemplo: nomes de clientes.

**TEXT**:
- Armazena grandes volumes de texto.
Exemplo: descrições de produtos, observações, artigos.

### Numérico
**INTEGER (INT)**:
- Armazena números inteiros (positivos ou negativos).
Exemplo: quantidade de itens.

**FLOAT (ou REAL)**:
- Armazena números com casas decimais, com menor precisão.
Exemplo: peso, altura.

**NUMERIC (ou DECIMAL)**:
- Armazena valores decimais com precisão exata (casas fixas). Ideal para valores financeiros.
Exemplo: preços, salários.

### Data e Hora
**DATE**:
- Armazena apenas data (ano-mês-dia). 
Exemplo: 2025-07-30.

**TIME**:
- Armazena apenas o horário (hora:minuto:segundo).
Exemplo: 14:30:00.

**TIMESTAMP**:
- Armazena data e hora juntas.
Exemplo: 2025-07-30 14:30:00.

### Booleano
**BOOLEAN (ou BOOL)**:
- Armazena valores lógicos: TRUE ou FALSE (ou 1 e 0 dependendo do SGBD).
Exemplo: cliente_ativo = TRUE

### Binário
**BLOB (Binary Large Object)**:
- Armazena arquivos binários, como imagens, vídeos, PDFs.
Exemplo: foto do perfil.

### BIT:
- Armazena valores binários simples (0 ou 1).
Exemplo: flag para "ligado/desligado".

## Cada SGBD (Sistema de Gerenciamento de Banco de Dados) pode ter variações ou tipos específicos. Alguns sistemas, como PostgreSQL ou MySQL, permitem até tipos personalizados.

## SQL: CREATE DATABASE, SCHEMA e TABELAS
**SQL** é uma linguagem de consulta estruturada que permite criar, modificar e gerenciar bancos de dados e seus objetos. Para criar **tabelas**, **bancos de dados** e **esquemas**, utilizamos o comando `CREATE`. Vamos entender a diferença entre essas estruturas:

### Banco de Dados
- Uma coleção de dados organizados e relacionados.
- Atua como um contêiner para objetos como tabelas, índices, procedures e esquemas.
- Pode conter múltiplos esquemas.
- É uma entidade de **nível superior** que armazena e gerencia informações em um SGBD.

### Esquema (Schema)
- Um contêiner lógico para objetos de banco, como tabelas e visões.
- Usado para organizar e segmentar os objetos dentro de um banco.
- Vários esquemas podem coexistir em um único banco de dados.
- Permite aplicar permissões específicas.
- É uma estrutura de **nível inferior** em relação ao banco de dados.

# Criando um Banco de Dados

**CREATE DATABASE BibliotecaDB;**

## Alterando e Excluindo Tabelas no SQL

## ALTER TABLE — Alterar uma tabela existente
A Hermex Import pediu uma nova coluna chamada Endereço_Cliente na tabela tabelaclientes. Para isso, usamos:

**ALTER TABLE tabelaclientes ADD Endereço_Cliente VARCHAR(250);**

Explicando:
**ALTER TABLE**: indica que queremos alterar a estrutura da tabela.
**ADD**: adiciona um novo elemento (nesse caso, uma coluna).
**VARCHAR(250)**: define que essa nova coluna armazenará textos de até 250 caracteres.

Após executar, a nova coluna aparecerá na lista da tabela, junto com as anteriores.

## DROP TABLE — Apagar uma tabela inteira
Se quisermos apagar completamente a tabela (com todos os dados e estrutura), usamos:

**DROP TABLE tabelaclientes;**

Atenção:
- Esse comando deleta tudo. Não dá para recuperar depois.
- Ideal apenas quando a tabela não é mais necessária ou precisa ser refeita do zero.

Também existe:

**DROP SCHEMA nomedobancodedados;**

Para apagar um banco de dados inteiro, com todas as suas tabelas. Use com muito cuidado.

Conclusão rápida:
- Use ALTER TABLE para modificar uma tabela já criada (como adicionar colunas).
- Use DROP TABLE para apagar uma tabela inteira.
- Esses comandos são úteis tanto para corrigir quanto para recomeçar parte do seu projeto SQL.


## Comando DROP — Apagando objetos do banco
Usado para excluir objetos como tabelas, bancos de dados, esquemas, índices, usuários, etc.

Sintaxe básica:

**DROP tipo_do_objeto nome_do_objeto;**

Exemplos:
-- Apagar a tabela Estudantes
**DROP TABLE Estudantes;**

-- Apagar o banco de dados Colégio_São_Paulo
**DROP DATABASE Colégio_São_Paulo;**

-- Apagar o esquema Turno_da_manhã
**DROP SCHEMA Turno_da_manhã;**

Atenção: Depois que o objeto é apagado, não há volta! Use com muita cautela.

## Comando ALTER — Modificando a estrutura da tabela
Usado para alterar tabelas já existentes: adicionar, modificar ou remover colunas; também para alterar restrições.

# Adicionar uma coluna:

**ALTER TABLE nome_da_tabela ADD nome_da_coluna tipo_de_dado;**

Exemplo:
**ALTER TABLE Estudantes ADD Idade INT;**

# Removendo uma coluna:

**ALTER TABLE nome_da_tabela DROP COLUMN nome_da_coluna;**

Exemplo:
**ALTER TABLE Estudantes DROP COLUMN Idade;**

Dicas importantes:
- Sempre teste os comandos ALTER e DROP em ambiente seguro antes de usar em produção.
- Faça backup dos dados antes de modificar a estrutura do banco.
- Esses comandos podem mudar a estrutura do banco de forma irreversível, então a cautela é essencial.









