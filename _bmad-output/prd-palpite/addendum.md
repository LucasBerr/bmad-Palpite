# Addendum — Palpite PRD

Conteúdo que apoia o PRD principal mas não pertence à narrativa (decisões técnicas detalhadas, matrizes de opções consideradas, dados de benchmark). Toda esta seção é hipótese/pesquisa externa, salvo onde citado explicitamente o transcript.

## A. Arquitetura — nativo x2 vs. framework único (decisão: React Native)

Critérios usados (agente BMAD Winston, Arquiteto):

| Opção | Custo/terceirização | Velocidade | Acesso nativo (câmera/ML futuro) |
|---|---|---|---|
| Nativo x2 (Kotlin + Swift) | Alto — dois times | Lenta — toda feature implementada duas vezes | Excelente |
| React Native | Baixo — maior pool de freelancers/agências no Brasil | Rápida — um código para os dois SOs | Boa |
| Flutter | Médio — pool menor no Brasil | Rápida | Boa, UI mais consistente |

Decisão: **React Native**, por (a) a fundadora terceirizar o desenvolvimento, (b) o ecossistema JS/TS ter maior mercado de terceirização barata no Brasil, (c) o desejo dela de manter controle de atualizações contínuas, (d) a filosofia de validar demanda rápido antes de escalar (dita explicitamente na entrevista). Nativo x2 descartado por não combinar com esse perfil.

## B. Sequência de lançamento Android/Apple

> Em 2026, Android detém entre 74% e 81% do market share móvel no Brasil, contra 20–26% do iOS (StatCounter, outubro de 2026).

A Apple exige Mac para build/assinatura, conta de desenvolvedor paga separada, e revisão historicamente mais lenta/rigorosa que a Google Play. Decisão: lançar primeiro no Google Play, depois Apple Store — mantém o compromisso de cobrir os dois SOs, só define a ordem.

Fontes: [Mobile OS Market Share Brazil — StatCounter](https://gs.statcounter.com/os-market-share/mobile/brazil) · [Android vs iOS Statistics 2026](https://www.tekrevol.com/blogs/android-vs-ios-statistics/)

## C. Modelo de distribuição — app único multi-tenant vs. White Label completo

Pesquisa de mercado mostrou que plataformas de coaching fitness/nutrição (Everfit, My PT Hub, FitBudd, Foodzilla, Nutritio) tipicamente oferecem **dois tiers**: app com marca aplicada dentro de uma base multi-tenant compartilhada (produto básico) e white label completo com listagem própria na loja (upgrade pago, ex.: My PT Hub cobra US$145+/mês por isso). O grupo decidiu adotar **apenas o tier básico (app único multi-tenant)** no MVP, descartando o white label completo — simplifica a arquitetura e o processo de publicação (uma única listagem, não uma por Assessoria).

Fontes: [White-Label Fitness App Platforms: 10 Compared](https://coachway.io/articles/branded-app-for-fitness-coaches/) · [Foodzilla White Label](https://foodzilla.com/pt/features/white-label-app)

## D. Monetização — faixas de preço por volume (hipótese, pendente de validação)

Dado real da entrevista: a fundadora mencionou vender um pacote de 10 alunos por R$60 (R$6,00/aluno), com a assessoria repassando ao aluno final dentro de uma mensalidade de R$150–160 (que inclui treino + nutrição).

Benchmarks de mercado (apps de coaching fitness/nutrição com pricing por atleta):

| Plataforma | Estrutura |
|---|---|
| Good Coach App | Grátis até 2 atletas; ~€3/atleta (3–15); ~€1,50 (16–29); ~€1 (100+) |
| TrainHeroic | $9,99 (1 atleta) → ~$2,33/atleta (até 15) → ~$1/atleta (até 100) → ~$0,40/atleta (1000) |
| Trainerize | ~$5/mês até 5 clientes → $250+/mês ilimitado |

Com base nisso, a faixa proposta para o Palpite (escolhida pela IA a pedido do grupo, pendente de validação com a fundadora):

| Faixa | Alunos | Preço/aluno |
|---|---|---|
| Pequena | até 10 | R$6,00 (dado real) |
| Média | 11–50 | R$4,00 (hipótese) |
| Grande | 51+ | R$2,50 (hipótese) |

Fontes: [Fitness Software Pricing 2026: 30 Platforms Compared](https://trainera.fit/blogs/fitness-software-pricing-index-2026) · [Best Coaching Apps for Endurance Sports 2026](https://goodcoach.app/en/best-coaching-apps) · [Best Nutrition Coaching Software 2026](https://elitecoachinghub.com/blog/best-nutrition-coaching-software-comparison)

## E. "IA" do motor de Palpite — regra determinística vs. machine learning

O termo "IA" foi usado de forma solta pela fundadora na entrevista, sem distinguir ML de automação por regras. Decisão do grupo (delegada à IA): motor de regras/fórmulas determinístico, aplicando o Guia Alimentar Brasileiro ao perfil do usuário. Justificativa: nenhum membro da equipe descrita na entrevista (fundadora, engenheira de alimentos, administradora) tem perfil de ciência de dados/ML; nenhum orçamento ou prazo para isso foi discutido; o MVP não precisa de aprendizado, só de cálculo nutricional padronizado comparado ao consumo registrado. Reconhecimento de imagem de despensa (mencionado como ideia futura) e personalização aprendida ficam fora do MVP, no roadmap futuro, quando poderia haver ML de fato.

## F. Compliance — achados de legislação brasileira

- **CFN Resolução nº 760/2023 (telenutrição):** serviço de nutrição por TICs deve ser prestado exclusivamente por nutricionista com inscrição ativa no CRN; exige TCLE assinado antes do primeiro atendimento. Fonte: [CFN](https://cfn.org.br/cfn-publica-resolucao-que-regulamenta-a-telenutricao/).
- **LGPD (Lei 13.709/2018):** dados de saúde são sensíveis (Art. 5º, II); exigem consentimento específico; proibido compartilhar dados sensíveis de saúde entre controladores com objetivo de vantagem econômica — motivou a decisão de não ter parcerias de mídia com supermercados no MVP (ideia do "Zafarin", citada na entrevista). Fonte: [Planalto — LGPD](https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm).
- **ANVISA (RDC 657/2022, RDC 751/2022 — SaMD):** softwares de wellness não ligados a diagnóstico/tratamento/prevenção de doença são excluídos do registro como dispositivo médico. Fonte: [ANVISA/SaMD](https://telepacs.com.br/software-como-dispositivo-medico/).

**Nenhum destes achados foi confirmado com a cliente real ou com um advogado** — todos permanecem como pendências de validação (ver PRD §8, Open Questions).

## G. Concorrentes identificados (pesquisa externa)

Everfit, My PT Hub, FitBudd, Foodzilla, Nutritio, MyFitnessPal (genérico) — plataformas que já comparam ingestão recomendada vs. consumida e/ou vendem white label B2B2C para coaches. Nenhuma menciona explicitamente considerar o perfil de renda/compra do usuário, o que sustentaria o diferencial alegado pela fundadora — mas isso nunca foi confrontado com ela usando esses nomes específicos (Open Question / pendência #8 do Party Mode, descartada pelo grupo como não prioritária para os artefatos finais).
