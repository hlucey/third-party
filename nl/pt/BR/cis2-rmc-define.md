---


copyright:
  years: 2018
lastupdated: "2018-08-21"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Etapa 2. Definindo a oferta no console de gerenciamento de recurso
{: #step2-define}

O console de gerenciamento de recurso é uma ferramenta que ajuda a orientá-lo na entrega da oferta de terceiro no catálogo do {{site.data.keyword.Bluemix_notm}}.
Agora que você está aprovado para entregar um serviço de faturamento integrado, está pronto para usar o console de
gerenciamento de recurso para registrar o serviço, iniciar o desenvolvimento e definir os planos de precificação. O console de
gerenciamento de recurso é uma ferramenta baseada na web que o ajuda a entregar o serviço de faturamento integrado para o
catálogo do {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Antes de começar
{: #pre-reqs}

1. Assegure-se de que tenha começado a trabalhar na [Etapa 1:
criar docs de serviço e anúncio de marketing (PWB)](/docs/third-party/cis1-docs-marketing.html).
2. Assegure-se de estar registrado no  {{site.data.keyword.Bluemix_notm}}. Se não, [registre](https://console.bluemix.net/registration) antes de continuar.
3. Assegure-se de que você esteja na conta correta quando começar a trabalhar no console de gerenciamento de recurso.
4. Prepare o nome do serviço do {{site.data.keyword.Bluemix_notm}}. Deve-se fornecer um nome de serviço que seja usado para identificar o serviço pela plataforma {{site.data.keyword.Bluemix_notm}} e um nome de exibição que seus clientes veem no catálogo do {{site.data.keyword.Bluemix_notm}}.

  Quando você registrar sua oferta com o console de gerenciamento de recurso, tenha o nome do serviço do {{site.data.keyword.Bluemix_notm}} pronto. O nome do serviço não é seu nome de exibição. Seu nome do serviço deve seguir estas regras:
   - Deve estar todo em minúsculas
   - Não pode incluir espaços, mas pode incluir hifens (`-`)
   - Deve ter menos de 32 caracteres

   Seu nome do serviço deve incluir o nome da sua empresa. Se sua empresa tiver mais de uma oferta, seu nome do serviço deverá incluir a empresa e a oferta como parte do nome. Por exemplo, a empresa Compose tem ofertas para Redis e Elasticsearch. Os nomes de serviço de amostra no {{site.data.keyword.Bluemix_notm}} para essas ofertas seriam `compose-redis` e `compose-elasticsearch`. Ambos os nomes de serviço têm nomes de exibição associados que são mostrados no catálogo do {{site.data.keyword.Bluemix_notm}}: *Compose Redis* e *Compose Elasticsearch*. Outra empresa (por exemplo, FastJetMail) pode ter somente a única oferta JetMail, nesse caso, o nome do serviço deve ser `fastjetmail`.

## Registrar sua oferta
{: #register}

Para começar, efetue login e registre sua oferta.

1. Efetue login no {{site.data.keyword.Bluemix_notm}}: [https://console.bluemix.net](https://console.bluemix.net){: new_window} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo") com seu ID do {{site.data.keyword.Bluemix_notm}}.
   **Aviso**: é crítico que você esteja na conta correta do {{site.data.keyword.Bluemix_notm}}. Se você tiver mais de uma conta, assegure-se de alternar para a correta.
2. Acesse o painel do console de gerenciamento de recurso: [ https://console.bluemix.net/onboarding/dashboard](https://console.bluemix.net/onboarding/dashboard){: new_window} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo").
3. Clique em **Novo recurso** para incluir seu recurso.
4. Inclua seu  ** Nome do recurso **. Esse valor é o seu nome do serviço exclusivo do {{site.data.keyword.Bluemix_notm}} que você derivou na seção anterior.
5. Neste ponto do processo, não esperamos que você tenha um broker de serviço hospedado existente, selecione **Não** para o campo **O seu broker está pronto para importação?** . Vamos guiá-lo pela criação de um broker em etapas posteriores e você retornará para o console de gerenciamento de recurso para importar seu broker depois que ele for desenvolvido e hospedado.
7. Depois de enviar, você será levado para a página **Resumo**. Conclua quaisquer valores *necessários* adicionais e clique em **Salvar**.

É possível salvar o progresso no console de gerenciamento de recurso e voltar mais tarde para incluir mais informações. O console de gerenciamento de recurso foi projetado para ajudá-lo a gerenciar o ciclo de vida de seu serviço, portanto, tudo bem se você não tiver todas as respostas para todos os campos imediatamente.
{: tip}

## Inserir seus metadados da oferta
{: #offering-metadata}

Na página **Oferta**, forneça os valores de metadados que são armazenados no catálogo do {{site.data.keyword.Bluemix_notm}}. Além disso, alguns desses valores precisam ser exportados e armazenados em seu broker de serviço no qual eles são usados para fornecimento e retornados como parte da Resposta `catalog (GET)`. Você usará esses valores para ajudar a iniciar o desenvolvimento de um broker de serviço em etapas posteriores.

1. No console de gerenciamento de recurso, clique na página **Oferta** e clique na guia **Página de listagem**. A **Página de listagem** define os metadados que são exibidos no painel de serviço de sua oferta do {{site.data.keyword.Bluemix_notm}}. Conclua todos os valores necessários e clique em **Salvar**. O console de gerenciamento de recurso executará um registro inicial de seu serviço com o {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM). Uma notificação de que seu serviço foi registrado com o IAM é exibida. Você fará muito mais com o IAM mais tarde.
2. Na página Oferta, clique na guia **Configurações**.
   1. Especifique se sua oferta permitirá **Mudanças de plano suportadas?**. O padrão é **Não**. Se você especificar **Sim**, será necessário estender o Open Service Broker para suportar mudanças de plano para instâncias provisionadas. Se sua oferta suportar múltiplos planos e você desejar que os usuários sejam capazes de mudar os planos para uma instância provisionada existente, será necessário ativar a capacidade para os usuários atualizarem suas instâncias de serviço. Para obter mais detalhes, veja o terminal `/v2/service_instances/{instance_id} PATCH` no [Open Service Broker API v2.12](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md#updating-a-service-instance){: new_window} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")
   2. Especifique se seu serviço será **Ligável**. O padrão é **Não**. Selecione **Sim** se o seu serviço puder ser ligado a aplicativos no {{site.data.keyword.Bluemix_notm}}. Se ligável, ele deve ser capaz de retornar os terminais e credenciais de API para seus consumidores do serviço. Ao desenvolver um serviço ligável, deve-se usar as [operações ligáveis no Open Service Broker API v2.12](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md#binding){: new_window} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")
   3. Preencha os campos obrigatórios adicionais e clique em **Salvar**.
3. A página Oferta deve agora ter um visto na navegação, indicando que você passou os requisitos mínimos para concluir esta página. Se a página ainda estiver marcada como incompleta, será necessário reabrir a página e verificar se há campos *obrigatórios* incompletos.

Sua carta de oferta inicial inclui uma URL de documentação de serviço que foi gerada pelo Provider Workbench. Deve-se inserir essa URL nos campos **URL da documentação** e **URL de instruções**
{: tip}

## Registrar com o IAM
{: #reg-iam}

O IAM é necessário para todos os serviços a serem integrados no {{site.data.keyword.Bluemix_notm}}. Veja [O que é IAM?](/docs/iam/index.html#what-is-cloud-iam-) para saber mais sobre os conceitos e os requisitos do IAM.

O console de gerenciamento de recurso gera os valores do IAM a seguir:
   - ID do serviço (gerado e armazenado)
   - Chave API (gerada, não armazenada - mostrada uma vez)
   - ID de cliente (gerado e armazenado)
   - Segredo do cliente (gerado, não armazenado)

O provedor de serviços precisa fornecer:
   - URI de redirecionamento (você retornará para o console de gerenciamento de recurso depois de ter desenvolvido seu OSB. Você será capaz de derivar o URI de redirecionamento do local do broker de serviço hospedado)

1. No console de gerenciamento de recurso, clique na página **Gerenciamento de acesso**.
2. Clique em **Ativar o IAM**. O console de gerenciamento de recurso registra seu serviço com o IAM, cria seu ID de serviço e Política e cria uma Chave API para você. Além disso, ele cria um ID de cliente e um Segredo incompletos. O ID de cliente deve ser atualizado com seu URI de redirecionamento depois de obtê-lo.
3. Clique em **Status** para ver o estado atual de sua ativação do IAM.

**Nota**: você precisará voltar para a página do IAM posteriormente para fornecer seu `URI de redirecionamento`. Você não terá esse valor até executar algum desenvolvimento adicional para construir um fluxo de autenticação. As etapas posteriores ajudarão a guiá-lo ao discernir o valor do URI de redirecionamento.

Você recebe sua Chave API ao **Ativar o IAM**. É crítico que você salve a Chave API. O valor não é mostrado novamente. Se você perder a sua chave API, será possível excluir a chave e criar uma nova: [Gerenciar chaves API do ID do serviço](/docs/iam/serviceid_keys.html#serviceidapikeys)
{: tip}

## Desenvolver um plano de precificação
{: #pricing-plan}

Ao integrar seu serviço ao {{site.data.keyword.Bluemix_notm}}, deve-se definir um plano de precificação. Se você tem conhecimento detalhado sobre como deseja cobrar os usuários por seu serviço, é possível fornecer essas informações em seu plano. No entanto, se você ainda não estabeleceu um plano pago, é possível começar ativando um plano grátis e, então, voltar e configurar um plano pago posteriormente.

1. No console de gerenciamento de recurso, clique na página **Precificação**.
2. Clique em **Incluir plano** para criar uma nova entrada de plano e clique em **Editar plano** para editar o plano.
   * **Plano grátis**: todas as ofertas podem ter um plano Lite que seja livre de encargos, permitindo que os usuários experimentem o seu serviço. Os planos grátis usam *Lite* para o **Nome de exibição** e *lite* para o **Nome programático**. Especifique **Sim** para **Este plano é grátis?**. Clique **Salvar.** Seu plano é publicado no catálogo do {{site.data.keyword.Bluemix_notm}}.
   * **Plano de assinatura**: especifique **Não** para **Este plano é grátis?**. Preencha os campos requeridos. Deixe a métrica  ** Métricas de Precificação **  padrão. Essa métrica padrão é fornecida para você usar para cobrar os usuários por uma taxa mensal única. Clique **Salvar.** Seu plano é publicado no catálogo do {{site.data.keyword.Bluemix_notm}}. Salve o comando curl de amostra para enviar o uso.
   * **Plano medido**: especifique **Não** para **Este plano é grátis?**. Preencha os campos requeridos. *Exclua* a métrica de assinatura padrão **Métricas de precificação**. Clique em **Incluir outra métrica**, conclua a página **Incluir métrica de precificação** e clique em **Incluir métrica**. Clique **Salvar.** Seu plano é publicado no catálogo do {{site.data.keyword.Bluemix_notm}}. Salve o comando curl de amostra para enviar o uso. Para ajudar a selecionar as métricas certas, veja [Integração de medição](/docs/third-party/metering.html).
3. A página **Precificação** deve agora ser marcada como concluída, indicando que você passou os requisitos mínimos para concluir esta página.

Os provedores de serviços precisam automatizar o envio de uso por hora para todos os planos medidos. Para obter mais informações, veja: [Enviando o uso para planos medidos](/docs/third-party/submitusage.html)
{: tip}

## Exportar seus metadados como JSON
{: #export-metadata}

Agora que você definiu seu serviço no console de gerenciamento de recurso, é possível fazer download de um arquivo catalog.json e usá-lo para informar o desenvolvimento de seu Open Service Broker. O catalog.json contém metadados que devem ser hospedados em seu broker. Esses valores definem o contrato entre o broker e a plataforma {{site.data.keyword.Bluemix_notm}} para os serviços e planos suportados pelo broker. Todos os metadados do catálogo adicionais que não são necessários para fornecimento são armazenados dentro do catálogo do {{site.data.keyword.Bluemix_notm}} e quaisquer atualizações nos valores de exibição do catálogo que são usados para renderizar seu painel, como links, ícones e metadados convertidos de i18n, devem ser atualizadas no console de gerenciamento de recurso e não alojadas em seu broker. Nenhum dos metadados armazenados em seu broker é exibido no console do {{site.data.keyword.Bluemix_notm}} ou na CLI do {{site.data.keyword.Bluemix_notm}}; o console e a CLI retornam o que foi configurado no console de gerenciamento de recurso e armazenado no catálogo do {{site.data.keyword.Bluemix_notm}}.

1. No console de gerenciamento de recurso, abra a página **Implementações**.
2. Clique em **Gerenciar**.
3. Clique em **Fazer download de definições**.

Salve seu arquivo  ` catalog.json ` . Você o usará para desenvolver seu Open Service Broker na próxima seção.

## Próximas Etapas
{: #next-steps}

Way to go! Você definiu sua oferta de serviços incluindo metadados de exibição do catálogo, registrando com o IAM e criando um ou mais planos de precificação. Em seguida, é possível tomar o JSON exportado e começar a desenvolver um broker de serviço. Veja [Etapa 3: desenvolvendo e hospedando brokers de serviço](/docs/third-party/cis3-broker.html).
