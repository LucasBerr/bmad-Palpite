# Composição dos participantes da sessão de elicitação (Party Mode)

**Projeto:** Palpite
**Etapa:** T1, item 5 — Definição dos participantes da elicitação
**Ambiente usado nesta etapa:** Claude Code atuando como facilitador do método BMAD, com apoio do skill `$bmad` instalado localmente em `.agents/skills/`. As skills `$bmad-party-mode` e `$bmad-prd` ainda estavam em processo de instalação no momento desta proposta (ver observação no final).

## Orientação usada para gerar a proposta

> Analise o caso apresentado e proponha os agentes e/ou personas que deveriam participar de uma sessão de elicitação de requisitos. Para cada participante, indique seu papel, interesses relacionados ao sistema e contribuição esperada. Não inicie a elicitação antes que o grupo analise a proposta.

A proposta foi construída a partir de:
- [Transcript_da_entrevista.csv](Transcript_da_entrevista.csv) — entrevista real com a stakeholder/fundadora do Palpite;
- [guia_bmad_requisitos.md](guia_bmad_requisitos.md) e [perguntas_iniciais.md](perguntas_iniciais.md) — contexto e roteiro preparados antes da entrevista.

## Distinção: agente BMAD vs. persona

- **Agente BMAD** (papel do método, não é stakeholder do Palpite): o facilitador/analista da sessão — organiza a discussão, registra o que é fato confirmado vs. hipótese, e conduz a elaboração do PRD depois do Party Mode.
- **Personas**: stakeholders simulados do domínio do Palpite, descritos abaixo.

## Composição inicialmente sugerida

| # | Persona | Papel | Interesses relacionados ao sistema | Contribuição esperada |
|---|---------|-------|--------------------------------------|------------------------|
| 1 | Fundadora/idealizadora do Palpite (reconstrução a partir da entrevista) | Dona do produto e da visão de negócio | Viabilidade comercial (B2B/White Label), diferencial competitivo (considerar o perfil de compra/renda do usuário, não só o que "deveria" comer), manter o MVP simples | Confirmar ou contestar interpretações do grupo sobre a fala dela na entrevista real |
| 2 | Nutricionista parceira/validadora | Responsável legal/técnica pela validação clínica do "palpite" | Não ser substituída pelo app, poder personalizar/ajustar recomendações, deixar claro que o app não diagnostica | Regras de negócio sobre o que o app pode/não pode afirmar, fluxo de validação, limites éticos (ex.: comorbidades como diabetes ficaram fora do MVP) |
| 3 | Gestor de empresa-cliente (ex.: dono de assessoria de corrida, RH de empresa, ou nutricionista de prefeitura/PUC) | Comprador B2B/B2B2C, não é o usuário final | Relatório agregado por grupo, custo por pacote de assinatura, processo de onboarding (CNPJ, convite por CPF) | Requisitos de gestão multiusuário, modelo de cobrança, exceções de cadastro (pessoa física sem empresa vinculada) |
| 4 | Usuário final (aluno/funcionário/beneficiário) | Quem recebe o "palpite", mas não paga diretamente | Sugestões que respeitem renda e rotina de compra real, privacidade dos próprios dados de saúde | Casos de uso do dia a dia (cadastro, consulta de dispensa, lembrete de compra), tensão entre "o que deveria comer" vs. "o que posso comprar" |
| 5 | Engenheira de alimentos / curadora da base de nutrientes | Responsável técnica pela confiabilidade dos dados nutricionais | Precisão vs. aproximação (maior risco técnico citado na entrevista), processo de atualização da base | Requisitos não funcionais de qualidade/confiabilidade de dados, limites de precisão a comunicar ao usuário |
| 6 | Especialista em privacidade/LGPD (persona de apoio, não citada na entrevista) | Representa uma lacuna que a entrevista não cobriu | Dados sensíveis (saúde, renda, geolocalização, hábitos alimentares — inclusive de crianças em escolas públicas) | Forçar perguntas sobre retenção, consentimento, compartilhamento com empresa/nutricionista |

## Alterações realizadas pelo grupo

Nenhuma. O grupo avaliou a proposta e decidiu manter a composição integralmente, sem remover, trocar ou adicionar participantes nesta rodada.

## Composição final utilizada

As 6 personas listadas acima, sem alterações.

## Justificativa da decisão do grupo

- As personas 1 a 5 cobrem os ângulos de negócio, validação clínica, comprador B2B e usuário final que apareceram explicitamente na entrevista, então têm aderência direta ao caso.
- A persona 6 (LGPD) foi mantida mesmo não tendo origem na entrevista, porque o domínio envolve dados de saúde, renda e, potencialmente, menores de idade (programa de escolas públicas de Gravataí) — uma lacuna real que vale a pena explorar no Party Mode, mesmo sendo uma sugestão da IA e não uma necessidade validada pela cliente.
- O grupo optou por não remover nenhuma persona nem adicionar novas nesta etapa (ex.: investidor, parceiro de mercado como o "Zafarin" citado na entrevista) para manter a primeira rodada de Party Mode focada.

## Observação sobre o ambiente BMAD

No momento desta proposta, apenas as skills `$bmad` (ajuda/setup) e `$bmad-build` estavam instaladas em `.agents/skills/`. A instalação de `$bmad-party-mode` e `$bmad-prd` via `npx skills add bmad-code-org/BMAD-METHOD --skill bmad-party-mode --skill bmad-prd` falhou porque o Node.js local (v18.19.1) é mais antigo que o exigido (≥22) pela CLI `skills`, e a instalação do `uv` (dependência do BMAD) via `pip` falhou por o ambiente Python ser "externally managed". Essas pendências de ambiente estão sendo resolvidas separadamente e serão registradas como evidência (item 10.1 do trabalho).
