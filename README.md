# Simulador-notas-alunos
Sistema para simulação e analise do desempenho acadêmico de alunos
#Quantidade de alunos defenida após iniciar programa.
nomes = []
import random
#defenido para 0 os status, para a contagem
status = {
    "aprovado_direto": 0,
    "reprovado_direto": 0,
    "aprovado_rec": 0,
    "reprovado_rec": 0
}

#loop para caso de erro de digitação
while True:
  try:
    quantidade_alunos = int(input("Quantos alunos serão exibidos? "))
    if quantidade_alunos > 0:
      break
    else:
      print("Digite um número maior que 0!")
  except ValueError:
    print("Digite apenas números inteiros!")

#definição dos nomes por exemplo aluno1
for i in range(1, quantidade_alunos + 1):
  nome = f"aluno{i}"
  print(f"\nDigite as notas de {nome}")
  AOP1 = round(random.uniform(0,1),2)
  AOP2 = round(random.uniform(0,2),2)
  AOP3 = round(random.uniform(0,1),2)
  PROVA_REGULAR = round(random.uniform(0,6),2)
  MM = AOP1 + AOP2 + AOP3 + PROVA_REGULAR

#comparação de notas e definição de seus status
  if MM >= 7.0:
    print(f"{nome}: Aprovado")
    status["aprovado_direto"] += 1
    situacao = "aprovado_direto"
    PROVA_RECUPERACAO = 0
    media_geral = MM
  elif MM < 3.0:
    print(f"{nome}: Reprovado")
    status["reprovado_direto"] += 1
    situacao = "reprovado_direto"
    PROVA_RECUPERACAO = 0
    media_geral = MM
  else:
    PROVA_RECUPERACAO = float(round(random.uniform(0,10),2))
    media_geral = (MM + PROVA_RECUPERACAO) / 2
    if media_geral >= 5.0:
      print(f"{nome}: Aprovado após recuperação")
      status["aprovado_rec"] += 1
      situacao = "Aprovado após recuperação"
    else:
      print(f"{nome}: Reprovado após recuperação")
      status["reprovado_rec"] += 1
      situacao = "Reprovado após recuperação"
  aluno = ({
    "Nome": nome,
    "AOP1": AOP1,
    "AOP2": AOP2,
    "AOP3": AOP3,
    "Prova_Regular": PROVA_REGULAR,
    "Media": MM,
    "Prova_Recuperação": PROVA_RECUPERACAO,
    "Media_Geral": media_geral,
    "Situação": situacao
    })
  nomes.append(aluno)

#relatorio primario referente a porcentagem dos status dos alunos
total = sum(status.values())

print("\nRELATÓRIO FINAL")
print(f"Quantidade de alunos aprovados diretamente: {status['aprovado_direto']} ({status['aprovado_direto']/total*100:.2f}% do total)")
print(f"Quantidade de alunos reprovados diretamente: {status['reprovado_direto']} ({status['reprovado_direto']/total*100:.2f}% do total)")
print(f"Quantidade de alunos aprovados após recuperação: {status['aprovado_rec']} ({status['aprovado_rec']/total*100:.2f}% do total)")
print(f"Quantidade de alunos reprovados após recuperação: {status['reprovado_rec']} ({status['reprovado_rec']/total*100:.2f}% do total)")
print("-------------------------------------//-------------------------------------")
print(f"Expecificação geral:")
print("")
print(f"Quantidade total de alunos aprovados sem recuperação: {status['aprovado_direto']} ({status['aprovado_direto']/total*100:.2f}% do total)")
print(f"Quantidade de alunos aprovados com a recuperação: {status['aprovado_rec']} ({status['aprovado_rec']/total*100:.2f}% do total)")
print(f"Quantidade total de alunos reprovados: {status['reprovado_direto'] + status['reprovado_rec']} ({(status['reprovado_direto'] + status['reprovado_rec'])/total*100:.2f}% do total)")

print("\n===== RELATÓRIO DOS ALUNOS =====")

#exibição de nomes, status e notas de cada aluno
for aluno in nomes:
    print(f"""
Nome: {aluno['Nome']}
AOP1: {aluno['AOP1']}
AOP2: {aluno['AOP2']}
AOP3: {aluno['AOP3']}
Prova Regular: {aluno['Prova_Regular']}
Média: {aluno['Media']:.2f}
Situação: {aluno['Situação']}
Prova Recuperação: {aluno['Prova_Recuperação']}
Media_Geral: {aluno['Media_Geral']:.2f}
""")
