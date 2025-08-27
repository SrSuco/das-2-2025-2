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
