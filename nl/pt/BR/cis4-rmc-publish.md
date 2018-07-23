---


copyright:
  years: 2018
lastupdated: "2018-06-27"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Etapa 5: publicando e testando seu serviço

Agora que você tem seu broker ou brokers hospedados que atendem à especificação do OSB, é possível retornar para o console de gerenciamento de recurso para publicar seu serviço no catálogo do {{site.data.keyword.Bluemix_notm}}. Conclua a guia *Implementações*: planeje a implementação de seus planos de serviço em uma ou mais regiões do catálogo do {{site.data.keyword.Bluemix_notm}}, teste seu broker ou brokers e, finalmente, publique no catálogo no modo de visibilidade limitada. Depois de implementar com êxito, teste sua oferta para certificar-se de que ela atenda aos critérios necessários e itere por meio do processo de publicação, conforme necessário.


## Antes de começar

Esta etapa supõe que você tenha sido aprovado para entregar um serviço de faturamento integrado. Se você ainda não concluiu o registro e a aprovação iniciais no Provider Workbench, veja o [Tutorial de introdução](/docs/third-party/index.md).
{: tip}

Assegure-se de ter iniciado a etapa 1 e concluído as etapas 2, 3 e 4:
1. [ Anúncios de serviço de autor e anúncio de marketing ](/docs/third-party/cis1-docs-marketing.html).
2. [Defina sua oferta no console de gerenciamento de recurso](/docs/third-party/cis2-rmc-define.html).
3. [Desenvolva e hospede seus brokers de serviço](/docs/third-party/cis3-broker.html).
3. [Desenvolva um fluxo de autenticação](/docs/third-party/cis-iam.html).

## Publicar seu serviço no {{site.data.keyword.Bluemix_notm}}

1. No console de gerenciamento de recurso, clique na página **Implementações**.
2. Clique na guia **Brokers** e clique em **Incluir broker**
3. Clique em **Gerenciar** para abrir a página Configuração de broker de serviço.
4. Inclua o seu broker hospedado e clique em **Registrar o broker**.
5. Depois de registrar com êxito, alterne para a guia **Implementações do catálogo**.
6. Clique em ** Incluir implementação** e selecione o plano e o broker que você deseja implementar.
7. Selecione a Região e o Data center no qual você deseja implementar seu serviço e clique em **Incluir**.
8. Na página **Implementações**, revise sua implementação não publicada e clique em **Publicar**.
9. Na página **Publicar no catálogo**, revise os detalhes de sua implementação e clique em **Publicar**.

A página Implementações deve agora ser marcada como concluída na navegação, indicando que você passou os requisitos mínimos.

Preso em uma falha de implementação? Entre em contato com seu representante IBM para obter ajuda.
{: tip}

## Testar sua oferta implementada 

Como a implementação foi no modo de visibilidade limitada, somente você pode ver a sua oferta no catálogo do {{site.data.keyword.Bluemix_notm}}. Usando a lista de verificação abaixo, efetue login no {{site.data.keyword.Bluemix_notm}} e trabalhe por meio dos critérios de teste.

1. Efetue login no {{site.data.keyword.Bluemix_notm}}: [https://console.bluemix.net](https://console.bluemix.net){: new_window} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo") com seu IBMid.
2. Assegure-se de que você esteja na conta correta (a mesma conta que usou para criar o serviço)
3. Clique no link **Catálogo** no cabeçalho e procure sua oferta. Pode ser necessário abrir o catálogo de serviço experimental?
4. Em seguida, use a lista de verificação abaixo para validar seu serviço.

### Lista de verificação - Testar seu serviço
1. Validar autenticação no painel da instância de serviço
2. O catálogo é exibido corretamente (Importar no broker é mostrado corretamente no console de gerenciamento de recurso)
3. A provisão funciona - é possível criar uma instância de serviço no plano de preferência
4. A remoção de provisão funciona - é possível excluir uma instância de serviço.
5. A ligação funciona - é possível clicar em **Conexões** e conectar seu serviço a outro aplicativo
6. A desvinculação funciona - é possível desconectar seu serviço e excluir a conexão.
7. Criar chave de serviço/Excluir chave de serviço - é possível clicar em **Credenciais** e gerar uma chave de serviço e, em seguida, excluir essa chave de serviço.
8. Teste `plan_changeable` se você suportar múltiplos planos. Se você ativar isso configurando Sim, será necessário estender o Open Service Broker para suportar mudanças de plano para instâncias provisionadas. Se a sua oferta suportar múltiplos planos e você desejar que os usuários possam mudar os planos para uma instância provisionada, será necessário ativar a capacidade para que os usuários atualizem suas instâncias de serviço. Para obter mais detalhes, veja o terminal /v2/service_instances/{instance_id} PATCH no Open Service Broker API v2.12 - Correção - exibir que o usuário pode mudar o plano na instância provisionada. Para testar, alterne o plano em uma instância de serviço provisionada existente.
9. A especificação do OSB não suporta um estado de instância desativada, mas ainda não excluiu o estado de instância. Para que o IBM Cloud suporte clientes que possam ter um lapso de faturamento ou outras situações que resultem em uma suspensão de conta (mas ainda não um cancelamento), o IBM Cloud definiu terminais de API estendidos que permitem que as instâncias de serviço sejam desativadas e reativadas. As extensões de terminal a seguir são **OBRIGATÓRIAS**; trabalhe com seu representante IBM e peça que ele teste seus terminais de ativação e desativação:
   - Ativar e desativar instâncias (GET): status - retorna o estado de sua instância de serviço.
   - Ativar e desativar instâncias (PUT): permite ativar ou desativar uma instância de serviço.
10. Teste o envio de uso se você suportar planos medidos. Para quaisquer planos com uso medido, deve-se validar o seguinte:
   - É possível executar curl da API de uso e retornar corretamente a precificação precisa com base no uso.
   - É possível demonstrar que você ativou o envio automatizado por hora para o uso, suportando todos os usuários que provisionam uma instância de seu serviço.

Se seus testes forem malsucedidos, repita as etapas anteriores para publicar seu serviço e testar novamente, iterando até que você obtenha êxito.


## Próximas Etapas

Agora que você tem um serviço funcional no catálogo, é possível construir uma Demo e solicitar a aprovação para liberar publicamente o seu serviço. Veja: [Etapa 6: liberar publicamente seu serviço](/docs/third-party/cis6-ga.html).
