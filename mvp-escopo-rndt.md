 Vou analisar os documentos anexados e elaborar um Documento de Escopo que referencie o Catálogo de Projetos do MVP, alinhado às preferências narrativas e diretrizes de feedback registradas.

---

# **DOCUMENTO DE ESCOPO — REDE NACIONAL DE DADOS DE TRANSPORTE (RNDT)**

## **Produto Mínimo Viável (MVP) | Versão 1.0**

---

> **"A RNDT não é um portal de dados abertos. É um ecossistema federado onde dados de transporte ganham vida como produtos, parcerias e decisões estratégicas — com soberania, confiança e interoperabilidade."**

---

| **Elemento** | **Descrição** |
|:---|:---|
| **Produto** | Rede Nacional de Dados de Transporte (RNDT) — Data Space de Transporte do Brasil |
| **Versão** | MVP 1.0 |
| **Referência Técnica** | Catálogo de Projetos Ágeis RNDT v2.0 (Junho/2026) |
| **Base Arquitetural** | IDS RAM 4.0, European Mobility Data Space (EMDS) |
| **Prazo de Entrega** | 30 dias (Modelo Squads Paralelos) |
| **Escopo Temporal** | Junho–Julho/2026 |
| **Elaboração** | Ministério dos Transportes |
| **Parceiros Piloto** | PRF, DNIT, ANTT, UFPE |

---

## **1. PROPÓSITO E NARRATIVA CENTRAL**

A RNDT resolve um problema estrutural do setor de transportes brasileiro: **a fragmentação de dados valiosos em silos institucionais que não conversam entre si**. Diferente de portais de dados abertos tradicionais — que simplesmente publicam arquivos estáticos sem controle sobre seu uso — a RNDT cria um **mercado federado de dados** onde cada órgão mantém a custódia de suas informações, define regras de uso vinculantes e gera valor através de novos produtos e parcerias.

O benefício central da RNDT não é tecnológico. É **estratégico e econômico**: quando a PRF compartilha dados de sinistros com o DNIT, ambos ganham — a PRF amplia o impacto de sua inteligência de segurança viária, e o DNIT prioriza obras de manutenção com base em evidências reais de risco. Quando uma concessionária privada consome dados de pavimentação do DNIT sob contrato digital, o DNIT financia a própria infraestrutura de coleta sem depender exclusivamente de verbas públicas.

Este documento de escopo consolida o que será entregue no MVP, referenciando diretamente o **Catálogo de Projetos Ágeis e Prompts LLM (v2.0)** como plano de execução técnico.

---

## **2. DIFERENCIAÇÃO ESTRATÉGICA: RNDT vs. PORTAIS DE DADOS ABERTOS**

| **Dimensão** | **Portal de Dados Abertos Tradicional** | **RNDT (Data Space)** |
|:---|:---|:---|
| **Controle pós-publicação** | Nenhum — o dado é copiado e o controle se perde | Total — contratos ODRL definem uso mesmo após a transferência |
| **Soberania** | O órgão perde visibilidade sobre quem usa e como | O provedor mantém controle jurídico e técnico sobre o dado |
| **Interoperabilidade** | Cada órgão publica em formatos próprios | Padrão único (DATEX II, mobilityDCAT-ap) garante compreensão universal |
| **Precificação** | Gratuito ou não aplicável | Modelos flexíveis: gratuito governamental, comercial, pay-as-you-go |
| **Auditoria** | Inexistente ou manual | Registro imutável na Clearing House prova quem recebeu o quê e quando |
| **Produtos derivados** | Dependem de esforço ad hoc do consumidor | Data Apps homologados geram valor sem expor dados brutos |

A RNDT não substitui portais como `dados.gov.br` — **os complementa com uma camada de governança, confiança e geração de valor** que portais abertos não conseguem oferecer.

---

## **3. DELIMITAÇÃO DO ESCOPO DO MVP**

### **3.1 O que está INCLUSO**

O MVP da RNDT será composto por **cinco projetos ágeis executados em squads paralelos**, conforme detalhado no Catálogo de Projetos v2.0:

| **Projeto** | **Squad** | **Entregável Principal** | **Prazo** | **Ref. Catálogo** |
|:---|:---|:---|:---|:---|
| **INFRA-CORE-001** | Infra & Core | Ambiente Kubernetes com Keycloak (DAPS), CKAN, Clearing House e Superset operacionais | Dia 15 | [Seção INFRA-CORE-001](sandbox:///mnt/agents/upload/catalogo-projetos-rndt-v2.0.md#-projeto-infra-core-001) |
| **DATA-PROV-002** | Data & Provider | Pipelines PRF Sinistros e DNIT Pavimentação transformados para DATEX II, com 2 assets cadastrados no EDC Provedor | Dia 15 | [Seção DATA-PROV-002](sandbox:///mnt/agents/upload/catalogo-projetos-rndt-v2.0.md#-projeto-data-prov-002) |
| **CONS-UFPE-003** | Consumer (UFPE) | Conector EDC consumidor da UFPE operacional, com pipeline de ingestão pós-recebimento e coleção Postman validada | Dia 15 | [Seção CONS-UFPE-003](sandbox:///mnt/agents/upload/catalogo-projetos-rndt-v2.0.md#-projeto-cons-ufpe-003) |
| **GOV-PORTAL-004** | Gov, Portal & Playbook | Portal RNDT com tema CKAN, dashboards Superset, templates ODRL e playbook de onboarding | Dia 30 | [Seção GOV-PORTAL-004](sandbox:///mnt/agents/upload/catalogo-projetos-rndt-v2.0.md#-projeto-gov-portal-004) |
| **INTEG-GOLIVE-005** | Integração & Go-Live | Testes E2E validados, simulação de 3º nó e evento de demonstração ao vivo | Dia 30 | [Seção INTEG-GOLIVE-005](sandbox:///mnt/agents/upload/catalogo-projetos-rndt-v2.0.md#-projeto-integ-golive-005) |

### **3.2 O que está EXCLUÍDO (Pós-MVP)**

| **Item** | **Justificativa** | **Previsão de Inclusão** |
|:---|:---|:---|
| Dados da ANTT e SENATRAN | Foco nos primeiros provedores (PRF + DNIT) para validar o modelo | Fase 2 (Dias 31–60) |
| App Store com Data Apps em produção | Conceito validado conceitualmente; execução prática requer maturidade dos conectores | Fase 3 (Dias 61–90) |
| Credenciais Verificáveis (VCs) completas | ICP-Brasil atende ao MVP com validade jurídica; VCs evoluem a arquitetura | 6–12 meses |
| Remote Attestation (TPM 2.0) | Nível de segurança máximo; não crítico para validação do modelo de negócio | 6–12 meses |
| Integração internacional (Gaia-X/EMDS) | Requer estabilidade da rede nacional primeiro | 12–24 meses |
| Sistemas de segurança física (CFTV, sensores de pista) | Fora do escopo de Data Space; são dados de entrada, não componentes da rede | Não aplicável |

---

## **4. PRODUTOS E SERVIÇOS DO MVP**

### **4.1 Produtos de Dados (Assets)**

| **Asset** | **Provedor** | **Descrição** | **Política de Acesso** |
|:---|:---|:---|:---|
| `asset-prf-sinistros-2026` | PRF | Dados geocodificados e corrigidos de acidentes em rodovias federais, formato DATEX II | Pública — uso estatístico e planejamento; proibição de reidentificação (LGPD) |
| `asset-dnit-pavimentacao-2026` | DNIT | Condições de pavimentação rodoviária (ICM), formato DATEX II | Governamental gratuita; comercial mediante assinatura |

### **4.2 Produtos de Visualização (Dashboards)**

| **Dashboard** | **Fonte de Dados** | **Público-Alvo** | **Valor Gerado** |
|:---|:---|:---|:---|
| "Saúde da RNDT" | Métricas dos conectores e contratos | Gestores do Ministério | Visão operacional da rede em tempo real |
| "Popularidade de Datasets" | Logs de busca e acesso do CKAN | Provedores de dados | Inteligência sobre demanda por dados |
| "Auditoria de Transferências" | Registros da Clearing House | Auditores e jurídico | Prova matemática de entregas e compliance |

### **4.3 Serviço de Onboarding**

O **Playbook de Onboarding** (entregável GOV-PORTAL-004.7) permitirá que novos órgãos se conectem à RNDT em **menos de 4 horas**, seguindo 4 passos documentados: Identidade → Infraestrutura → Configuração → Integração.

---

## **5. ARQUITETURA DE REFERÊNCIA DO MVP**

A arquitetura do MVP segue o modelo de camadas do IDS RAM 4.0, adaptado à realidade institucional brasileira:

```
┌─────────────────────────────────────────────────────────────────┐
│  CAMADA DE GOVERNANÇA (Ministério dos Transportes)              │
│  Políticas, normas, precificação, homologação de participantes  │
├─────────────────────────────────────────────────────────────────┤
│  COMPONENTES COMPARTILHADOS (Squad 1 + Squad 4)                 │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌──────────┐ │
│  │  Keycloak   │ │    CKAN     │ │   Clearing  │ │ Superset │ │
│  │   (DAPS)    │ │  (Broker)   │ │   House     │ │(BI/Gov)  │ │
│  └─────────────┘ └─────────────┘ └─────────────┘ └──────────┘ │
├─────────────────────────────────────────────────────────────────┤
│  CONECTORES EDC (Squads 2, 3 e parceiros)                       │
│  ┌─────────────────┐    ┌─────────────────┐    ┌─────────────┐ │
│  │ PRF (Provedor)  │◄──►│  UFPE (Consum.) │    │ DNIT (Prov.)│ │
│  │ • Apache Camel  │    │ • PostGIS/BI    │    │ • Camel     │ │
│  │ • DATEX II      │    │ • Postman       │    │ • DATEX II  │ │
│  └─────────────────┘    └─────────────────┘    └─────────────┘ │
├─────────────────────────────────────────────────────────────────┤
│  PADRÕES SEMÂNTICOS                                             │
│  DATEX II • mobilityDCAT-ap • ODRL • JSON-LD • DSP v0.8        │
└─────────────────────────────────────────────────────────────────┘
```

Para especificação técnica completa das interfaces entre componentes, consultar o **Anexo A (Especificação Técnica das Interfaces)** e o **Anexo B (Mock Server)** do Catálogo de Projetos v2.0.

---

## **6. CRONOGRAMA E MARCOS**

| **Marco** | **Data** | **Entregáveis** | **Critério de Sucesso** |
|:---|:---|:---|:---|
| **M1: IDD Baseline** | Dia 7 | Interface Definition Document v1.2 validado; mocks operacionais; Postman Collection 100% | Todos os squads executam testes contra mocks com sucesso |
| **M2: Infraestrutura Core** | Dia 15 | Keycloak, CKAN, Clearing House e Superset deployados; certificados ICP-Brasil ativos | Squad 2 e 3 conseguem autenticar e catalogar assets |
| **M3: Dados e Consumo** | Dia 15 | 2 assets cadastrados; conector UFPE operacional; pipeline de ingestão validado | Transferência de teste entre PRF/DNIT e UFPE com sucesso |
| **M4: Portal e Governança** | Dia 25 | Portal RNDT acessível; dashboards operacionais; playbook publicado | Stakeholders navegam no portal e solicitam acesso a dados |
| **M5: Go-Live** | Dia 30 | Testes E2E validados; demo ao vivo; documentação completa | Demonstração do ciclo DSP completo (descoberta → negociação → transferência → auditoria) |

---

## **7. GOVERNANÇA E PRECIFICAÇÃO DO MVP**

### **7.1 Tipos de Acesso**

| **Tipo** | **Aplicabilidade** | **Modelo** |
|:---|:---|:---|
| **Público** | Pesquisa acadêmica, jornalismo, cidadania | Gratuito, sem registro |
| **Governamental** | Órgãos públicos federais, estaduais, municipais | Gratuito, com contrato ODRL de finalidade |
| **Comercial** | Concessionárias, seguradoras, startups de mobilidade | Assinatura mensal ou pay-as-you-go |
| **Restrito** | Dados sensíveis (sinistros com identificação) | Credenciamento + security clearance |

### **7.2 Precificação de Referência (MVP)**

| **Asset/ Serviço** | **Modalidade** | **Valor** |
|:---|:---|:---|
| Sinistros PRF (anônimos) | Gratuito governamental | R$ 0,00 |
| Pavimentação DNIT | Assinatura mensal (comercial) | R$ 5.000,00/mês |
| Telemetria de carga (futuro) | Pay-as-you-go | R$ 0,10/1.000 eventos |
| Execução de Data App | Por processamento | R$ 500,00/execução |

---

## **8. INDICADORES DE SUCESSO (KPIs)**

| **Indicador** | **Meta MVP (30 dias)** | **Meta 12 meses** |
|:---|:---|:---|
| Provedores de dados ativos | 2 (PRF + DNIT) | 10+ |
| Consumidores conectados | 1 (UFPE) | 50+ |
| Assets catalogados | 2 | 100+ |
| Contratos ODRL negociados | 5 | 1.000+ |
| Transferências de dados executadas | 10 | 10.000+ |
| Tempo médio de onboarding | < 4 horas | < 1 dia útil |
| Disponibilidade do sistema | 99,5% | 99,9% |

---

## **9. RISCOS E MITIGAÇÕES**

| **Risco** | **Probabilidade** | **Impacto** | **Mitigação** |
|:---|:---|:---|:---|
| Resistência institucional à troca de dados | Alta | Alto | Demonstração de valor via dashboards; enquadramento como parceria estratégica, não perda de controle |
| Complexidade de integração com legados | Alta | Médio | Apache Camel como camada de abstração; equipe de integração dedicada; mocks para desenvolvimento paralelo |
| Indisponibilidade de certificados ICP-Brasil | Média | Alto | Processo de aquisição antecipado; |
| Vazamento de dados pessoais (LGPD) | Baixa | Crítico | Políticas ODRL rigorosas; anonimização em pipeline; Data Apps para processamento local |
| Escalabilidade do CKAN com muitos assets | Média | Médio | Arquitetura de microserviços; cache Redis; Solr otimizado |

---

## **10. PRÓXIMOS PASSOS PÓS-MVP**

| **Horizonte** | **Iniciativa** | **Descrição** |
|:---|:---|:---|
| **Fase 2 (Dias 31–60)** | Expansão de provedores | Onboarding da ANTT e SENATRAN; novos assets (telemetria, fretes) |
| **Fase 3 (Dias 61–90)** | App Store e computação próxima ao dado | Primeiro Data App homologado; execução de algoritmos em sandbox do provedor |
| **6–12 meses** | Evolução para DIDs/VCs | Credenciais verificáveis descentralizadas; integração com Gaia-X Trust Framework |
| **12–24 meses** | Interoperabilidade internacional | Conexão com European Mobility Data Space (EMDS); hub latino-americano |
| **3–5 anos** | Economia de dados de transporte | Marketplace maduro com precificação dinâmica; integração V2X e cidades inteligentes |

---

## **11. REFERÊNCIAS**

1. **Catálogo de Projetos Ágeis e Prompts LLM — RNDT MVP v2.0** (Junho/2026). Ministério dos Transportes. Define os 5 projetos de squads paralelos, prompts LLM para geração de código, especificações técnicas de interfaces e mocks. *[Documento anexo]*

2. **Documento Técnico de Referência — Arquitetura, Componentes e Guia de Implementação do MVP** (Junho/2026). Ministério dos Transportes. Fundamentação teórica do IDS RAM 4.0, macrofluxos de provedor e consumidor, componentes open-source e casos de uso. *[Documento anexo]*

3. **IDS RAM 4.0** — International Data Spaces Reference Architecture Model. International Data Spaces Association (IDSA), 2023.

4. **Dataspace Protocol v0.8** — Eclipse Foundation / IDSA, 2024.

5. **mobilityDCAT-ap** — W3ID Transport Ontology, 2024.

---

## **12. APROVAÇÕES**

| **Função** | **Nome** | **Assinatura** | **Data** |
|:---|:---|:---|:---|
| Arquiteto RNDT | | | |
| Product Owner — Squad Infra | | | |
| Product Owner — Squad Data | | | |
| Product Owner — Squad Consumer | | | |
| Product Owner — Squad Gov/Portal | | | |
| Gestor de Projetos — Integração | | | |

---

*Documento de Escopo — RNDT MVP v1.0*
*Baseado no Catálogo de Projetos Ágeis v2.0 e no Documento Técnico de Referência*
*Ministério dos Transportes | Brasília, Junho de 2026*
