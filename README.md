# py
um banco de dados em python é sql


import sqlite3 
from tkinter import * 
 
root = Tk() 
root.title("Cadastro de Alunos") 
root.geometry("400x400") 
 
# Criação do banco de dados 
conn = sqlite3.connect('alunos.db') 
 
# Criação da tabela 
c = conn.cursor() 
''' 
c.execute("""CREATE TABLE alunos ( 
            nome text, 
            cpf text, 
            mae text, 
            data_nasc text, 
            idade integer, 
            serie text 
            )""") 
''' 
 
# Função para adicionar aluno ao banco de dados 
def submit(): 
    # Criação do banco de dados 
    conn = sqlite3.connect('alunos.db') 
 
    # Criação da tabela 
    c = conn.cursor() 
 
    # Inserção dos dados na tabela 
    c.execute("INSERT INTO alunos VALUES (:nome, :cpf, :mae, :data_nasc, :idade, :serie)", 
              { 
                  'nome': nome.get(), 
                  'cpf': cpf.get(), 
                  'mae': mae.get(), 
                  'data_nasc': data_nasc.get(), 
                  'idade': idade.get(), 
                  'serie': serie.get() 
              }) 
 
    # Commitando as mudanças no banco de dados 
    conn.commit() 
 
    # Fechando a conexão com o banco de dados 
    conn.close() 
 
    # Limpando as caixas de texto após a submissão dos dados 
    nome.delete(0, END) 
    cpf.delete(0, END) 
    mae.delete(0, END) 
    data_nasc.delete(0, END) 
    idade.delete(0, END) 
    serie.delete(0, END) 
 
# Função para mostrar os alunos cadastrados no banco de dados 
def query(): 
    # Criação do banco de dados 
    conn = sqlite3.connect('alunos.db') 
 
    # Criação da tabela 
    c = conn.cursor() 
 
    # Selecionando todos os alunos da tabela 
    c.execute("SELECT *, oid FROM alunos") 
    records = c.fetchall() 
 
    # Loop através dos resultados e mostrando-os na tela 
    print_records = '' 
    for record in records: 
        print_records += str(record[0]) + " " + str(record[1]) + " " + str(record[2]) + " " + str( 
            record[3]) + " " + str(record[4]) + " " + str(record[5]) + "\n" 
 
    query_label = Label(root, text=print_records) 
    query_label.grid(row=8, column=0, columnspan=2) 
 
    # Commitando as mudanças no banco de dados 
    conn.commit() 
 
    # Fechando a conexão com o banco de dados 
    conn.close() 
 
# Criação das caixas de texto para inserir os dados do aluno 
nome_label = Label(root, text="Nome") 
nome_label.grid(row=0, column=0) 
nome = Entry(root, width=30) 
nome.grid(row=0, column=1) 
 
cpf_label = Label(root, text="CPF") 
cpf_label.grid(row=1, column=0) 
cpf = Entry(root, width=30) 
cpf.grid(row=1, column=1) 
 
mae_label = Label(root, text="Nome da Mãe") 
mae_label.grid(row=2, column=0) 
mae = Entry(root, width=30) 
mae.grid(row=2, column=1) 
 
data_nasc_label = Label(root, text="Data de Nascimento") 
data_nasc_label.grid(row=3, column=0) 
data_nasc = Entry(root, width=30) 
data_nasc.grid(row=3, column=1) 
 
idade_label = Label(root, text="Idade") 
idade_label.grid(row=4, column=0) 
idade = Entry(root, width=30) 
idade.grid(row=4, column=1) 
 
serie_label = Label(root, text="Série") 
serie_label.grid(row=5, column=0) 
serie = Entry(root, width=30) 
serie.grid(row=5, column=1) 
 
# Botão para submeter os dados do aluno ao banco de dados 
submit_btn = Button(root, text="Adicionar Aluno ao Banco de Dados", command=submit) 
submit_btn.grid(row=
