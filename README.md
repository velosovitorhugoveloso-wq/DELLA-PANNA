# DelaPlana

Aplicação web simples em Flask, preparada para desenvolvimento local e deploy no Render.

## Estrutura

```text
DelaPlana/
├── app.py
├── gunicorn.conf.py
├── requirements.txt
├── .python-version
├── .gitignore
├── templates/
│   └── index.html
└── static/
    └── style.css
```

O `requirements.txt` fica na raiz, no mesmo nível do `app.py`. A configuração do Gunicorn lê a variável `PORT` do Render e escuta em `0.0.0.0`.

## Rodar localmente

Requer Python 3.12.

```bash
python -m venv .venv
```

Ative o ambiente virtual:

```bash
# Windows PowerShell
.venv\Scripts\Activate.ps1

# macOS ou Linux
source .venv/bin/activate
```

Instale as dependências e inicie o servidor de desenvolvimento:

```bash
pip install -r requirements.txt
python app.py
```

Abra `http://127.0.0.1:5000`. A rota `http://127.0.0.1:5000/health` retorna `ok`. Se definir `PORT`, o servidor local usa essa porta.

## Deploy no Render

1. Envie esta pasta para um repositório Git e crie um **Web Service** no Render conectado a esse repositório.
2. Configure **Root Directory** como `DelaPlana` se o serviço estiver usando o repositório-pai.
3. Selecione **Python 3** como runtime.
4. Configure os comandos:

   - **Build Command:** `pip install -r requirements.txt`
   - **Start Command:** `gunicorn app:app`

5. Faça o deploy. O Gunicorn lê `PORT` automaticamente de `gunicorn.conf.py`.

O Render pode usar a versão de Python indicada em `.python-version` (3.12).
