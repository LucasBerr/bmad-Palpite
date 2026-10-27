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

## Pendências acumuladas até o momento (sessão não encerrada)

| # | Pendência | Origem |
|---|-----------|--------|
| 1 | Ambiguidade sobre público-alvo (sedentário vs. apenas atleta da assessoria) tratada como resolvida pelo grupo — validar com a cliente real | Decisão de escopo do grupo |
| 2 | Prioridade entre Android e iOS | Lacuna — nunca perguntado |
| 3 | Suporte offline (quais fluxos, se algum) | Lacuna — nunca perguntado |
| 4 | Quem paga a publicação nas lojas (Play Store/Apple Store) | Pendente no transcript, pergunta feita mas não respondida |
| 5 | "CNPJ vinculado em app único" vs. "White Label com marca própria por empresa" — mesmo modelo ou dois modelos concorrentes? | Contradição não resolvida no transcript |

## Próximos passos

Continuar a sessão de Party Mode na próxima aula a partir dessas pendências, seguindo para o item 7 (verificação final de encerramento) quando o grupo considerar suficiente, e então o item 8 (elaboração do PRD via `$bmad-prd`).
