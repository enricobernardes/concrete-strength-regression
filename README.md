# Previsão da resistência do concreto (R² 0,91)

Modelo de regressão que estima a resistência à compressão do concreto (MPa) a partir da composição do traço e da idade de cura.

## Resumo

Com o traço em mãos, dá para estimar a resistência do concreto antes do ensaio, com erro médio de ~3,5 MPa. Isso antecipa a decisão: ganha prazo de obra, evita retrabalho e, sem superdimensionar a mistura, economiza cimento, um dos insumos mais caros do traço. O modelo não substitui o ensaio, que segue obrigatório.

O Random Forest foi o melhor modelo: explica 91% da variação da resistência (R² 0,91), enquanto o chute pela mediana erra em média ~14 MPa. Cimento, idade e superplastificante são os fatores mais ligados à resistência.

## Problema
A resistência do concreto só é confirmada no ensaio, em geral aos 28 dias. Até lá, ajustes no traço são decididos sem esse dado.

## Dados
- [Concrete Compressive Strength (Kaggle)](https://www.kaggle.com/datasets/elikplim/concrete-compressive-strength-data-set), originalmente do repositório UCI
- 1.030 traços (1.005 após remover 25 duplicados), 8 variáveis de entrada em kg/m³ e dias, alvo em MPa

## Abordagem
1. Qualidade dos dados: duplicados, nulos e conferência se os valores fazem sentido na prática (ex.: nenhuma idade de cura 0 dias)
2. Correlação com a resistência e entre as variáveis
3. Split treino/teste 80/20
4. Baseline (`DummyRegressor`, mediana) vs Regressão Linear, KNN e Random Forest
5. Escala (`StandardScaler`) só para Regressão Linear e KNN

## Resultados

| Modelo | MAE (MPa) | RMSE (MPa) | R² |
|---|---|---|---|
| Baseline (mediana) | 13,97 | 17,42 | −0,02 |
| Regressão Linear | 8,90 | 11,19 | 0,58 |
| KNN | 7,13 | 9,19 | 0,72 |
| **Random Forest** | **3,50** | **5,26** | **0,91** |


## Próximos passos
- Ajuste de hiperparâmetros (`GridSearchCV`) e validação cruzada
- Importância das variáveis do Random Forest

## Tecnologias
Python · Pandas · NumPy · Matplotlib · Seaborn · Scikit-learn

## Como rodar
Abra `concrete_strength_regression.ipynb` no Kaggle (com o dataset acima anexado) ou no Jupyter, ajustando o caminho do CSV.

---
*Sintaxe com apoio de guias pessoais e IA; análise e conclusões são minhas.*
