# Passo-a-passo de Execução

Esta pasta contém o código do agente financeiro.

## Setup do Ollama

```bash
# 1. Instalar Ollama (ollama.com)
# 2. Baixar um modelo lece
ollama pull qwen3.1-8b

# 3. Testar se funciona
ollama run qwen3.1-8b "Olá!"
```

## Estrutura

```
src/
└── app.py              # Aplicação (Streamlit)
```

## Exemplo de requirements.txt

```
streamlit
openai
python-dotenv
```

## Como Rodar

```bash
# Instalar dependências
pip install streamlit pandas requests

# Garantir que Ollama está rodando
ollama serve

# Rodar a aplicação
streamlit run app.py
```
