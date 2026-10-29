# Skills do Gabriel Sartori

As skills e os kits que aparecem em [gsartori.com](https://gsartori.com), prontos para instalar. Este repositório é
gerado automaticamente pelo catálogo do site: não edite à mão, as mudanças são substituídas na próxima publicação.

## Três jeitos de instalar

**1. Uma skill só, em qualquer agente** (Claude Code, Codex, Cursor e outros):

```bash
npx skills add gssartori/skills --skill gsart-gerar-srt
```

**2. Pelo Claude Code, como plugin:**

```text
/plugin marketplace add gssartori/skills
/plugin install gsart-avulsas@gsartori
```

`gsart-avulsas` traz as skills soltas; cada kit é um plugin próprio (`gsart-<kit>@gsartori`).

**3. À mão:** copie a pasta da skill (`plugins/<plugin>/skills/<skill>`) para `~/.claude/skills/`.

Cada página do site mostra o comando certo para aquela skill ou kit.
