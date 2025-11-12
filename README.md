# Programa EnterpriseFlow

## Caras do Codigo corp

### Dev group 1

O programa EnterpriseFlow, da Caras do Codigo corp, é um sistema de organização de vendas, estoque, entre outras funçoes basicas que são dificieis de manter conta.
Focando na função de simplificar a organização e distribuição de vendas e estoques e controle das informaçoes relevantes para pequenos comercios.
O programa é focado na simplicidade, com uma interface feita completamente em Java e integrado com Banco de dados pessoal, para individualização do sistema.
Utiliza uma implimentação com PowerBi para trazer uma simulação e visão mais precisa dos dados analizados.

### SM: Henrique Rodrigues

### PO: Arthur Vargas

Dev Team: Vitor Harthmann, Bruno Soares, Otavio Martins, Gabriel Brandão

---

## Tecnologias utilizadas

- ![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=java&logoColor=white)
- ![Swing](https://img.shields.io/badge/Swing-0081CB?style=for-the-badge&logo=java&logoColor=white)
- ![MySQL](https://img.shields.io/badge/MySQL-005C84?style=for-the-badge&logo=mysql&logoColor=white)
- ![JDBC](https://img.shields.io/badge/JDBC-07405E?style=for-the-badge&logo=java&logoColor=white)
- [jBCrypt]([https://mvnrepository.com/artifact/org.mindrot/jbcrypt](https://img.shields.io/badge/jBCrypt-cyan
)) (hash seguro de senhas)
- [PowerBi](https://img.shields.io/badge/PowerBI-yellow)
---

## Estrutura do projeto

text
src/br/ulbra/
 ├─ dao/         → Classes DAO (AbstractDAO, UsuarioDAO, ClienteDAO)
 ├─ controller/  → Lógica de controle (UsuarioController, ClienteController)
 ├─ model/       → Modelos (Usuario.java, Cliente.java)
 ├─ view/        → Interfaces gráficas (LoginView, MenuPrincipalView, UsuarioView, ClienteView)
 └─ img/         → Ícones


---

## Banco de Dados

 sql
--
-- Banco de dados: `dbenterpriseflow`
--

-- --------------------------------------------------------

--
-- Estrutura para tabela `fornecedor`
--

CREATE TABLE `fornecedor` (
  `idFornecedor` int(11) NOT NULL,
  `razaoSocial` varchar(255) NOT NULL,
  `nomeFantasia` varchar(255) NOT NULL,
  `cnpj` varchar(255) NOT NULL,
  `email` varchar(255) NOT NULL,
  `telefone` varchar(255) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

-- --------------------------------------------------------

--
-- Estrutura para tabela `itensvenda`
--

CREATE TABLE `itensvenda` (
  `idVenda` int(11) NOT NULL,
  `idProduto` int(11) NOT NULL,
  `quantidadeProd` int(11) NOT NULL,
  `precoUnit` double NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

-- --------------------------------------------------------

--
-- Estrutura para tabela `produto`
--

CREATE TABLE `produto` (
  `idProduto` int(11) NOT NULL,
  `nomeProduto` varchar(255) NOT NULL,
  `descricao` varchar(255) NOT NULL,
  `valorUnitario` double NOT NULL,
  `quantEstoque` int(11) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

-- --------------------------------------------------------

--
-- Estrutura para tabela `produtofornecedor`
--

CREATE TABLE `produtofornecedor` (
  `idProduto` int(11) NOT NULL,
  `idFornecedor` int(11) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

-- --------------------------------------------------------

--
-- Estrutura para tabela `venda`
--

CREATE TABLE `venda` (
  `idVenda` int(11) NOT NULL,
  `dataVenda` date NOT NULL,
  `valorTotal` double NOT NULL,
  `idVendedor` int(11) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

-- --------------------------------------------------------

--
-- Estrutura para tabela `vendedor`
--

CREATE TABLE `vendedor` (
  `idVendedor` int(11) NOT NULL,
  `nome` varchar(255) NOT NULL,
  `cpf` varchar(255) NOT NULL,
  `sexo` varchar(150) NOT NULL,
  `email` varchar(150) NOT NULL,
  `ativo` tinyint(1) NOT NULL,
  `dataAdmissao` date NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Índices para tabelas despejadas
--

--
-- Índices de tabela `fornecedor`
--
ALTER TABLE `fornecedor`
  ADD PRIMARY KEY (`idFornecedor`);

--
-- Índices de tabela `itensvenda`
--
ALTER TABLE `itensvenda`
  ADD KEY `fkVenda` (`idVenda`),
  ADD KEY `fkProduto` (`idProduto`);

--
-- Índices de tabela `produto`
--
ALTER TABLE `produto`
  ADD PRIMARY KEY (`idProduto`);

--
-- Índices de tabela `venda`
--
ALTER TABLE `venda`
  ADD PRIMARY KEY (`idVenda`),
  ADD KEY `fkVendaVendedor` (`idVendedor`);

--
-- Índices de tabela `vendedor`
--
ALTER TABLE `vendedor`
  ADD PRIMARY KEY (`idVendedor`);

--
-- AUTO_INCREMENT para tabelas despejadas
--

--
-- AUTO_INCREMENT de tabela `fornecedor`
--
ALTER TABLE `fornecedor`
  MODIFY `idFornecedor` int(11) NOT NULL AUTO_INCREMENT;

--
-- AUTO_INCREMENT de tabela `produto`
--
ALTER TABLE `produto`
  MODIFY `idProduto` int(11) NOT NULL AUTO_INCREMENT;

--
-- AUTO_INCREMENT de tabela `venda`
--
ALTER TABLE `venda`
  MODIFY `idVenda` int(11) NOT NULL AUTO_INCREMENT;

--
-- AUTO_INCREMENT de tabela `vendedor`
--
ALTER TABLE `vendedor`
  MODIFY `idVendedor` int(11) NOT NULL AUTO_INCREMENT;

--
-- Restrições para tabelas despejadas
--

--
-- Restrições para tabelas `itensvenda`
--
ALTER TABLE `itensvenda`
  ADD CONSTRAINT `fkProduto` FOREIGN KEY (`idProduto`) REFERENCES `produto` (`idProduto`),
  ADD CONSTRAINT `fkVenda` FOREIGN KEY (`idVenda`) REFERENCES `venda` (`idVenda`);

--
-- Restrições para tabelas `venda`
--
ALTER TABLE `venda`
  ADD CONSTRAINT `fkVendaVendedor` FOREIGN KEY (`idVendedor`) REFERENCES `vendedor` (`idVendedor`);
COMMIT;


## 👤 Criando o primeiro usuário (ADM)

### Opção 1 — Gerar hash manual
Use esta classe para gerar o hash:
java
import org.mindrot.jbcrypt.BCrypt;
public class HashGenerator {
    public static void main(String[] args) {
        System.out.println(BCrypt.hashpw("admin123", BCrypt.gensalt()));
    }
}

Depois insira no banco:
sql
INSERT INTO usuario (login, senha, nome, ativo)
VALUES ('adm', '$2a$10$HASHGERADO...', 'Administrador', 1);


### Opção 2 — Criar automaticamente no código
No CadastroUsuarioView.form, antes de abrir a tela de login, verifique se há usuários e crie o *adm/admin123* caso não exista.

---

## ▶️ Execução
1. Rode o projeto (classe CadastroUsuario.view é a principal).
2. Faça login:
   - Usuário: adm
   - Senha: admin123
3. Após autenticação, o sistema abre o *Main.view*.

---

## 🔒 Segurança
- Senhas são armazenadas com *jBCrypt*, nunca em texto puro.
- Recomenda-se usar um usuário MySQL dedicado em produção:
sql
CREATE USER 'appuser'@'localhost' IDENTIFIED BY 'senhaSegura';
GRANT ALL PRIVILEGES ON cruddb1.* TO 'appuser'@'localhost';


---
## 👨‍🏫 Sobre
Este projeto foi desenvolvido para fins *educacionais, como exemplo de CRUD com **Java + MySQL + Swing*, servindo de base para práticas de programação fullstack. Além disso, utiliza da collaboração entre alunos, ensinando-os as dificuldes do mercado de trabalho e como o ambiente de trabalho funciona.
