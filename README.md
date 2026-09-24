# Detecção de Fraudes em Cartão de Crédito — DIO

Projeto desenvolvido no bootcamp **Bradesco — Dados, Cibersegurança & GenAI**, com Machine Learning aplicado à detecção de fraudes.

## Objetivo
O dataset possui 284.807 transações e 492 fraudes (aprox. 0,17%). Como a classe é extremamente desbalanceada, **acurácia isolada pode enganar**. O projeto prioriza o **Recall da classe fraude**, acompanhado por Precision, F1, ROC-AUC, AUC-PR e matriz de confusão.

## Etapas
1. Carregamento e análise exploratória.
2. Preparação dos dados e divisão estratificada treino/teste.
3. Comparação entre Regressão Logística, Random Forest e XGBoost.
4. Ajuste do threshold de classificação e análise do trade-off Precision x Recall.
5. Explicabilidade do modelo de árvores com SHAP.

## Dataset
Credit Card Fraud Detection (ULB/Kaggle). As variáveis V1–V28 são componentes anonimizados por PCA; também há Time, Amount e Class (0 = legítima, 1 = fraude).

https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud

O notebook tenta carregar uma cópia pública diretamente. Se a URL estiver indisponível, baixe `creditcard.csv` e coloque-o na raiz do projeto.

## Por que Recall?
Um **falso negativo** é uma fraude real classificada como legítima. Nesse contexto, Recall é essencial para medir quantas fraudes reais o modelo consegue detectar. Precision continua importante para evitar excesso de falsos alertas.

O threshold padrão de 0,50 também não é tratado como regra fixa. O notebook demonstra como diferentes limiares alteram Precision, Recall e a matriz de confusão.

## Estrutura
```
.
├── README.md
├── deteccao_fraudes.ipynb
├── requirements.txt
└── .gitignore
```

## Execução
```bash
pip install -r requirements.txt
jupyter notebook deteccao_fraudes.ipynb
```

Também pode ser executado no Google Colab.

## Conclusão
O projeto demonstra que, em classificação extremamente desbalanceada, a escolha da métrica é parte central do problema. Os resultados numéricos são calculados pelo notebook durante a execução — não são inseridas métricas inventadas. O ajuste de threshold permite analisar o custo entre falsos negativos e falsos positivos, enquanto SHAP adiciona interpretabilidade às previsões.

## Autor
**Lucas Mafra**  
Desafio de Projeto — DIO
