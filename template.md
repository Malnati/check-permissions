<!-- template.md -->
📋 Lista de checagem de merge e proteção de branch:

**Configuração de merge do repositório:**
- Rebase merge habilitado: $ALLOW_REBASE_EMOJI
- Squash merge habilitado: $ALLOW_SQUASH_EMOJI
- Merge commit habilitado: $ALLOW_MERGE_COMMIT_EMOJI
- Auto-merge habilitado: $ALLOW_AUTO_MERGE_EMOJI
- Deletar branch no merge: $DELETE_BRANCH_ON_MERGE_EMOJI
- Branch padrão do repositório: `$DEFAULT_BRANCH`

$PROTECTION_NOTE

**Proteção do branch base \`$BASE_BRANCH\`:**
- Histórico linear obrigatório: $LINEAR_HISTORY_EMOJI
- Status checks obrigatórios: $REQUIRED_STATUS_EMOJI
$STRICT_LINE
- Reviews obrigatórios: $REQUIRED_APPROVING aprovação(ões)
- Regras válidas também para admins: $ENFORCE_ADMINS_EMOJI
- Restrição de quem pode pushar: $RESTRICTIONS_EMOJI
