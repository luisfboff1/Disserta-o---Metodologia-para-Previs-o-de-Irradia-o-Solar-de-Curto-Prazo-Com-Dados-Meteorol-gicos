# Metodologia para Previsão de Irradiação Solar de Curto Prazo Com Dados Meteorológicos

## 📋 Descrição

Este repositório contém a dissertação de mestrado sobre **Metodologia para Previsão de Irradiação Solar de Curto Prazo Com Dados Meteorológicos**, desenvolvida no Programa de Pós-Graduação em Engenharia Elétrica (PPGEE) da Universidade Federal do Rio Grande do Sul (UFRGS).

A pesquisa propõe uma metodologia para a previsão da irradiância solar global, com resolução de 15 minutos para o dia seguinte, baseada em técnicas de aprendizado de máquina e análise de dados. O trabalho explora diferentes modelos e estratégias de tratamento de dados, buscando identificar a configuração ótima para diferentes contextos e volumes históricos.

## 🎯 Motivação

A crescente adoção de energia solar fotovoltaica no Brasil e o desenvolvimento de sistemas de gerenciamento energético residencial (HEMS - Home Energy Management System) demandam previsões precisas de irradiação solar. A previsão acurada permite:

- ✅ Otimização de despacho energético
- ✅ Operação eficiente de baterias
- ✅ Integração de microredes ao sistema de distribuição
- ✅ Redução de custos para consumidores
- ✅ Apoio à transição energética sustentável

## 🎓 Autor e Orientação

- **Autor:** Luis Fernando Boff
- **Orientador:** Prof. Dr. Roberto Chouhy Leborgne (PPGEE - UFRGS)
  - PhD pela Chalmers University of Technology, Gothenburg, Sweden

## 📚 Objetivos

### Objetivo Principal
Prever a irradiância solar para o dia seguinte com **resolução temporal de 15 minutos**, utilizando dados históricos de irradiância e variáveis meteorológicas associadas.

### Objetivos Específicos
1. Avaliar diferentes arquiteturas de modelagem (LSTM, XGBoost, ARIMA)
2. Analisar o impacto das variáveis de entrada (meteorológicas e históricas)
3. Investigar a influência de diferentes tamanhos de janelas de entrada
4. Realizar otimização de hiperparâmetros
5. Comparar modelos em termos de desempenho (RMSE e R²)
6. Explorar aplicabilidade prática em cenários reais

## 🗂️ Estrutura do Repositório

```
.
├── 1. Introdução/           # Motivação, objetivos e estrutura do trabalho
├── 2. Revisão Bibliográfica/ # Estado da arte e fundamentação teórica
├── 3. Metodologia/          # Metodologia proposta e modelagem
├── 4. Estudo de Caso/       # Estudo de caso com dados reais
├── 5. Resultados/           # Resultados e discussões
├── Figuras/                 # Figuras e gráficos da dissertação
├── Tese.tex                 # Documento principal da dissertação
├── bibliografia.bib         # Referências bibliográficas
└── delaetex.cls            # Classe LaTeX para formatação DELET/UFRGS
```

## 🔬 Metodologia

A metodologia proposta segue um fluxo estruturado:

```
Seleção da Base de Dados
         ↓
Limpeza e Padronização
         ↓
Engenharia de Atributos e Análise Exploratória
         ↓
Consolidação da Base Final
         ↓
Escolha do Modelo de Previsão
         ↓
Otimização de Hiperparâmetros
         ↓
Previsão e Avaliação
```

### Atributos Principais
- **Índice de claridade atmosférica** (k_t*)
- **Variáveis sazonais:** hora do dia e mês (codificação cíclica)
- **Resíduos ARIMA:** captura de padrões não lineares
- **Variáveis meteorológicas:** temperatura, umidade relativa, pressão atmosférica

## 🤖 Modelos Implementados

### 1. ARIMA (AutoRegressive Integrated Moving Average)
- Modelo: ARIMA(2,0,0)(1,0,0)₆₄
- Captura padrões lineares e sazonalidade diária
- Resíduos utilizados como feature adicional

### 2. LSTM (Long Short-Term Memory)
- Redes neurais recorrentes
- Captura dependências temporais de longo prazo
- Adequado para séries temporais com padrões complexos

### 3. XGBoost (eXtreme Gradient Boosting)
- Modelos baseados em árvores de decisão
- Robusto para relações não lineares
- Alta eficiência computacional

### Otimização de Hiperparâmetros
- **Grid Search:** avaliação exaustiva de combinações
- **Bayesian Optimization:** busca guiada no espaço de parâmetros

## 📊 Base de Dados

### Fonte Principal: Estação BSRN de São Martinho da Serra (SMS)

- **Fonte:** Repositório PANGAEA
- **Código da estação:** 70
- **Localização:** -29,44278° (lat), -53,82305° (lon), 489m altitude
- **Período:** 2006-2017
- **Resolução original:** 1 minuto
- **Resolução de trabalho:** 15 minutos (reamostrada)
- **Janela operacional:** 5h-20h (período com irradiação significativa)

### Variáveis Principais
- **SWD:** Shortwave Downwelling Radiation (irradiância global)
- **Temperatura do ar:** a 2m
- **Umidade relativa**
- **Pressão atmosférica**
- **SWD_clear_sky:** Irradiância sob céu limpo (modelo Ineichen)

### Tratamento de Dados
- Conversão de UTC para UTC-3 (fuso local)
- Interpolação linear para lacunas curtas (< 30 min)
- Remoção de dias com falhas extensas (> 30 min)
- Base final: **2.305.920 amostras** (153.728 intervalos de 15 min)

## 📈 Métricas de Avaliação

- **RMSE (Root Mean Square Error):** Erro quadrático médio
- **R² (Coeficiente de Determinação):** Capacidade explicativa do modelo
- **Análise por horizonte:** Desempenho ao longo das 24h do dia seguinte
- **Análise por cenário:** Desempenho em condições de céu limpo vs. nublado

## 🔑 Palavras-chave

- Previsão de Irradiação Solar
- Aprendizado de Máquina
- Sustentabilidade
- Sistema de gerenciamento de casas inteligentes
- Energia Fotovoltaica
- Séries Temporais

## 🛠️ Como Compilar a Dissertação

### Requisitos
- LaTeX (TeX Live, MiKTeX ou similar)
- Classe `delaetex.cls` (incluída no repositório)
- Pacotes: graphicx, amsmath, abntex2cite, entre outros

### Compilação
```bash
# Compilar o documento principal
pdflatex Tese.tex

# Gerar bibliografia
bibtex Tese

# Recompilar para atualizar referências
pdflatex Tese.tex
pdflatex Tese.tex
```

Ou use seu editor LaTeX preferido (TeXstudio, Overleaf, etc.) para compilar o arquivo `Tese.tex`.

## 📖 Estrutura da Dissertação

### Capítulo 1 - Introdução
- Motivação e contexto
- Objetivos e contribuições
- Estrutura do trabalho

### Capítulo 2 - Revisão Bibliográfica
- Estado da arte em previsão solar
- Fundamentos de irradiância
- Variáveis meteorológicas
- Sistemas HEMS
- Métodos de previsão

### Capítulo 3 - Metodologia
- Seleção da base de dados
- Pré-processamento
- Análise exploratória
- Modelagem (LSTM, XGBoost, ARIMA)
- Otimização de hiperparâmetros

### Capítulo 4 - Estudo de Caso
- Descrição da estação SMS
- Análise de dados
- Tratamento e preparação

### Capítulo 5 - Resultados e Discussões
- Resultados do ARIMA
- Resultados do LSTM
- Resultados do XGBoost
- Comparação entre modelos

### Capítulo 6 - Conclusão
- Conclusões gerais
- Trabalhos futuros

## 📚 Principais Referências

- **ABSOLAR** (2025). Dados e estatísticas do setor solar fotovoltaico no Brasil
- **Voyant et al.** (2017). Machine learning methods for solar radiation forecasting: A review
- **Qing & Niu** (2018). Hourly day-ahead solar irradiance prediction using weather forecasts
- **Pal et al.** (2019). A Review on Home Energy Management System Architectures
- **Pereira et al.** (2018). BSRN Station São Martinho da Serra data

## 🌟 Contribuições Científicas

Este trabalho contribui para:
1. **Metodologia estruturada** para previsão intradiária de irradiância
2. **Comparação rigorosa** entre diferentes arquiteturas de ML
3. **Engenharia de atributos** com fundamento físico e estatístico
4. **Estudo aplicado** com dados reais de estação BSRN no Brasil
5. **Suporte à tomada de decisão** em sistemas HEMS e operação de microrredes

## 📧 Contato

Para mais informações sobre esta pesquisa, entre em contato através do PPGEE-UFRGS.

---

## 📄 Licença

Este trabalho acadêmico está disponível para fins educacionais e de pesquisa. A classe LaTeX `delaetex.cls` é distribuída sob GNU GPL.

---

**Universidade Federal do Rio Grande do Sul (UFRGS)**  
**Programa de Pós-Graduação em Engenharia Elétrica (PPGEE)**  
**Departamento de Engenharia Elétrica (DELET)**
