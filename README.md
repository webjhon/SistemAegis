# Integração JavaScript OOP → PHP → MySQL

## 📖 Contexto do Projeto

A empresa já possui um **programador sênior especializado em PHP**, responsável por manter e evoluir os módulos back-end.
Este profissional desenvolveu um código em PHP capaz de **receber listas no formato JSON e salvar diretamente no banco de dados MySQL**.

Contudo, este programador **não possui experiência em JavaScript**, o que impossibilita a implementação da camada de front-end responsável por coletar os dados, estruturar as listas em arrays de objetos e enviá-las corretamente ao PHP.

Por esse motivo, a empresa busca os serviços de outra equipe com profissionais capacitados em **Programação Orientada a Objetos com JavaScript**, que deverão desenvolver toda a lógica de geração de listas no front-end, realizar a integração com o código PHP já existente e entregar o sistema funcional.

O trabalho será avaliado inicialmente apenas sobre **uma tabela (funcionários)** e **uma classe (funcionários)**.
Após esta primeira entrega, a empresa analisará a escrita do código, sua clareza e organização, para então avaliar a possibilidade de efetivação do contrato para expansão do projeto.

---

## 🗄️ Estrutura do Banco de Dados

```sql
CREATE DATABASE empresa;
USE empresa;

CREATE TABLE funcionarios (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nome VARCHAR(100),
  cargo VARCHAR(100),
  email VARCHAR(150)
);
```

---

## 🔗 Código PHP fornecido

```php
<?php
// salvar.php
$servidor = "localhost";
$usuario  = "root";
$senha    = "";
$banco    = "empresa";

$conn = new mysqli($servidor, $usuario, $senha, $banco);
if ($conn->connect_error) {
    die("Erro: " . $conn->connect_error);
}

// Receber dados JSON do JavaScript
$entrada = file_get_contents("php://input");
$dados = json_decode($entrada, true);

if (!$dados) {
    die("Nenhum dado recebido!");
}

// Prepared Statement
$stmt = $conn->prepare("INSERT INTO funcionarios (nome, cargo, email) VALUES (?, ?, ?)");
$stmt->bind_param("sss", $nome, $cargo, $email);

foreach ($dados as $d) {
    $nome  = $d['nome'] ?? '';
    $cargo = $d['cargo'] ?? '';
    $email = $d['email'] ?? '';
    $stmt->execute();
}

echo "Lista salva com sucesso!";

$stmt->close();
$conn->close();
?>
```

---

## 📋 O que deve ser desenvolvido

* Implementação em **JavaScript orientado a objetos** para gerar listas de dados (funcionários).
* Criação de páginas **front-end em HTML** para entrada de dados.
* Integração entre o JavaScript e o PHP fornecido.
* Ajustes no banco de dados e inserts, se necessário.
* Documentação técnica do sistema, descrevendo arquitetura, fluxo e uso.
* Versionamento no GitHub, através de **fork** do repositório base disponibilizado pela empresa.

---

## ✅ Critérios de Aceite

* Código JavaScript desenvolvido em **paradigma orientado a objetos**.
* Front-end funcional para entrada de dados.
* Integração validada entre **JS → PHP → MySQL**.
* Banco de dados configurado corretamente.
* Documentação técnica entregue junto ao sistema.
* Código versionado e entregue em repositório GitHub (via *fork*).
* O sistema deve estar funcional com **cadastro de funcionários** já implementado.

---

## 🏁 Entrega Inicial

O primeiro módulo a ser entregue é o **cadastro de funcionários**.
Após validação deste módulo pela empresa, novos cadastros e funcionalidades poderão ser solicitados para expansão do sistema.

---

## 🚀 Como Iniciar

1. Realizar um **fork** do repositório base fornecido.
2. Configurar o banco de dados MySQL conforme o script fornecido.
3. Implementar a lógica em JavaScript (OOP) e o front-end correspondente.
4. Validar a integração com o PHP existente.
5. Escrever documentação técnica do sistema.
6. Subir o código no GitHub e disponibilizar o link do repositório para avaliação.

---

## 📂 Estrutura Sugerida do Repositório

```
/
├── /src
│   ├── index.html        # Página inicial do sistema
│   ├── script.js         # Lógica JavaScript OOP
│   └── salvar.php        # Endpoint PHP de integração
│
├── /db
│   └── schema.sql        # Script de criação do banco de dados
│
├── /docs
│   └── DOCUMENTACAO.md   # Documentação técnica do sistema
│
  └── README.md             # Instruções gerais do projeto
```

Essa estrutura facilita a manutenção, separando claramente os arquivos de front-end, back-end, banco de dados e documentação.
