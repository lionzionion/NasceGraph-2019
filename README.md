# NasceGraph-2019

# Projeto de Análise de Nascimentos - README
## Descrição do Projeto
Este projeto tem como objetivo realizar uma análise dos dados de nascimentos, utilizando conjuntos de dados referentes aos meses de março, abril, maio, junho e dezembro do ano de 2019. Os dados são provenientes do Sistema de Nascidos Vivos (SINASC) do estado de Rondônia.

## Como Executar o Código
### Pré-requisitos
Certifique-se de ter instalado as seguintes bibliotecas antes de executar o código:
```python
pip install pandas matplotlib
```
### Executando o Código
O código está disponível em um Jupyter Notebook (analise_nascimentos.ipynb). Execute as células do notebook para gerar os gráficos relacionados aos meses selecionados.

## Automatização da Análise
Para facilitar a geração de novos gráficos para diferentes meses ou anos, consideramos a implementação de uma função que permite ao usuário escolher os meses desejados. Isso oferece maior flexibilidade e personalização na análise dos dados.

### Função para Escolher Meses

```python
import pandas as pd
import matplotlib.pyplot as plt

def obter_meses_desejados():
    meses = input("Digite os números dos meses desejados separados por vírgula (por exemplo, 1,2,3): ")
    meses = [int(m) for m in meses.split(',')]
    return meses

# Leitura do arquivo CSV
df = pd.read_csv('SINASC_RO_2019.csv')

# Convertendo a coluna 'DTNASC' para o formato de data
df['DTNASC'] = pd.to_datetime(df['DTNASC'], errors='coerce')

# Obter os meses desejados do usuário
meses_desejados = obter_meses_desejados()

# Filtrando para incluir apenas os meses desejados
df = df[(df['DTNASC'].dt.month.isin(meses_desejados)) & (df['DTNASC'].dt.year == 2019)].copy()

# Criando a coluna de mês em português usando .loc para evitar SettingWithCopyWarning
df.loc[:, 'MES_NASC'] = df['DTNASC'].dt.month_name()

# Contagem de registros por mês
contagem_por_mes = df['MES_NASC'].value_counts().sort_index()

# Reordenar o índice para que os meses apareçam em ordem
contagem_por_mes = contagem_por_mes.reindex(['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'])

# Gráfico de barras para a contagem de registros por mês
plt.figure(figsize=(10, 6))
barplot = contagem_por_mes.plot(kind='bar', color='skyblue')

# Adicionando rótulos nas barras com a contagem
for i, valor in enumerate(contagem_por_mes):
    plt.text(i, valor + 50, str(valor), ha='center', va='bottom', fontsize=8)

# Configurações do gráfico
plt.title('Contagem de Nascimentos por Mês em 2019')
plt.xlabel('Mês de Nascimento')
plt.ylabel('Contagem')

# Formatando os rótulos do eixo x
plt.xticks(rotation=45, ha='right')

plt.grid(axis='y', linestyle='--', alpha=0.7)

# Exibindo o gráfico
plt.show()
```
### Contribuição
Se você deseja contribuir para o projeto, siga as diretrizes de contribuição.

### Licença
Este projeto está sob a licença MIT. Consulte o arquivo LICENSE para obter mais detalhes.

### Reconhecimentos
Agradecemos aos colaboradores e às fontes de dados que tornaram este projeto possível.

### Contato
Para mais informações ou dúvidas, entre em contato através do email: amadeudevpython@gmail.com.
