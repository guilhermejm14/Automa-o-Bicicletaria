# Automa-o-Bicicletaria
Treinamento de Phyton DIO 
import json
import os

class GerenciadorBicicletas:
    def __init__(self):
        self.arquivo = 'estoque_bikes.json'
        self.bicicletas = self.carregar_dados()

    def carregar_dados(self):
        if os.path.exists(self.arquivo):
            with open(self.arquivo, 'r') as f:
                return json.load(f)
        return []

    def salvar_dados(self):
        with open(self.arquivo, 'w') as f:
            json.dump(self.bicicletas, f, indent=4)

    def adicionar_bike(self, modelo, marca, preco):
        nova_bike = {
            "id": len(self.bicicletas) + 1,
            "modelo": modelo,
            "marca": marca,
            "preco": preco
        }
        self.bicicletas.append(nova_bike)
        self.salvar_dados()
        print(f"\n✅ {modelo} adicionada com sucesso!")

    def listar_bikes(self):
        print("\n--- ESTOQUE ATUAL ---")
        for bike in self.bicicletas:
            print(f"ID: {bike['id']} | {bike['marca']} {bike['modelo']} - R$ {bike['preco']}")

def menu():
    manager = GerenciadorBicicletas()
    while True:
        print("\n1. Adicionar Bicicleta")
        print("2. Listar Estoque")
        print("3. Sair")
        opcao = input("Escolha uma opção: ")

        if opcao == '1':
            marca = input("Marca: ")
            modelo = input("Modelo: ")
            preco = input("Preço: ")
            manager.adicionar_bike(modelo, marca, preco)
        elif opcao == '2':
            manager.listar_bikes()
        elif opcao == '3':
            break
        else:
            print("Opção inválida!")

if __name__ == "__main__":
    menu()
