# Base de Conhecimento

## Dados Utilizados

Descreva se usou os arquivos da pasta `data`, por exemplo:

| Arquivo | Formato | Utilização no Agente |
|---------|---------|---------------------|
| `perfil_investidor.json` | JSON | Personalizar recomendações |
| `produtos_financeiros.json` | JSON | Sugerir produtos adequados ao perfil |
| `transacoes.csv` | CSV | Analisar padrão de gastos do amigo |

> [!TIP]
> **Para um dataset mais robusto:** Pode-se utilizar datasets públicos do [Hugging Face](https://huggingface.co/datasets) relacionados a finanças, desde que sejam adequados ao contexto do desafio.

---

## Adaptações nos Dados

> Você modificou ou expandiu os dados mockados? Descreva aqui.

Sem modificações. Atualizar conforme mudanças em parâmetros econômicos.

---

## Estratégia de Integração

### Como os dados são carregados?
> Descreva como seu agente acessa a base de conhecimento.

```python
import pandas as pd 
import json
# CSVs
transacoes = pd.read_csv("data/transacoes.csv")
# JSONs 
with open("data/perfil_invastidor.json", "r", encoding="utf-8") as f: 
  perfil = json.load(f)
with open("data/produtos_financeiros.json", "r", encoding='utf-8') as f:
  produtos = json.load(f)
```

### Como os dados são usados no prompt?
> Os dados vão no system prompt? São consultados dinamicamente?

```
Os dados são consultados dinamicamente e injetados no contexto da conversa no momento da interação. A estratégia segue este fluxo:

Contextualização do Perfil: O perfil_investidor.json é lido no início para definir "quem" é o amigo com quem o Beto está conversando (ex: se é alguém conservador ou arrojado). Isso molda o tom das recomendações.

Injeção de Memória de Gastos: Os dados do transacoes.csv são processados para identificar padrões. Se o usuário pergunta "posso investir 500 reais?", o código consulta esse arquivo e injeta no prompt: "O usuário gastou R$ 400 em bares e restaurantes no último mês". O Beto então usa isso para dizer: "Cara, se você trocar duas rodadas de chopp por mês, esses 500 reais aparecem num estalar de dedos!".

Filtragem de Produtos: O arquivo produtos_financeiros.json serve como o "cardápio" do Beto. O código filtra apenas os produtos que fazem sentido para o perfil do usuário e entrega para a IA como: "Opções disponíveis: CDB Banco X, Tesouro Selic".

O que vai no System Prompt: Apenas a instrução de como usar esses dados.

```



---

## Exemplo de Contexto Montado

> Mostre um exemplo de como os dados são formatados para o agente.

```
Dados do Cliente:
- Nome: João Silva
- Perfil: Moderado
- Saldo disponível: R$ 5.000

Últimas transações:
- 01/11: Supermercado - R$ 450
- 03/11: Streaming - R$ 55
...
```
