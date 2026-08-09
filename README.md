
🚀 Materials Management System - Industrial Cost & Inventory Management

Este projeto é uma solução full-stack desenvolvida para a gestão de produção industrial, focada na precisão de cálculos de custos de matéria-prima e eficiência de processamento. 
A aplicação demonstra o uso de tecnologias modernas para resolver problemas reais de logística e manufatura.

## 🏗️ Arquitetura e Tecnologias

A solução foi construída utilizando uma arquitetura conteinerizada, garantindo isolamento e escalabilidade:

* **Backend:** **Java 21** com **Spring Boot 3**. Utiliza **Virtual Threads** (Project Loom) para processamento paralelo de alta performance,
*  permitindo que múltiplos cálculos de estimativa sejam feitos simultaneamente sem sobrecarga do sistema.
* **Frontend:** **Vue.js 3** com **Vite**. Interface reativa e rápida, focada na experiência do usuário (UX) e na clareza dos dados financeiros com formatação em dólar (USD).
* **Banco de Dados:** **PostgreSQL 16**. Persistência robusta com integridade referencial para o vínculo entre Produtos e Matérias-Primas.
* **Infraestrutura:** **Docker & Docker Compose**. Orquestração completa para que o ambiente suba com um único comando.
* **Documentação:** **Swagger (OpenAPI 3)** para mapeamento e teste dos endpoints da API.

---

### 1. Validação do Comportamento Lógico
O sistema conta com verificações para assegurar que o comportamento das regras de negócio permaneça consistente:
* **Precisão de Processamento:** Garantia de que as operações financeiras e de conversão de valores mantenham a exatidão necessária para o ambiente fabril.
* **Tratamento de Excessões:** Assegura que o sistema responda de forma previsível a diferentes entradas de estoque e quantidades, evitando estados inconsistentes na interface.

## 🧠 Detalhamento da Regra de Cálculo e Fluxo de Dados

Para garantir a transparência e a confiabilidade dos dados, a regra de negócio foi implementada para reagir a mudanças manuais de inventário, funcionando como um assistente de decisão para o gestor.

### 1. O Vínculo de Composição
Cada **Produto Final** está atrelado a uma **Matéria-Prima** específica. O cálculo base segue a fórmula:
> `Valor Estimado = (Quantidade do Produto) × (Preço da Matéria-Prima Vinculada)`

### 2. A Dinâmica do Estoque (Cenários de Uso)
O sistema monitora a disponibilidade de material para garantir que a estimativa financeira seja realista:
* **Cenário de Leitura:** Ao carregar os dados do banco, o sistema exibe os valores já consolidados e persistidos.
* **Cenário de Edição:** Se o usuário identifica que o estoque real mudou e edita o campo **Estoque** na tela, o sistema entra em estado de "Recálculo Pendente".
* **Cenário Crítico:** Se o valor inserido no estoque for menor que a quantidade necessária, o sistema permite visualizar o impacto antes mesmo de salvar no banco.

### 3. O Botão "Calcular": Checkpoint de Integridade
O botão **Calcular** foi desenhado para ser o **único gatilho de atualização** manual dos valores. É vital compreender sua dinâmica para avaliar o sistema:

* **Integridade de Dados:** Se você clicar em "Calcular" logo após carregar a página (sem alterar valores), o sistema não apresentará mudanças.
* Isso ocorre porque o valor vindo do banco já é o valor correto. **O botão não "falha"; ele protege o dado verificado.**
* **Gatilho Reativo:** O botão "desperta" e processa a lógica no momento em que detecta uma edição manual (especialmente no campo de estoque).
* Ele confirma a intenção do usuário: *"Eu alterei o estoque e quero ver o impacto real no valor estimado agora"*.
* **Formatação Visual:** Ao calcular, o sistema aplica instantaneamente a máscara monetária (USD), garantindo que os centavos e separadores de milhar estejam corretos.

---

## 🐳 Como Rodar o Projeto via Docker

O ambiente foi totalmente dockerizado para eliminar a necessidade de configurações manuais.

1.  **Subindo os Containers:**
    Abra o terminal na pasta raiz do projeto e execute:
    ```bash
    docker-compose up -d --build
    ```
    *A flag `-d` (detached) subirá os serviços em segundo plano. Caso deseje acompanhar os logs de inicialização (como o log das Virtual Threads), utilize apenas `docker-compose up`.*

2.  **Acesso às Interfaces:**
    * **Frontend (Interface do Usuário):** [http://localhost:5173](http://localhost:5173)
    * **Backend (Documentação Swagger):** [http://localhost:8080/swagger-ui/index.html](http://localhost:8080/swagger-ui/index.html)
    * **Banco de Dados:** Acesso via porta `5432` (PostgreSQL).

---

## 🛠️ Testando a API via Swagger

Para demonstrar a robustez do Backend desenvolvido, a documentação Swagger está ativa. Nela, é possível testar todos os endpoints de CRUD e processamento de forma independente do Frontend. Isso garante que a API é uma entidade autônoma, pronta para integração com outros serviços.

---

 Desenvolver esta solução foi uma excelente oportunidade para aplicar conceitos avançados como **Virtual Threads no Java 21** e a reatividade do **Vue.js 3**.

**Carlos Roberto Ribeiro Santos Junior**

![foto1](https://github.com/user-attachments/assets/1ee110f5-4e92-4115-8e73-ac43bace74fc)

![foto2](https://github.com/user-attachments/assets/d9bd634b-2cf2-43ed-bda1-c850052d9217)

![foto3](https://github.com/user-attachments/assets/84cf91b2-b529-485e-a769-bd3cb39710b3)

![foto4](https://github.com/user-attachments/assets/639bfb7a-3522-4772-a72a-8596b6cae7c0)

![foto5](https://github.com/user-attachments/assets/a3f0eddf-d0f7-440e-8b89-bbefbf97777e)
