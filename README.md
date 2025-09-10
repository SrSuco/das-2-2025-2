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
- Lembrar do desenho -> `regiou_sa-east-1 = [availability-zone,availability-zone,availability-zone]`
- Cada AZ -> `availability-zone = [data-center-1, data-center-2, data-center-3]`
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
