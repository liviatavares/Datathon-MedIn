# Como Exportar um Modelo Preditivo

Este tutorial explica como exportar e salvar modelos preditivos de machine learning para uso posterior, incluindo melhores práticas para reprodutibilidade e deploy.

## Objetivos do Tutorial

- Aprender diferentes métodos de serialização de modelos
- Garantir reprodutibilidade dos modelos
- Preparar modelos para deploy em produção
- Documentar adequadamente o processo

## 1. Exportando Modelos com Pickle

O método mais comum para exportar modelos em Python é usando a biblioteca `pickle`.

### Salvando o Modelo

```python
import pickle
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import train_test_split
import pandas as pd

# Exemplo com dados do datathon
df = pd.read_csv('train.csv')
X = df.drop(['id', 'num'], axis=1)
y = df['num']

# Treinar o modelo
model = RandomForestClassifier(random_state=42, n_estimators=100)
model.fit(X, y)

# Salvar o modelo
with open('heart_disease_model.pkl', 'wb') as file:
    pickle.dump(model, file)

print("Modelo salvo com sucesso!")
```

### Carregando o Modelo

```python
# Carregar o modelo salvo
with open('heart_disease_model.pkl', 'rb') as file:
    loaded_model = pickle.load(file)

# Usar o modelo carregado para predições
predictions = loaded_model.predict(X_test)
```

## 2. Exportando Modelos com Joblib

Para modelos de scikit-learn, `joblib` é mais eficiente que pickle.

```python
import joblib

# Salvar modelo
joblib.dump(model, 'heart_disease_model.joblib')

# Carregar modelo
loaded_model = joblib.load('heart_disease_model.joblib')
```

## 3. Exportando Pipeline Completo

É importante salvar todo o pipeline de pré-processamento junto com o modelo.

```python
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.ensemble import RandomForestClassifier

# Criar pipeline completo
pipeline = Pipeline([
    ('scaler', StandardScaler()),
    ('classifier', RandomForestClassifier(random_state=42))
])

# Treinar pipeline
pipeline.fit(X, y)

# Salvar pipeline completo
joblib.dump(pipeline, 'complete_pipeline.joblib')
```

## 4. Estrutura de Arquivos Recomendada

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

## 5. Script de Inferência (inference.py)

```python
import joblib
import pandas as pd
import numpy as np

class HeartDiseasePredictor:
    def __init__(self, model_path):
        self.model = joblib.load(model_path)
    
    def predict(self, data):
        """
        Faz predições para novos dados
        
        Args:
            data: DataFrame com as features necessárias
            
        Returns:
            Array com predições (0 ou 1)
        """
        return self.model.predict(data)
    
    def predict_proba(self, data):
        """
        Retorna probabilidades das predições
        """
        return self.model.predict_proba(data)

# Exemplo de uso
if __name__ == "__main__":
    # Carregar modelo
    predictor = HeartDiseasePredictor('models/heart_disease_model.joblib')
    
    # Carregar dados de teste
    test_data = pd.read_csv('data/test.csv')
    X_test = test_data.drop('id', axis=1)
    
    # Fazer predições
    predictions = predictor.predict(X_test)
    
    # Criar submissão
    submission = pd.DataFrame({
        'id': test_data['id'],
        'num': predictions
    })
    
    submission.to_csv('submission.csv', index=False)
    print("Submissão criada com sucesso!")
```

### Salvar Configurações

```python
import json

# Salvar configurações do modelo
config = {
    'model_type': 'RandomForestClassifier',
    'parameters': {
        'n_estimators': 100,
        'random_state': 42,
        'max_depth': 10
    },
    'features_used': list(X.columns),
    'training_date': '2025-09-29',
    'performance_metrics': {
        'train_accuracy': 0.95,
        'validation_recall': 0.88
    }
}

with open('model_config.json', 'w') as f:
    json.dump(config, f, indent=2)
```

## 6. Versionamento de Modelos

```python
import datetime
import os

def save_versioned_model(model, base_name='heart_disease_model'):
    """Salva modelo com timestamp"""
    timestamp = datetime.datetime.now().strftime('%Y%m%d_%H%M%S')
    filename = f"{base_name}_{timestamp}.joblib"
    
    # Criar diretório se não existir
    os.makedirs('models/versions', exist_ok=True)
    
    filepath = f"models/versions/{filename}"
    joblib.dump(model, filepath)
    
    # Salvar também como 'latest'
    joblib.dump(model, f"models/{base_name}_latest.joblib")
    
    return filepath
```

## 7. Validação do Modelo Exportado

```python
def validate_exported_model(original_model, exported_model_path, X_test):
    """Valida se o modelo exportado funciona corretamente"""
    
    # Carregar modelo exportado
    loaded_model = joblib.load(exported_model_path)
    
    # Comparar predições
    original_pred = original_model.predict(X_test)
    loaded_pred = loaded_model.predict(X_test)
    
    # Verificar se são idênticas
    if np.array_equal(original_pred, loaded_pred):
        print("✅ Modelo exportado corretamente!")
        return True
    else:
        print("❌ Erro na exportação do modelo!")
        return False

# Exemplo de uso
validate_exported_model(model, 'heart_disease_model.joblib', X_test)
```

## 8. Checklist para Exportação

- [ ] Modelo treinado e validado
- [ ] Pipeline de pré-processamento incluído
- [ ] Configurações salvas em arquivo separado
- [ ] Script de inferência criado e testado
- [ ] Dependências listadas em requirements.txt
- [ ] Documentação clara no README.md
- [ ] Modelo versionado adequadamente
- [ ] Validação da exportação realizada

## Próximos Passos

Após exportar seu modelo:

1. Teste o script de inferência com dados de validação
2. Documente o processo no README.md
3. Prepare a submissão seguindo o formato exigido
4. Considere métricas de monitoramento para produção

## Recursos Adicionais

- [Documentação do Scikit-learn sobre Persistência](https://scikit-learn.org/stable/model_persistence.html)
- [MLflow para Gerenciamento de Modelos](https://mlflow.org/)
- [Boas Práticas em MLOps](https://ml-ops.org/)