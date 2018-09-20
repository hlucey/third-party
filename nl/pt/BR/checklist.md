---

copyright:
  years: 2018
lastupdated: "2018-09-05"

---

{:right: .ph data-hd-position='right'}
{:shortdesc: .shortdesc}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# Listas de verificação de ponta a ponta
{: #checklist}

Use as listas de verificação a seguir para rastrear todas as tarefas necessárias para definir, desenvolver e publicar seu serviço de faturamento integrado.
{:shortdesc}

## Definindo seu Serviço
{: #define}

| Atividade | Subtarefas | Descrição | Ambiente |
|------| ----------| ------------|-----|
| Aprenda sobre a plataforma  {{site.data.keyword.Bluemix}} . | ☐ Entendo como a camada de fornecimento, o
{{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM), o catálogo, o Open Service Broker e o serviço de medição funcionam juntos. | Diferente de um serviço referencial do {{site.data.keyword.Bluemix_notm}}, um serviço de faturamento integrado usa a plataforma {{site.data.keyword.Bluemix_notm}} para criar, ligar, excluir e cobrar por instâncias de serviço. [Conheça](/docs/third-party/platform.html#how-it-works)
os componentes críticos que compõem a plataforma para acelerar o desenvolvimento. | Documentação |
| Registre a oferta no ambiente de trabalho do Provedor {{site.data.keyword.Bluemix_notm}}. | A conclusão da tarefa de conteúdo foi concluída. <br><br>☐ Recebi a aprovação para publicar a oferta como um serviço de faturamento integrado. <br><br> ☐ Recebi um e-mail com o valor
da URL da documentação. <br><br> | A primeira etapa é registrar a oferta no ambiente de trabalho do Provedor. Para obter mais detalhes, consulte o
[Tutorial de introdução](/docs/third-party/index.html#get-started). | Workbench do Provedor |
| Publique os docs do {{site.data.keyword.Bluemix_notm}}. | ☐ Iniciei a tarefa de orientação no ambiente de trabalho
do Provedor. <br><br>O recebimento do  ` URL da Documentação ` foi recebido. <br><br> Eu publique com sucesso minhas docas. <br><br> | Sabemos que a documentação de terceiro hospedada em seu website é ótima. No entanto, agora que você está entregando um serviço de
faturamento integrado no {{site.data.keyword.Bluemix_notm}}, é necessário entregar a documentação customizada para
a sua experiência de faturamento integrada do {{site.data.keyword.Bluemix_notm}}. Para obter mais detalhes, consulte
[Criando a documentação](/docs/third-party/cis1-docs-marketing.html#docs). | Workbench do Provedor |
| Publique seu anúncio de marketing. | ☐ Comecei a tarefa de marketing no ambiente de trabalho do provedor. <br><br>  ☐ Publiquei com
sucesso o anúncio de marketing. <br><br>  | Crie o material paralelo de marketing para anunciar a disponibilidade para
o serviço por meio do newsletter do {{site.data.keyword.Bluemix_notm}} e dos canais de mídia social. Para obter mais
detalhes, consulte [Criando o anúncio de marketing](/docs/third-party/cis1-docs-marketing.html#announcement). | Workbench do Provedor |
| Registre a oferta no console de gerenciamento de recurso. | ☐ Defini um `service-name` exclusivo e significativo
como o nome do recurso.<br><br>  ☐ Validei com êxito que tenho um registro no console de gerenciamento de
recurso. <br><br>  | Use o console de gerenciamento de recurso para criar uma oferta exclusiva. Para obter mais detalhes, consulte
[as etapas para registrar a oferta](/docs/third-party/cis2-rmc-define.html#register). | Console de gerenciamento de recurso |
| Preencha a página Oferta no console de gerenciamento de recurso. | ☐ Usando o valor fornecido no e-mail da oferta do
ambiente de trabalho do Provedor, eu configurei corretamente a URL da documentação e a URL da instrução. <br><br>  ☐ Forneci uma
URL que aponta para um termo exclusivo da página de serviço sem cláusulas de faturamento ou de pagamento.<br><br>  ☐ Eu entendi e especifiquei corretamente se **Mudanças do plano suportadas?** está ativado. ☐ Compreendi e especifiquei corretamente se o serviço é de ligação.| Forneça os metadados do catálogo no console de gerenciamento de
recurso exibido no quadro do {{site.data.keyword.Bluemix_notm}}. Para obter mais detalhes, consulte [as etapas para inserir os metadados da oferta](/docs/third-party/cis2-rmc-define.html#offering-metadata). | Console de gerenciamento de recurso |
| Preencha a página Gerenciamento de acesso no console de gerenciamento de recurso. | O IAM ativou com êxito o IAM. <br><br>  ☐ Salvei
a chave API única do IAM gerada que foi criada para mim e entendo que ela não está armazenada no console
de gerenciamento de recurso e que não posso recuperá-la posteriormente.<br><br> ☐ Entendo que a página Gerenciamento de acesso não pode
ser preenchida até que eu desenvolva e hospede um broker de serviço aberto e, em seguida, derive o URI de
redirecionamento.<br><br> ☐ Depois de hospedar o broker de serviço aberto, eu retornei à página do IAM e a preenchi com êxito.| Registre a oferta com o IAM do {{site.data.keyword.Bluemix_notm}} no console de gerenciamento de recurso. O IAM permite que você autentique os usuários com segurança para os serviços de plataforma e controle o acesso aos recursos de forma consistente na plataforma {{site.data.keyword.Bluemix_notm}}. Para obter mais detalhes, consulte [as etapas para registrar com o IAM](/docs/third-party/cis2-rmc-define.html#reg-iam). | Console de gerenciamento de recurso |
| Desenvolva um ou mais planos de precificação no console de gerenciamento de recurso. | ☐ Eu forneci um plano grátis com um nome exclusivo.<br><br>  ☐ (Opcional) Trabalhei com o representante IBM para definir um plano pago, de assinatura ou medido, e entendo que devo remover o plano
de assinatura padrão para criar um plano medido.<br><br> ☐ (Opcional) Entendo que devo hospedar e desenvolver o envio de uso por
hora automatizado.| Como você cobrará pelo serviço? O console de gerenciamento de recurso fornece planos grátis ou pagos. Para obter mais detalhes, consulte [as etapas para desenvolver um plano de precificação](/docs/third-party/cis2-rmc-define.html#pricing-plan). | Console de gerenciamento de recurso |
| Exporte os metadados do catálogo do console de gerenciamento de recurso. | ☐ Entendo que alguns dos metadados que forneço nas
páginas Oferta e Precificação do console de gerenciamento de recurso devem ser exportados e fornecidos no Open Service Broker. <br><br>  ☐ Obtive o arquivo `catalog.json` na página Implementações e estou pronto para mapear a matriz de serviços
para os metadados no Open Service Broker.<br><br> | Agora que você definiu o serviço no console de gerenciamento de recurso,
é possível fazer download de um arquivo `catalog.json` e usá-lo para informar o desenvolvimento do Open Service
Broker. Para obter mais detalhes, consulte [as etapas para exportar seus metadados](/docs/third-party/cis2-rmc-define.html#export-metadata). | Console de gerenciamento de recurso |
{: caption="Tabela 1. Definindo o serviço de faturamento integrado" caption-side="top"}

## Desenvolvendo o serviço
{: #develop}

| Atividade | Subtarefas | Descrição | Ambiente |
|------| ----------| ------------|-----|
| Conheça a especificação do Open Service Broker versão 2.12. | ☐ Li a especificação do Open Service Broker e entendo que
devo desenvolver o meu próprio Open Service Broker. <br><br>  |  Os brokers de serviço gerenciam o ciclo de vida de serviços. A
plataforma {{site.data.keyword.Bluemix_notm}} interage com os Open Service Brokers para fornecer e gerenciar as instâncias
de serviço e as ligações de serviço. Para obter mais detalhes, consulte
[Desenvolvendo e hospedando os brokers de serviço](/docs/third-party/cis3-broker.html#step3-osb). | Documentação |
| Visualize as amostras do  {{site.data.keyword.Bluemix_notm}}  intermediário. | ☐ Clonei o repositório, pesquisei as
amostras do broker e estou pronto para usá-las para iniciar o desenvolvimento. <br><br>  |  [https://github.com/IBM/sample-resource-service-brokers](https://github.com/IBM/sample-resource-service-brokers){: new_window} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo") | Exemplos de código |
| Visualize a documentação da API do Open Service Broker do {{site.data.keyword.Bluemix_notm}}. | ☐ Entendo que há vários
terminais necessários que o código no Open Service Broker deve suportar. <br><br>  ☐ Entendo que, se o serviço puder ser ligado aos
apps no {{site.data.keyword.Bluemix_notm}}, ele deverá ser capaz de retornar os terminais de API e as credenciais para
os usuários do serviço. <br><br> ☐ Entendo que o {{site.data.keyword.Bluemix_notm}} definiu terminais de API estendidos
que permitem que as instâncias de serviço sejam desativadas e reativadas. |  O Open Service Broker do {{site.data.keyword.Bluemix_notm}} estende a especificação do Open Service Broker 2.12. [Conheça](/docs/third-party/cis3-broker.html#docs) os terminais necessários que o broker de serviço deve usar. | Documentação |
| Use os metadados do catálogo para iniciar o desenvolvimento do broker de serviço. | ☐ Entendo que alguns dos metadados que
forneci no console de gerenciamento de recurso devem ser exportados e fornecidos no Open Service Broker.  <br><br>  ☐ Incluí os
GUIDs e outros valores necessários listados no arquivo `catalog.json` para a matriz
de serviços no Open Service Broker de amostra. | Depois de fazer download de um arquivo `catalog.json` do console
de gerenciamento de recurso, é possível usá-lo para informar o desenvolvimento do Open Service Broker. Para obter mais detalhes,
consulte [as etapas para usar os metadados exportados para guiar o
desenvolvimento](/docs/third-party/cis3-broker.html#use-metadata). | Ambiente de desenvolvimento e documentação |
| Hospeda o Open Service Broker. | ☐ Entendo que o local hospedado do broker de serviço deve seguir o protocolo de Segurança da
Camada de Transporte (TLS) versão 1.2. <br><br> | O broker de serviço deve ser hospedado como parte de um app que pode
responder às chamadas da API de REST. E seu local hospedado deve atender às diretrizes de segurança do {{site.data.keyword.Bluemix_notm}}. Para obter mais detalhes, consulte [as etapas para hospedar o broker de serviço](/docs/third-party/cis3-broker.html#host). | Ambiente de desenvolvimento e documentação |
| Teste seu host Open Service Broker hospedado. | ☐ Validei cada um dos terminais de API que o broker de serviço
suporta executando os comandos curl com relação ao broker de serviço hospedado. <br><br> | Valide o broker de serviço executando
os comandos curl com relação aos diferentes terminais que você está ativando. Para obter mais detalhes, consulte
[as etapas para testar o broker de serviço](/docs/third-party/cis3-broker.html#test).| Ambiente de desenvolvimento e documentação |
| Derive e configure o URI de redirecionamento do IAM. | ☐ Derivei com êxito o URI de redirecionamento do IAM usando o local
hospedado do Open Service Broker e algumas informações sobre autenticação. <br><br> ☐ Preenchi com êxito a página
Gerenciamento de acesso especificando o URI de redirecionamento e configurando corretamente o identificador de cliente. <br><br> | Ao definir o serviço no console de gerenciamento de recurso, um identificador de cliente é gerado, mas observe que
provavelmente você não tinha um URI de redirecionamento no momento. Isso significa que o identificador de cliente está
configurado como `false`. Até você retornar ao console de gerenciamento de recurso com o URI de redirecionamento, não terá um identificador de cliente
true. Para obter mais detalhes, consulte [as etapas para derivar o URI de redirecionamento](/docs/third-party/cis5-iam.html#redirect-uri). | O ambiente de desenvolvimento e o console de gerenciamento de recurso |
| Desenvolva o fluxo do Open Authorization (OAuth) para a autenticação. | ☐ Eu entendo que o IAM suporta o Open ID Connect (OIDC). <br><br> ☐ Eu descobri meu terminal regional do IAM e eu redireciono com êxito os usuários de `dashboard_url` para o meu URI de redirecionamento montado e eu armazeno o `access_token` do usuário retornado em minha resposta para que possa ser usado durante a autenticação. <br><br> | Os usuários que visitam o painel de serviço devem ser autenticados corretamente. Desenvolva a autenticação baseada em token do OAuth e a autorização usando o IAM. Para obter mais detalhes, consulte
[as etapas para desenvolver o fluxo do OAuth](/docs/third-party/cis5-iam.html#oauth). | Ambiente de desenvolvimento e documentação|
| Validar autorização do usuário. | ☐ Posso obter um token de acesso para uma chave API. <br><br> ☐ Posso validar a autorização para
os usuários para a instância de serviço. <br><br> | Depois de desenvolver o fluxo do OAuth para a autenticação, deve-se validar que
os usuários estejam corretamente autorizados, assegurando que os usuários do serviço possam acessar o painel de serviço. Para obter
mais detalhes, consulte [as etapas para validar](/docs/third-party/cis5-iam.html#validate). | Ambiente de desenvolvimento e documentação |
{: caption="Tabela 2. Desenvolvendo o serviço de faturamento integrado" caption-side="top"}

## Publicando e testando seu serviço
{: #pubtest}

| Atividade | Subtarefas | Descrição | Ambiente |
|------| ----------| ------------|-----|
| Publique o serviço no modo de visibilidade limitada. | ☐ O Open Service Broker hospedado foi registrado com êxito na página
Implementações no console de gerenciamento de recurso. <br><br> ☐ As novas implementações foram criadas com êxito e a oferta
publicada para uma ou mais regiões. <br><br> |  Agora que os brokers de serviço hospedados atendem à especificação do Open
Service Broker, é possível publicar o serviço no catálogo do {{site.data.keyword.Bluemix_notm}}. Para obter mais detalhes,
consulte [as etapas para publicar o serviço](/docs/third-party/cis4-rmc-publish.html#publish). | Console de gerenciamento de recurso |
| Teste sua oferta. | ☐ Posso ver o serviço no catálogo. <br><br> ☐ A autenticação foi validada por meio do painel da instância de serviço. <br><br> ☐ Validei que o serviço é exibido corretamente no catálogo. <br><br> ☐ Posso selecionar um plano e criar uma instância de serviço. <br><br> ☐
Posso excluir uma instância de serviço. <br><br> ☐ Posso conectar o serviço a outro aplicativo. <br><br> ☐ Posso desconectar o
serviço e excluir a conexão. <br><br>  ☐ Posso gerar uma chave de serviço e excluí-la. <br><br> ☐ Eu trabalhei com meu representante IBM para validar que minha oferta suporta corretamente os terminais de ativação e desativação. <br><br> ☐ Porque a oferta tem um plano medido, testei com sucesso o envio de uso. | Agora que os brokers de serviço hospedados atendem à
especificação do Open Service Broker, é possível publicar o serviço no catálogo do {{site.data.keyword.Bluemix_notm}}. Para
obter mais detalhes, consulte [as etapas para testar o serviço](/docs/third-party/cis4-rmc-publish.html#test). | Console do {{site.data.keyword.Bluemix_notm}} |
{: caption="Tabela 3. Publicando e testando o serviço de faturamento integrado" caption-side="top"}

