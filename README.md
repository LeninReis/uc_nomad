# UC NOMAD — Gerador de Contratos (Vercel)

## Deploy em 3 passos

### 1. Instale a Vercel CLI (uma vez só)
```bash
npm install -g vercel
```

### 2. Faça login
```bash
vercel login
```

### 3. Deploy
```bash
cd uc-nomad-vercel
vercel --prod
```

Pronto. A URL de produção aparece no terminal.

---

## Estrutura

```
uc-nomad-vercel/
├── public/
│   └── index.html        # Frontend completo (formulário + preview)
├── api/
│   └── gerar-pdf.js      # Serverless function — gera PDF com Puppeteer
├── package.json          # Dependências Node.js
├── vercel.json           # Configuração do Vercel
└── README.md
```

## Como funciona

- `public/index.html` é servido estático pelo Vercel
- Ao clicar em **Baixar PDF**, o frontend faz POST para `/gerar-pdf`
- A serverless function `api/gerar-pdf.js` usa **Puppeteer + Chromium** para gerar o PDF
- O PDF é retornado como binário e o navegador faz o download automático

## Dependências

| Pacote | Uso |
|--------|-----|
| `puppeteer-core` | Controla o Chromium headless |
| `@sparticuz/chromium` | Chromium compilado para ambiente serverless (Vercel/Lambda) |

## Ajustes

### Dados da CONTRATADA
Em `public/index.html`, buscar por:
```
Chrysthian Jhun Ueki Coelho
CNPJ: 61.704.097/0001-08
```

### Adicionar serviços / cláusulas
Em `public/index.html`, função `contractHTML()`.

### Mudar memória/timeout da função
Em `vercel.json`:
```json
"functions": {
  "api/gerar-pdf.js": {
    "memory": 1024,
    "maxDuration": 30
  }
}
```
