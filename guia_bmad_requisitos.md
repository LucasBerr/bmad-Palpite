# Guia rápido: BMAD para levantamento de requisitos

**Projeto:** Palpite  
**Objetivo:** usar o BMAD como apoio à elicitação, mantendo o grupo responsável por conduzir perguntas, avaliar respostas e registrar pendências.

> No Codex, as instruções abaixo são chamadas no chat por meio de skills, como `$bmad` e `$bmad-party-mode`. Não são comandos para digitar diretamente no PowerShell.

## 1. Situação atual deste projeto

As skills locais estão em `.agents/skills/` e valem somente para este repositório.

Atualmente estão instaladas:

- `$bmad`: ajuda, configuração, status e orientação do método;
- `$bmad-build`: implementação de código; **não é necessário para a elicitação inicial**;
- os metadados `bmod-core-tools` e `bmod-method`.

Para realizar o T1, ainda serão necessários os workflows abaixo:

- `$bmad-party-mode`: discussão entre agentes e personas;
- `$bmad-prd`: criação, atualização e validação do PRD.

Instalem-nos localmente, na raiz deste projeto:

```powershell
npx skills add bmad-code-org/BMAD-METHOD --skill bmad-party-mode --skill bmad-prd
```

O BMAD também exige o utilitário `uv` para executar seus scripts e concluir a configuração. Neste computador, o `uv` ainda não está disponível. Antes da aula, peça ao agente: **“instale e configure o uv para mim”**. Depois, execute `$bmad setup` no chat.

## 2. Comandos/skills principais

| Skill ou comando no chat | Quando usar | Exemplo de pedido |
| --- | --- | --- |
| `$bmad setup` | Após instalar ou atualizar skills; cria ou repara a configuração local `_bmad/`. | `$bmad setup` |
| `$bmad status` | Para verificar se o BMAD está instalado, atualizado e se falta alguma configuração. | `$bmad status` |
| `$bmad` | Para ajuda, descobrir workflows, verificar ou criar a iniciativa ativa e decidir o próximo passo. | `$bmad: quais skills e agentes estão disponíveis para o T1?` |
| `$bmad-party-mode` | Para conduzir a sessão de elicitação com agentes e personas. | `$bmad-party-mode: inicie uma sessão de elicitação do Palpite com os participantes definidos pelo grupo.` |
| `$bmad-prd` | Após a elicitação, para criar um PRD a partir das evidências coletadas. | `$bmad-prd: crie um PRD usando as notas da entrevista e da sessão de Party Mode anexadas.` |
| `$bmad-advanced-elicitation` *(opcional)* | Para revisar criticamente um resultado recente e buscar lacunas, conflitos ou suposições. | `$bmad-advanced-elicitation: faça perguntas socráticas sobre as lacunas deste resumo.` |

Na versão instalada, `bmad-help` foi renomeado para **`bmad`**. Portanto, para ajuda, use `$bmad` e descreva a dúvida.

## 3. Fluxo recomendado para o T1

### Antes da aula

1. Confiram a instalação:

   ```text
   $bmad status
   ```

2. Se necessário, preparem o ambiente:

   ```text
   $bmad setup
   ```

3. Verifiquem os recursos disponíveis:

   ```text
   $bmad: liste os agentes, personas e workflows disponíveis nesta instalação e explique como iniciar o Party Mode e o PRD.
   ```

4. Mantenham abertos durante a entrevista:

   - [perguntas_iniciais.md](perguntas_iniciais.md);
   - o Termo de Abertura do Projeto;
   - um documento para registrar respostas, exemplos, dúvidas e pendências.

### Após a entrevista com a stakeholder

1. Organizem as anotações, sem misturar fatos confirmados com interpretações do grupo.
2. Perguntem ao BMAD quais participantes seriam úteis **antes** de abrir o Party Mode:

   ```text
   $bmad: analise o caso do Palpite e proponha agentes e/ou personas para uma sessão de elicitação de requisitos. Para cada participante, informe papel, interesses relacionados ao sistema e contribuição esperada. Não inicie a elicitação antes de o grupo analisar a proposta.
   ```

3. Avaliem criticamente a proposta. Registrem a composição sugerida, alterações, composição final e justificativa.

### Durante o Party Mode

Iniciem a sessão apenas depois de definir os participantes:

```text
$bmad-party-mode: conduza uma sessão de elicitação para o projeto Palpite. Participarão [listar agentes e personas aprovados]. O grupo de alunos conduzirá a discussão. Use como fatos confirmados somente as notas abaixo; identifique claramente hipóteses, conflitos e questões pendentes.

[colar as notas da entrevista]
```

Durante a conversa, o grupo deve fazer perguntas próprias. Exemplos:

```text
Essa necessidade foi confirmada pela stakeholder ou é uma suposição? Registre a origem da informação.
```

```text
Quais exceções podem ocorrer para esse fluxo? Dê exemplos de situações reais.
```

```text
Há conflito entre a necessidade do usuário e a restrição apresentada? Quais alternativas existem?
```

```text
Quais requisitos não funcionais, regras de negócio ou dados sensíveis ainda não foram explorados?
```

```text
Antes de encerrar, liste dúvidas, conflitos, exceções, informações ausentes e suposições que ainda precisam de validação com a stakeholder.
```

Não use apenas um pedido como “gerem os requisitos desse sistema”. O valor da atividade está nas perguntas, contrapontos e decisões tomadas pelo grupo.

### Após o Party Mode

1. Salvem ou exportem o histórico da sessão e registrem as intervenções feitas pelos alunos.
2. Separem as informações em quatro grupos:

   - confirmadas pela stakeholder;
   - levantadas por agentes ou personas;
   - interpretações/decisões do grupo;
   - hipóteses ou pendências a validar.

3. Criem o PRD somente com esse contexto explícito:

   ```text
   $bmad-prd: crie um PRD para o Palpite com base nas evidências abaixo. Identifique como [ASSUMPTION] qualquer informação não confirmada pela stakeholder. Não trate sugestões do Party Mode como fatos validados.

   [colar entrevista, decisões do grupo, resumo do Party Mode e pendências]
   ```

4. Revisem o PRD. Para cada informação adicionada pelo BMAD que não veio da stakeholder, decidam se ela será:

   - mantida como hipótese ou premissa para validação;
   - modificada, com justificativa;
   - descartada, com justificativa.

## 4. Evidências que devem ser preservadas

Guardem no repositório ou em uma pasta compartilhada:

- identificação da ferramenta/IA e versão do BMAD, quando disponível;
- resultado de `$bmad status`;
- composição inicial e final de agentes/personas, com justificativas;
- histórico ou exportação do Party Mode;
- registro das perguntas e intervenções feitas pelo grupo;
- registro da verificação final e das pendências;
- PRD gerado pelo `$bmad-prd`;
- análise crítica do grupo sobre o PRD.

## 5. Regra essencial

O BMAD é apoio à investigação. Ele pode sugerir participantes, perguntas, riscos e requisitos, mas não valida informações em nome da stakeholder. Sempre identifiquem a origem de cada informação e tratem aquilo que não foi confirmado como hipótese, premissa ou pendência.
