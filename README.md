# 🌈 Aprendendo Juntos

Site estático com dois módulos de estudo de alfabetização, unificados em um único arquivo HTML.

## Módulos

| Módulo | Descrição | localStorage key |
|--------|-----------|-----------------|
| **🔤 Sílabas** | Cartões com sílabas isoladas — marque acertos e erros por sílaba | `cartoes_v1` |
| **📚 Palavras** | 26 cartões com palavras misturadas — expanda para ver ilustração e marque como concluído | `silabas_cards_mistos_v1` |

O progresso de cada módulo é salvo automaticamente no `localStorage` do navegador. A aba ativa também é lembrada entre sessões.

---

## Rodar localmente

Basta abrir o arquivo diretamente no navegador — não precisa de servidor, build ou dependências:

```bash
# Opção 1: duplo clique no arquivo
open index.html

# Opção 2: servidor local simples com Python (evita problemas de CORS em alguns navegadores)
python3 -m http.server 8080
# Acesse: http://localhost:8080

# Opção 3: com Node.js (npx)
npx serve .
# Acesse: http://localhost:3000
```

---

## Deploy — GitHub Pages ✅ (escolha recomendada)

### Por que GitHub Pages?

- **Gratuito** para repositórios públicos
- **Zero configuração** — funciona com HTML puro, sem build pipeline
- **Sem servidor** necessário
- Deploy automático a cada `git push`
- URL limpa: `https://<seu-usuario>.github.io/<nome-do-repo>/`

### Passo a passo

**1. Crie um repositório no GitHub**

Acesse [github.com/new](https://github.com/new) e crie um repositório público (ex: `aprendendo-juntos`).

**2. Suba o arquivo**

```bash
# Se ainda não tem git configurado localmente:
git init
git add index.html README.md
git commit -m "feat: projeto inicial consolidado"

# Adicione o remote e suba
git remote add origin https://github.com/<seu-usuario>/aprendendo-juntos.git
git branch -M main
git push -u origin main
```

**3. Ative o GitHub Pages**

- Vá em **Settings** → **Pages** (menu lateral esquerdo)
- Em *Source*, selecione **Deploy from a branch**
- Branch: `main` | Pasta: `/ (root)`
- Clique em **Save**

**4. Aguarde ~1 minuto e acesse**

```
https://<seu-usuario>.github.io/aprendendo-juntos/
```

> A URL fica disponível logo acima do botão Save após a primeira build.

---

## Alternativa: Vercel

O Vercel também funciona bem, mas adiciona uma etapa de conta/projeto extra sem vantagem real para HTML puro.

```bash
npx vercel deploy --prod
```

Para este projeto (arquivo único estático), **GitHub Pages é suficiente e mais simples**.

---

## Estrutura do projeto

```
aprendendo-juntos/
├── index.html   ← entrypoint único com tudo dentro
└── README.md
```

### Decisões técnicas

- **CSS namespacing**: todos os estilos do App 1 estão sob `.app-silabas`, e do App 2 sob `.app-palavras`, evitando conflitos.
- **JS isolado**: cada módulo está envolto em uma IIFE `(() => { ... })()` para evitar vazamento de variáveis globais.
- **Navegação por tabs**: troca visibilidade com `display: block/none` + `localStorage` para persistir a aba ativa.
- **localStorage separado**: cada módulo usa sua própria chave (`cartoes_v1` e `silabas_cards_mistos_v1`), sem risco de colisão.
