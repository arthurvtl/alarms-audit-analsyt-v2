# Sistema de Análise de Alarmes (SGD) v2.0

Sistema completo para análise de alarmes de usinas de energia solar, desenvolvido com FastAPI (backend) e React (frontend).

![Logo ATI](ati_automacao_telecomunicacoes_e_informatica_logo.jpeg)

## 📋 Descrição do Projeto

O Sistema de Análise de Alarmes (SGD) é uma plataforma web completa para monitoramento, análise e geração de relatórios de alarmes de usinas solares. O sistema permite:

- ✅ Visualização de dados de alarmes de múltiplas usinas
- ✅ Análise de períodos específicos (até 3 meses não consecutivos)
- ✅ Busca de alarmes por descrição com autocomplete
- ✅ Geração de relatórios em PDF, Excel e CSV
- ✅ Visualização de dashboards interativos com gráficos (ECharts)
- ✅ Monitoramento de erros do sistema
- ✅ Interface totalmente em Português (PT-BR)
- ✅ Tema com cores azul, cinza e branco

## 🏗️ Arquitetura do Sistema

```
sistema_analise_alarmes_sgd/
├── backend/                    # API FastAPI
│   ├── app/
│   │   ├── config/            # Configurações (database, settings)
│   │   ├── models/            # Modelos SQLAlchemy
│   │   ├── routes/            # Endpoints da API
│   │   ├── services/          # Lógica de negócio
│   │   ├── utils/             # Funções auxiliares
│   │   └── main.py            # Arquivo principal
│   ├── requirements.txt       # Dependências Python
│   └── .env                   # Variáveis de ambiente
│
├── frontend/                  # Aplicação React
│   ├── public/               # Arquivos públicos
│   ├── src/
│   │   ├── assets/           # Imagens e recursos
│   │   ├── components/       # Componentes React
│   │   ├── pages/            # Páginas da aplicação
│   │   ├── services/         # Comunicação com API
│   │   ├── utils/            # Funções auxiliares
│   │   ├── App.js            # Componente principal
│   │   └── index.js          # Ponto de entrada
│   ├── package.json          # Dependências Node
│   └── .env                  # Variáveis de ambiente
│
└── README.md                 # Este arquivo
```

## 🔧 Tecnologias Utilizadas

### Backend
- **Python**: 3.9 ou superior
- **FastAPI**: Framework web moderno e rápido
- **SQLAlchemy**: ORM para banco de dados
- **PostgreSQL**: Banco de dados (com psycopg2)
- **ReportLab**: Geração de PDFs
- **Pandas/OpenPyXL**: Exportação para Excel/CSV
- **Uvicorn**: Servidor ASGI

### Frontend
- **React**: 18.2 ou superior
- **Material-UI (MUI)**: Biblioteca de componentes
- **ECharts**: Biblioteca de visualização de dados
- **Axios**: Cliente HTTP
- **React Router**: Roteamento

## 📦 Pré-requisitos

Antes de começar, certifique-se de ter instalado:

- **Python 3.9+** - [Download Python](https://www.python.org/downloads/)
- **Node.js 16+** e **npm** - [Download Node.js](https://nodejs.org/)
- **PostgreSQL** - [Download PostgreSQL](https://www.postgresql.org/download/)
- **Git** (opcional) - [Download Git](https://git-scm.com/)

### Verificar Versões

```bash
# Verificar Python
python --version

# Verificar Node.js e npm
node --version
npm --version

# Verificar PostgreSQL
psql --version
```

## 🚀 Instalação e Configuração

### 1. Configuração do Banco de Dados

O sistema utiliza um banco de dados PostgreSQL com a seguinte estrutura:

**URL de Conexão:**
```
postgresql+psycopg2://postgres:arthur@localhost:5432/ATI_IVI_Backup
```

**Estrutura de Tabelas:**
- `power_station` - Tabela de usinas
- `alarm` - Tabela base de alarmes
- `alarm_<ID_USINA>_<ANO>_<MES>` - Tabelas particionadas de alarmes
  - Exemplo: `alarm_100_2025_06` (Alarmes da usina 100 em Junho/2025)

**Restaurar Banco de Dados** (se necessário):

Os arquivos SQL estão em `/home/ubuntu/Uploads/`. Para restaurar:

```bash
# Combinar arquivos SQL (se em partes)
cat ivi_20250623_ssit_ivi.part*.sql > backup_completo.sql

# Restaurar no PostgreSQL
psql -U postgres -d ATI_IVI_Backup -f backup_completo.sql
```

### 2. Configuração do Backend

```bash
# Navegar para o diretório do backend
cd backend/

# Criar ambiente virtual Python
python -m venv venv

# Ativar ambiente virtual
# Windows:
venv\Scripts\activate
# Linux/Mac:
source venv/bin/activate

# Instalar dependências
pip install -r requirements.txt
```

**Arquivo `.env` do Backend:**

O arquivo `.env` já está configurado com:

```env
DB_URL=postgresql+psycopg2://postgres:arthur@localhost:5432/ATI_IVI_Backup
APP_NAME=Sistema de Análise de Alarmes (SGD)
APP_VERSION=2.0
DEBUG=True
HOST=0.0.0.0
PORT=8000
```

**Ajuste a URL do banco se necessário!**

### 3. Configuração do Frontend

```bash
# Navegar para o diretório do frontend
cd frontend/

# Instalar dependências
npm install
```

**Arquivo `.env` do Frontend:**

O arquivo `.env` já está configurado com:

```env
REACT_APP_API_URL=http://localhost:8000
REACT_APP_NAME=Sistema de Análise de Alarmes (SGD)
REACT_APP_VERSION=2.0
```

## ▶️ Executando o Sistema

### Executar Backend (Terminal 1)

```bash
cd backend/

# Ativar ambiente virtual
# Windows:
venv\Scripts\activate
# Linux/Mac:
source venv/bin/activate

# Executar servidor
python -m uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

O backend estará disponível em:
- **API**: http://localhost:8000
- **Documentação Swagger**: http://localhost:8000/docs
- **Documentação ReDoc**: http://localhost:8000/redoc

### Executar Frontend (Terminal 2)

```bash
cd frontend/

# Executar aplicação React
npm start
```

O frontend estará disponível em:
- **Aplicação**: http://localhost:3000

## 📱 Usando o Sistema

### Página 1: Home
- Apresentação do sistema
- Descrição das funcionalidades
- Instruções de uso

### Página 2: Operações
1. **Selecione a Usina** - Escolha uma usina disponível no dropdown
2. **Selecione o Período** - Escolha entre 1 ou 3 meses
   - Para 3 meses: Marque os checkboxes dos meses desejados (não precisam ser consecutivos)
   - Botão "Selecionar Automaticamente" escolhe os meses mais recentes
3. **Carregar Dados** - Clique para buscar os alarmes
4. **Buscar Alarmes** - Use a barra de busca para filtrar por descrição

### Página 3: Dashboards e Resultados
- Visualize **resumo** com total de alarmes e tempo em alarme
- **Gráficos interativos** (ECharts):
  - Distribuição por Severidade (Barras)
  - Proporção por Severidade (Pizza)
  - Top 10 Equipamentos com Mais Alarmes
- **Exportar Relatórios**:
  - 📄 **PDF** - Relatório em A4 vertical com cabeçalho
  - 📊 **Excel** - Múltiplas sheets (Alarmes, Resumo, Severidade)
  - 📋 **CSV** - Arquivo CSV simples

### Página 4: Erros
- Visualize todos os erros registrados pelo sistema
- Útil para debug e monitoramento
- Atualização em tempo real

## 🔌 Endpoints da API

### Alarmes
- `GET /api/alarmes/usinas` - Lista de usinas disponíveis
- `GET /api/alarmes/usinas/{id}/meses` - Meses disponíveis para uma usina
- `POST /api/alarmes/dados` - Dados de alarmes para períodos selecionados
- `POST /api/alarmes/buscar` - Busca de alarmes por termo

### Relatórios
- `POST /api/relatorios/pdf` - Gera relatório PDF
- `POST /api/relatorios/excel` - Gera relatório Excel
- `POST /api/relatorios/csv` - Gera relatório CSV

### Erros
- `GET /api/erros?limit=100` - Lista de erros registrados

### Saúde
- `GET /health` - Status da aplicação e banco de dados

## 📦 Dependências Detalhadas

### Backend (requirements.txt)

```txt
fastapi==0.104.1
uvicorn[standard]==0.24.0
python-multipart==0.0.6
sqlalchemy==2.0.23
psycopg2-binary==2.9.9
python-dotenv==1.0.0
pydantic==2.5.0
pydantic-settings==2.1.0
reportlab==4.0.7
pandas==2.1.3
openpyxl==3.1.2
python-json-logger==2.0.7
```

### Frontend (package.json)

```json
{
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-router-dom": "^6.20.0",
    "axios": "^1.6.2",
    "echarts": "^5.4.3",
    "echarts-for-react": "^3.0.2",
    "@mui/material": "^5.14.18",
    "@mui/icons-material": "^5.14.18",
    "@emotion/react": "^11.11.1",
    "@emotion/styled": "^11.11.0",
    "date-fns": "^2.30.0"
  }
}
```

## 🎨 Tema e Design

O sistema utiliza um tema personalizado com as seguintes cores:

- **Primário (Azul)**: #1976d2
- **Secundário (Cinza)**: #757575
- **Fundo**: #f5f5f5 (cinza claro)
- **Papel**: #ffffff (branco)
- **Texto**: #212121 (preto suave)

## 🐛 Troubleshooting

### Erro de Conexão com Banco de Dados

**Problema**: Backend não conecta ao PostgreSQL

**Solução**:
1. Verifique se o PostgreSQL está rodando
2. Confirme usuário, senha e porta no arquivo `.env`
3. Teste a conexão manualmente:
   ```bash
   psql -U postgres -d ATI_IVI_Backup
   ```

### Erro de CORS no Frontend

**Problema**: Frontend não consegue se comunicar com o backend

**Solução**:
1. Verifique se o backend está rodando em `http://localhost:8000`
2. Confirme a URL no arquivo `.env` do frontend
3. Verifique as origens permitidas em `backend/app/config/settings.py`

### Módulos Python Não Encontrados

**Problema**: `ModuleNotFoundError` ao executar backend

**Solução**:
```bash
# Ativar ambiente virtual
cd backend/
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows

# Reinstalar dependências
pip install -r requirements.txt
```

### Dependências Node Não Encontradas

**Problema**: Erros ao executar `npm start`

**Solução**:
```bash
cd frontend/
rm -rf node_modules package-lock.json
npm install
npm start
```

### Tabela de Alarmes Não Existe

**Problema**: "Table alarm_X_Y_Z does not exist"

**Solução**:
- A tabela de alarmes deve seguir o padrão `alarm_<USINA_ID>_<ANO>_<MES>`
- Verifique se as tabelas existem no banco de dados
- Restaure o backup SQL se necessário

## 📝 Observações Importantes

1. **Não há sistema de login** - O sistema é de uso local e não requer autenticação
2. **Máximo 3 meses** - Por performance, limite a seleção a 3 meses
3. **Meses não consecutivos** - É possível selecionar qualquer combinação de meses
4. **Autocomplete** - A busca de alarmes funciona na descrição carregada
5. **SessionStorage** - Dados são mantidos na sessão do navegador entre páginas

## 🔐 Segurança

- Sistema para uso **LOCAL** (Windows sem Docker)
- Não expor para internet sem configurar autenticação
- Alterar credenciais padrão do banco de dados
- Usar HTTPS em ambiente de produção

## 👥 Suporte

Para dúvidas ou problemas:
- Verifique a seção de Troubleshooting
- Consulte os logs em `backend/logs/`
- Acesse a página "Erros" no sistema
- Consulte a documentação da API em `/docs`

## 🎉 Conclusão

O Sistema de Análise de Alarmes (SGD) está pronto para uso!

