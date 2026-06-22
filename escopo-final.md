# **DOCUMENTO DE ESCOPO — REDE NACIONAL DE DADOS DE TRANSPORTE (RNDT)**

## **Produto Mínimo Viável (MVP) | Versão 1.0**

---

> *“A RNDT não é um portal de dados abertos. É um ecossistema federado onde dados de transporte ganham vida como produtos, parcerias e decisões estratégicas — com soberania, confiança e interoperabilidade.”*

---

| **Elemento** | **Descrição** |
|:---|:---|
| **Produto** | Rede Nacional de Dados de Transporte (RNDT) — *Data Space* de Transporte do Brasil |
| **Versão** | MVP 1.0 |
| **Base Arquitetural** | IDS RAM 4.0, *European Mobility Data Space* (EMDS) |
| **Prazo Total** | 30 dias (modelo de squads paralelos com semana inicial de imersão) |
| **Período** | Junho–Julho/2026 |
| **Elaboração** | Ministério dos Transportes |
| **Parceiros Piloto** | PRF, DNIT, ANTT, UFPE |

---

## **1. PROPÓSITO E NARRATIVA CENTRAL**

A RNDT resolve um problema estrutural do setor de transportes brasileiro: **a fragmentação de dados valiosos em silos institucionais que não conversam entre si**. Ao contrário de portais de dados abertos tradicionais — que publicam arquivos estáticos sem controlar seu uso — a RNDT cria um **mercado federado de dados** onde cada órgão mantém a custódia de suas informações, define regras de uso vinculantes e gera valor por meio de novos produtos e parcerias.

O benefício central não é apenas tecnológico, mas **estratégico e econômico**: quando a PRF compartilha dados de sinistros com o DNIT, ambos ganham — a PRF amplia o impacto de sua inteligência de segurança viária, e o DNIT prioriza obras de manutenção com base em evidências reais de risco. Quando uma concessionária privada consome dados de pavimentação do DNIT sob contrato digital, o DNIT financia sua própria infraestrutura de coleta sem depender exclusivamente de verbas públicas.

---

## **2. DIFERENCIAÇÃO ESTRATÉGICA: RNDT vs. PORTAIS DE DADOS ABERTOS**

| **Dimensão** | **Portal de Dados Abertos Tradicional** | **RNDT (Data Space)** |
|:---|:---|:---|
| **Controle pós-publicação** | Nenhum — o dado é copiado e o controle se perde | Total — contratos ODRL definem uso mesmo após a transferência |
| **Soberania** | O órgão perde visibilidade sobre quem usa e como | O provedor mantém controle jurídico e técnico sobre o dado |
| **Interoperabilidade** | Cada órgão publica em formatos próprios | Padrão único (DATEX II, mobilityDCAT‑ap) garante compreensão universal |
| **Precificação** | Gratuito ou não aplicável | Modelos flexíveis: gratuito governamental, comercial, pay‑as‑you‑go |
| **Auditoria** | Inexistente ou manual | Registro imutável na *Clearing House* prova quem recebeu o quê e quando |
| **Produtos derivados** | Dependem de esforço ad hoc do consumidor | *Data Apps* homologados geram valor sem expor dados brutos |

A RNDT não substitui portais como `dados.gov.br` — **complementa‑os com uma camada de governança, confiança e geração de valor**.

---

## **3. DELIMITAÇÃO DO ESCOPO DO MVP**

### **3.1 O que está INCLUSO**

O MVP será executado por **cinco squads paralelos**, com o seguinte fluxo:

1. **Semana 1 (Dias 1–7): Imersão e Estudo** – cada squad dedica‑se ao conhecimento das ferramentas (EDC, Keycloak, CKAN, Clearing House, Superset, Camel) e à experimentação local.
2. **Dias 8–10: Definição de Interface** – com base na experiência prática, os tech leads consolidam o *Interface Definition Document* (IDD) que servirá de contrato entre os squads.
3. **Dias 11–25: Desenvolvimento Paralelo** – cada squad executa seu projeto conforme o IDD.
4. **Dias 26–30: Integração e Go‑Live** – todos os componentes são reunidos, testados em conjunto e apresentados no evento de lançamento.

Os projetos e suas responsabilidades são:

| **Projeto** | **Squad** | **Entregável Principal** | **Prazo** |
|:---|:---|:---|:---|
| **INFRA‑CORE** | Infra & Core | Ambiente Kubernetes com Keycloak (DAPS), CKAN, Clearing House e Superset operacionais | Dia 25 |
| **DATA‑PROV** | Data & Provider | Pipelines PRF Sinistros e DNIT Pavimentação transformados para DATEX II, com 2 *assets* cadastrados no EDC Provedor | Dia 25 |
| **CONS‑UFPE** | Consumer (UFPE) | Conector EDC consumidor da UFPE operacional, pipeline de ingestão e coleção Postman validada | Dia 25 |
| **GOV‑PORTAL** | Gov, Portal & Playbook | Portal RNDT com tema CKAN, dashboards Superset, templates ODRL e *playbook* de *onboarding* | Dia 30 |
| **INTEG‑GOLIVE** | Integração & Go‑Live | Testes E2E validados, simulação de 3º nó e evento de demonstração ao vivo | Dia 30 |

### **3.2 O que está EXCLUÍDO (Pós‑MVP)**

| **Item** | **Justificativa** | **Previsão de Inclusão** |
|:---|:---|:---|
| Dados da ANTT e SENATRAN | Foco nos primeiros provedores (PRF + DNIT) para validar o modelo | Fase 2 (Dias 31–60) |
| *App Store* com *Data Apps* em produção | Conceito validado conceitualmente; exige maturidade dos conectores | Fase 3 (Dias 61–90) |
| Credenciais Verificáveis (VCs) completas | ICP‑Brasil atende ao MVP com validade jurídica; VCs evoluem a arquitetura | 6–12 meses |
| *Remote Attestation* (TPM 2.0) | Nível de segurança máximo; não crítico para validação do modelo de negócio | 6–12 meses |
| Integração internacional (Gaia‑X/EMDS) | Requer estabilidade da rede nacional primeiro | 12–24 meses |
| Sistemas de segurança física (CFTV, sensores de pista) | Fora do escopo de *Data Space*; são dados de entrada | Não aplicável |

---

## **4. PRODUTOS E SERVIÇOS DO MVP**

### **4.1 Produtos de Dados (*Assets*)**

| **Asset** | **Provedor** | **Descrição** | **Política de Acesso** |
|:---|:---|:---|:---|
| `asset‑prf‑sinistros‑2026` | PRF | Dados geocodificados e corrigidos de acidentes em rodovias federais, formato DATEX II | Pública — uso estatístico e planejamento; proibição de reidentificação (LGPD) |
| `asset‑dnit‑pavimentacao‑2026` | DNIT | Condições de pavimentação rodoviária (ICM), formato DATEX II | Governamental gratuita; comercial mediante assinatura |

### **4.2 Produtos de Visualização (Dashboards)**

| **Dashboard** | **Fonte de Dados** | **Público‑Alvo** | **Valor Gerado** |
|:---|:---|:---|:---|
| *“Saúde da RNDT”* | Métricas dos conectores e contratos | Gestores do Ministério | Visão operacional da rede em tempo real |
| *“Popularidade de Datasets”* | Logs de busca e acesso do CKAN | Provedores de dados | Inteligência sobre demanda por dados |
| *“Auditoria de Transferências”* | Registros da *Clearing House* | Auditores e jurídico | Prova matemática de entregas e *compliance* |

### **4.3 Serviço de *Onboarding***

O **Playbook de Onboarding** (entregável do GOV‑PORTAL) permitirá que novos órgãos se conectem à RNDT em **menos de 4 horas**, seguindo 4 passos documentados: Identidade → Infraestrutura → Configuração → Integração.

---

## **5. ARQUITETURA DE REFERÊNCIA DO MVP (IDS RAM 4.0)**

A arquitetura segue as camadas do *International Data Spaces Reference Architecture Model* 4.0, adaptada ao contexto brasileiro:

```
┌─────────────────────────────────────────────────────────────────┐
│  CAMADA DE GOVERNANÇA (Ministério dos Transportes)              │
│  Políticas, normas, precificação, homologação de participantes  │
├─────────────────────────────────────────────────────────────────┤
│  COMPONENTES COMPARTILHADOS                                     │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌──────────┐ │
│  │  Keycloak   │ │    CKAN     │ │   Clearing  │ │ Superset │ │
│  │   (DAPS)    │ │  (Broker)   │ │   House     │ │(BI/Gov)  │ │
│  └─────────────┘ └─────────────┘ └─────────────┘ └──────────┘ │
├─────────────────────────────────────────────────────────────────┤
│  CONECTORES EDC (Provedores e Consumidores)                     │
│  ┌─────────────────┐    ┌─────────────────┐    ┌─────────────┐ │
│  │ PRF (Provedor)  │◄──►│  UFPE (Consum.) │    │ DNIT (Prov.)│ │
│  │ • Apache Camel  │    │ • PostGIS/BI    │    │ • Camel     │ │
│  │ • DATEX II      │    │ • Postman       │    │ • DATEX II  │ │
│  └─────────────────┘    └─────────────────┘    └─────────────┘ │
├─────────────────────────────────────────────────────────────────┤
│  PADRÕES SEMÂNTICOS E PROTOCOLOS                               │
│  DATEX II • mobilityDCAT‑ap • ODRL • JSON‑LD • DSP v0.8        │
└─────────────────────────────────────────────────────────────────┘
```

Todos os componentes comunicam‑se via protocolos padronizados (DSP, OAuth2, mTLS) e utilizam certificados ICP‑Brasil para autenticação mútua.

---

## **6. CRONOGRAMA E MARCOS**

| **Marco** | **Data** | **Entregáveis** | **Critério de Sucesso** |
|:---|:---|:---|:---|
| **M0: Imersão e Estudo** | Dias 1–7 | Cada squad compreende as ferramentas; laboratórios locais funcionando | Todos os membros executam *tutoriais* básicos das ferramentas |
| **M1: IDD Baseline** | Dia 10 | Interface Definition Document v1.2 validado; mocks operacionais; Postman Collection 100% | Todos os squads executam testes contra mocks com sucesso |
| **M2: Infraestrutura Core** | Dia 25 | Keycloak, CKAN, Clearing House e Superset implantados; certificados ICP‑Brasil ativos | Squad de dados e consumidor conseguem autenticar e catalogar *assets* |
| **M3: Dados e Consumo** | Dia 25 | 2 *assets* cadastrados; conector UFPE operacional; pipeline de ingestão validado | Transferência de teste entre PRF/DNIT e UFPE com sucesso |
| **M4: Portal e Governança** | Dia 28 | Portal RNDT acessível; dashboards operacionais; *playbook* publicado | *Stakeholders* navegam no portal e solicitam acesso a dados |
| **M5: Go‑Live** | Dia 30 | Testes E2E validados; demonstração ao vivo; documentação completa | Demonstração do ciclo DSP completo (descoberta → negociação → transferência → auditoria) |

---

## **7. GOVERNANÇA E PRECIFICAÇÃO DO MVP**

### **7.1 Tipos de Acesso**

| **Tipo** | **Aplicabilidade** | **Modelo** |
|:---|:---|:---|
| **Público** | Pesquisa acadêmica, jornalismo, cidadania | Gratuito, sem registro |
| **Governamental** | Órgãos públicos federais, estaduais, municipais | Gratuito, com contrato ODRL de finalidade |
| **Comercial** | Concessionárias, seguradoras, startups de mobilidade | Assinatura mensal ou *pay‑as‑you‑go* |
| **Restrito** | Dados sensíveis (sinistros com identificação) | Credenciamento + *security clearance* |

### **7.2 Precificação de Referência (MVP)**

| **Asset / Serviço** | **Modalidade** | **Valor** |
|:---|:---|:---|
| Sinistros PRF (anônimos) | Gratuito governamental | R$ 0,00 |
| Pavimentação DNIT | Assinatura mensal (comercial) | R$ 5.000,00/mês |
| Telemetria de carga (futuro) | *Pay‑as‑you‑go* | R$ 0,10/1.000 eventos |
| Execução de *Data App* | Por processamento | R$ 500,00/execução |

---

## **8. INDICADORES DE SUCESSO (KPIs)**

| **Indicador** | **Meta MVP (30 dias)** | **Meta 12 meses** |
|:---|:---|:---|
| Provedores de dados ativos | 2 (PRF + DNIT) | 10+ |
| Consumidores conectados | 1 (UFPE) | 50+ |
| *Assets* catalogados | 2 | 100+ |
| Contratos ODRL negociados | 5 | 1.000+ |
| Transferências de dados executadas | 10 | 10.000+ |
| Tempo médio de *onboarding* | < 4 horas | < 1 dia útil |
| Disponibilidade do sistema | 99,5% | 99,9% |

---

## **9. RISCOS E MITIGAÇÕES**

| **Risco** | **Probabilidade** | **Impacto** | **Mitigação** |
|:---|:---|:---|:---|
| Resistência institucional à troca de dados | Alta | Alto | Demonstração de valor via dashboards; enquadramento como parceria estratégica, não perda de controle |
| Complexidade de integração com legados | Alta | Médio | Apache Camel como camada de abstração; equipe de integração dedicada; mocks para desenvolvimento paralelo |
| Indisponibilidade de certificados ICP‑Brasil | Média | Alto | Processo de aquisição antecipado; certificados de teste para desenvolvimento |
| Vazamento de dados pessoais (LGPD) | Baixa | Crítico | Políticas ODRL rigorosas; anonimização em pipeline; *Data Apps* para processamento local |
| Escalabilidade do CKAN com muitos *assets* | Média | Médio | Arquitetura de microserviços; cache Redis; Solr otimizado |

---

## **10. EQUIPES E PERFIS**

Cada squad é multidisciplinar e conta com os seguintes papéis:

| **Squad** | **Papéis** | **Perfil Técnico** |
|:---|:---|:---|
| **Infra & Core** | 1 Tech Lead, 2 DevOps, 1 Security | Experiência em Kubernetes, Helm, certificados digitais, Keycloak, PostgreSQL |
| **Data & Provider** | 1 Tech Lead, 2 Engenheiros de Dados, 1 Integrador | Conhecimento em Apache Camel, DATEX II, ETL, Java/Kotlin, S3/MinIO |
| **Consumer (UFPE)** | 1 Tech Lead, 2 Engenheiros de Dados, 1 Analista de BI | Experiência em EDC, PostGIS, pipelines de dados, Python, dashboards |
| **Gov, Portal & Playbook** | 1 Tech Lead, 1 Front‑end, 1 UX/UI, 1 Redator Técnico | Domínio de CKAN, Superset, HTML/CSS, documentação técnica, ODRL |
| **Integração & Go‑Live** | 1 Tech Lead, 1 QA, 1 Gerente de Projetos, 1 Especialista em Segurança | Visão sistêmica, automação de testes, orquestração de eventos, conformidade |

Todos os membros participam da semana de imersão inicial para nivelar conhecimentos sobre o *Data Space* e as ferramentas do *stack*.

---

## **11. AMBIENTE NECESSÁRIO (HARDWARE E SOFTWARE)**

### **11.1 Servidor (On‑Premises ou Nuvem Pública)**

| **Recurso** | **Mínimo para o MVP** | **Observação** |
|:---|:---|:---|
| **Nós Kubernetes** | 3 nós (1 master + 2 workers) | Cada nó: 8 vCPU, 32 GB RAM, 100 GB SSD |
| **Armazenamento Persistente** | 500 GB (distribuído entre componentes) | Usar *StorageClass* com *ReadWriteOnce* |
| **Rede** | 1 Gbps, IP público fixo para o *Ingress* | Firewall liberado para portas 443, 8443 (mTLS) |
| **Certificados** | ICP‑Brasil (e‑CNPJ) para cada participante | Renovação anual; adquiridos antes do início do projeto |

### **11.2 Software Base**

| **Componente** | **Versão** | **Função** |
|:---|:---|:---|
| Kubernetes | 1.28+ | Orquestração de contêineres |
| Helm | 3.12+ | Gerenciamento de *charts* |
| Keycloak | 24.x | DAPS (autenticação e autorização) |
| CKAN | 2.10+ | *Metadata Broker* (catálogo) |
| Eclipse EDC | 0.7.x | Conectores provedor/consumidor |
| IDS Clearing House | Fraunhofer ISST | Auditoria e imutabilidade |
| Apache Superset | 3.x | Dashboards de governança |
| Apache Camel | 4.x | Pipelines de transformação ETL |
| PostgreSQL | 15+ | Bancos de dados relacionais |
| Redis | 7.x | Cache e sessões |
| MinIO | RELEASE 2024‑05‑* | Armazenamento de objetos (arquivos DATEX II) |
| Nginx Ingress Controller | 1.9+ | Roteamento e TLS |

Todos os componentes são *open‑source* e executados em contêineres Docker, com imagens oficiais ou fornecidas pelos respectivos mantenedores.

---

## **12. ESTRATÉGIA DE INTEGRAÇÃO**

A integração final ocorre em quatro etapas:

1. **Pré‑Integração (Dias 23–24):** Cada squad executa seus testes internos e valida os próprios *endpoints* contra os mocks do IDD.

2. **Integração Controlada (Dia 25):** Os squads conectam seus componentes no ambiente de *staging* (Kubernetes compartilhado), utilizando certificados de teste. Um *script* automatizado verifica a comunicação entre Keycloak ↔ EDC Provedor ↔ EDC Consumidor ↔ CKAN ↔ Clearing House.

3. **Teste de Carga e Resiliência (Dia 26–27):** Simula‑se 10 transferências simultâneas entre os três nós (PRF, DNIT, UFPE) e monitoram‑se latência, taxa de sucesso e integridade dos recibos.

4. **Teste E2E com *Onboarding* (Dia 28–29):** Um novo nó (simulado) é incorporado seguindo o *playbook*; todo o ciclo é executado do zero, medindo o tempo total.

Os resultados são consolidados em um *dashboard* de integração, e qualquer falha aciona um *rollback* para a versão estável anterior.

---

## **13. PRÓXIMOS PASSOS PÓS‑MVP**

| **Horizonte** | **Iniciativa** | **Descrição** |
|:---|:---|:---|
| **Fase 2 (Dias 31–60)** | Expansão de provedores | *Onboarding* da ANTT e SENATRAN; novos *assets* (telemetria, fretes) |
| **Fase 3 (Dias 61–90)** | *App Store* e computação próxima ao dado | Primeiro *Data App* homologado; execução de algoritmos em *sandbox* do provedor |
| **6–12 meses** | Evolução para DIDs/VCs | Credenciais verificáveis descentralizadas; integração com *Gaia‑X Trust Framework* |
| **12–24 meses** | Interoperabilidade internacional | Conexão com *European Mobility Data Space* (EMDS); hub latino‑americano |
| **3–5 anos** | Economia de dados de transporte | *Marketplace* maduro com precificação dinâmica; integração V2X e cidades inteligentes |

---

## **14. REFERÊNCIAS**

1. **Catálogo de Projetos Ágeis e Prompts LLM — RNDT MVP v2.0** (Junho/2026). Ministério dos Transportes. Define os projetos, especificações de interfaces e mocks. *(Documento interno)*

2. **Documento Técnico de Referência — Arquitetura, Componentes e Guia de Implementação do MVP** (Junho/2026). Ministério dos Transportes. Fundamentação teórica do IDS RAM 4.0, macrofluxos e casos de uso. *(Documento interno)*

3. **IDS RAM 4.0** — International Data Spaces Reference Architecture Model. International Data Spaces Association (IDSA), 2023.

4. **Dataspace Protocol v0.8** — Eclipse Foundation / IDSA, 2024.

5. **mobilityDCAT‑ap** — W3ID Transport Ontology, 2024.

---

## **15. APROVAÇÕES**

| **Função** | **Nome** | **Assinatura** | **Data** |
|:---|:---|:---|:---|
| Arquiteto RNDT | | | |
| Product Owner — Squad Infra | | | |
| Product Owner — Squad Data | | | |
| Product Owner — Squad Consumer | | | |
| Product Owner — Squad Gov/Portal | | | |
| Gerente de Projetos — Integração | | | |

---

*Documento de Escopo — RNDT MVP v1.0*  
*Ministério dos Transportes | Brasília, Junho de 2026*
