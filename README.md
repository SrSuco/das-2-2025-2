# das-2-2025-2

## AWS
- Boas praticas na arquitetura e tomadas de decisão
- Documento de boas práticas da AWS: https://aws.amazon.com/pt/architecture/well-architected/
- Serviços AWS.

## AWS Cloud Computing:
- Surgiu originalmente com 3 serviços:
  - Amazon SQS(Serviço de fila, push|pop), Amazon S3(Armazenamento), Amazon EC2(máquinas virtuais).
- Cloud Architecture:
  - Requisitos -> design de estrutura -> arquitetura completa
  - Planejamento -> Pesquisa -> Construção.

##  Pilares:
### Confiabilidade:
- Recupração rápida
- Atender dinâmicamente a demanda de computação.
- Mitigação de disrupções.

### Performance e eficiência:
- Escolha e manutenção eficiente de recursos.
- Democratização de tecnologias avançadas.
- Empregar simpatia mecânica.

### Otimização de custos
- Medir eficiência.
- Eliminar despesas desnecessárias.
- Adoção de modelo de consumo correto.
- Considerar serviços gerenciados.

### Sustentabilidade:
- Estabelecer metas de sustentabilidade.
- Maximizar a utilização.
- Escolher hardware eficiente.

### Regiões
- Na núvem, temos estruturas para tornar o datacenter transparente e abstraí-lo
- A região é uma localização do mundo onde a AWS tem um conjunto de datacenters
- Geralmente tem 2 ou 3 Zonas de Disponibilidade
### AZ ou Zona de Disponibildade
- AWS tem um backbone de rede proprietária para trafegar os dados
- AZs são interconetadas, mas são isoladas em caso de falha
- AZ = Alta Disponibilidade
- O nome da zona pode rotacionar (manutenção, etc) já o ID não muda
### Local Zones  ou Zonas Locais
- Argentina não é tão grande pra justificar uma AZ, mas tem demanda pra ter essa estrutura específica um pouco menor
- o IP publico é local, apensar de estar debaixo da Região North Virginia



### Securing Access

### AWS Shared responsability model
A responsa por ataques é sempre compartilhada, tem um desenho que mostra o que é da AWS e o que é do cliente.

- IaaS

- A AWS tem que garantir a estrutura, a networking, a database

- O Cliente tem que proteger o tráfico de dados, a encripção de dados Server-Side, a encripção de dados Client-Side

- Existe um modelo onde tenho menos responsa? Sim, no modelo PaaS (Plataform as a Service) onde a AWS te dá todo o ambiente configurado
- Existe um modelo com a menor responsa? Sim, no modelo SaaS

### Design principles for the security pillar
- Implement a strong identity fontadtion** (last login, where login, last pw reset, impossible travel)
- Protect data in transit and at rest** autoexplicativo
- Apply security layers** Preciso de multiplas camadas,não confiar só no firewall
- Keep data away from people** Usuário deve ter apenas o acesso que precisa
- Maintain traceability** Monitoramento, logs, etc
- Prepare for security events** Pra onde correr na hora que der B.O.
- Automate security best practices** Se possível automatizar tudo


#### Authorization

- O que quem está acessando pode ou não fazer (permito ou não permito)
- IAM controla na faixa essa autenticação, tem granularidade até o nivel de tabela do banco de dados.
- IAM tem user, roles, policies e role.
- Se não tiver permissões o AWS IAM assume que não pode ver nada

#### Melhores práticas
- Principio do privilégio mínimo
- MFA
- Temporary and rotation of keys
- Secure local creds
- Enable AWS CloudTrail
- Protect the root user: Criou o root já habilita MFA

#### IAM Roles

- Credencial temporária
- Tem que sair da cozinha (tem o link) e ir pro caixa

### S3:
- Buckets tem nomes diferentes entre eles, não existem 2 buckets no mundo com o mesmo nome.
- Tudo no bucket tem URL própria.
- Providencia 99.99% de disponibilidade.
- Utilizado para hospedar sites estáticos.
- Subir coisas para S3 é acelerado, não tem imprevisibilidade, conecta com uma edge location que transfere para a AWS este serviço é pago.
- Object Storage classes(Quentes): S3 Standard(Custo de armazenamento mais caro, pode ser baixado e acessado múltiplas vezes), S3 Standard-IA(Mais barato para armazenar, mais caro para acessar), S3 One Zone-IA(Para pouco acesso).
- Object Storage classes(Frias): S3 Glacier Deep Archive(Não está online, necessário "rehidratar" mandar para um s3 para acesso, média de 12h-48h para acesso), S3 Glacier Flex Retrival(Um pouco mais rápido para o retorno que o anterior), S3 Glacier Instant Retrival(Volta instântaneamente, porém mais caro e volta quase instântaneamente).
- Object Storage classes: S3 Intelligent-Tiering(É cobrado uma taxa para uso porém faz o gerenciamento do ciclo dos seus arquivos de acordo com uso/regra).
- Bucket fica em uma região, para escolher a região é necessário pensar de forma respectiva: Leis e regulações, latência, disponibilidade de serviço e custo efetivo.

###  VMs do EC2 + Anatomia

- EC2 provem VMs (servidores) na núvel
- Provem recursos em minutos
- Permite escalar vertical e horizontalmente
- Camadas -> EC2 Instances | Hypervisor (abstrai computador para vms permitindo rodar linux e win) | cpus + rãs |
- Dá pra customizar o uso de recursos
- A máquina tem rede
- A máquina tem EBS

Nome do EC2 é uma tag -> Metadado ataxado em um recurso

Amazon Machine Image -> Base para criar o servidor
- Tem snapchot da imagem
- A ordem de montagem
- Permissões

### Placement Groups

Placement Groups são um recurso que permite controlar onde a AWS aloca suas instâncias dentro de uma Região e suas Zonas de Disponibilidade (AZs). Você pode escolher entre três estratégias diferentes:

- Cluster: Todas as máquinas ficam próximas fisicamente dentro da mesma AZ, o que não garante alta disponibilidade. Se houver uma falha grave na AZ, todas as instâncias podem ser impactadas simultaneamente.
- Partition: Uma abordagem intermediária onde os dados e processos são divididos em partições lógicas entre múltiplos servidores. Ideal para sistemas como Kafka, Hadoop ou Spark, que trabalham com dados fragmentados e replicados.
- Spread: Distribui suas instâncias entre o maior número possível de AZs, aumentando a resiliência e a disponibilidade. Se uma AZ falhar, as outras continuam funcionando normalmente.

---

### Pricing

Modelos de compra que oferecem desconto:

- On-Demand: Pague pelo uso conforme precisar, sem compromisso de longo prazo.
- **Reserved Instances**: Reserve capacidade por um período (ex: 1 ou 3 anos), com opções de pagamento total antecipado, parcelado ou parcialmente adiantado. Menos flexível para alterar tipo de instância ou região.
- **Savings Plans**: Compromisso de gasto fixo por hora, durante o período contratado, com mais flexibilidade para trocar região e tipo de máquina. Existem variantes como AURI, PURI e NURI.
- **Amazon EC2 Spot**: Use capacidade ociosa da AWS por um preço reduzido, mas a qualquer momento a AWS pode recuperar essa capacidade.

Modelos de reserva de capacidade: Permitem reservar capacidade específica com desconto.

Modelos dedicados: Reservam servidores físicos completos para você, geralmente com custo maior.

---

### Networking e Content Delivery

- Subnets: Segmentam a rede para controlar o tráfego e impedir comunicação direta entre diferentes partes.

- CIDR Calculator: Ferramenta para calcular o tamanho e o intervalo de IPs da sua rede na nuvem.

---

### Amazon VPC | Virtual Private Cloud

- Rede definida por software construída sobre a infraestrutura física da AWS.
- Cada VPC está ligada a uma infraestrutura física localizada na mesma região onde seus recursos residem.
- O tamanho da VPC varia entre /16 (maior) e /28 (menor).
- Subnet pública: Possui acesso à internet bidirecionalmente. Para criá-la, são necessários:
  1. Internet Gateway — atua como um roteador (similar ao NAT da sua casa).
  2. Rotas na tabela de rotas direcionadas ao Internet Gateway.
  3. IP público associado ao recurso.
- Subnet privada: Sem comunicação externa, nem mesmo com outros serviços AWS fora da VPC. Instâncias aqui não acessam a internet.

- Peering: Comunicação entre diferentes VPCs, inclusive de clientes distintos na AWS.

---

### AWS Direct Connect

Conexão dedicada e privada que cria um túnel exclusivo entre sua rede local e a AWS, garantindo maior estabilidade e segurança.

O único componente que não pode falhar é o **banco de dados**, pois sua queda paralisa todo o sistema.

O **frontend**, por outro lado, pode ser facilmente escalado e distribuído em múltiplos servidores.

Sempre que existe um **ponto único de falha**, há também **alto acoplamento**.

A AWS recomenda o uso de um **load balancer**, que funciona assim:
1. A requisição chega ao load balancer, que verifica o estado das máquinas.
2. O tráfego é direcionado apenas para as instâncias saudáveis.
3. É necessário utilizar outra tecnologia para substituir automaticamente as máquinas com problemas.

Arquiteturas baseadas em **microserviços** ajudam a melhorar a disponibilidade, assim como modelos **orientados a eventos**.

---

## Amazon SQS – *Simple Queue Service*

Funciona com um **Produtor** e um **Consumidor**, no formato *point-to-point*, ou seja, uma mensagem gerada será consumida por apenas um consumidor.

O SQS surgiu junto com a própria AWS, com foco em **desacoplamento temporal**.

- Cada mensagem pode ter no máximo **256 KB**. Para tamanhos maiores, o conteúdo é armazenado no **S3**, e o SQS envia apenas o caminho do arquivo.

Existem dois tipos de fila:

- **Standard:**  
  - Não garante ordem  
  - Não assegura entrega única  
  - Sem limitação de throughput

- **FIFO:**  
  - Mantém a ordem  
  - Garante entrega única  
  - Suporta até **3.000 mensagens por segundo**

Após diversas tentativas de processamento, a mensagem é enviada para a **Dead Letter Queue (DLQ)**.

Também é possível separar filas para **clientes pagos** e **clientes gratuitos**.

Características:
- **Producer–Consumer**
- **One-to-One**
- **Pull (ativo)**

---

## Amazon SNS – *Simple Notification Service*

Capaz de processar **12 milhões de mensagens por segundo**.  
Permite envio via **e-mail**, **SMS**, **HTTP**, entre outros.

É ideal para padrões de **Fan-out**.

Diferente do SQS, o **tópico não armazena mensagens**; quem armazena são os consumidores (como filas), que também lidam com *retry*, *timeout*, etc.

Características:
- **Publisher–Subscriber**
- **One-to-Many**
- **Push (passivo)**

A **arquitetura Serverless** é útil especialmente para reduzir o impacto quando regiões como **Norte da Virgínia** apresentam instabilidades.

### Principais serviços:

- **Cognito** – Usado para autenticação, podendo atuar com IP empresarial.  
- **Amplify** – Facilita o desenvolvimento frontend, geração de código e web hosting.  
- **AppSync** – Solução de APIs utilizando **GraphQL**, oferecendo geração e gerenciamento.  
- **Step Functions** – Ferramenta para **orquestração** de fluxos.  
- **EventBridge** – Barramento de eventos em **tempo real**, permitindo capturar eventos conforme ocorrem.

### Arquitetura comum:
- **API Gateway + Lambda + DynamoDB** → Lógica da aplicação  
- **S3 + CloudFront** → Interface (frontend)  
- **Cognito** → Autenticação

---

## Microsserviços

A ideia é dividir um sistema em **módulos independentes**, transformando o monolito em pequenos serviços completamente isolados.  
O principal motivo para adotar microsserviços é a **complexidade crescente** do sistema, que torna o monolito difícil de manter.

### Benefícios:

- Maior **agilidade** para os times  
- **Escalabilidade** flexível  
- **Liberdade de tecnologia** (cada serviço pode usar sua própria stack)  
- Mais **resiliência**, evitando que uma falha derrube todo o sistema  

---

# Três formas de implementar microsserviços

1. **Síncrono**  
   - A requisição passa pelo API Gateway, aciona a Lambda, consulta o DynamoDB e retorna ao cliente.

2. **Streaming**  
   - As requisições chegam em fluxo contínuo e novas instâncias de Lambda são criadas conforme a demanda.

3. **Containerizado**  
   - Os microsserviços rodam dentro de containers.

---

# Lambda

- Tempo máximo de execução: **15 minutos**  
- Memória máxima: **10 GB**  
- Atualmente há casos de uso de **LLMs dentro de Lambdas** para realizar inferência.

---

# Route 53 – DNS público da AWS

Quando ocorre uma consulta, o DNS local tenta resolver o endereço. Caso não consiga, a busca segue para a internet.

O Route 53 pode trabalhar com:
- **DNS público** (*public hosted zone*)
- **DNS privado** (*private hosted zone*)

### Tipos de roteamento possíveis:

- **Geolocalização** – Retorna um IP específico para cada país.  
- **Latência** – Direciona para o servidor mais próximo e rápido.  
- **Peso (Weighted)** – Distribui porcentagens do tráfego entre destinos.  
- **Failover** – Caso o destino principal falhe (ex: *us-east-1*), redireciona para outro (ex: *sa-east-1*).  
- **Simples** – Relação 1:1 entre nome e IP.  
- **Multivalue** – Retorna vários IPs e o cliente escolhe um.  
- **IP-Based** – Resposta baseada no IP de origem.

Também é possível criar **mapas de roteamento baseados em IP**, definindo áreas específicas.

---

## Kit de sobrevivência para qualquer sistema DNS

- **Comprei um domínio, como aponto para meu site?**
  - Criar um registro **A** → aponta para um IPv4.  
  - Criar um registro **AAAA** → aponta para um IPv6.  
  - **CNAME** → Um nome DNS aponta para outro, delegando a resolução.  
  - **TXT** → Armazena informações diversas (ex: validação de propriedade do domínio).

---

# Automate Your Architecture

Depois de dominar os serviços, o próximo passo é **automatizar rotinas**, evitando ações manuais para lidar com falhas ou mudanças.

### Problemas de fazer tudo manualmente:

- Inconsistências  
- Falta de versionamento  
- Falta de rastreamento (audit trails)

---

## Infra as Code (IaC)

A ideia é **definir infraestruturas por meio de templates**; a ferramenta executa a criação para você.

- **CloudFormation** → Funciona de forma semelhante ao Terraform, porém é totalmente integrado e focado na AWS.

### Benefícios da IaC:

- Repetibilidade  
- Deploy rápido de infraestruturas complexas  
- Remoção limpa de todos os recursos via *stack*  
- Reutilização, consistência e melhor manutenção  

### Stack

Uma *stack* é a representação lógica de todos os recursos criados por um template, exibida na interface do CloudFormation.

### CloudFormation

- Serviço gratuito  
- Base de funcionamento do **Elastic Beanstalk** (que cria automaticamente servidores, como para apps Spring Boot)  
- É interessante aprender também **Beanstalk** e **SAM** para trabalhar com AWS

---

## Using Conditions

Permite que um mesmo template gere ambientes diferentes, como **dev** e **prod**.

---

## Drift

O CloudFormation detecta quando algo foi alterado fora do template e notifica o usuário.

---

# Amazon Q

A Amazon investe há muitos anos em IA.  
Um exemplo clássico é o modelo que identificava se um gato estava carregando um rato, usando imagens rotuladas para ensinar o sistema a reconhecer o cenário e controlar uma portinhola automática.

### Amazon Q Developer

Ferramenta destinada a desenvolvedores:
- Analisa códigos em busca de vulnerabilidades  
- Integrado diretamente ao console da AWS  
- Auxilia em manutenção, refatorações e correções de bugs  

---

### Por que utilizar caching?

- Quando o volume de requisições por segundo é muito alto, não é viável consultar o banco repetidamente com a mesma query.  
- Ideal para dados **altamente estáticos**.  
- Ajuda a evitar consultas mais lentas e pesadas.  

O objetivo é **obter dados de um local mais próximo e mais rápido**, reduzindo carga no banco de dados.

É essencialmente o que já foi visto sobre Redis nas aulas do Glaucio, mas agora aplicado no contexto AWS (“versão Herbert Bezos”).

---

## Elasticache

Usado como uma camada na frente do banco de dados.

Aplicações comuns:
- Quando há **problemas de tempo de resposta**.  
- Quando o **banco está sobrecarregado** e não suporta mais a demanda.  
- Quando se busca **reduzir custos** de banco de dados.  

### Tecnologias suportadas:

- **Memcached** – Armazenamento simples **<K, V>**.  
- **Redis** – Armazena em disco além da memória; suporta **estruturas de dados complexas**.  
- **Valkey** – Alternativa mais barata ao Redis.


