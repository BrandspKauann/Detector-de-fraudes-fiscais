# 🛡️ Detector de Fraudes Financeiras (Machine Learning)

## 💡 Visão Geral do Projeto

Este projeto implementa um modelo de **Machine Learning (ML) de Classificação Supervisionada** para identificar transações **fraudulentas (1)** em um cenário comum e desafiador: um conjunto de dados altamente **desbalanceado**.

O foco principal é criar um sistema que priorize a segurança, garantindo um **alto Recall** para a classe de fraude e minimizando os **Falsos Negativos** (fraudes reais que passariam despercebidas), que representam o maior risco financeiro.

---

## 🚀 Tecnologias e Metodologia

| Fase | Descrição | Foco | Ferramentas Chave |
| :--- | :--- | :--- | :--- |
| **Data Prep** | Criação e estruturação de dados simulados com desequilíbrio de classes (17 transações normais vs. 3 fraudes). | Desequilíbrio de Classes | `Pandas` |
| **Pré-processamento** | Separação **estratificada** (`stratify=y`) dos dados para garantir que a proporção de fraudes seja mantida nos conjuntos de treino e teste. | Mitigação de Viés | `scikit-learn` |
| **Algoritmo** | **Regressão Logística** (Modelo de base, escolhido por sua simplicidade e interpretabilidade em finanças). | Transparência (Caixa-Branca) | `sklearn.linear_model.LogisticRegression` |
| **Avaliação** | Análise de **Recall** e **Matriz de Confusão**, priorizando a detecção máxima de fraudes. | Detecção Máxima | `sklearn.metrics` |

---

## 📊 Estrutura e Variáveis do Dataset

O modelo foi treinado com features que refletem o comportamento de risco em transações financeiras:

| Coluna | Tipo | Descrição |
| :--- | :--- | :--- |
| `Valor_Transacao` | `Float` | Valor da transação. |
| `Idade_Conta` | `Int` | Tempo de existência da conta (em meses). |
| `Local_Risco` | `Int` | Nível de risco da localização (1=Baixo a 5=Alto). |
| `Hora_Dia` | `Int` | Hora da transação (0 a 23). |
| **`Fraude`** | **`Int` (Target)** | **1 (Fraude) / 0 (Não Fraude)** |

---

Análise da Matriz: O resultado mais importante é o **Falso Negativo (FN = 0)**. Isso significa que nenhuma fraude real passou despercebida pelo modelo de teste, atingindo o objetivo de alto **Recall**.

### Explicabilidade (Motivação da Decisão)
O uso da Regressão Logística permite a **Interpretabilidade Imediata**. O modelo chegou às suas conclusões porque as *features* de Alto Risco e Horário Suspeito ativaram os **pesos negativos (coeficientes)** aprendidos, empurrando a probabilidade para 100% de fraude.

### 3. Simulação em Produção (Dados Novos)
O modelo foi testado em um cenário de uso real, sem a coluna Fraude:

| Caso | Valor\_Transacao | Local\_Risco | Hora\_Dia | Probabilidade\_Fraude | Previsão |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Suspeito** | R$ 3.500 | 5 (Alto) | 1 (Madrugada) | 1.00 | **1 (Bloquear)** |
| **Normal** | R$ 150 | 1 (Baixo) | 15 (Comercial) | $7.28e-11$ | **0 (Liberar)** |

O modelo demonstrou capacidade de **bloquear transações suspeitas** com alta confiança e **liberar transações normais**.

---
