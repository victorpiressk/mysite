# 📝 Django Blog

![Python](https://img.shields.io/badge/python-3.14-3776AB)
![Django](https://img.shields.io/badge/django-5.2.8-092E20)
![pytest](https://img.shields.io/badge/pytest-9.0.1-0A9EDC)
![SQLite](https://img.shields.io/badge/sqlite-local-003B57)

Blog simples desenvolvido com Django como exercício prático de backend em Python. O projeto permite que posts sejam criados e gerenciados via painel administrativo, enquanto a página inicial apresenta esses conteúdos de forma pública, acessível a qualquer visitante sem necessidade de login.

---

## 🚀 Tecnologias

- **Python 3.14**
- **Django 5.2.8** — framework web com painel admin integrado
- **SQLite** — banco de dados local, gerado automaticamente ao rodar as migrações
- **pytest 9.0.1** + **pytest-django 4.11.1** — testes automatizados
- **factory_boy 3.3.3** + **Faker 38.0.0** — geração de dados fictícios nos testes

---

## 📋 Sobre o Projeto

Este projeto foi desenvolvido como exercício introdutório de Django em um curso de Python Backend. O objetivo era demonstrar na prática o funcionamento do ORM, das views baseadas em classes, do sistema de URLs e do painel administrativo do Django.

A aplicação permite que administradores criem e publiquem posts pelo painel `/admin/`, enquanto qualquer visitante pode ler os posts publicados na página inicial sem precisar de login.

### 🌐 Sobre os templates em inglês

Os templates HTML foram fornecidos pelo tutor do curso como material de apoio, pois o foco do exercício era o backend — models, views, URLs e admin — e não o desenvolvimento frontend. Por isso, os textos da interface estão em inglês e o visual é básico, sem customizações.

---

## 📂 Estrutura do Projeto

```
py-modulo-06-exercicio/
└── mysite/                         # Raiz do projeto
    ├── blog/                       # App principal — models, views, admin, urls
    │   ├── migrations/             # Migrações do banco de dados
    │   ├── models/                 # Model Post
    │   ├── views/                  # Views baseadas em classe (ListView, DetailView)
    │   ├── admin.py                # Configuração do painel admin para Post
    │   ├── apps.py
    │   ├── factories.py            # Factories para geração de dados nos testes
    │   └── urls.py                 # Rotas do blog
    ├── config/                     # Configurações do projeto Django
    │   ├── settings.py
    │   ├── urls.py                 # URLs raiz (admin + blog)
    │   ├── wsgi.py
    │   └── asgi.py
    ├── templates/                  # Templates HTML (fornecidos pelo tutor)
    │   ├── base.html
    │   ├── index.html              # Lista de posts publicados
    │   ├── post_detail.html        # Detalhe de um post
    │   └── sidebar.html
    ├── tests/                      # Testes automatizados
    │   ├── models/
    │   │   └── test_post.py        # Testa criação de post via factory
    │   └── views/
    │       └── test_post.py        # Testa que a home retorna status 200
    ├── manage.py
    ├── pytest.ini
    └── requirements.txt
```

---

## 💻 Como rodar localmente

### Pré-requisitos

- Python 3.x instalado
- `pip` disponível no terminal

### 1. Fork do repositório

Clique no botão **Fork** no GitHub para criar uma cópia do repositório na sua conta.

### 2. Clone o seu fork

```bash
git clone https://github.com/<seu-usuario>/<nome-do-repositorio>.git
cd <nome-do-repositorio>/mysite
```

### 3. Crie e ative o ambiente virtual

```bash
python -m venv env
```

**Windows:**
```powershell
.\env\Scripts\Activate.ps1
```

**macOS/Linux:**
```bash
source env/bin/activate
```

### 4. Instale as dependências

```bash
pip install -r requirements.txt
```

### 5. Aplique as migrações

```bash
python manage.py migrate
```

### 6. Crie um superusuário

Para acessar o painel admin e criar posts, você precisará de um superusuário:

```bash
python manage.py createsuperuser
```

Siga as instruções no terminal para definir usuário, e-mail e senha.

### 7. Rode o servidor

```bash
python manage.py runserver
```

A aplicação estará disponível em `http://127.0.0.1:8000/`.

---

## 🔑 Painel Administrativo

O painel admin é onde os posts são criados e gerenciados. Para acessá-lo:

1. Acesse `http://127.0.0.1:8000/admin/`
2. Faça login com o superusuário criado no passo anterior
3. Clique em **Posts** para criar, editar ou excluir posts
4. Para que um post apareça na home, defina o campo **Status** como `Publish` ao criá-lo ou editá-lo

> Posts com status `Draft` não aparecem na página inicial — ficam visíveis apenas no admin.

---

## 🧪 Testes

Com o ambiente virtual ativado, rode:

```bash
pytest
```

A suite possui 2 testes:

- `tests/models/test_post.py` — verifica a criação de um post via factory
- `tests/views/test_post.py` — verifica que a home retorna status HTTP 200

---

## 🏗️ Arquitetura

### Fluxo da aplicação

```
Visitante → GET /          → PostView (ListView)   → index.html       → Lista posts publicados
Visitante → GET /<slug>/   → PostDetail (DetailView) → post_detail.html → Detalhe do post
Admin     → GET /admin/    → Django Admin           → Gerencia posts
```

### Decisões técnicas

**Views baseadas em classe** — `PostView` herda de `generic.ListView` e `PostDetail` de `generic.DetailView`, aproveitando o comportamento padrão do Django sem necessidade de código extra.

**Filtragem por status** — o queryset de `PostView` filtra apenas posts com `status=1` (Publish), garantindo que rascunhos nunca sejam exibidos publicamente.

**Slug como identificador de URL** — o model `Post` usa um campo `slug` único, gerado automaticamente a partir do título no admin, que serve como identificador amigável na URL do detalhe do post.

**SQLite** — banco de dados padrão do Django, adequado para desenvolvimento local. O arquivo `db.sqlite3` é gerado na raiz do projeto e está no `.gitignore`.

---

## 👨‍💻 Autor

**Victor Pires** — [@victorpiressk](https://github.com/victorpiressk) — [LinkedIn](https://www.linkedin.com/in/victor-p-rego/)

---

**Versão:** 1.0.0
**Última atualização:** 17/04/2026
**Status:** ✅ Concluído