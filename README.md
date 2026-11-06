# Demo: uma skill, dois ambientes

**Objetivo:** carregar a mesma skill `release-notes` no Copilot CLI e no
Copilot em modo agente no VS Code. A tarefa, os dados, o procedimento e o
template são os mesmos; o cliente usado para executá-los muda.

Este pacote é uma demonstração independente em português, não uma demo
original de Andrea Griffiths ou Shishir Tewari. Os dados e links são fictícios.
Não precisa de GitHub Actions, MCP, acesso a PRs, publicação ou dependências
do projeto. Os clientes ainda precisam estar instalados, autenticados e ter
acesso ao Copilot e às ferramentas de leitura.

## O que está em cada lugar

```text
demo-release-notes/
├── .github/skills/release-notes/
│   ├── SKILL.md                  procedimento e descrição para descoberta
│   ├── references/categorias.md  regras do time
│   └── assets/template.md        formato do documento
├── dados/mudancas.md             entrada fictícia: 3 mudanças + 1 de outro produto
├── PROMPT.txt                   o mesmo pedido para os dois clientes
├── esperado/pagamentos.md        exemplo de referência, escrito para a demo
├── resultados/                  saída real e evidência resumida do CLI
└── README.md
```

Abra esta pasta como raiz do workspace nos dois clientes. A pasta `.github`
é oculta em alguns gerenciadores de arquivos, mas faz parte do pacote.
Não precisa registrar ou modificar nenhum dos seus repositórios existentes.

```text
          UMA FONTE DO PROCEDIMENTO
   .github/skills/release-notes/SKILL.md
      + categorias + template
                 │
          ┌──────┴──────┐
          ↓             ↓
     Copilot CLI   Copilot no VS Code
          │             │
          └──────┬──────┘
                 ↓
   notas que seguem as mesmas regras
```

Aqui os dois clientes leem os mesmos arquivos físicos. Se quiser distribuir
a skill para outro workspace no futuro, copie a pasta `release-notes` inteira,
incluindo referências e assets. Não copie somente o `SKILL.md`.

## Preparar antes de apresentar

1. Extraia o ZIP e localize `demo-release-notes`.
2. Use versões dos clientes que suportem Agent Skills e confirme seu login.
3. Abra a pasta inteira no VS Code com **File > Open Folder**. Não abra apenas
   o arquivo de dados ou apenas a subpasta da skill.
4. No VS Code, abra o Chat em **modo agente** com Copilot. Digite `/` e procure
   `release-notes`. Em versões recentes, **Chat: Open Customizations > Skills**
   também permite inspecionar a skill e sua localização.
5. No terminal, entre na mesma pasta e execute `copilot`. Dentro do CLI, use
   `/skills list` e `/skills info release-notes`. Se adicionou a skill durante
   a sessão, execute `/skills reload`.
6. Confirme que a localização é a `.github/skills/release-notes` desta demo,
   não outra skill pessoal ou de plugin com o mesmo nome.

Não é necessário alterar configurações globais. Se a skill não aparecer,
confirme a raiz do workspace, o nome exato `SKILL.md`, a versão do cliente e
as políticas da organização. Não substitua essa descoberta por um prompt
colando o procedimento: isso demonstraria reutilização de prompt, não de skill.

## O mesmo prompt nos dois ambientes

```text
Use a skill /release-notes para gerar as notas da versão 2.4.0 de pagamentos a partir de dados/mudancas.md.
```

Copie o texto de `PROMPT.txt` em duas conversas novas, uma em cada cliente.
Permita a leitura dos arquivos da demo quando o cliente solicitar.

O pedido não contém as categorias, os passos ou o template. Essas
informações precisam vir dos arquivos da skill.

Observe a atividade de ferramentas: a skill deve ser carregada e os arquivos
`references/categorias.md`, `assets/template.md` e `dados/mudancas.md` devem
ser consultados. Uma resposta que apenas diga "usei a skill" não prova isso.
Dependendo do cliente, parte do carregamento pode aparecer como contexto
anexado, em vez de uma chamada explícita de leitura.

O exemplo `esperado/pagamentos.md` é uma referência humana, não uma saída
medida de um agente. Não o anexe ao prompt nem o abra no contexto do chat
durante a demonstração.

O mesmo vale para `resultados/`: os arquivos são evidências de uma execução
anterior, não entradas para o agente. Não os anexe ao novo pedido.

## Estado da demonstração preparada

- **Copilot CLI:** o prompt de `PROMPT.txt` foi executado. Foi observada a
  ativação de `release-notes` e a leitura dos dados, das categorias e do
  template. A saída real está em `resultados/copilot-cli.md`.
- **Evidência resumida:** `resultados/evidencia-cli.json` registra somente o
  pedido da demo, os caminhos relativos consultados e os hashes dos arquivos
  da skill. Não contém logs completos, configurações pessoais ou credenciais.
- **VS Code:** o pacote usa a localização de skills documentada para esse
  cliente, mas a execução no Chat do VS Code ainda precisa ser ensaiada.
  Não foi medida ou confirmada uma segunda execução nesse ambiente.

O resultado do CLI foi conferido para categorias, fontes, filtragem por produto,
data, indicação de dados fictícios, migração e ausência de campos não preenchidos.

## Conferir os dois resultados

Os textos podem variar. Compare as regras, não a identidade palavra por palavra:

| Critério | Resultado esperado |
|---|---|
| Produto e versão | pagamentos 2.4.0 |
| Data | 2026-11-06 |
| Novidades | PAY-101: exportação em CSV |
| Correções | PAY-102: exportação inclui páginas seguintes |
| Mudanças incompatíveis | PAY-103: `name` para `full_name`, com ação de migração |
| Fontes | 3 links, cada um com o identificador correto |
| Filtragem | CAT-201 não aparece: pertence ao catálogo |
| Contexto | O documento indica que os dados são fictícios |
| Lacunas | "Informações pendentes" contém "Nenhuma." |
| Evidência de uso | Carregamento da skill e consulta aos recursos |

Não trate um documento plausível, por si só, como prova de ativação da skill.

## Fala e sequência: aproximadamente 3 minutos

**0:00–0:40 — Mostrar a fonte**

> "O procedimento está escrito uma vez neste SKILL.md. As categorias estão
> nesta referência e o formato está neste template. Não vou colar essas regras
> em cada conversa."

Abra os três arquivos e a entrada. Mostre que há uma mudança de catálogo
misturada às de pagamentos.

**0:40–1:35 — Executar no CLI**

> "Agora peço as notas de pagamentos. O prompt identifica a tarefa, a versão
> e a entrada. O modo de trabalhar vem da skill."

Mostre a skill disponível, envie o prompt e observe seu carregamento.

**1:35–2:30 — Executar no VS Code**

> "Mudei o cliente, não a skill. Vou usar os mesmos arquivos e o mesmo pedido."

Em uma conversa nova no modo agente, envie o mesmo prompt e mostre a consulta
aos recursos.

**2:30–3:00 — Comparar**

> "Os dois seguiram as mesmas categorias, preservaram as fontes e excluíram
> a mudança de catálogo. Isso é reutilizar o procedimento. Não significa que
> todas as frases serão idênticas ou que qualquer agente seja compatível."

O tempo é uma meta de ensaio, não uma duração medida. O carregamento e as
respostas dependem do cliente e da rede. Prepare uma gravação antes do evento;
se usar saídas previamente gravadas, identifique-as como tal.

## Seleção automática: uma verificação separada

Para esta demo, o nome da skill é explícito para tornar a execução previsível.
Em outra conversa nova, você pode experimentar:

```text
Gere as notas da versão 2.4.0 de pagamentos a partir de dados/mudancas.md.
```

Verifique se o cliente seleciona a skill. A descoberta não garante ativação
automática em todos os pedidos. Não confunda esse teste de seleção com o teste
de executar o mesmo pacote em dois clientes.

## Limite da conclusão

Esta demonstração usa **dois clientes Copilot compatíveis**. Ela não prova
compatibilidade com todos os agentes, outros fornecedores ou todos os modelos.
Não há um agente implementado dentro desta skill; os agentes são fornecidos
pelos próprios clientes.

## Documentação

- Copilot CLI: https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/add-skills
- VS Code: https://code.visualstudio.com/docs/agent-customization/agent-skills
- Padrão Agent Skills: https://agentskills.io
