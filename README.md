# Sistema-Simples-de-Gerenciamento-de-Biblioteca
# Sistema simples de gerenciamento de livros
# Atividade: Bibliotecas e Módulos em Python

from collections import Counter
import matplotlib.pyplot as plt

# Classe que representa cada livro cadastrado.
class Livro:
    def __init__(self, titulo, autor, genero, quantidade):
        self.titulo = titulo
        self.autor = autor
        self.genero = genero
        self.quantidade = quantidade

    def __str__(self):
        return (f"Título: {self.titulo} | Autor: {self.autor} | "
                f"Gênero: {self.genero} | Quantidade disponível: {self.quantidade}")


# Lista que armazena os livros da biblioteca.
livros = []


# Cadastra um livro novo.
def cadastrar_livro(titulo, autor, genero, quantidade):
    if quantidade < 0:
        print("A quantidade não pode ser negativa.")
        return
    livro = Livro(titulo, autor, genero, quantidade)
    livros.append(livro)
    print(f'Livro "{titulo}" cadastrado com sucesso!')


# Exibe todos os livros cadastrados
def listar_livros():
    if not livros:
        print("Nenhum livro cadastrado.")
        return
    print("\n--- LIVROS CADASTRADOS ---")
    for livro in livros:
        print(livro)


# Procura livros por título
def buscar_livro(titulo):
    encontrados = [livro for livro in livros
                   if titulo.casefold() in livro.titulo.casefold()]
    if encontrados:
        print("\n--- RESULTADO DA BUSCA ---")
        for livro in encontrados:
            print(livro)
    else:
        print(f'Nenhum livro encontrado com o título "{titulo}".')


# Cria um gráfico com a quantidade total de exemplares por gênero.
def gerar_grafico():
    if not livros:
        print("Cadastre pelo menos um livro antes de gerar o gráfico.")
        return

    quantidades = Counter()
    for livro in livros:
        quantidades[livro.genero] += livro.quantidade

    generos = list(quantidades.keys())
    totais = list(quantidades.values())

    plt.figure(figsize=(8, 5))
    barras = plt.bar(generos, totais)
    plt.title("Quantidade de livros disponíveis por gênero")
    plt.xlabel("Gênero")
    plt.ylabel("Quantidade disponível")
    plt.bar_label(barras)
    plt.tight_layout()
    plt.show()


# Livros cadastrados
cadastrar_livro("Dom Casmurro", "Machado de Assis", "Romance", 4)
cadastrar_livro("O Hobbit", "J. R. R. Tolkien", "Fantasia", 3)
cadastrar_livro("A Hora da Estrela", "Clarice Lispector", "Romance", 2)
cadastrar_livro("Sapiens", "Yuval Noah Harari", "História", 5)

# Testes das funcionalidades solicitadas
listar_livros()
buscar_livro("hobbit")
gerar_grafico()
