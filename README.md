<!-- README.md -->

# check-permissions

GitHub Action para coletar as configurações de merge e a proteção de um branch em um repositório GitHub, gerando uma **checklist formatada** pronta para ser usada em comentários de Pull Request.

A Action consulta:

- Configurações de merge do repositório:
  - rebase, squash, merge commit, auto-merge, delete branch on merge
- Proteção do branch base:
  - histórico linear
  - status checks obrigatórios (e se exigem branch atualizado)
  - quantidade de reviews obrigatórios
  - aplicação das regras para admins
  - restrições de push (users/teams/apps)

O resultado é devolvido em um único campo de saída (`message_checklist`), no formato Markdown.

## Inputs

| Nome          | Obrigatório | Descrição                                                          |
|---------------|------------:|--------------------------------------------------------------------|
| `token`       | sim         | Token GitHub (geralmente `${{ secrets.GITHUB_TOKEN }}`)           |
| `base_branch` | sim         | Nome do branch base a ser verificado (ex.: `main`, `staging`)     |

## Outputs

| Nome               | Descrição                                                                 |
|--------------------|---------------------------------------------------------------------------|
| `message_checklist`| Texto em Markdown com a checklist de merge e proteção do branch base.    |

## Exemplo de uso

```yaml
name: "Exemplo de uso do check-permissions"

on:
  pull_request:
    types: [opened, synchronize, reopened]

jobs:
  permissions-check:
    runs-on: ubuntu-latest

    steps:
      - name: Coletar checklist de proteção do branch
        id: repo-settings
        uses: Malnati/check-permissions@v1
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          base_branch: ${{ github.event.pull_request.base.ref }}

      - name: Comentar checklist na PR
        uses: Malnati/pr-comment@v1
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          pr_number: ${{ github.event.pull_request.number }}
          header_actor: ${{ github.actor }}
          header_title: "📋 Checklist de proteção de branch"
          header_subject: "Regras aplicadas ao branch base ${{ github.event.pull_request.base.ref }}"
          body_message: ${{ steps.repo-settings.outputs.message_checklist }}
          body_scope: ""
          body_todo: ""
          footer_result: "Checklist gerada automaticamente pelo workflow."
          footer_advise: "Revise as regras antes de ajustar a estratégia de merge."
