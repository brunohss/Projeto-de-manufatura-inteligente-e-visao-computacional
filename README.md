# 🔍 Sistema de Detecção de Defeitos com Visão Computacional

Sistema completo de inspeção visual automatizada para detecção de defeitos em peças automotivas usando Visão Computacional, Machine Learning e IoT.

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![OpenCV](https://img.shields.io/badge/OpenCV-4.8-green.svg)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)

## 📋 Índice

- [Visão Geral](#visão-geral)
- [Características](#características)
- [Arquitetura](#arquitetura)
- [Instalação](#instalação)
- [Uso](#uso)
- [Tecnologias](#tecnologias)
- [Dashboards](#dashboards)
- [Roadmap](#roadmap)

## 🎯 Visão Geral

Sistema de Manufatura 4.0 que utiliza câmera para inspecionar peças automotivas em tempo real, detecta anomalias usando Machine Learning e gera alertas via IoT. Inclui dashboards interativos com métricas de produção.

### Funcionalidades Principais

- ✅ Captura de imagens em tempo real via câmera
- ✅ Pré-processamento avançado de imagens (OpenCV)
- ✅ Detecção de defeitos usando ML (Random Forest, SVM, Neural Networks)
- ✅ Alertas em tempo real via MQTT (IoT)
- ✅ Banco de dados para rastreabilidade
- ✅ Dashboard interativo (Streamlit)
- ✅ Exportação de relatórios (PowerBI/Grafana)

## 🚀 Características

### Tipos de Defeitos Detectados

1. **Riscos** - Marcas superficiais
2. **Trincas** - Fraturas no material
3. **Deformações** - Alterações na geometria
4. **Manchas** - Imperfeições de acabamento

### Métricas Monitoradas

- Taxa de defeitos em tempo real
- Tempo médio de processamento
- Distribuição de tipos de defeitos
- Confiança das predições
- Uptime do sistema

## 🏗️ Arquitetura

```
┌─────────────────┐
│   Câmera/Image  │
└────────┬────────┘
         │
         ▼
┌─────────────────────────┐
│  Captura & Processamento│ (OpenCV)
└────────┬────────────────┘
         │
         ▼
┌─────────────────────────┐
│   Modelo ML             │ (Scikit-learn)
│   - Random Forest       │
│   - SVM                 │
│   - Neural Network      │
└────────┬────────────────┘
         │
         ├──────────────────┬──────────────────┐
         ▼                  ▼                  ▼
┌──────────────┐   ┌──────────────┐   ┌──────────────┐
│ MQTT Broker  │   │  Database    │   │  Dashboard   │
│ (Alertas IoT)│   │ (SQLite/PG)  │   │ (Streamlit)  │
└──────────────┘   └──────────────┘   └──────────────┘
```

## 📦 Instalação

### Pré-requisitos

- Python 3.8 ou superior
- Câmera conectada (webcam ou câmera USB)
- (Opcional) MQTT Broker (Mosquitto)
- (Opcional) PostgreSQL

### Passo a Passo

1. **Clone o repositório**

```bash
git clone https://github.com/brunohss/Projeto-de-manufatura-inteligente-e-visao-computacional/edit/main/deteccao-defeitos.git
cd deteccao-defeitos
```

2. **Crie ambiente virtual**

```bash
python -m venv venv
source venv/bin/activate  # Linux/Mac
# ou
venv\Scripts\activate  # Windows
```

3. **Instale dependências**

```bash
pip install -r requirements.txt
```

4. **Configure o sistema**

Edite `config.yaml` com suas configurações:

```yaml
CAMERA:
  device_id: 0  # 0 para webcam padrão
  resolution:
    width: 1280
    height: 720

MQTT:
  broker: "localhost"
  port: 1883

DATABASE:
  type: "sqlite"
  sqlite_path: "data/deteccao_defeitos.db"
```

5. **(Opcional) Inicie MQTT Broker**

```bash
# Instalar Mosquitto
sudo apt-get install mosquitto mosquitto-clients  # Linux
# ou
brew install mosquitto  # Mac

# Iniciar broker
mosquitto -v
```

## 🎮 Uso

### 1. Treinar Modelo

#### Opção A: Dataset Sintético (para testes)

```bash
cd scripts
python train_model.py --synthetic --model random_forest
```

#### Opção B: Dataset Real

Organize suas imagens:
```
data/dataset/
  ├── OK/
  │   ├── image1.jpg
  │   └── image2.jpg
  ├── Trinca/
  │   └── image1.jpg
  ├── Risco/
  │   └── image1.jpg
  └── ...
```

Execute o treinamento:
```bash
python train_model.py --dataset data/dataset --model random_forest --augment
```

### 2. Executar Sistema de Inspeção

```bash
cd src
python main.py --mode camera
```

**Comandos durante execução:**
- `i` - Inspecionar frame atual
- `q` - Sair

### 3. Iniciar Dashboard

```bash
cd dashboards
streamlit run streamlit_dashboard.py
```

Acesse: `http://localhost:8501`

### 4. Modo Batch (processar múltiplas imagens)

```bash
python main.py --mode batch --input-folder data/images/test
```

## 🛠️ Tecnologias

### Visão Computacional
- **OpenCV** 4.8 - Processamento de imagens
- **Pillow** - Manipulação de imagens

### Machine Learning
- **Scikit-learn** - Modelos ML (Random Forest, SVM)
- **NumPy** - Operações numéricas
- **Pandas** - Manipulação de dados

### IoT & Comunicação
- **Paho-MQTT** - Protocolo MQTT para alertas
- **MQTT Broker** - Mosquitto

### Banco de Dados
- **SQLAlchemy** - ORM
- **SQLite** - Banco local
- **PostgreSQL** - Banco em produção (opcional)

### Dashboards & Visualização
- **Streamlit** - Dashboard interativo
- **Plotly** - Gráficos interativos
- **Matplotlib/Seaborn** - Visualizações estáticas

### Integrações
- **PowerBI** - Relatórios empresariais
- **Grafana** - Monitoramento industrial

## 📊 Dashboards

### Streamlit Dashboard

Interface web interativa com:
- KPIs em tempo real
- Gráficos de taxa de defeitos
- Distribuição de tipos de defeitos
- Histórico de inspeções
- Alertas e notificações

### PowerBI Integration

1. Exporte dados do banco:
```python
from database.db_manager import DatabaseManager
db = DatabaseManager()
db.export_to_csv('inspections', 'data/exports/inspections.csv')
```

2. Importe no PowerBI e crie visualizações customizadas

### Grafana Integration

1. Configure datasource PostgreSQL no Grafana
2. Importe dashboard template: `dashboards/grafana/dashboard.json`
3. Customize queries e painéis

## 📈 Estrutura de Dados

### Tabela: inspections
```sql
- id: INTEGER PRIMARY KEY
- timestamp: DATETIME
- image_path: VARCHAR(500)
- defect_class: VARCHAR(100)
- confidence: FLOAT
- is_defect: BOOLEAN
- processing_time_ms: FLOAT
- operator_id: VARCHAR(100)
- line_id: VARCHAR(100)
```

### Tabela: defect_records
```sql
- id: INTEGER PRIMARY KEY
- inspection_id: INTEGER
- timestamp: DATETIME
- defect_type: VARCHAR(100)
- severity: VARCHAR(50)
- confidence: FLOAT
- image_path: VARCHAR(500)
- notes: TEXT
- resolved: BOOLEAN
- resolved_at: DATETIME
```

### Tabela: production_metrics
```sql
- id: INTEGER PRIMARY KEY
- timestamp: DATETIME
- total_inspected: INTEGER
- defects_found: INTEGER
- defect_rate: FLOAT
- uptime_hours: FLOAT
- line_id: VARCHAR(100)
- shift: VARCHAR(50)
```

## 🔧 Configuração Avançada

### Ajuste de Parâmetros do Modelo

Edite `config.yaml`:

```yaml
MODEL:
  type: "random_forest"
  confidence_threshold: 0.85  # Threshold de confiança
  model_path: "models/detector_defeitos.pkl"
```

### Configuração de Alertas

```yaml
ALERTS:
  enable_mqtt: true
  enable_email: false
  enable_sound: true
  min_interval_seconds: 10  # Intervalo mínimo entre alertas
```

## 📝 Roadmap

### Fase 1: Core (Concluído ✅)
- [x] Captura de imagens
- [x] Processamento OpenCV
- [x] Modelo ML básico
- [x] MQTT IoT
- [x] Banco de dados
- [x] Dashboard Streamlit

### Fase 2: Melhorias
- [ ] Deep Learning (CNN)
- [ ] Transfer Learning (ResNet, EfficientNet)
- [ ] Segmentação de imagens
- [ ] Detecção de múltiplos defeitos
- [ ] API REST
- [ ] Mobile app

### Fase 3: Produção
- [ ] Docker deployment
- [ ] CI/CD pipeline
- [ ] Load balancing
- [ ] Cloud integration (AWS/Azure)
- [ ] A/B testing de modelos

## 🤝 Contribuindo

Contribuições são bem-vindas! Por favor:

1. Fork o projeto
2. Crie uma branch (`git checkout -b feature/NovaFuncionalidade`)
3. Commit suas mudanças (`git commit -m 'Adiciona nova funcionalidade'`)
4. Push para a branch (`git push origin feature/NovaFuncionalidade`)
5. Abra um Pull Request

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo `LICENSE` para mais detalhes.

## 👥 Autores

- Bruno Henrique - [@brunohss](https://github.com/brunohss)

## 📧 Contato

Para dúvidas ou sugestões, abra uma issue no GitHub.

---

**Desenvolvido com ❤️ para Manufatura 4.0**
