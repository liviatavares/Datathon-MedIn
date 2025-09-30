---
sidebar_position: 1
---

# Datathon MedIn — Heart Disease Prediction

Bem-vindo ao Datathon MedIn, um desafio técnico que convida membros da Liga de Engenharia Biomédica MedIn a desenvolver modelos preditivos capazes de identificar pacientes com doença cardíaca.

## Objetivo

Desenvolver modelos de classificação binária que, usando apenas o dataset oficial fornecido, consigam identificar corretamente pacientes com doença cardíaca (num = 1), maximizando recall nessa classe — ou seja, priorizar a detecção de casos positivos.

## Público-alvo

- Destinado a membros da Liga MedIn
- Participação individual
- Voltado a estudantes e profissionais interessados em machine learning aplicado à saúde

## Dataset

### Arquivos Fornecidos
- **train.csv** — conjunto de treino, inclui a coluna alvo `num`
- **test.csv** — conjunto de teste, sem a coluna alvo
- **sample_submission.csv** — exemplo de formato de submissão

### Variáveis Principais
- **age** — idade do paciente em anos
- **sex** — sexo (0 = feminino, 1 = masculino)
- **cp** — tipo de dor no peito (0-3)
- **trestbps** — pressão arterial em repouso (mm Hg)
- **chol** — colesterol sérico (mg/dl)
- **fbs** — glicemia de jejum > 120 mg/dl (1 = verdadeiro, 0 = falso)
- **restecg** — resultados do ECG em repouso (0-2)
- **thalach** — frequência cardíaca máxima atingida
- **exang** — angina induzida por exercício (1 = sim, 0 = não)
- **oldpeak** — depressão do segmento ST
- **slope** — inclinação do segmento ST (0-2)
- **ca** — número de vasos principais (0-3)
- **thal** — resultado do exame de tálio (3, 6, 7)
- **num** — variável alvo (0 = sem doença, 1 = com doença)

## Avaliação

- **Métrica principal**: Recall da classe positiva (num = 1) e F1-Score
- **Critério de desempate**: Qualidade técnica, documentação e explicabilidade
- **Limite**: 5 submissões por dia por equipe

## Como Começar

1. Baixe os arquivos `train.csv`, `test.csv` e `sample_submission.csv`
2. Treine seu modelo apenas com `train.csv`
3. Gere previsões binárias (0/1) para `test.csv`
4. Submeta no formato: `id,num`
5. Documente seeds e decisões técnicas

## Entregáveis Finais

Para equipes finalistas:
- Código de treinamento e inferência
- `inference.py`
- `requirements.txt` ou `environment.yml`
- `model.pkl` (ou equivalente)
- `README.md` com instruções claras
