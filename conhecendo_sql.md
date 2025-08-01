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

### Cada SGBD (Sistema de Gerenciamento de Banco de Dados) pode ter variações ou tipos específicos. Alguns sistemas, como PostgreSQL ou MySQL, permitem até tipos personalizados.

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

### ALTER TABLE — Alterar uma tabela existente
A Hermex Import pediu uma nova coluna chamada Endereço_Cliente na tabela tabelaclientes. Para isso, usamos:

**ALTER TABLE tabelaclientes ADD Endereço_Cliente VARCHAR(250);**

Explicando:
**ALTER TABLE**: indica que queremos alterar a estrutura da tabela.
**ADD**: adiciona um novo elemento (nesse caso, uma coluna).
**VARCHAR(250)**: define que essa nova coluna armazenará textos de até 250 caracteres.

Após executar, a nova coluna aparecerá na lista da tabela, junto com as anteriores.

### DROP TABLE — Apagar uma tabela inteira
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


### Comando DROP — Apagando objetos do banco
Usado para excluir objetos como tabelas, bancos de dados, esquemas, índices, usuários, etc.

Sintaxe básica:

**DROP tipo_do_objeto nome_do_objeto;**

Exemplos:
- Apagar a tabela Estudantes
**DROP TABLE Estudantes;**

- Apagar o banco de dados Colégio_São_Paulo
**DROP DATABASE Colégio_São_Paulo;**

- Apagar o esquema Turno_da_manhã
**DROP SCHEMA Turno_da_manhã;**

Atenção: Depois que o objeto é apagado, não há volta! Use com muita cautela.

### Comando ALTER — Modificando a estrutura da tabela
Usado para alterar tabelas já existentes: adicionar, modificar ou remover colunas; também para alterar restrições.

### Adicionar uma coluna:

**ALTER TABLE nome_da_tabela ADD nome_da_coluna tipo_de_dado;**

Exemplo:
**ALTER TABLE Estudantes ADD Idade INT;**

### Removendo uma coluna:

**ALTER TABLE nome_da_tabela DROP COLUMN nome_da_coluna;**

Exemplo:
**ALTER TABLE Estudantes DROP COLUMN Idade;**

Dicas importantes:
- Sempre teste os comandos ALTER e DROP em ambiente seguro antes de usar em produção.
- Faça backup dos dados antes de modificar a estrutura do banco.
- Esses comandos podem mudar a estrutura do banco de forma irreversível, então a cautela é essencial.

## PRIMARY KEY (Chave Primária)
É uma coluna(ou conjunto de colunas) em uma tabela de banco de dados que serve para identificar de forma única cada registro.

- **Unicidade**: Nenhum valor pode se repetir na coluna da chave primária. Cada registro tem um valor exclusivo.
- **Não pode ser nulo**: A chave primária deve ter um valor preenchido para todos os registros — não pode faltar.
- **Índice automático**: Os sistemas de banco de dados criam índices para essa coluna, o que torna as buscas por registros muito mais rápidas.

### Por que a Primary Key é tão importante?

- **Identificação única**: Permite localizar qualquer registro de forma rápida e segura, sem confusão.
- **Integridade referencial**: Em bancos relacionais, ela é usada para conectar tabelas — garantindo que os dados relacionados entre tabelas estejam corretos e consistentes.
- **Performance**: A indexação automática facilita consultas e atualizações rápidas no banco de dados.

## FOREIGN KEY (Chave Estrangeira)
A chave estrangeira é uma coluna numa tabela que serve para fazer a ligação entre essa tabela e outra tabela. Ela aponta para a chave primária da tabela relacionada, permitindo conectar informações entre elas.

Exemplo prático:
- Na tabela pedidos, existe a coluna Cliente que guarda o ID do cliente.
- Esse ID vem da tabela clientes, mas aqui ele aparece apenas para identificar quem fez o pedido.
- Assim, a coluna Cliente em pedidos é uma chave estrangeira que aponta para a chave primária da tabela clientes.
- Isso evita repetir todos os dados do cliente em várias tabelas e mantém o banco organizado.

### Criando a tabela de produtos com chave estrangeira

**CREATE TABLE tabelaprodutos (**
 **ID_Produto INT PRIMARY KEY,**
  **Nome_do_Produto VARCHAR(250),**
  **Descrição TEXT,**
  **Categoria INT,**
  **Preco_de_Compra DECIMAL(10,2),**
  **Unidade VARCHAR(50),**
  **Fornecedor INT,**
  **Data_de_Inclusao DATE,**
  **FOREIGN KEY (Categoria) REFERENCES tabelacategorias(ID_Categoria),**
  **FOREIGN KEY (Fornecedor) REFERENCES tabelafornecedores(ID)**
**);**

**Explicando o código:**

**ID_Produto**: chave primária, identifica exclusivamente cada produto.
**Categoria**: número inteiro que será uma chave estrangeira, ligada à tabela tabelacategorias na coluna ID_Categoria.
**Fornecedor**: número inteiro que será outra chave estrangeira, ligada à tabela tabelafornecedores na coluna ID.
**As outras colunas armazenam informações do produto, como nome, descrição, preço, unidade e data.**

Criamos a tabela produtos relacionando com as tabelas de categorias e fornecedores através de chaves estrangeiras, reforçando a estrutura do banco de dados.

# Inserindo dados na tabela com o comando INSERT

### Passo a passo para inserir dados na tabela clientes
1. Abrir uma nova aba de código no SQLite Online para manter o código organizado.
2. Usar o comando:

**INSERT INTO tabelaclientes (id_cliente, nome_cliente, informacoes_de_contato, Endereço_Cliente)**
**VALUES ('1', 'Ana Silva', 'ana.silva@email.com', 'rua flores - casa 1');**

**INSERT INTO** indica que vamos inserir dados.

Entre parênteses, colocamos os nomes das colunas que receberão os dados.
Depois, com VALUES, colocamos os dados correspondentes na mesma ordem das colunas.
Textos vão entre aspas simples '...'.
Números podem ou não ir entre aspas, dependendo do uso.
Executar o comando para inserir a primeira linha.
Fazer um SELECT para conferir:

**SELECT * FROM tabelaclientes;**

Você verá a linha inserida na tabela.

Exemplo de inserção múltipla de clientes:

**INSERT INTO tabelaclientes**
**(id_cliente,**
 **nome_cliente,**
 **informacoes_de_contato,**
 **Endereço_Cliente)**
**VALUES**
 **(2, 'João Santos', 'joao.santos@provedor.com', 'Rua dos pinheiros, 25'),**
 **(3, 'Maria Fernandes', 'maria.fernandes@email.com', 'Rua Santo Antonio, 10'),**
 **(4,'Carlos Pereira', 'carlos.pereira@email.com', 'Avenida rio, 67');**

## Passo a passo para criar a tabela e copiar dados filtrados com INSERT + SELECT
1. Criar a tabela de pedidos padrão ouro (tabelapedidosgold)

CREATE TABLE tabelapedidosgold (
 ID_pedido_gold INT PRIMARY KEY,
 Data_Do_Pedido_gold DATE,
 Status_gold VARCHAR(50),
 Total_Do_Pedido_gold DECIMAL(10, 2),
 Cliente_gold INT,
 Data_De_Envio_Estimada_gold DATE,
 FOREIGN KEY (cliente_gold) REFERENCES tabelaclientes(id_cliente)
);

2. Inserir dados na nova tabela, selecionando somente pedidos com valor >= 400 da tabela original (tabelapedidos)

INSERT INTO tabelapedidosgold
    (ID_pedido_gold, 
     Data_Do_Pedido_gold, 
     Status_gold, 
     Total_Do_Pedido_gold, 
     Cliente_gold, 
     Data_De_Envio_Estimada_gold)
SELECT
    id,
    data_do_pedido,
    status,
    total_do_pedido,
    cliente,
    data_de_envio_estimada
FROM tabelapedidos
WHERE total_do_pedido >= 400;

3. Consultar para verificar se os dados foram inseridos corretamente

SELECT * FROM tabelapedidosgold;

Explicação:
CREATE TABLE cria a estrutura da nova tabela, com as mesmas colunas da tabela original, mas com nomes diferentes (com o sufixo _gold).
INSERT INTO ... SELECT ... FROM ... WHERE ...:
Insere dados na tabela destino (tabelapedidosgold) com base no resultado da consulta SELECT feita na tabela origem (tabelapedidos).
O filtro WHERE total_do_pedido >= 400 garante que só os pedidos com valor igual ou maior que 400 serão copiados.
Assim, você cria uma tabela nova já filtrada, sem precisar inserir dados linha a linha.

**Principais pontos sobre INSERT + SELECT**
1. Colunas devem estar alinhadas
A lista de colunas na cláusula INSERT INTO deve corresponder, em número e ordem, à lista de colunas do SELECT.
Os tipos de dados precisam ser compatíveis para evitar erros.
2. Uso da cláusula **WHERE**
Fundamental para filtrar os dados que serão copiados, evitando inserir tudo sem critério.
Pode usar condições simples, múltiplas, até subconsultas.
3. Cuidado com chaves primárias
Se a tabela destino tem uma coluna chave primária, os valores inseridos devem ser únicos para evitar conflito.
Em alguns SGDBs, pode-se usar comandos como INSERT OR REPLACE (SQLite) ou ON DUPLICATE KEY UPDATE (MySQL) para evitar erros.
4. Aplicações comuns:
- Backup parcial de dados
- Migração entre tabelas
- População inicial de tabelas
- Criação de tabelas derivadas filtradas
- Atualização em massa (com ajuda de UPDATE e JOIN)

Exemplo prático para reforçar:

Imagine:
Tabela clientes_ativos com colunas (id_cliente, nome, status)

Tabela clientes_inativos com mesmas colunas


Queremos mover todos os clientes cujo status é 'inativo' para a tabela clientes_inativos:

- Inserir clientes inativos na tabela destino
INSERT INTO clientes_inativos (id_cliente, nome, status)
SELECT id_cliente, nome, status
FROM clientes_ativos
WHERE status = 'inativo';

- Remover os clientes inativos da tabela original
DELETE FROM clientes_ativos
WHERE status = 'inativo';

# Operados lógicos-matemáticos

São símbolos como:

**> (maior que)**
**< (menor que)**
**>= (maior ou igual a)**
**<= (menor ou igual a)**
**= (igual a)**
**<> (diferente de)**

Exemplos práticos:

- Filtrar pedidos com valor maior que R$ 200:
**SELECT * FROM tabelapedidos WHERE total_do_pedido > 200;**
Aqui, só aparecem pedidos com valor maior que 200.
Incluir pedidos com valor igual a R$ 200 também:

- **SELECT * FROM tabelapedidos WHERE total_do_pedido >= 200;**
Agora aparecem pedidos com valor igual ou maior que 200.
Filtrar pedidos menores ou iguais a R$ 200:
**SELECT * FROM tabelapedidos WHERE total_do_pedido <= 200;**

- Excluir pedidos com valor igual a R$ 200:
**SELECT * FROM tabelapedidos WHERE total_do_pedido <> 200;**
Ou só os pedidos com valor exatamente igual a 200:
SELECT * FROM tabelapedidos WHERE total_do_pedido = 200;

### Filtrando texto (strings)
Também dá para usar operadores em textos — eles são ordenados alfabeticamente.

Exemplos: listar clientes com nome começando a partir da letra C:
**SELECT * FROM tabelaclientes WHERE nome_cliente > 'C';**
Assim, nomes que começam com A ou B não aparecem.

**SELECT * FROM Produtos WHERE Nome LIKE '%computador%';**
Esse comando busca produtos que tenham "computador" em qualquer parte do nome.

### Filtrando datas
Datas são filtradas seguindo a ordem cronológica.

Exemplo: mostrar pedidos feitos após 19 de setembro de 2023:
**SELECT * FROM tabelapedidos WHERE data_do_pedido > '2023-09-19';**

### Operadores Lógicos
Permitem combinar várias condições ao mesmo tempo para filtros mais complexos.

**AND** (e) — todas as condições precisam ser verdadeiras
**OR** (ou) — pelo menos uma condição precisa ser verdadeira
**NOT** (não) — inverte a condição

Exemplos:
**SELECT * FROM Clientes WHERE Idade > 30 AND Sexo <> 'Masculino';**
Aqui, trazemos clientes com mais de 30 anos e que não sejam do sexo masculino.

**SELECT * FROM tabelapedidos WHERE total_do_pedido >= 200 AND status = 'Pendente';**
Só aparecem pedidos que atendem as duas condições — valor >= 200 e status pendente.

**SELECT * FROM tabelapedidos WHERE status = 'Pendente' OR status = 'Processando';**
Traz pedidos que estão em qualquer um desses dois status.

**SELECT * FROM tabelapedidos WHERE NOT status = 'Pendente';**
Traz pedidos com status diferentes de "Pendente" (ex: "Processando", "Enviado", etc.).

**SELECT * FROM tabelapedidos WHERE data_de_envio_estimada BETWEEN '2023-08-01' AND '2023-09-01';**
Traz só os pedidos com datas dentro desse intervalo.


## Ordenando resultados com ORDER BY no SQL
Depois de aprender a filtrar dados com condições, agora é hora de ordenar os resultados para facilitar a análise.

1. **Ordenar textos (alfabética)**
Queremos produtos com preço entre R$ 200 e R$ 600, ordenados pelo nome do produto, em ordem alfabética:

**SELECT * FROM tabelaprodutos WHERE preco_de_compra BETWEEN 200 AND 600 ORDER BY nome_do_produto;**
Produtos aparecem de A a Z pelo nome.

Se quiser a ordem decrescente (do maior para o menor), basta usar o DESC:

**SELECT * FROM tabelaprodutos WHERE preco_de_compra BETWEEN 200 AND 600 ORDER BY fornecedor DESC;**

2. **Ordenar datas**
Para ordenar os produtos pelo campo de data de inclusão (do mais antigo para o mais recente):

**SELECT * FROM tabelaprodutos WHERE preco_de_compra BETWEEN 200 AND 600 ORDER BY data_de_inclusao;**

3. **Ordenar valores numéricos**
Por padrão, a ordenação é ascendente (do menor para o maior). Para ordenar produtos pelo ID do fornecedor:

**SELECT * FROM tabelaprodutos WHERE preco_de_compra BETWEEN 200 AND 600 ORDER BY fornecedor;**


# ALIAS 
ALIAS é um nome temporário que você dá para uma coluna ou tabela dentro de uma consulta SQL. Ele ajuda a deixar os resultados mais claros e o código mais fácil de entender.

Para colunas você pode renomear uma coluna no resultado da consulta usando a palavra-chave AS.
Exemplo:
**SELECT Nome AS NomeCompleto FROM Clientes;**

Aqui, a coluna Nome vai aparecer como NomeCompleto no resultado, sem mudar o nome original da tabela.

Para tabelas quando você faz junções (JOIN) entre tabelas que têm colunas com nomes iguais, pode usar ALIAS para renomear as tabelas e evitar confusão.
Exemplo:
**SELECT P.ID AS IDPedido, C.ID AS IDCliente FROM Pedidos AS P JOIN Clientes AS C ON P.ClienteID = C.ID;**

Nesse caso, Pedidos virou P e Clientes virou C só dentro da consulta, facilitando a escrita e leitura do código.

### Por que usar ALIAS?
- Facilita a leitura do resultado das consultas.
- Evita ambiguidades em consultas com várias tabelas.
- Permite dar nomes mais amigáveis ou claros para colunas temporariamente.
- É uma prática comum para deixar consultas complexas mais organizadas.


# Atualizando dados no banco com o comando UPDATE
Como alterar dados de verdade dentro do banco, de forma definitiva, usando o comando UPDATE.

Exemplo 1: Atualizar o status dos pedidos

A empresa Hermex Import quer mudar o status de todos os pedidos que estão “processando” para “enviado”, porque esses pedidos já foram despachados.
O comando SQL para isso é:

**UPDATE tabelapedidos SET status = 'Enviado' WHERE status = 'Processando';**

**UPDATE tabelapedidos**: diz que vamos mexer na tabela de pedidos.
**SET status** = 'Enviado': define que o campo status deve virar “Enviado”.
**WHERE status**= 'Processando': só altera onde o status ainda está “Processando”.

Isso faz com que só os pedidos “processando” sejam atualizados — os outros permanecem iguais.

### Por que usar o WHERE é tão importante?
Se você fizer só:

**UPDATE tabelapedidos SET status = 'Enviado';**

Sem o WHERE, todos os pedidos vão mudar para “Enviado”! Isso pode ser um problema sério, porque pode alterar dados que não queríamos.

Exemplo 2: Atualizar várias colunas em uma linha específica
Agora, vamos atualizar o contato e o endereço do cliente com ID 2.
O comando:

**UPDATE tabelaclientes SET informacoes_de_contato = 'j.santos@email.com',nendereco_cliente = 'Rua dos paralelepipedos, 30'bWHERE id_cliente = 2;**

Isso altera duas colunas ao mesmo tempo da linha específica onde o cliente tem ID 2.

# DELETE 
Depois de usar o UPDATE, sempre vale a pena verificar o resultado com um SELECT para garantir que as mudanças ocorreram corretamente.
Apagando dados do banco com a cláusula DELETE

Exemplo 1: Excluir fornecedores de um país específico
A Hermex Import quer cancelar relações com todos os fornecedores da Turquia.
O comando para apagar esses fornecedores é:

**DELETE FROM tabelafornecedores WHERE pais_de_origem = 'Turquia';**

**DELETE FROM tabelafornecedores**: indica que vamos apagar dados da tabela de fornecedores.
**WHERE pais_de_origem = 'Turquia'**: especifica que só serão apagados os registros onde o país de origem é Turquia.
Após rodar isso, nenhum fornecedor da Turquia mais aparecerá na tabela.

Exemplo 2: Excluir fornecedores com ID maior que 35
Se queremos apagar todos os fornecedores cujo ID seja maior que 35, usamos:

**DELETE FROM tabelafornecedores WHERE id > 35;**

Isso elimina de uma vez todos esses fornecedores.

Importante: cuidado com o uso do DELETE 
Assim como no UPDATE, o WHERE é fundamental! Se você fizer:

**DELETE FROM tabelafornecedores;**

Sem o WHERE, todos os fornecedores da tabela serão apagados — cuidado para não causar prejuízos!

Como confirmar o resultado
Sempre faça um SELECT após o DELETE para verificar os dados restantes:

**SELECT * FROM tabelafornecedores;**


Em resumo:
DELETE FROM [tabela] WHERE [condição]; apaga linhas específicas.
Use o WHERE para delimitar o que será excluído.
Verifique com SELECT o resultado da exclusão.

# Cascata com DELETE CASCADE
A cláusula DELETE CASCADE é uma funcionalidade usada em bancos de dados relacionais para manter a integridade referencial entre tabelas relacionadas. Quando configurada, a exclusão de um registro na tabela "pai" automaticamente exclui também todos os registros relacionados nas tabelas "filhas". Isso evita que registros fiquem "órfãos", ou seja, apontando para dados que não existem mais.

Como funciona?
Você define uma chave estrangeira numa tabela filha que referencia a tabela pai.
Nessa definição, usa a opção ON DELETE CASCADE.
Ao deletar um registro da tabela pai, o banco de dados automaticamente deleta todos os registros na tabela filha que fazem referência a ele.

Exemplo prático: 

**CREATE TABLE Clientes ( ID INT PRIMARY KEY, Nome VARCHAR(50));**

**CREATE TABLE Pedidos (PedidoID INT PRIMARY KEY, ClienteID INT, Descricao VARCHAR(100), FOREIGN KEY (ClienteID) REFERENCES Clientes(ID) ON DELETE CASCADE);**

Se um cliente for excluído da tabela Clientes, todos os seus pedidos na tabela Pedidos serão excluídos automaticamente.

### Atenção
DELETE CASCADE é poderoso e deve ser usado com cuidado!
Ele pode causar perda de dados em cascata sem aviso, então entenda bem suas tabelas e relacionamentos.
Verifique sempre o impacto antes de aplicar em produção.











