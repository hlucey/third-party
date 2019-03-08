---

copyright:

  years: 2018, 2019

lastupdated: "2019-02-25"

keywords: billing service, resource management console, IBM Cloud, RMC, 

subcollection: third-party

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Visão geral: desenvolvendo um serviço de faturamento integrado
{: #overview}

Este tópico introduz as etapas que são necessárias para desenvolver e publicar seu serviço de faturamento integrado de terceiro no {{site.data.keyword.Bluemix}}. 
{:shortdesc}

Depois de ser aprovado para entregar sua oferta no catálogo do {{site.data.keyword.Bluemix_notm}}, você começa a desenvolver sua oferta no console de gerenciamento de recurso, uma experiência de IU guiada. Você projeta seus metadados do catálogo, configura os planos de precificação de serviço e integra ao {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM). 

Em seguida, fora do console de gerenciamento de recurso, você executa o desenvolvimento de código para construir e hospedar um novo broker de serviço aberto. Amostras do broker e docs da API do iniciador são fornecidos e você usa o IAM para desenvolver um fluxo de autenticação. Depois de concluir essas etapas, você retorna para o console de gerenciamento de recurso para implementar seu serviço no catálogo em um modo de visibilidade limitada, no qual é possível testar e validar requisitos distribuíveis. Quando você estiver pronto e sua oferta atender a todos os requisitos, seu serviço se tornará totalmente visível no catálogo do {{site.data.keyword.Bluemix_notm}}.


## Como o processo funciona
{: #process}

Para entregar um serviço de faturamento integrado, você trabalha com o ambiente de trabalho do Provedor, o console de gerenciamento de recursos e o ambiente de desenvolvimento de sua escolha. Veja a [lista de verificação](/docs/third-party?topic=third-party-checklist#checklist) para ajudar a rastrear essas etapas.

Essas etapas assumem que você foi aprovado para entregar um serviço de Faturamento integrado. Se você não concluiu o registro e a aprovação iniciais no PWB, veja: [Introdução à publicação de sua oferta de terceiros no {{site.data.keyword.Bluemix_notm}}](/docs/third-party/index.md?topic=third-party-get-started#get-started)
{: tip}

1. [ Crie sua documentação e anúncio de marketing ](/docs/third-party?topic=third-party-content-tasks#content-tasks).
2. [Defina sua oferta no console de gerenciamento de recurso{{site.data.keyword.Bluemix_notm}}](/docs/third-party?topic=third-party-step2-define#step2-define).
3. [Desenvolva e hospede seus brokers de serviço](/docs/third-party?topic=third-party-step3-osb#step3-osb).
4. [ Desenvolva um fluxo de autenticação ](/docs/third-party?topic=third-party-step4-iam#step4-iam).
5. [ Teste seu serviço ](/docs/third-party?topic=third-party-step5-pubtest#step5-pubtest).
6. [ Liberar seu serviço publicamente ](/docs/third-party?topic=third-party-public-releasing#public-releasing).

## Suporte
{: #support}

Os serviços de faturamento integrados requerem que os provedores de oferta de terceiros forneçam seu próprio modelo de suporte. Seu representante IBM pode ajudá-lo a ativar seu modelo de suporte e assegurar que, se um usuário abrir um chamado com o suporte do {{site.data.keyword.Bluemix_notm}}, o chamado será roteado para o site de suporte de terceiro.

## Atualizações contínuas
{: #maintain}

Após o seu serviço ser liberado, é possível continuar a iterar e fazer atualizações trabalhando diretamente com o seu representante do {{site.data.keyword.Bluemix_notm}}.



