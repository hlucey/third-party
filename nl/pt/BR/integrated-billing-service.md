---


copyright:
  years: 2018
lastupdated: "2018-06-28"


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

Este tópico foi projetado para guiar você pelas etapas necessárias para desenvolver e publicar o seu serviço de Faturamento Integrado de terceiro no {{site.data.keyword.Bluemix_notm}}. Depois que for aprovado para entregar sua oferta no catálogo do {{site.data.keyword.Bluemix_notm}}, você começará a desenvolver sua oferta no console de gerenciamento de recurso (console de gerenciamento de recurso), uma experiência de IU orientada. No console de gerenciamento de recurso, você projetará os metadados do catálogo, configurando os planos de precificação de serviço e integrando com o IBM Cloud Access Management (IAM). Em seguida, fora do console de gerenciamento de recurso, você executará o desenvolvimento de código para construir e hospedar um novo Open Service Broker (as amostras do broker iniciador e os docs da API serão fornecidos) e usará o IAM para desenvolver um fluxo de autenticação. Após essas etapas serem concluídas, você retornará para o console de gerenciamento de recurso para implementar seu serviço no catálogo em um modo de visibilidade limitada que permite testar e validar múltiplos requisitos distribuíveis. Quando estiver pronto e sua oferta atender a todos os requisitos, seu serviço ficará totalmente visível no catálogo do {{site.data.keyword.Bluemix_notm}}!


## O que eu preciso fazer para entregar um serviço de Faturamento Integrado?

Você trabalhará no PWB, no console de gerenciamento de recurso e do ambiente de desenvolvimento de sua escolha para entregar esses objetivos. Veja a [lista de verificação](/docs/third-party/checklist.html#checklist) para ajudar a rastrear essas etapas.

As etapas a seguir resumem o processo de integração em um alto nível:

Estas etapas supõem que você está aprovado para entregar um serviço de Faturamento Integrado. Se você não concluiu o registro e a aprovação iniciais no PWB, veja: [Introdução à publicação de sua oferta de terceiros no {{site.data.keyword.Bluemix_notm}}](/docs/third-party/index.md)
{: tip}

1. [Criar: crie docs de serviço e anúncio de marketing (PWB)](/docs/third-party/cis1-docs-marketing.html)
2. [Definir: defina sua oferta no console de gerenciamento de recurso {{site.data.keyword.Bluemix_notm}}](/docs/third-party/cis2-rmc-define.html)
3. [Desenvolver: desenvolva e hospede um ou mais brokers de serviço usando a especificação do Open Service Broker API](/docs/third-party/cis3-broker.html)
4. [IAM: desenvolva um fluxo de autenticação (OAuth), valide a autorização do usuário (v2/authz) e derive seu URI de redirecionamento](/docs/third-party/cis5-iam.html)
5. [Publicar e testar: conecte o seu OSB ao console de gerenciamento de recurso, publique o seu serviço no modo de visibilidade limitada no catálogo do {{site.data.keyword.Bluemix_notm}} e teste a sua oferta](/docs/third-party/cis4-rmc-publish.html).
6. [Solicitar aprovação para GA de seu serviço](/docs/third-party/cis6-ga.html)

## Suporte

Os serviços de faturamento integrado requerem que os provedores de serviços de terceiros forneçam seu próprio modelo de suporte. Seu representante IBM ajudará a ativar seu modelo de suporte e assegurará que, se um usuário abrir um chamado com o suporte do {{site.data.keyword.Bluemix_notm}}, o suporte do {{site.data.keyword.Bluemix_notm}} encaminhará o chamado para o site de suporte do terceiro.

## Atualizações contínuas

Após o seu serviço ser liberado, é possível continuar a iterar e fazer atualizações trabalhando diretamente com o seu representante do {{site.data.keyword.Bluemix_notm}}.



