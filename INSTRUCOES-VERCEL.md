# Michelle Oficial — implantação na Vercel

## Configuração
1. Importe o repositório do GitHub e mantenha o framework Vite.
2. Em **Settings → Environment Variables**, configure:
   - `ATENASPAY_API_KEY`: chave da API obtida em Atenas Pay → Integrações → API Keys.
   - `ATENASPAY_WEBHOOK_SECRET`: segredo HMAC, somente se estiver configurado no painel Atenas Pay.
   - `APP_BASE_URL`: URL HTTPS final do projeto na Vercel.
3. Não coloque credenciais no frontend, no GitHub ou em variáveis `VITE_*`.
4. Cadastre o webhook `https://SEU-DOMINIO/api/webhooks/atenaspay` no painel, caso vá usar webhook.
5. Faça uma cobrança de teste de baixo valor. Confirme a geração do QR/copia-e-cola e que o acesso só libera quando a consulta retornar status pago.

## Endpoints usados
- Criar Pix: `POST https://nexuspag.com/api/pix/create` com `x-api-key`.
- Consultar Pix: `GET https://nexuspag.com/api/pix/{id}` com `x-api-key`.
- Endpoint de webhook do projeto: `/api/webhooks/atenaspay`.

O checkout não solicita nome, e-mail, CPF ou telefone, porque esses campos não são exigidos no endpoint documentado de criação de Pix da Atenas Pay. Não considere a integração validada até testar com a chave real da sua conta.
