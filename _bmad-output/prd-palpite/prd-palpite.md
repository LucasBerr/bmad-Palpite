---
title: Palpite
status: final
created: 2026-11-05
updated: 2026-11-05
---

# PRD: Palpite
*Working title — confirm com a fundadora.*

## 0. Document Purpose

Este PRD é destinado ao grupo (atuando como engenheiros de requisitos), ao professor avaliador do T1, e a qualquer leitor que precise entender o escopo do MVP do Palpite antes de evoluir para arquitetura, UX ou backlog. Ele foi construído a partir de três fontes, citadas ao longo do texto: a entrevista real com a fundadora ([Transcript_da_entrevista.csv](../../Transcript_da_entrevista.csv)), a sessão de elicitação em Party Mode com agentes e personas ([sessao_party_mode.md](../../sessao_party_mode.md)), e pesquisa externa (concorrentes, legislação brasileira, benchmarks de mercado) feita durante essa sessão. Vocabulário fixado no Glossário (§3); FRs numeradas globalmente e agrupadas por feature (§4); toda suposição não confirmada pela cliente real está marcada inline como `[ASSUMPTION]` e indexada em §9. Detalhes de trade-off técnico e de precificação que não pertencem à narrativa principal estão em [addendum.md](addendum.md).

## 1. Vision

Palpite é um aplicativo mobile que ajuda assessorias de corrida a oferecer, além do treino, acompanhamento nutricional aos seus alunos — sem precisar que a assessoria tenha sua própria equipe de nutrição do zero. O app compara o que o guia alimentar brasileiro recomenda para o perfil de cada aluno (peso, altura, objetivo, atividade física) com o que ele realmente consome, e gera um "palpite": uma sugestão de ajuste, nunca um diagnóstico. Toda sugestão é validada por uma nutricionista vinculada à própria assessoria antes de chegar ao aluno.

O valor central não é apenas calcular macros — é fazer isso **respeitando a rotina e o orçamento real do aluno**, em vez de prescrever uma dieta ideal que ignora se a pessoa tem tempo ou dinheiro para cumpri-la. É esse o diferencial que a fundadora relatou na entrevista real, e que distingue o Palpite de calculadoras nutricionais genéricas.

O modelo de negócio é B2B2C: a fundadora vende o acesso a assessorias de corrida (via contato direto, não autosserviço), que por sua vez liberam o app para seus próprios alunos e para sua própria nutricionista.

## 2. Target User

### 2.1 Jobs To Be Done

- **Aluno da assessoria:** "Quero saber se estou comendo de um jeito compatível com meu treino, sem ter que seguir uma dieta genérica que não cabe na minha rotina ou no meu bolso."
- **Nutricionista da assessoria:** "Quero validar e personalizar, com meu respaldo profissional, o que cada grupo de alunos recebe — sem precisar montar tudo manualmente do zero."
- **Dono/gestor da assessoria:** "Quero oferecer acompanhamento nutricional como diferencial competitivo da minha assessoria, sem contratar e gerenciar uma equipe de nutrição própria."
- **Fundadora (dona do produto):** "Quero uma fonte de receita recorrente e escalável, vendendo em pacote para grupos, mantendo controle total do produto e da capacidade de atualizá-lo."

### 2.2 Non-Users (v1)

- Pessoas físicas sem vínculo com uma assessoria contratante — `[ASSUMPTION confirmada pelo transcript]` não há autocadastro individual.
- Escolas públicas, prefeituras/universidades (modelo PUC) e empresas genéricas (RH) — decisão de escopo do grupo; a ideia apareceu na entrevista mas foi explicitamente descartada do MVP.
- Público sedentário como segmento comercial — o campo de atividade física aceita "sedentário" como dado de perfil, mas não é para quem a assessoria vende.
- Nutricionistas autônomas vendendo serviço direto a múltiplas empresas dentro do app — ideia que a própria fundadora chamou de "versão 3", fora do MVP.

### 2.3 Key User Journeys

- **UJ-1. Marcos recebe seu primeiro palpite.**
  - **Persona + contexto:** Marcos, 34 anos, corredor amador, aluno de uma assessoria que acabou de contratar o Palpite.
  - **Estado de entrada:** não autenticado, baixou o app pela loja depois de receber um convite da assessoria.
  - **Caminho:** instala o app → é convidado a se cadastrar com CPF, vê que já está vinculado ao CNPJ da assessoria → completa perfil (peso, altura, objetivo, atividade física, frequência de compra) → vê o conteúdo do TCLE e aceita → registra o que consumiu no dia.
  - **Clímax:** o app mostra a comparação entre o recomendado e o consumido, com um "palpite" marcado como **pendente de validação da nutricionista**.
  - **Resolução:** Marcos é notificado quando a nutricionista valida o palpite; só então ele vê a recomendação final, sempre com o aviso de que não substitui orientação profissional.
  - **Caso de exceção:** se Marcos tentar abrir o app sem internet antes do primeiro cadastro completo, não há nada em cache ainda — ele só consegue tentar de novo quando houver conexão (realiza FR-7).

- **UJ-2. Dra. Helena valida o palpite de uma turma inteira.**
  - **Persona + contexto:** Dra. Helena, nutricionista registrada dentro da conta da assessoria.
  - **Estado de entrada:** autenticada no perfil de nutricionista, vinculado à assessoria.
  - **Caminho:** abre a fila de palpites pendentes de validação → revisa o palpite gerado pelo motor de regras para cada aluno → ajusta manualmente quando julgar necessário → aprova.
  - **Clímax:** ao aprovar, o palpite passa a ficar visível para o aluno.
  - **Resolução:** ela consegue ver, por aluno, se o TCLE já foi aceito antes de validar (realiza FR-4, FR-5).
  - **Caso de exceção:** se o TCLE do aluno ainda não foi aceito, o sistema bloqueia a validação até o aceite existir.

- **UJ-3. Carla contrata o Palpite para sua assessoria.**
  - **Persona + contexto:** Carla, dona de uma assessoria de corrida com 15 alunos.
  - **Estado de entrada:** fora do app, contato comercial direto com a fundadora (não há checkout self-service).
  - **Caminho:** negocia a faixa de preço pelo volume de alunos (11–50) → recebe o CNPJ vinculado → acessa o papel de gestora dentro do app → convida alunos e sua nutricionista.
  - **Clímax:** os alunos convidados baixam o mesmo app público e, ao se autenticarem, já aparecem vinculados à assessoria de Carla.
  - **Resolução:** Carla acompanha quantos alunos ativaram o acesso.
  - **Caso de exceção `[ASSUMPTION]`:** se Carla ultrapassar os 50 alunos contratados, o comportamento do sistema (upgrade automático, bloqueio de novos convites, ou cobrança proporcional) não foi decidido — ver Open Question 1.

- **UJ-4. Marcos confere o último palpite no vestiário, sem internet.**
  - **Persona + contexto:** mesmo Marcos da UJ-1, depois de já ter usado o app algumas vezes.
  - **Estado de entrada:** autenticado anteriormente, sem conexão agora.
  - **Caminho:** abre o app → tela mostra o último palpite validado, já em cache.
  - **Clímax:** ele consegue ver a recomendação sem precisar de internet.
  - **Resolução:** qualquer tentativa de registrar novo consumo fica bloqueada com aviso, até haver conexão (realiza FR-7).

## 3. Glossary

- **Palpite** — sugestão de ajuste nutricional gerada pelo motor de regras do app, comparando o recomendado (via Guia Alimentar Brasileiro + perfil) com o consumo registrado pelo aluno. Nunca é diagnóstico.
- **Assessoria (de corrida)** — empresa cliente (comprador B2B) vinculada a um CNPJ, que contrata o Palpite e distribui o acesso a seus Alunos e sua Nutricionista.
- **Aluno** — usuário final, vinculado a uma Assessoria, que registra consumo e recebe Palpites.
- **Nutricionista (da assessoria)** — perfil registrado dentro da conta da Assessoria (não é parceira externa do Palpite), responsável por validar/ajustar cada Palpite antes de liberá-lo ao Aluno, conforme exigido pela Resolução CFN nº 760/2023.
- **Gestor da assessoria** — perfil com poder de liberar/revogar acesso de Alunos e da Nutricionista dentro da conta da Assessoria.
- **TCLE (Termo de Consentimento Livre e Esclarecido)** — termo que o Aluno deve aceitar antes do primeiro Palpite validado, conforme a Resolução CFN nº 760/2023 sobre telenutrição.
- **Faixa de alunos** — tier de precificação do plano da Assessoria, definido pela quantidade de Alunos ativos (ver §7 Monetização no addendum).
- **Guia Alimentar Brasileiro** — fonte oficial usada pelo motor de regras para calcular as necessidades nutricionais recomendadas por perfil.

## 4. Features

### 4.1 Cadastro e perfil nutricional

**Descrição:** O Aluno se cadastra vinculado ao CNPJ da Assessoria que o convidou, preenchendo dados de perfil (peso, altura, objetivo, atividade física/esporte praticado, frequência de compra). `[ASSUMPTION]` perfil socioeconômico/renda é coletado para habilitar o diferencial de "respeitar o perfil de compra", mas o formulário exato não foi detalhado na entrevista. Realiza UJ-1.

**Functional Requirements:**

#### FR-1: Cadastro vinculado a uma Assessoria
Um usuário convidado pode se cadastrar no app público apenas quando seu CPF estiver associado a um CNPJ de Assessoria já liberado pelo Gestor. Realiza UJ-1, UJ-3.

**Consequences (testable):**
- Tentativa de cadastro com CPF não vinculado a nenhuma Assessoria é rejeitada.
- Após vínculo, o Aluno só acessa funcionalidades depois de completar o perfil mínimo (peso, altura, objetivo, atividade física).

#### FR-2: Perfil nutricional do Aluno
O Aluno pode preencher e editar peso, altura, objetivo, atividade física/esporte praticado e frequência de compra de alimentos.

**Consequences (testable):**
- Alterações de perfil disparam novo cálculo de recomendação na próxima geração de Palpite.

**Out of Scope:**
- Cadastro de exames metabólicos individuais (mencionado pela fundadora como ideia futura, fora do MVP).

### 4.2 Motor de comparação (Palpite)

**Descrição:** Motor de regras determinístico, baseado nas recomendações do Guia Alimentar Brasileiro aplicadas ao perfil do Aluno, comparado ao consumo registrado. **Decisão do grupo:** não é machine learning no MVP — ver `addendum.md` para a justificativa completa. Realiza UJ-1, UJ-4.

**Functional Requirements:**

#### FR-3: Geração do Palpite
O sistema pode calcular, para cada Aluno, a diferença entre o consumo recomendado (perfil + Guia Alimentar Brasileiro) e o consumo registrado, e apresentar isso como um Palpite.

**Consequences (testable):**
- O Palpite nunca é apresentado ao Aluno como diagnóstico ou prescrição — todo Palpite carrega aviso de que não substitui orientação profissional.
- Um Palpite só é visível ao Aluno depois de validado pela Nutricionista (depende de FR-5).

**Feature-specific NFRs:**
- Precisão: o sistema deve comunicar que os valores são aproximados (não há medição exata de porções) — maior risco técnico identificado pela própria fundadora na entrevista.

### 4.3 Validação pela Nutricionista e TCLE

**Descrição:** Toda liberação de Palpite ao Aluno depende de validação de uma Nutricionista vinculada à mesma Assessoria, e do aceite prévio do TCLE pelo Aluno — exigências derivadas da Resolução CFN nº 760/2023 sobre telenutrição. Realiza UJ-1, UJ-2.

**Functional Requirements:**

#### RF-01 / FR-4: Apresentação e aceite do TCLE antes da primeira validação nutricional
O sistema deve apresentar ao Aluno o conteúdo do TCLE referente à telenutrição antes de liberar o primeiro Palpite validado pela Nutricionista. Realiza UJ-1.

**Consequences (testable):**
- Aluno não recebe nenhum Palpite validado sem aceite do TCLE registrado previamente.
- `[ASSUMPTION — com ressalva jurídica]` aceite digital com timestamp é tratado como assinatura válida; **isso precisa de revisão por advogado/CRN antes de produção real** (Open Question 2).

#### RNF-01 / FR-5: Rastreabilidade e auditabilidade do aceite do TCLE
O aceite do TCLE deve ser registrado de forma auditável (Aluno, data, hora) e consultável pela Nutricionista responsável. Realiza UJ-2.

**Consequences (testable):**
- A Nutricionista consegue visualizar, por Aluno, se e quando o TCLE foi aceito, antes de validar qualquer Palpite.

#### FR-6: Fila de validação da Nutricionista
A Nutricionista pode visualizar os Palpites pendentes de validação dos Alunos da sua Assessoria, ajustá-los manualmente e aprová-los. Realiza UJ-2.

**Consequences (testable):**
- Um Palpite não aprovado não é visível ao Aluno.

### 4.4 Gestão multi-tenant da Assessoria

**Descrição:** Um único app multi-tenant, publicado pela fundadora; cada Assessoria opera dentro do seu próprio CNPJ, com um Gestor que libera/revoga acesso de Alunos e da Nutricionista. Decisão do grupo — descarta o modelo de White Label com app próprio por empresa (ver `addendum.md`). Realiza UJ-3.

**Functional Requirements:**

#### FR-7: Provisionamento de Assessoria
Após contrato comercial direto com a fundadora (sem autosserviço), a Assessoria recebe um CNPJ provisionado e um perfil de Gestor. Realiza UJ-3.

#### FR-8: Convite e vínculo de Alunos e Nutricionista
O Gestor pode convidar Alunos e a Nutricionista da sua Assessoria, vinculando CPFs ao CNPJ da Assessoria. Realiza UJ-3.

**Consequences (testable):**
- Um CPF convidado só ganha acesso funcional após o vínculo ser confirmado pelo Gestor.

**Notes:**
- `[NOTE FOR PM]` Comportamento quando o número de Alunos ativos excede a Faixa de alunos contratada não foi decidido (Open Question 1).
- `[NOTE FOR PM]` Comportamento de exclusão/bloqueio de dados quando um Aluno é desvinculado da Assessoria não foi decidido (Open Question 3) — tem implicação direta de LGPD.

### 4.5 Consulta offline do último Palpite

**Descrição:** O Aluno pode visualizar, sem conexão, o último Palpite já validado e sincronizado. Nenhum registro de dado (consumo, cadastro) funciona offline. Decisão do grupo, inspirada em padrão de mercado (ver `addendum.md`). Realiza UJ-4.

**Functional Requirements:**

#### FR-9: Cache local do último Palpite validado
O app armazena localmente o último Palpite validado para consulta sem conexão.

**Consequences (testable):**
- Com o dispositivo offline, o Aluno consegue abrir o app e ver o último Palpite validado já sincronizado.
- Qualquer tentativa de registrar novo consumo ou editar perfil offline é bloqueada, com aviso, até haver conexão.

## 5. Non-Goals (Explicit)

- O Palpite não é, e não pretende se tornar, uma ferramenta de diagnóstico clínico ou de prescrição nutricional autônoma — sempre depende de validação humana de uma Nutricionista.
- O Palpite não atende diretamente consumidores finais sem vínculo com uma Assessoria contratante no MVP.
- O Palpite não trata comorbidades (ex. diabetes) nesta versão.
- O Palpite não oferece acompanhamento de treino — isso continua sendo responsabilidade da própria Assessoria e de suas ferramentas existentes (ex. Garmin, Strava, mencionadas na entrevista como referência externa).
- O Palpite não firma parcerias de mídia/publicidade com supermercados ou redes de varejo no MVP (decisão do grupo, motivada por risco de LGPD sobre dados sensíveis de saúde).
- O Palpite não é um app White Label com listagem própria por Assessoria — é um único app multi-tenant.

## 6. MVP Scope

### 6.1 In Scope

- Cadastro de Aluno vinculado a uma Assessoria via CNPJ.
- Perfil nutricional básico (peso, altura, objetivo, atividade física, frequência de compra).
- Motor de regras determinístico gerando o Palpite (Guia Alimentar Brasileiro vs. consumo registrado).
- TCLE com aceite digital rastreável, antes da primeira validação.
- Fila de validação/ajuste da Nutricionista por Assessoria.
- Gestão multi-tenant (Gestor convida/revoga Alunos e Nutricionista).
- Consulta offline (somente leitura) do último Palpite validado.
- App mobile em React Native, lançamento Android primeiro, depois Apple Store.
- Monetização por Faixa de alunos (pacote cobrado da Assessoria).

### 6.2 Out of Scope for MVP

- `[NON-GOAL for MVP]` Reconhecimento de imagem da despensa/geladeira e sugestão de reaproveitamento de alimentos — mencionado pela fundadora como ideia futura explícita.
- `[NON-GOAL for MVP]` Acompanhamento de treino e integrações com Garmin/Strava.
- `[NON-GOAL for MVP]` Suporte a comorbidades (diabetes e similares).
- `[NON-GOAL for MVP]` Nutricionistas autônomas vendendo serviço a múltiplas empresas dentro do app ("versão 3", nas palavras da fundadora).
- `[NON-GOAL for MVP]` Parcerias de mídia/publicidade com supermercados (ex. ideia do "Zafarin" citada na entrevista).
- `[NON-GOAL for MVP]` Machine learning / personalização aprendida — o motor é de regras determinísticas nesta versão.
- `[NON-GOAL for MVP]` Escolas públicas, prefeituras/universidades, empresas genéricas (RH) como segmento comercial.

## 7. Success Metrics

`[ASSUMPTION]` Nenhuma métrica de sucesso foi discutida com a cliente real nem na sessão de Party Mode — as métricas abaixo são propostas pela IA como ponto de partida, pendentes de validação com a fundadora.

**Primary**
- **SM-1**: Número de Assessorias com contrato ativo ao final dos primeiros 3 meses pós-lançamento — meta a definir com a fundadora. Valida FR-7.
- **SM-2**: Percentual de Alunos convidados que completam o cadastro e aceitam o TCLE — meta a definir. Valida FR-1, FR-4.

**Secondary**
- **SM-3**: Percentual de Palpites gerados que são validados pela Nutricionista em até 48h. Valida FR-6.

**Counter-metrics (do not optimize)**
- **SM-C1**: Taxa de Palpites aprovados sem ajuste pela Nutricionista — um número muito alto pode indicar validação superficial, não qualidade real do motor de regras. Contrabalança SM-3.

## 8. Open Questions

1. O que acontece quando o número de Alunos ativos de uma Assessoria excede a Faixa de alunos contratada — upgrade automático, bloqueio de novos convites, ou cobrança proporcional? (Levantada na verificação final do Party Mode, item 7.)
2. O aceite digital com timestamp é juridicamente equivalente a uma assinatura para fins do TCLE exigido pela Resolução CFN nº 760/2023? Requer consulta a advogado/CRN antes de produção real.
3. O que acontece aos dados do Aluno quando ele é desvinculado da Assessoria — exclusão ou apenas bloqueio de acesso? Tem implicação direta de LGPD (direito à exclusão).
4. O que acontece se a Assessoria atrasar o pagamento da assinatura — suspensão imediata de acesso dos Alunos, ou período de carência?
5. Quem efetivamente paga a publicação nas lojas (Google Play e Apple Store) — o grupo assumiu "fundadora e sócias" como premissa de trabalho, mas isso nunca foi confirmado literalmente pela cliente real.
6. As faixas de preço por volume (§ addendum, Monetização) — a faixa de até 10 alunos vem de um dado real da entrevista (R$60/10 alunos); as faixas de 11–50 e 51+ são extrapolação de benchmarks de mercado internacional, não validadas com a fundadora.
7. Nenhuma meta numérica de sucesso (§7) foi discutida com a cliente real.

## 9. Assumptions Index

- §2.2 — Não há autocadastro individual sem vínculo a uma Assessoria (confirmado pelo transcript, mas vale reconfirmar o escopo "só assessorias de corrida" como frase fechada com a cliente).
- §4.1 FR-1 — O formulário exato de perfil socioeconômico/renda não foi detalhado na entrevista; apenas o princípio de "respeitar o perfil de compra" foi confirmado.
- §4.3 FR-4 — Aceite digital tratado como assinatura válida do TCLE, pendente de revisão jurídica (Open Question 2).
- §6.1 Monetização por Faixa de alunos — apenas a primeira faixa (até 10 alunos = R$60) é dado real; as demais são hipótese de mercado (ver addendum.md).
- §7 — Todas as métricas de sucesso (SM-1 a SM-C1) são propostas da IA, não validadas com a fundadora.
