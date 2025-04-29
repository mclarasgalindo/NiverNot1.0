# NiverNote - Sistema de Lembretes de Aniversários para MS-DOS
```markdown
![Descrição da Imagem](file:///u:/Users/41571365869/Downloads/642e8dee-9523-4cd2-a4cf-5a86046e32ca.png)
```

## Descrição do Projeto;

O NiverNote foi desenvolvido para resolver um problema comum dos anos 1980: o esquecimento de datas de aniversário importantes. Antes da era dos smartphones e calendários digitais avançados, as pessoas dependiam de calendários físicos e anotações em papel, o que frequentemente resultava em esquecimentos.

Este programa para MS-DOS oferece uma solução simples e eficiente, exibindo automaticamente lembretes na tela quando é o aniversário de alguém cadastrado no sistema.

## Descrição breve da linguagem e estrutura utilizada:
Este código é escrito em Python e utiliza a biblioteca gráfica CustomTkinter (customtkinter) para criar uma interface para o aplicativo Evernote, o qual é destinado a armazenar e notificar aniversários.

## Estrutura;
## Bibliotecas usadas: 
- `customtkinter, json, datetime, os, plyer.notification`
  
## Funções auxiliares:`
### Cuidam do carregamento, salvamento e validação dos dados, além de calcular o tempo restante para os aniversários.

- `carregar_aniversarios():` Lê os aniversários salvos do arquivo JSON.

- `salvar_aniversarios(aniversarios):` Grava os aniversários no arquivo.

- `validar_data(data):` Verifica se a data está no formato **DD/MM**.

- `dias_para_aniversario(data_str):` Calcula quanto tempo falta para o próximo aniversário.
  
## Funções principais: 
### Gerenciam a adição de novos aniversários, a verificação das datas e a exibição de notificações.

- `adicionar_aniversario():` Pega os dados inseridos, valida e salva um novo aniversário.

- `verificar_aniversarios():` Compara os aniversários salvos com a data atual e monta mensagens de aviso.

- `´notificar_aniversarios(nomes, hoje=True):` Mostra uma notificação no sistema se houver aniversários hoje ou amanhã.

## Interface gráfica (GUI):
- É construída com campos de entrada, botões e rótulos, permitindo interação com o usuário de forma intuitiva.

# Código Fonte;

```batch
import customtkinter as ctk
import json
from datetime import datetime, timedelta
import os
from plyer import notification

ARQUIVO_ANIVERSARIOS = "aniversarios.json"

ctk.set_appearance_mode("System")
ctk.set_default_color_theme("blue")

def carregar_aniversarios():
    if os.path.exists(ARQUIVO_ANIVERSARIOS):
        with open(ARQUIVO_ANIVERSARIOS, "r") as f:
            return json.load(f)
    return {}

def salvar_aniversarios(aniversarios):
    with open(ARQUIVO_ANIVERSARIOS, "w") as f:
        json.dump(aniversarios, f, indent=4)

def validar_data(data):
    try:
        datetime.strptime(data, "%d/%m")
        return True
    except ValueError:
        return False

def dias_para_aniversario(data_str):
    hoje = datetime.now()
    dia, mes = map(int, data_str.split("/"))
    ano_atual = hoje.year
    proximo = datetime(ano_atual, mes, dia)

    if proximo < hoje:
        proximo = datetime(ano_atual + 1, mes, dia)

    delta = proximo - hoje
    total_dias = delta.days
    meses = total_dias // 30
    dias = total_dias % 30

    return meses, dias, total_dias

def adicionar_aniversario():
    nome = entry_nome.get().strip()
    data = entry_data.get().strip()
    if nome and validar_data(data):
        aniversarios = carregar_aniversarios()
        aniversarios[nome] = data
        salvar_aniversarios(aniversarios)
        label_resultado.configure(text=f"✅ Aniversário de {nome} salvo!")
    else:
        label_resultado.configure(text="⚠️ Nome ou data inválida (use DD/MM)")

def verificar_aniversarios():
    hoje = datetime.now()
    data_hoje = hoje.strftime("%d/%m")
    data_amanha = (hoje + timedelta(days=1)).strftime("%d/%m")

    aniversarios = carregar_aniversarios()
    mensagens = []

    for nome, data in aniversarios.items():
        if data == data_hoje:
            mensagens.append(f"🎂 Hoje é aniversário de {nome}!")
            notificar_aniversarios([nome], hoje=True)
        elif data == data_amanha:
            mensagens.append(f" Amanhã é aniversário de {nome}!")
            notificar_aniversarios([nome], hoje=False)
        else:
            meses, dias, total = dias_para_aniversario(data)
            mensagens.append(f"⏳ Faltam {meses} mes(es) e {dias} dia(s) para o aniversário de {nome}.")

    label_resultado.configure(text="\n\n".join(mensagens))

def notificar_aniversarios(nomes, hoje=True):
    if nomes:
        titulo = "🎉 NiverNote - Aniversários de Hoje" if hoje else "⏰ NiverNote - Lembrete de Amanhã"
        mensagem = f"Aniversário de: {', '.join(nomes)}"
        notification.notify(
            title=titulo,
            message=mensagem,
            app_name="NiverNote"
        )


app = ctk.CTk()

app.title("NiverNote")
app.geometry("400x300")

label_nome = ctk.CTkLabel(app, text="Nome:")
label_nome.pack(pady=5)

entry_nome = ctk.CTkEntry(app)
entry_nome.pack(pady=5)

label_data = ctk.CTkLabel(app, text="Data de Aniversário (DD/MM):")
label_data.pack(pady=5)

entry_data = ctk.CTkEntry(app)
entry_data.pack(pady=5)

botao_adicionar = ctk.CTkButton(app, text="Adicionar Aniversário", command=adicionar_aniversario)
botao_adicionar.pack(pady=10)

botao_verificar = ctk.CTkButton(app, text="Verificar Aniversários", command=verificar_aniversarios)
botao_verificar.pack(pady=10)

label_resultado = ctk.CTkLabel(app, text="")
label_resultado.pack(pady=10)

app.mainloop()

