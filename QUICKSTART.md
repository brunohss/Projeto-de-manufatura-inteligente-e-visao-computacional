# 🚀 Guia de Início Rápido - 5 Minutos

## Passo 1: Instalação (2 min)

```bash
# Clone o repositório
git clone https://github.com/seu-usuario/deteccao-defeitos.git
cd projeto1_deteccao_defeitos

# Crie ambiente virtual e instale dependências
python -m venv venv
source venv/bin/activate  # Linux/Mac
pip install -r requirements.txt
```

## Passo 2: Treinar Modelo com Dados Sintéticos (1 min)

```bash
cd scripts
python train_model.py --synthetic --model random_forest
```

**Saída esperada:**
```
=== Treinamento do Modelo ===
Dataset gerado: 2000 amostras
Treinando modelo...
✓ Acurácia: 0.9850
✓ Modelo salvo em: models/detector_defeitos.pkl
```

## Passo 3: Executar Sistema (1 min)

```bash
cd ../src
python main.py --mode camera
```

**Na janela que abrir:**
- Pressione `i` para inspecionar a imagem atual
- Pressione `q` para sair

## Passo 4: Ver Dashboard (1 min)

Em outro terminal:

```bash
cd dashboards
streamlit run streamlit_dashboard.py
```

Abra o navegador em: `http://localhost:8501`

---

## ⚡ Teste Rápido Sem Câmera

Se não tiver câmera disponível:

```bash
# Gerar imagens de teste
cd scripts
python generate_test_images.py

# Processar em modo batch
cd ../src
python main.py --mode batch --input-folder ../images/samples
```

---

## 🎯 Próximos Passos

1. **Personalizar Configurações**: Edite `config.yaml`
2. **Treinar com Seus Dados**: Organize imagens e execute `train_model.py --dataset sua_pasta`
3. **Integrar MQTT**: Inicie broker Mosquitto para alertas IoT
4. **Explorar Dashboard**: Customize visualizações no Streamlit

---

## 🆘 Problemas Comuns

### Erro: "Câmera não encontrada"
- Verifique se a câmera está conectada
- Mude `device_id` em `config.yaml` (tente 0, 1, 2)

### Erro: "Módulo não encontrado"
- Certifique-se que está no ambiente virtual ativado
- Execute: `pip install -r requirements.txt`

### MQTT não conecta
- Instale Mosquitto: `sudo apt-get install mosquitto`
- Ou desative MQTT em `config.yaml`: `enable_mqtt: false`

---

**Pronto! Seu sistema está funcionando! 🎉**
