# Detecção de Fraudes em Cartão de Crédito — DIO

Projeto desenvolvido no bootcamp **Bradesco — Dados, Cibersegurança & GenAI**, com Machine Learning aplicado à detecção de fraudes.

## Problema e objetivo
O dataset possui 284.807 transações e 492 fraudes (aprox. 0,17%). Como a classe é extremamente desbalanceada, um modelo que classificasse quase tudo como legítimo teria alta acurácia e pouca utilidade. Por isso, o projeto prioriza **Recall da classe fraude**, acompanhado por Precision, F1, ROC-AUC, AUC-PR e matriz de confusão.

## Dataset
Credit Card Fraud Detection (ULB/Kaggle). As variáveis `V1` a `V28` são componentes anonimizados por PCA; também há `Time`, `Amount` e `Class` (0 = legítima; 1 = fraude).

Dataset: https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud

O notebook tenta carregar uma cópia pública diretamente por URL. Se a fonte estiver indisponível, pode-se baixar `creditcard.csv` e colocá-lo localmente na raiz. O dataset não é versionado neste repositório.

## Preparação dos dados
- análise da distribuição da classe e valores ausentes;
- criação de `Amount_log = log1p(Amount)` para reduzir a assimetria dos valores;
- padronização de `Time`, `Amount` e `Amount_log` com `StandardScaler`;
- divisão treino/teste com `stratify=y`, preservando a proporção de fraudes;
- tratamento do desbalanceamento com `class_weight='balanced'` e `scale_pos_weight`.

## Modelos comparados
1. Regressão Logística — baseline interpretável;
2. Random Forest — modelo de árvores não linear;
3. XGBoost — boosting com peso específico para a classe minoritária.

A comparação usa **Precision, Recall e F1 da fraude**, além de ROC-AUC e AUC-PR. Também são gerados relatórios de classificação, matrizes de confusão, **curvas ROC e Precision-Recall**.

## Por que Recall?
Um falso negativo representa uma fraude real classificada como legítima. O Recall mede a proporção de fraudes reais encontradas pelo modelo. Precision também é analisada para controlar falsos alertas, e F1 resume o equilíbrio entre as duas métricas.

## Ajuste do limiar
O threshold padrão de 0,50 não é tratado como regra fixa. O notebook demonstra a busca de um limiar que alcance Recall de pelo menos 90% e, entre os candidatos, favoreça maior Precision. Essa etapa é didática; em produção, o threshold deve ser escolhido em um conjunto de validação separado.

## Explicabilidade
O projeto utiliza **SHAP** no melhor modelo de árvores segundo Recall e também apresenta a importância global das variáveis. Como `V1`–`V28` foram anonimizadas por PCA, é possível identificar componentes relevantes, mas não traduzi-los diretamente para atributos de negócio.

## O que evoluí em relação ao fluxo base da Expert
Além de reproduzir o pipeline central do desafio, este projeto:
- compara três famílias de modelos no mesmo fluxo;
- inclui `Amount_log` como engenharia de atributo;
- usa pesos de classe sem alterar o conjunto de teste;
- compara ROC e Precision-Recall;
- automatiza a comparação das métricas em uma tabela;
- demonstra ajuste de threshold com uma meta explícita de Recall;
- combina SHAP com importância global das variáveis.

Undersampling e oversampling foram mantidos como alternativas de evolução. Aqui, optou-se por pesos de classe para preservar todas as observações de treinamento e manter o projeto objetivo.

## Estrutura
```
.
├── README.md
├── deteccao_fraudes.ipynb
├── requirements.txt
└── .gitignore
```

## Como executar
```bash
pip install -r requirements.txt
jupyter notebook deteccao_fraudes.ipynb
```

Também pode ser executado no Google Colab. Execute as células em ordem e salve o notebook após a execução para manter as tabelas e curvas visíveis no GitHub.

## Conclusão
Em fraude, a escolha da métrica faz parte da solução. Recall mostra a capacidade de detectar fraudes reais; Precision mede a qualidade dos alertas; F1 ajuda a observar o equilíbrio. O ajuste do threshold permite adaptar esse compromisso, enquanto SHAP ajuda a explicar as previsões.

Os resultados numéricos são produzidos pela execução do notebook, evitando registrar métricas não verificadas.

## Autor
**Lucas Mafra**  
Desafio de Projeto — DIO | Bradesco — Dados, Cibersegurança & GenAI
