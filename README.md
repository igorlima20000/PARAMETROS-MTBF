# PARAMETROS-MTBF
import numpy as np
import matplotlib.pyplot as plt
from matplotlib.ticker import FuncFormatter

# Definir parâmetros
MTBF_12000 = 12000  # Tempo médio entre falhas em horas (12.000h)
MTBF_24000 = 24000  # Tempo médio entre falhas em horas (24.000h)
anos = 6  # Tempo máximo em anos
horas_por_ano = 8760  # Número de horas em um ano
tempo = np.linspace(0, anos * horas_por_ano, 100)  # Criar um vetor de tempo

# Função de confiabilidade para ambos os MTBFs
confiabilidade_12000 = np.exp(-tempo / MTBF_12000)
confiabilidade_24000 = np.exp(-tempo / MTBF_24000)

# Confiabilidade no intervalo de 1 ano para ambos os MTBFs
confiabilidade_1_ano_12000 = np.exp(-horas_por_ano / MTBF_12000)
confiabilidade_1_ano_24000 = np.exp(-horas_por_ano / MTBF_24000)

print(f"Confiabilidade após 1 ano (MTBF 12000h): {confiabilidade_1_ano_12000 * 100:.2f}%")
print(f"Confiabilidade após 1 ano (MTBF 24000h): {confiabilidade_1_ano_24000 * 100:.2f}%")

# Gerar o gráfico
plt.figure(figsize=(8, 5))

# Plotando as duas curvas de confiabilidade
plt.plot(tempo / horas_por_ano, confiabilidade_12000 * 100, label=f'MTBF = {MTBF_12000} horas', color='b', linestyle='--')  # Linha pontilhada
plt.plot(tempo / horas_por_ano, confiabilidade_24000 * 100, label=f'MTBF = {MTBF_24000} horas', color='g')

# Personalizando o gráfico
plt.xlabel('Tempo (anos)')
plt.ylabel('Confiabilidade (%)')  # Exibindo o título com o símbolo %
plt.title('Comparação de Confiabilidade de um Sistema ao Longo do Tempo')
plt.grid()
plt.legend()

# Formatar o eixo Y para exibir valores em porcentagem
plt.gca().yaxis.set_major_formatter(FuncFormatter(lambda x, _: f'{x:.0f}%'))

plt.show()
