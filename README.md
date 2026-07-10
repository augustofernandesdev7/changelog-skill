# changelog-skill

Skill pessoal do Claude Code para gerar o HTML de changelog/apresentação de projeto — o formato padrão usado para mostrar progresso técnico a públicos não-técnicos (chefe, sócio, cliente), com simulações interativas reais de cada tela nova.

## Instalar

Copie a pasta `assets/` e o `SKILL.md` para dentro de `~/.claude/skills/project-changelog/` (Windows: `C:\Users\<usuario>\.claude\skills\project-changelog\`):

```
git clone https://github.com/augustofernandesdev7/changelog-skill.git
cp -r changelog-skill/* ~/.claude/skills/project-changelog/
```

Depois disso, basta pedir ao Claude Code um "changelog" ou "html de apresentação do projeto" em qualquer projeto que a skill será usada automaticamente.

## Conteúdo

- `SKILL.md` — instruções da skill (estrutura obrigatória, como adaptar cores/branding, onde publicar).
- `assets/template.html` — template completo de referência (design tokens, tema claro/escuro, componentes reutilizáveis e simulações em JS puro), extraído do primeiro changelog criado (projeto BarberIA, 10/07/2026).
