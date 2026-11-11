# Sessão de Party Mode — Palpite

**Projeto:** Palpite
**Etapa:** T1, item 6 — Sessão de elicitação em Party Mode
**Data desta parte da sessão:** 2026-10-26
**Status:** em andamento — a continuar na próxima aula (sessão ainda não encerrada; o item 7, verificação final e pendências, ainda não foi feito)

## Ambiente utilizado

- **Ferramenta/IA:** Claude Code (sessão no diretório `Brazil-Healthcare-Capacity-Analytics-Engine`, operando sobre o repositório `bmad-Palpite`).
- **BMAD:** versão `6.13.0-next`. Módulos instalados: `bmod-core-tools` (skills `bmad`, `bmad-party-mode`) e `bmod-method` (skills `bmad-build`, `bmad-prd`).
- `$bmad-party-mode` e `$bmad-prd` foram instalados nesta sessão via `npx skills add bmad-code-org/BMAD-METHOD --skill bmad-party-mode --skill bmad-prd`, usando um Node.js 22 baixado localmente (o Node do sistema é v18, abaixo do mínimo exigido pela CLI `skills`). `uv` foi instalado via o instalador oficial (`astral.sh/uv/install.sh`), pois a instalação via `pip` falhou (ambiente Python "externally managed").
- `_bmad/` foi criado via `bmad setup` (primeira instalação, sem perguntas de configuração pendentes).
- O roster padrão resolvido pelo `bmad-party-mode` (`resolve_party.py`) só traz grupos genéricos (ex.: `code-review-crew`, `product-team`, `anti-consensus-club`), sem personas do domínio do Palpite. Por isso a sessão usa um **cast nomeado inline**, conforme a própria skill permite, com as personas definidas em [composicao_participantes.md](composicao_participantes.md).

## Participantes desta sessão

Ver composição completa e justificativa em [composicao_participantes.md](composicao_participantes.md). Nesta parte da sessão, dois participantes foram referidos com um nome mais específico ao escopo (ver decisão de escopo abaixo):

- 🧑‍💼 Fundadora (voz reconstruída a partir da entrevista real — ver [Transcript_da_entrevista.csv](Transcript_da_entrevista.csv))
- 🥗 Nutricionista parceira
- 🏢 Gestor de empresa-cliente → renomeado para **Dono de assessoria de corrida** após a decisão de escopo
- 🏃 Usuário final → **Aluno da assessoria**
- 🔬 Engenheira de alimentos
- 🛡️ Especialista em LGPD (persona de lacuna, não veio da entrevista)
- 🎙️ Facilitador (papel do método BMAD, não é stakeholder)

## Decisão de escopo registrada pelo grupo

O grupo decidiu restringir o MVP ao segmento de **assessorias de corrida**, descartando escolas públicas/Gravataí, prefeitura/PUC e empresas genéricas (RH) como fora de escopo nesta rodada.

**Ressalva registrada pelo facilitador:** essa não é uma frase única e fechada da cliente no transcript — a fala sobre escolas/Gravataí aparece no meio da entrevista, e perto do fim há uma tensão não resolvida ("o público é qualquer pessoa que queira... só que o público da assessoria não é esse público") sobre se o produto aceita público sedentário ou só atleta. A decisão do grupo trata essa ambiguidade como resolvida a favor do segmento de corrida — **isso é uma interpretação do grupo, não um fato confirmado pela cliente**, e deve ser validado com ela.

---

## Transcrição da sessão

### 1. Abertura da sala

🎙️ **Facilitador (BMAD):** Sala aberta para o Palpite. Participantes no roster desta sessão:

- 🧑‍💼 **Fundadora** (voz reconstruída a partir da entrevista real — tudo que ela disser aqui que não estiver no transcript é hipótese, não fato validado)
- 🥗 **Nutricionista parceira** — validação clínica
- 🏢 **Gestor de empresa-cliente** (assessoria/RH/prefeitura) — comprador B2B
- 🏃 **Usuário final** (aluno/beneficiário) — experiência do dia a dia
- 🔬 **Engenheira de alimentos** — qualidade da base de nutrientes
- 🛡️ **Especialista em LGPD** — persona de lacuna, não veio da entrevista

🧑‍💼 **Fundadora:** Oi, gente! Animada pra essa conversa — já expliquei bastante coisa na entrevista, mas topo detalhar.

🥗 **Nutricionista:** E eu topo discordar dela sempre que for preciso.

🎙️ **Facilitador:** Não vou formular as perguntas de elicitação por vocês. Qual é a primeira coisa que o grupo quer investigar ou questionar nessa sala?

### 2. Pergunta do grupo: "Nos informe uma visão geral do app Palpite"

🎙️ **Facilitador:** Essa visão geral é inteiramente reconstruída do que já está confirmado no transcript da entrevista real. Não estou inventando nada aqui; só estou organizando em formato de "pitch" o que ela já disse.

🧑‍💼 **Fundadora:** A ideia nasceu assim: todo guia alimentar — eu uso o Guia Alimentar Brasileiro — diz quanto de proteína, energia e fibra uma pessoa *deveria* consumir por dia, dado o perfil dela. O problema é que ninguém faz o "MET" disso com o que realmente consome. É aí que entra a IA: ela compara o que deveria com o que consome e me dá um **palpite** — não um diagnóstico, um palpite — de ajuste.

🏢 **Gestor de empresa-cliente:** E aí o modelo de vocês não é vender direto pro usuário final, né? Pelo que entendi, eu não consigo nem me cadastrar sozinho.

🧑‍💼 **Fundadora:** Exato, é B2B2C. Comecei pensando em assessorias de corrida — o treinador passa o treino, mas não sabe o que o aluno come. Depois o escopo esbarrou num programa de inovação em Gravataí, pra aplicar em crianças de escolas públicas que comem mal e têm sobrepeso por ultraprocessado. Mas sempre é White Label: vendo pra uma empresa, assessoria ou prefeitura, que tem CNPJ, e ela distribui pros usuários finais vinculados àquele CNPJ.

🥗 **Nutricionista parceira:** E eu entro porque ela não pode — nem quer — dar um palpite de alimentação sem validação profissional. Isso não é detalhe, é o motivo de eu existir no fluxo: todo "palpite" carrega aviso pra procurar uma nutricionista, e eu posso ajustar as recomendações por grupo.

🏃 **Usuário final:** E o diferencial pra mim é que o app leva em conta meu perfil de compra e renda — não me diz "coma morango" se eu tenho seis filhos e não tenho dinheiro pra isso. Isso foi dito bem direto na entrevista como o diferencial frente à concorrência.

🔬 **Engenheira de alimentos:** Tecnicamente, a base de nutrientes é validada por mim, mas o maior risco que a própria fundadora admitiu é precisão de porção — ninguém pesa comida em grama em casa, então o desafio é ter credibilidade com aproximação, não exatidão.

🛡️ **Especialista em LGPD:** Só registrando uma lacuna, não uma resposta da entrevista: isso envolve dados de saúde, renda e, se for pra escola pública, de crianças. Isso ainda não foi perguntado na entrevista, mas eu adoraria ser questionada sobre isso.

🎙️ **Facilitador:** Fora do MVP, ela já descartou explicitamente: comorbidades (diabetes), redução de desperdício via foto da despensa, e acompanhamento de treino — isso fica para versões futuras. Modelo de negócio é assinatura por pacote (ex.: faixa de alunos/funcionários), app instalável de verdade (recusou virar PWA), acesso bloqueado sem vínculo a um CNPJ.

### 3. Decisão do grupo: restringir o MVP às assessorias de corrida

> *(ver seção "Decisão de escopo registrada pelo grupo" acima para o texto completo e a ressalva do facilitador)*

Visão geral resumida, já com o escopo restrito:

🧑‍💼 **Fundadora:** Palpite compara o que o perfil da pessoa deveria consumir (proteína, energia, fibra, via guia alimentar) com o que ela realmente consome, e gera um palpite de ajuste — nunca diagnóstico.

🏢 **Dono de assessoria de corrida** *(renomeado pro escopo)*: Eu compro por pacote de alunos, é White Label — meu CNPJ, minha marca, meus alunos vinculados. Sem mim, o usuário não se cadastra.

🥗 **Nutricionista parceira:** Valido e ajusto o palpite por grupo; o app sempre recomenda procurar profissional.

🏃 **Aluno da assessoria (usuário final):** O diferencial é respeitar meu perfil de compra/renda e minha rotina de treino, não só me dizer o ideal nutricional.

🔬 **Engenheira de alimentos:** Maior risco é precisão de porção — aproximação, não gramas exatos.

🎙️ **Facilitador:** Fora do MVP continuam: comorbidades, reaproveitamento de alimentos via foto da despensa, acompanhamento de treino.

### 4. Pergunta do grupo: "Como o aplicativo deve ser implementado? App, web? Online, offline?"

🎙️ **Facilitador:** Nota de rastreabilidade — a troca sobre PWA vs. app instalável no transcript aconteceu originalmente no contexto de PUC/Moodle, que já foi tirado de escopo. Mas há outro trecho, já dentro do escopo de assessoria, que confirma o mesmo formato.

🧑‍💼 **Fundadora:** É app de verdade, instalável — recusei a ideia de ser só PWA/Moodle. E quando falei do fluxo com a assessoria, mencionei explicitamente o APK, o arquivo Android, como o que ela recebe.

🏢 **Dono de assessoria de corrida:** E aí fica em aberto uma coisa que eu perguntei e não fechamos: pôr no ar na Play Store e na Apple Store custa (ela citou algo como R$700), mas **quem paga isso**? Eu, como comprador do White Label, ou ela mantém e eu só recebo acesso? Isso ficou pendente no transcript, não foi respondido.

**Fatos confirmados:**
- Aplicativo mobile instalável (não PWA, não web app).
- Distribuição via loja (Play Store citada explicitamente; Apple Store mencionada só pelo custo).
- Acesso bloqueado até vincular a um CNPJ (a assessoria) — qualquer um baixa, ninguém usa sem vínculo.
- A fundadora quer manter controle das atualizações/integrações futuras (não é um "entregar e esquecer").

**Lacunas registradas:**
1. Android vs. iOS — só o Android foi citado concretamente (APK); prioridade nunca foi perguntada nem respondida.
2. Offline — nunca apareceu na entrevista. Pendência total (cadastro, consulta de dispensa, qualquer fluxo offline).
3. Quem paga a publicação nas lojas — pendente.

### 5. Pergunta do grupo: qual das duas opções de distribuição é a correta — (A) publicação na loja + assinatura, ou (B) envio de APK com o grupo se tornando "dono" do produto?

🎙️ **Facilitador:** Resposta por evidência, não por preferência de negócio. A opção **A** é a confirmada quase literalmente no transcript:

> "Ficaria na App Store, Play Store, para instalar qualquer pessoa, mas não conseguiria fazer nada com o aplicativo, porque não estaria vinculado a nada."

Isso descarta a opção B — em nenhum momento ela fala em entregar um APK para o grupo "virar dono do produto". Pelo contrário:

> "Então se ficar comigo eu consigo fazer essas atualizações e fazer outras integrações que tecnologia faz."

🧑‍💼 **Fundadora:** Exatamente. Eu publico na loja, a assessoria paga assinatura e vincula o CNPJ dela pra liberar o acesso dos alunos. Eu não abro mão do produto.

🏢 **Dono de assessoria de corrida:** Isso até me favorece — eu não quero ficar responsável por manter/atualizar um app, só quero pagar e usar.

🎙️ **Facilitador — pendência real:** o transcript tem uma segunda camada que não combina 100% com a opção A pura: logo depois, surge uma discussão sobre "White Label" onde se diz que "ela vai ser específica para uma empresa" e "eles vão dar a cara" (marca própria por empresa) — o que soa mais como um app rebrandado por cliente do que um único app multi-tenant com CNPJ. Essa parte fica contraditória e não foi resolvida na entrevista (termina com "Se eu estiver dentro, você vai fazer alguma manutenção?" sem resposta clara).

**Conclusão registrada:** opção A é o modelo de distribuição confirmado (loja + assinatura + vínculo por CNPJ, fundadora mantém controle). Pendência: esclarecer se "CNPJ vinculado num app único" e "White Label com marca própria por empresa" são o mesmo modelo ou dois modelos concorrentes que a cliente ainda não distinguiu.

---

## Pendências ao final da Parte 1 (sessão não encerrada)

| # | Pendência | Origem |
|---|-----------|--------|
| 1 | Ambiguidade sobre público-alvo (sedentário vs. apenas atleta da assessoria) tratada como resolvida pelo grupo — validar com a cliente real | Decisão de escopo do grupo |
| 2 | Prioridade entre Android e iOS | Lacuna — nunca perguntado |
| 3 | Suporte offline (quais fluxos, se algum) | Lacuna — nunca perguntado |
| 4 | Quem paga a publicação nas lojas (Play Store/Apple Store) | Pendente no transcript, pergunta feita mas não respondida |
| 5 | "CNPJ vinculado em app único" vs. "White Label com marca própria por empresa" — mesmo modelo ou dois modelos concorrentes? | Contradição não resolvida no transcript |

---

## Parte 2 — continuação da sessão (mesma aula, mesma data)

Reabertura com o mesmo roster. A partir daqui o grupo passou a cruzar pendências com pesquisa externa (web) e a tomar decisões explícitas, uma a uma.

### 6. Pendência #1 (público-alvo) — resolvida com evidência do transcript

🎙️ **Facilitador:** duas falas do transcript, lidas juntas, afastam a contradição:

> "Pode ser sedentário." / "Não precisa praticar." / "Mas o público alvo é pessoas que praticam esportes." / "Isso."

> "Só que tu disse que o público é qualquer pessoa que queira, pode ser a pessoa sedentária, porém o público da assessoria não é esse público." → "Não, não. Digo. Ela pode ter opção."

**Conclusão:** "sedentário" é só uma opção do campo de atividade física do cadastro (pra cálculo de gasto calórico); o público-alvo comercial pelo canal da assessoria são praticantes de esporte. Considerado esclarecido pelo transcript, não mais uma contradição — mas ainda vale confirmar a leitura com a cliente real.

### 7. Pergunta do grupo: prioridade entre Android e iOS

🎙️ **Facilitador:** **Não há base no transcript.** Só o Android foi citado concretamente (o APK); a Apple Store só aparece junto do custo de publicação (~R$700), sem indicar prioridade. Qualquer prioridade aqui seria inferência da IA, não fato — não tratado como decisão nesse momento.

### 8. Decisão do grupo: ambos os sistemas operacionais

> "Precisa ter acesso aos 2 dispositivos, porque o comprador (assessoria de corrida) quer que os seus alunos tenham acesso ao app não importando o SO de cada dispositivo."

Registrado como **decisão do grupo** (não dito pela cliente). Consequências levantadas: (a) reabre a pendência de quem paga a publicação, agora com duas lojas; (b) levanta lacuna nova — arquitetura multiplataforma (nativo duplicado vs. framework único) nunca discutida.

### 9. Convocação do agente BMAD Winston (Arquiteto)

🎙️ **Facilitador:** checagem em `.agents/skills/bmod-method/roster.toml` confirma: **Winston é um agente do método BMAD** (`bmad-agent-architect`, 🏗️ System Architect), não uma persona/stakeholder do Palpite. Skill completa não instalada; voz trazida pela persona do roster (comando de instalação, se quiserem o agente completo: `npx skills add bmad-code-org/BMAD-METHOD --skill bmad-agent-architect`).

🏗️ **Winston:** trade-offs entre nativo x2 (melhor performance, dobra custo/time, mal combina com filosofia de MVP rápido da fundadora), framework cross-platform — React Native ou Flutter (um código, mais barato, mais rápido de atualizar) e PWA (já descartada pela fundadora). Recomendação inicial (não decisão): cross-platform, dado o perfil de terceirização e o desejo dela de manter controle de atualizações.

### 10. Decisão do grupo: quem paga a publicação nas lojas

> "Quem vai pagar a publicação vai ser a fundadora e suas sócias."

Registrado como **decisão do grupo**, não confirmada pela cliente (ela nunca respondeu essa pergunta no transcript). A fundadora (voz reconstruída) levantou, em reação, que o custo dobrado (2 lojas) precisa entrar na conta do preço do pacote — nova lacuna de precificação.

### 11. Pergunta do grupo: uso offline — onde o aluno estará?

🎙️ **Facilitador:** **pendência total, zero dados no transcript.** Toda especulação das personas abaixo é hipótese explícita, não testemunho real:

- 🏃 Aluno da assessoria (hipótese): provavelmente em casa, antes/depois do treino.
- 🏢 Dono de assessoria (hipótese): talvez durante o treino, pra ver o palpite do dia.

Recomendado registrar como pergunta aberta pra devolver à cliente real, não como requisito decidido.

### 12. Pesquisa de concorrentes reais (pesquisa externa, hoje)

Via `WebSearch`, identificados concorrentes reais que já fazem o "MET" ingestão recomendada vs. consumida e/ou vendem White Label B2B2C pra coaches: **Everfit**, **My PT Hub**, **FitBudd**, **Foodzilla**, **Nutritio**, **MyFitnessPal** (genérico). Nenhum menciona explicitamente considerar o perfil de renda/compra do usuário — o que sustentaria o diferencial que a fundadora alegou na entrevista, mas isso não foi validado contra esses nomes específicos com ela.

Fontes: [Best White Label Fitness Apps 2026](https://hubfit.com/blog/best-white-label-fitness-apps) · [7 Nutrition Coaching Platforms 2026](https://blog.everfit.io/top-nutrition-coaching-platforms) · [White-Label Fitness App Platforms: 10 Compared](https://coachway.io/articles/branded-app-for-fitness-coaches/) · [Foodzilla White Label](https://foodzilla.com/pt/features/white-label-app) · [Nutritio White-Label](https://nutritioapp.com/white-label-nutrition-software/)

### 13. Hipóteses de mercado para as pendências #3 (offline) e #5 (CNPJ único vs. White Label)

**Offline (padrão MyFitnessPal):** cache local permite visualizar dados recentes; busca na base completa, novo registro e sincronização exigem internet. Proposta (hipótese, não confirmada): visualizar o último palpite funciona offline; gerar novo palpite ou editar cadastro exige internet.

**CNPJ único vs. White Label (padrão de mercado):** não são mutuamente exclusivos — muitas plataformas oferecem **dois níveis**: app com marca aplicada dentro de uma base multi-tenant compartilhada (produto básico) e white label completo com listagem própria na loja (upgrade pago, ex.: My PT Hub cobra US$145+/mês por isso). 🏗️ Winston recomendou essa estrutura de dois tiers como solução de arquitetura; a fundadora (voz reconstruída) notou que o tier premium ajudaria a cobrir o custo extra de publicação.

Fontes: [MyFitnessPal — acesso sem internet](https://support.myfitnesspal.com/hc/en-us/articles/360032622851-Can-I-access-MyFitnessPal-when-I-don-t-have-an-internet-connection) · [White-Label Fitness App Platforms: 10 Compared](https://coachway.io/articles/branded-app-for-fitness-coaches/)

### 14. Pergunta do grupo: planos mensais e monetização

**Confirmado no transcript:** assinatura por pacote, por faixa de quantidade de alunos; exemplo dado — 10 alunos por R$60 (preço de atacado); a assessoria repassa com margem (~R$10/aluno); o aluno final paga R$150–160/mês pelo pacote completo (treino + nutrição via Palpite). Venda em grupo/pacote é estratégia deliberada da fundadora pra receita recorrente: *"vender por pacote é muito mais fácil... pra ter a renda recorrente."*

**Lacunas de precisão:** valor exato do limite de alunos que define o desconto por volume; quanto do R$150–160 é especificamente repasse do Palpite vs. preço do treino que já existia antes; onde entra a remuneração da nutricionista no modelo atual (parcialmente esclarecido no item 15, abaixo).

### 15. Esclarecimento do grupo: a nutricionista é da própria assessoria

> "A assessoria tem que ter uma nutricionista para sempre validar." / "Dentro da assessoria tem a nutricionista que vai fazer a análise." / "Eu vou ter o perfil do nutricionista, que vai estar ligado à company, à companhia."

Persona renomeada: **"Nutricionista parceira" → "Nutricionista da assessoria"** — é um perfil registrado dentro da conta da assessoria (junto com gestor e alunos), não uma parceira externa do Palpite. Isso esclarece que, no escopo atual, ela é remunerada pela própria assessoria — a ideia de "nutricionista autônoma vendendo serviço direto a empresas" (mencionada pela fundadora como "versão 3") é um modelo futuro e diferente, não deve ser confundido com este perfil.

### 16. Pontos de vista da legislação brasileira (pesquisa externa, hoje)

- **CFN Resolução nº 760/2023 (telenutrição):** serviço de nutrição por TICs deve ser prestado exclusivamente por nutricionista com inscrição ativa no CRN; exige Termo de Consentimento Livre e Esclarecido (TCLE), assinado, antes do primeiro atendimento. Valida a arquitetura já desenhada pela fundadora (nutricionista sempre valida).
- **LGPD (Lei 13.709/2018):** dados de saúde são dados sensíveis (Art. 5º, II); exigem consentimento específico e destacado; **é proibido compartilhar dados sensíveis de saúde entre controladores com objetivo de vantagem econômica**, salvo portabilidade consentida. 🛡️ **Especialista em LGPD:** *"Isso me faz puxar um ponto que passou batido antes: lá na entrevista, teve uma menção a um parceiro de mercado — 'O Zafarin vai pagar para você fazer a propaganda ali dentro' — ou seja, um supermercado pagando para aparecer quando o app sugere onde comprar, com base no perfil (inclusive de saúde/consumo) do aluno. Isso é exatamente o tipo de uso comercial de dado sensível de saúde que a LGPD restringe."*
- **ANVISA (RDC 657/2022, RDC 751/2022 — Software como Dispositivo Médico):** softwares de wellness não ligados a diagnóstico/tratamento/prevenção de doença são excluídos da exigência de registro. Como o Palpite é expressamente "não diagnóstico", tende a ficar fora dessa exigência — a confirmar formalmente.

Fontes: [CFN — resolução telenutrição](https://cfn.org.br/cfn-publica-resolucao-que-regulamenta-a-telenutricao/) · [LGPD — Planalto](https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm) · [Proteção de dados na saúde](https://www.projuris.com.br/blog/protecao-de-dados-na-saude/) · [SaMD — ANVISA](https://telepacs.com.br/software-como-dispositivo-medico/)

### 17. Requisitos formalizados a partir do achado do TCLE

**RF-01 — Apresentação e aceite do TCLE antes da primeira validação nutricional**
- Descrição: o sistema deve apresentar ao aluno o conteúdo do TCLE referente à telenutrição antes de liberar o primeiro palpite validado pela nutricionista da assessoria.
- Critério de aceite: aluno não recebe palpite validado sem aceite registrado do TCLE.
- Prioridade: alta (obrigação profissional vinculada à nutricionista).
- Origem: Agente BMAD (Winston) + pesquisa jurídica externa (CFN 760/2023). **Não confirmado pela cliente real.**

**RNF-01 — Rastreabilidade e auditabilidade do aceite do TCLE**
- Descrição: aceite do TCLE registrado de forma auditável (aluno, data, hora), consultável pela nutricionista responsável.
- Critério de aceite: nutricionista visualiza, por aluno, se e quando o TCLE foi aceito.
- Prioridade: alta.
- Origem: idem RF-01. **Não confirmado pela cliente real.**

**Ressalva (Especialista em LGPD):** incerto se aceite digital com timestamp conta como "assinatura" para fins do CFN/CRN — recomenda-se confirmar com advogado ou direto com o CRN, não tratar como resolvido.

### 18. Lista consolidada de requisitos/questões ainda não bem esclarecidos (antes das decisões da seção 19)

1. Suporte offline — lacuna total (onde/quando o aluno usaria o app).
2. Modelo de distribuição por marca (CNPJ único vs. White Label completo vs. dois tiers).
3. Arquitetura multiplataforma (nativo x2 vs. framework único).
4. Sequência de lançamento Android/iOS.
5. Confirmação, com a cliente, de quem paga a publicação.
6. Valor exato do limite de alunos pro desconto por volume.
7. Quanto do valor final é repasse do Palpite vs. preço do treino.
8. Diferencial competitivo frente a concorrentes reais (Everfit, FitBudd, My PT Hub...).
9. "IA" como motor de regras determinístico vs. machine learning real, e orçamento/prazo.
10. Uso comercial de dados de saúde com parceiro de mídia (Zafarin) — risco de violar LGPD.
11. TCLE — aceite digital conta como assinatura, pra fins do CFN/CRN?
12. Registro ANVISA (SaMD) — a confirmar formalmente.
13. Reconfirmar com a cliente o escopo "só assessorias de corrida".

### 19. Decisões tomadas pelo grupo, uma a uma, a partir da lista da seção 18

**Decisão #1 (item 1 — offline):** suporte offline permitido apenas para **visualizar** o último palpite já gerado; nenhum registro/cadastro funciona offline (sincroniza só com conexão). Decisão do grupo, inspirada no padrão de mercado (seção 13); não validada com a cliente.

**Decisão #2 (item 2 — modelo de distribuição):** **app único multi-tenant.** A fundadora publica um único app, disponível para qualquer download; uma assessoria contrata o plano via **contato direto com a fundadora** (não é autosserviço); após contratar, a própria assessoria libera o acesso dentro do app para seus alunos e para sua nutricionista. Descarta o White Label com listagem própria por empresa. Consequências novas (ainda não decididas): onboarding assistido por vendas (não há fluxo de autocadastro de assessoria) e necessidade de um papel de "gestor" com poder de liberar/revogar acesso.

**Decisão #3 (item 3 — arquitetura multiplataforma):** **React Native.** Critérios usados (Winston): custo de terceirização (ela terceiriza o dev; mercado de freelancers/agências React Native é maior e mais barato no Brasil que Flutter), velocidade de atualização contínua (um código-base, alinhado ao desejo dela de manter controle), filosofia de MVP rápido. Nativo x2 descartado por não combinar com o perfil de terceirização dela.

**Decisão #4 (item 4 — sequência de lançamento):** **Android primeiro, depois Apple Store.** Critério: Android detém entre 74% e 81% do market share móvel no Brasil em 2026 (StatCounter); Apple exige Mac, conta de desenvolvedor paga e tem revisão historicamente mais lenta/rigorosa. Mantém o requisito de cobrir os dois SOs, só define a ordem de publicação.

Fontes (decisão #4): [Mobile OS Market Share Brazil — StatCounter](https://gs.statcounter.com/os-market-share/mobile/brazil) · [Android vs iOS Statistics 2026](https://www.tekrevol.com/blogs/android-vs-ios-statistics/)

**Decisão #6 (item 6 — faixas de preço por volume) — escolhida pela IA a pedido do grupo, para validar com a fundadora depois:**

Benchmarks de mercado usados como referência (Good Coach App, TrainHeroic, Trainerize — todos usam 3–4 faixas, com preço por aluno caindo bastante a cada faixa). Combinado com o único dado real da cliente (10 alunos por R$60 = R$6/aluno nessa faixa), a estrutura proposta é:

| Faixa | Alunos | Preço sugerido por aluno |
|---|---|---|
| Pequena | até 10 | R$6,00 (dado real da entrevista) |
| Média | 11–50 | R$4,00 (hipótese, extrapolada do padrão de queda do mercado) |
| Grande | 51+ | R$2,50 (hipótese, idem) |

**Status:** hipótese escolhida pela IA a pedido explícito do grupo. **Precisa de validação direta com a fundadora** — ela nunca confirmou faixas além do primeiro dado (10 alunos/R$60), e os valores das faixas média/grande são extrapolação de benchmark de mercado internacional, não de pesquisa de preço no Brasil.

Fontes: [Fitness Software Pricing 2026: 30 Platforms Compared](https://trainera.fit/blogs/fitness-software-pricing-index-2026) · [Best Coaching Apps for Endurance Sports 2026](https://goodcoach.app/en/best-coaching-apps) · [Best Nutrition Coaching Software 2026](https://elitecoachinghub.com/blog/best-nutrition-coaching-software-comparison)

---

## Pendências abertas ao final da Parte 2

| # | Pendência | Status |
|---|-----------|--------|
| 5 | Confirmar com a cliente quem paga a publicação (decisão do grupo, não validada) | Decidida pelo grupo, pendente de validação |
| 6 | Faixas de preço por volume (ver decisão #6 acima) | Hipótese da IA, pendente de validação com a fundadora |
| 7 | Quanto do valor final (R$150–160) é repasse do Palpite vs. preço do treino | Lacuna de precisão |
| 8 | Diferencial competitivo frente a concorrentes reais nomeados (Everfit, FitBudd, My PT Hub) | Achado de pesquisa, não validado |
| 9 | "IA" como regra determinística vs. ML, orçamento/prazo | Ambiguidade de termo, não esclarecida |
| 10 | Uso comercial de dados de saúde com parceiro de mídia (Zafarin) | Risco legal levantado, não resolvido |
| 11 | TCLE — aceite digital conta como assinatura para fins do CFN/CRN? | Interpretação jurídica incerta |
| 12 | Registro ANVISA (SaMD) | Achado de pesquisa, a confirmar formalmente |
| 13 | Reconfirmar com a cliente o escopo "só assessorias de corrida" | Interpretação do grupo, a reconfirmar |

### 20. Resolução em bloco das pendências #5 a #13

O grupo decidiu, de uma vez, tratar as pendências restantes como segue (todas marcadas pelo grupo como "pegue isso como verdade" — ou seja, premissas de trabalho para os artefatos, não necessariamente confirmação literal da cliente real em todos os casos):

- **#5 (quem paga a publicação):** fundadora + sócias. Fechado como premissa de trabalho; **ainda não é confirmação literal da cliente real**.
- **#6 (faixas de preço):** mantidas as faixas já propostas (até 10 alunos = R$6/aluno; 11–50 = R$4; 51+ = R$2,50).
- **#7 (repasse Palpite vs. preço do treino):** esclarecido — a tabela de faixas da #6 **é** o modelo de monetização do Palpite (o que a assessoria cobra do aluno final é precificação interna dela, fora do escopo de especificação do produto).
- **#8 (diferencial competitivo):** descartado como item a validar — o grupo decidiu que não importa para os artefatos.
- **#9 ("IA" regra vs. ML):** decisão delegada à IA pelo grupo. Decidido: **motor de regras/fórmulas determinístico**, baseado no Guia Alimentar Brasileiro — não machine learning. Justificativa: time atual sem perfil de ML, nenhum orçamento discutido, e o MVP não exige aprendizado, só cálculo nutricional padronizado comparado ao consumo registrado. ML (reconhecimento de imagem, personalização aprendida) permanece no roadmap futuro, já fora do MVP.
- **#10 (parceria com supermercados, ex. "Zafarin"):** não entra no MVP. Isso também resolve, para esta fase, o risco de LGPD levantado — é decisão de escopo, não análise jurídica completa (revisitar com advogado se a ideia for retomada no futuro).
- **#11 (TCLE — aceite digital como assinatura):** aceito como válido para os artefatos do trabalho, **com a ressalva explícita de que precisa de revisão por um advogado antes de produção real**. Ressalva mantida junto ao RNF-01.
- **#12 (ANVISA/SaMD):** confirmado — fica fora do registro por não ser diagnóstico.
- **#13 (escopo):** reconfirmado — apenas assessorias de corrida.

---

## Item 7 — Encerramento da sessão: verificação final

🎙️ **Facilitador:** Antes de encerrar, rodada final com os participantes — dúvidas, exceções não exploradas, perspectivas não consideradas, conflitos e informações ausentes.

🏢 **Dono de assessoria de corrida:** Uma exceção que não tratamos: **o que acontece se a assessoria atrasar o pagamento da assinatura?** Os alunos perdem acesso imediatamente, ou há um período de carência?

🥗 **Nutricionista da assessoria:** E se o **número de alunos ativos passar da faixa contratada** (ex.: de 10 para 12)? É upgrade automático de faixa, bloqueio de novos cadastros, ou cobrança proporcional?

🏃 **Aluno da assessoria:** E se eu **saio da assessoria no meio do mês** (trocar de academia, parar de treinar)? Meu perfil e histórico de dados continuam? A assessoria consegue revogar meu acesso unilateralmente?

🛡️ **Especialista em LGPD:** Perspectiva que não consideramos ainda: a assessoria, ao revogar o acesso de um aluno, está **excluindo os dados dele ou só bloqueando**? Isso tem implicação direta de LGPD (direito à exclusão).

🎙️ **Facilitador — conflitos:** o único conflito não resolvido que o grupo já havia identificado (modelo multi-tenant vs. White Label com marca própria) foi resolvido pela Decisão #2. Não há conflitos abertos entre personas neste momento.

🎙️ **Facilitador — pendências que permanecem sem resposta ao final da sessão:**

| # | Pendência final | Natureza |
|---|---|---|
| A | Confirmar com a cliente real quem paga a publicação (premissa de trabalho, não fato) | Validação pendente |
| B | Revisão jurídica do aceite digital como assinatura válida para o TCLE | Validação pendente |
| C | O que acontece em caso de atraso de pagamento da assessoria (suspensão imediata vs. carência) | Exceção levantada no encerramento, não explorada |
| D | O que acontece quando o número de alunos excede a faixa contratada (upgrade automático, bloqueio, ou cobrança proporcional) | Exceção levantada no encerramento, não explorada |
| E | O que acontece com os dados do aluno quando ele sai da assessoria/é desvinculado (exclusão vs. bloqueio) | Exceção levantada no encerramento, não explorada — tem implicação de LGPD |

🎙️ **Facilitador:** Com a verificação final feita e essas 5 pendências registradas (ao invés de inventadas sem base), **a sessão de Party Mode está formalmente encerrada.**

## Próximos passos

Item 8 — elaboração do PRD via `$bmad-prd`, usando como contexto tudo o que foi registrado nesta sessão (fatos confirmados, decisões do grupo, achados de pesquisa externa e as pendências A–E acima, que devem ser tratadas como hipóteses/pendências no PRD, não como fatos).
