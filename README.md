# Sistema de Gestão de Contos de Fadas

Este sistema tem como objetivo organizar e gerenciar informações sobre contos de fadas, autores, personagens e interações entre personagens. A estrutura de dados é projetada para facilitar o armazenamento e consulta dessas informações, permitindo representar a complexidade das histórias, seus personagens e relações.

## Estrutura do Banco de Dados

O banco de dados é composto por quatro tabelas principais:

1. **Autor**
2. **Contos de Fadas**
3. **Personagens**
4. **Interações entre Personagens**

### 1. **Tabela `autor`**

Armazena as informações sobre os autores dos contos de fadas, incluindo o nome e a data de nascimento.

#### Campos:
- **id**: Identificador único do autor (chave primária).
- **nome**: Nome do autor.
- **data_nascimento**: Data de nascimento do autor.

### 2. **Tabela `conto_de_fadas`**

Armazena os contos de fadas com título, resumo, data de publicação e o autor responsável pela criação do conto.

#### Campos:
- **id**: Identificador único do conto (chave primária).
- **titulo**: Título do conto de fadas.
- **resumo**: Resumo ou sinopse do conto de fadas.
- **data_publicacao**: Data de publicação do conto.
- **autor_id**: Identificador do autor (chave estrangeira referenciando a tabela `autor`).

### 3. **Tabela `tipo_personagem`**

Armazena os tipos de personagens que podem existir nos contos de fadas (ex: Herói, Vilão, Coajuvante, etc.).

#### Campos:
- **id**: Identificador único do tipo de personagem (chave primária).
- **descricao**: Descrição do tipo de personagem (ex: "Herói", "Vilão").

### 4. **Tabela `personagem`**

Armazena informações sobre os personagens, incluindo nome, descrição, tipo (herói, vilão, coajuvante) e qual conto de fadas o personagem pertence.

#### Campos:
- **id**: Identificador único do personagem (chave primária).
- **nome**: Nome do personagem.
- **descricao**: Descrição do personagem.
- **tipo_personagem_id**: Identificador do tipo de personagem (chave estrangeira referenciando a tabela `tipo_personagem`).
- **conto_de_fadas_id**: Identificador do conto de fadas ao qual o personagem pertence (chave estrangeira referenciando a tabela `conto_de_fadas`).

### 5. **Tabela `interacao_personagem`**

Armazena as interações entre os personagens dos contos de fadas. Cada interação descreve uma ação ou evento que envolve dois personagens.

#### Campos:
- **id**: Identificador único da interação (chave primária).
- **personagem1_id**: Identificador do primeiro personagem envolvido na interação (chave estrangeira referenciando a tabela `personagem`).
- **personagem2_id**: Identificador do segundo personagem envolvido na interação (chave estrangeira referenciando a tabela `personagem`).
- **descricao**: Descrição da interação entre os personagens.

## Funcionalidades

O sistema permite realizar diversas operações relacionadas aos contos de fadas e seus personagens. As principais funcionalidades incluem:

### 1. **Cadastro de Autores**

A tabela `autor` armazena informações sobre os autores dos contos de fadas. Você pode registrar novos autores e suas datas de nascimento.

### 2. **Cadastro de Contos de Fadas**

A tabela `conto_de_fadas` permite registrar os contos, com título, resumo, data de publicação e o autor responsável pela obra.

### 3. **Cadastro de Tipos de Personagens**

A tabela `tipo_personagem` define os tipos de personagens, como heróis, vilões e coadjuvantes. Isso permite classificar os personagens de maneira mais organizada.

### 4. **Cadastro de Personagens**

A tabela `personagem` registra os personagens dos contos de fadas, associando-os aos contos específicos e aos tipos de personagens (herói, vilão, coadjuvante).

### 5. **Cadastro de Interações entre Personagens**

A tabela `interacao_personagem` descreve as interações entre personagens dos contos de fadas. Ela permite registrar eventos ou ações que envolvem dois personagens, como conflitos, alianças ou encontros.

### 6. **Consultas de Informações**

O banco de dados permite realizar várias consultas úteis, como:
- Buscar todos os personagens de um conto de fadas.
- Buscar as interações entre personagens.
- Consultar o autor de um conto e seus detalhes.
- Consultar personagens por tipo (herói, vilão, coadjuvante).

## Exemplo de Dados

### Inserção de Autores

```sql
INSERT INTO autor (nome, data_nascimento) VALUES ('Irmãos Grimm', '1785-01-01');
INSERT INTO autor (nome, data_nascimento) VALUES ('Hans Christian Andersen', '1805-04-02');
```

### Inserção de Contos de Fadas

```sql
INSERT INTO conto_de_fadas (titulo, resumo, data_publicacao, autor_id) 
VALUES ('Chapeuzinho Vermelho', 'Uma menina visita sua avó e encontra um lobo no caminho.', '1812-01-01', 1);

INSERT INTO conto_de_fadas (titulo, resumo, data_publicacao, autor_id) 
VALUES ('A Pequena Sereia', 'Uma sereia se apaixona por um príncipe humano e deseja se tornar humana.', '1837-01-01', 2);
```

### Inserção de Tipos de Personagem

```sql
INSERT INTO tipo_personagem (descricao) VALUES ('Herói');
INSERT INTO tipo_personagem (descricao) VALUES ('Vilão');
INSERT INTO tipo_personagem (descricao) VALUES ('Coajuvante');
```

### Inserção de Personagens

```sql
-- Personagens de Chapeuzinho Vermelho
INSERT INTO personagem (nome, descricao, tipo_personagem_id, conto_de_fadas_id) 
VALUES ('Chapeuzinho Vermelho', 'Uma menina que usa um capuz vermelho.', 1, 1);

INSERT INTO personagem (nome, descricao, tipo_personagem_id, conto_de_fadas_id) 
VALUES ('Lobo Mau', 'Um lobo astuto e malvado.', 2, 1);

INSERT INTO personagem (nome, descricao, tipo_personagem_id, conto_de_fadas_id) 
VALUES ('Vovó', 'A avó de Chapeuzinho Vermelho.', 3, 1);

-- Personagens de A Pequena Sereia
INSERT INTO personagem (nome, descricao, tipo_personagem_id, conto_de_fadas_id) 
VALUES ('Pequena Sereia', 'Uma sereia curiosa e apaixonada.', 1, 2);

INSERT INTO personagem (nome, descricao, tipo_personagem_id, conto_de_fadas_id) 
VALUES ('Príncipe', 'Um príncipe humano por quem a Pequena Sereia se apaixona.', 1, 2);

INSERT INTO personagem (nome, descricao, tipo_personagem_id, conto_de_fadas_id) 
VALUES ('Bruxa do Mar', 'Uma bruxa que faz um acordo com a Pequena Sereia.', 2, 2);
```

### Inserção de Interações entre Personagens

```sql
INSERT INTO interacao_personagem (personagem1_id, personagem2_id, descricao) 
VALUES (1, 2, 'O Lobo Mau tenta enganar Chapeuzinho Vermelho.');

INSERT INTO interacao_personagem (personagem1_id, personagem2_id, descricao) 
VALUES (2, 3, 'O Lobo Mau se disfarça de Vovó para enganar Chapeuzinho Vermelho.');

INSERT INTO interacao_personagem (personagem1_id, personagem2_id, descricao) 
VALUES (4, 5, 'A Pequena Sereia salva o Príncipe de um naufrágio.');
```

## Consultas Comuns

### Consultar Todos os Contos de Fadas

```sql
SELECT * FROM conto_de_fadas;
```

### Consultar Todos os Personagens de um Conto de Fadas

```sql
SELECT p.nome, p.descricao, t.descricao AS tipo_personagem
FROM personagem p
JOIN tipo_personagem t ON p.tipo_personagem_id = t.id
WHERE p.conto_de_fadas_id = 1;  -- Exemplo para o conto "Chapeuzinho Vermelho"
```

### Consultar Interações entre Personagens

```sql
SELECT p1.nome AS personagem1, p2.nome AS personagem2, i.descricao AS interacao
FROM interacao_personagem i
JOIN personagem p1 ON i.personagem1_id = p1.id
JOIN personagem p2 ON i.personagem2_id = p2.id;
```

### Consultar Autores e Seus Contos

```sql
SELECT a.nome AS autor, c.titulo AS conto
FROM autor a
JOIN conto_de_fadas c ON a.id = c.autor_id;
```

## Conclusão

Este sistema de gestão de contos de fadas organiza e permite consultar de maneira eficiente os dados sobre autores, personagens, interações e contos de fadas. Ele pode ser expandido para incluir outros tipos de informações, como adaptacões de contos, ilustrações e versões dos contos, oferecendo uma plataforma flexível para gerenciar essas histórias encantadas
