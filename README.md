# Resumo-sobre-Step-Functions-e-ASL


### *Step Functions*

O **AWS Step Functions** é um serviço oferecido pela Amazon Web Services que permite a criação e gerenciamento de fluxos de trabalho (workflows) de maneira visual e intuitiva. 

- **Automação de Processos Complexos**: 

Com o Step Functions, podemos orquestrar diferentes serviços da AWS, como Lambda, S3, DynamoDB e SNS, facilitando a automação de tarefas que envolvem múltiplos passos e serviços.


- **Gerenciamento de Erros e Exceções**: 

Um dos grandes benefícios é que ele fornece recursos embutidos para lidar com erros. Isso significa que, se algo der errado em um dos passos do workflow, podemos definir ações específicas para recuperá-lo ou notificar os responsáveis.


- **Escalabilidade**: 

O Step Functions é projetado para escalar automaticamente, permitindo gerenciar desde pequenos processos até grandes aplicações.

### *ASL (Amazon State Language)*

A **Amazon State Language (ASL)** é uma linguagem específica desenvolvida para descrever os workflows no Step Functions.

- **Definição de Fluxos de Trabalho**: Com ASL, podemos especificar cada passo do workflow de maneira clara. Incluindo não apenas as ações a serem executadas, mas também as condições sob as quais essas ações devem ocorrer.

- **Complexidade nas Definições**: A ASL permite a criação de fluxos complexos através do uso de estados como "Choice" (decisões), "Parallel" (execução paralela) e "Map" (execução em lote), oferecendo flexibilidade na lógica do seu workflow.

- **Integração com Outros Serviços**: ASL facilita a interação com outros serviços da AWS, permitindo criar automações sofisticadas sem precisar escrever código extenso.



### *Workflows*

Os **workflows** são sequências ordenadas de passos que realizam uma tarefa específica.

- **Estrutura dos Workflows**: 

Eles podem incluir diferentes tipos de passos como atividades simples (funções Lambda), decisões baseadas em condições (usando o estado "Choice"), loops (com o estado "Map") e execuções paralelas (com o estado "Parallel").


- **Visibilidade e Monitoramento**: 

O Step Functions oferece uma interface gráfica onde podemos visualizar o estado atual do workflow. Isso é extremamente útil para monitorar o progresso e diagnosticar problemas rapidamente.


- **Persistência de Estado**: 

Os workflows mantêm o estado entre os passos automaticamente, permitindo que dados sejam passados facilmente entre diferentes etapas do processo.



### *Exemplos Práticos*

#### 1. Processamento de Imagens

**Passo-a-passo detalhado**:

1. Um usuário faz upload de uma imagem para o Amazon S3.
2. O Step Functions inicia automaticamente o workflow associado ao processamento da imagem.
3. A ASL define os seguintes passos:
   - **Redimensionar Imagem**: Uma função Lambda é chamada para redimensionar a imagem conforme as especificações desejadas.
   - **Aplicar Filtro**: Outra função Lambda aplica filtros artísticos à imagem.
   - **Salvar Imagem Processada**: A imagem final é salva novamente no S3.
4. O Step Functions monitora todo o processo e gerencia erros. Por exemplo, se a função de redimensionamento falhar, ele poderá tentar novamente ou enviar uma notificação.

#### 2. Envio de Notificações

**Passo-a-passo detalhado**:

1. Uma mensagem chega à fila do Amazon SQS.
2. O Step Functions inicia o workflow para processar essa mensagem.
3. A ASL define os seguintes passos:
   - **Verificar Assinatura**: Uma função Lambda valida se a mensagem possui a assinatura correta.
   - **Enviar Notificação**: Se a assinatura estiver válida, uma notificação é enviada através do Amazon SES (Simple Email Service).
   - **Atualizar Status**: O status da mensagem processada é atualizado em uma tabela do DynamoDB.
4. O Step Functions monitora todo esse processo e pode registrar falhas ou sucessos em tempo real.
