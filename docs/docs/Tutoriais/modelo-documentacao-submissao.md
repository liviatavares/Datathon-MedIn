# Modelo de Documentação de Submissão

Este documento serve como template para a documentação da sua submissão no Datathon MedIn. Uma documentação clara e completa é essencial para reprodutibilidade e pode ser um critério de desempate.

## Template README.md

# Heart Disease Prediction

## Resumo da Solução

Breve descrição da abordagem utilizada (2-3 parágrafos):
- Algoritmo principal escolhido
- Estratégia de pré-processamento
- Técnicas de validação
- Principais insights dos dados

## Configuração do Ambiente

### Dependências

```bash
pip install -r requirements.txt
```

### Versões Utilizadas
- Python: 3.9.x
- Scikit-learn: 1.3.x
- Pandas: 2.0.x
- Numpy: 1.24.x

## Metodologia

### 1. Análise Exploratória dos Dados
- [Descreva principais descobertas]
- [Distribuição das classes]
- [Correlações importantes]

### 2. Pré-processamento
- [Tratamento de valores ausentes]
- [Normalização/Padronização]
- [Feature engineering]

### 3. Modelagem
- [Algoritmos testados]
- [Hiperparâmetros otimizados]
- [Validação cruzada utilizada]

### 4. Avaliação
- [Métricas de validação]
- [Recall da classe positiva]
- [F1-Score]

## Reprodução dos Resultados

### Treinamento do Modelo

```bash
python src/train.py
```

### Geração de Predições

```bash
python inference.py
```

## Estrutura do Projeto

```
projeto/
├── models/
│   └── heart_disease_model.joblib
├── src/
│   ├── train.py
│   ├── preprocessing.py
│   └── utils.py
├── notebooks/
│   └── exploratory_analysis.ipynb
├── submissions/
│   └── final_submission.csv
├── inference.py
├── requirements.txt
└── README.md
```

## Resultados

### Validação Cruzada (5-fold)
- **Recall médio**: X.XX ± X.XX
- **F1-Score médio**: X.XX ± X.XX
- **Acurácia média**: X.XX ± X.XX

### Métricas no Conjunto de Validação
- **Recall**: X.XX
- **F1-Score**: X.XX
- **Precisão**: X.XX
- **Acurácia**: X.XX

## Principais Insights

1. [Insight 1 sobre os dados ou modelo]
2. [Insight 2 sobre features importantes]
3. [Insight 3 sobre desafios encontrados]

## Decisões Técnicas

### Por que escolhemos [Algoritmo X]?
- [Justificativa baseada nos dados]
- [Performance superior em métricas relevantes]
- [Interpretabilidade]

### Feature Engineering
- [Novas features criadas]
- [Features removidas e por quê]
- [Transformações aplicadas]

### Estratégia de Validação
- [Método de validação escolhido]
- [Como garantimos que o modelo generaliza]

## Limitações e Melhorias Futuras

- [Limitação 1 da abordagem atual]
- [Limitação 2 identificada]
- [Sugestões para versões futuras]

## Referências

- [Paper 1 que inspirou a abordagem]
- [Documentação de biblioteca utilizada]
- [Artigo sobre o domínio médico]

---

**Data de submissão**: DD/MM/AAAA
**Versão**: 1.0
```

## Exemplo Prático

Aqui está um exemplo real de como preencher a documentação:

```markdown
# Heart Disease Prediction - Team DataHeart

## Informações da Equipe

- **Nome da Equipe**: DataHeart
- **Membros**: 
  - João Silva - joao.silva@sou.inteli.edu.br
  - Maria Santos - maria.santos@sou.inteli.edu.br
- **Liga**: MedIn

## Resumo da Solução

Desenvolvemos um ensemble de Random Forest e XGBoost com foco na maximização do recall para detecção de doença cardíaca. Nossa abordagem combinou feature engineering baseada em conhecimento médico com otimização de hiperparâmetros via Optuna. O modelo final alcançou recall de 0.92 na validação cruzada.

A estratégia principal foi criar features compostas (razões entre variáveis) e aplicar SMOTE para balanceamento, seguido de um ensemble ponderado que prioriza a detecção de casos positivos.

## Configuração do Ambiente

### Dependências

```bash
pip install -r requirements.txt
```

### Versões Utilizadas
- Python: 3.9.16
- Scikit-learn: 1.3.0
- XGBoost: 1.7.4
- Pandas: 2.0.3
- Numpy: 1.24.3

## Metodologia

### 1. Análise Exploratória dos Dados
- Dataset balanceado (54% sem doença, 46% com doença)
- Correlações fortes: thalach vs age (-0.4), oldpeak vs num (0.43)
- Missing values: nenhum detectado

### 2. Pré-processamento
- Padronização Z-score para variáveis contínuas
- One-hot encoding para variáveis categóricas (cp, slope, thal)
- Feature engineering: idade²/thalach, chol/age, oldpeak*slope

### 3. Modelagem
- Algoritmos testados: RF, XGBoost, SVM, LightGBM
- Hiperparâmetros otimizados via Optuna (100 trials)
- Validação cruzada estratificada 5-fold

### 4. Avaliação
- Recall validação: 0.92 ± 0.03
- F1-Score validação: 0.89 ± 0.02

## Reprodução dos Resultados

### Treinamento do Modelo

```bash
python src/train.py
```

### Geração de Predições

```bash
python inference.py
```

## Resultados

### Validação Cruzada (5-fold)
- **Recall médio**: 0.92 ± 0.03
- **F1-Score médio**: 0.89 ± 0.02
- **Acurácia média**: 0.87 ± 0.04

### Feature Importance (Top 5)
1. ca (0.18)
2. thal (0.16)
3. oldpeak (0.14)
4. age_squared_thalach (0.12)
5. cp (0.11)

## Principais Insights

1. **Ca e thal são os preditores mais importantes**, confirmando a literatura médica
2. **Features compostas melhoraram o recall em 0.05**, especialmente idade²/thalach
3. **Ensemble reduziu overfitting** comparado a modelos individuais

## Decisões Técnicas

### Por que escolhemos Random Forest + XGBoost?
- RF: robusto a outliers e interpretável
- XGBoost: captura interações não-lineares complexas
- Ensemble: combina estabilidade do RF com poder preditivo do XGBoost

### Estratégia de Balanceamento
- SMOTE aplicado apenas no treino (evita data leakage)
- Pesos de classe ajustados para priorizar recall

## Limitações e Melhorias Futuras

- Validação externa necessária para confirmar generalização
- Análise de fairness entre subgrupos demográficos
- Incorporação de conhecimento médico mais específico

---

**Data de submissão**: 20/09/2025
**Versão**: 1.0
```

## Dicas Importantes

### O que INCLUIR:
- Justificativas técnicas para decisões
- Métricas de validação detalhadas
- Estrutura clara de arquivos
- Instruções de reprodução

### O que EVITAR:
- Documentação genérica sem detalhes específicos
- Resultados sem metodologia de validação
- Código sem comentários
- Falta de versionamento de dependências

### Critérios de Qualidade

1. **Reprodutibilidade**: Outros podem recriar seus resultados?
2. **Clareza**: A documentação é autoexplicativa?
3. **Profundidade técnica**: As decisões são bem justificadas?
4. **Organização**: Código e arquivos bem estruturados?

## Checklist Final

- [ ] README.md completo e bem formatado
- [ ] requirements.txt com versões específicas
- [ ] inference.py funcional e documentado
- [ ] Estrutura de pastas organizada
- [ ] Resultados de validação reportados
- [ ] Código comentado e limpo
- [ ] Decisões técnicas justificadas

Lembre-se: uma boa documentação pode ser o diferencial em caso de empate técnico!