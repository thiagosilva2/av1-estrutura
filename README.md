# av1-estrutura
Meu trabalho

#include <iostream>

using namespace std;

struct Pessoa
{
	int idade  = 0;
	string cpf = "0";
	int sexo = 0;
	bool esta_gravida = false;

	Pessoa* proximo = NULL;
	Pessoa* anterior = NULL;
};

void printPessoa(Pessoa pessoa);
int lerInteiro(string campo);
string lerString(string campo);

int main(void)
{
	Pessoa* inicioLista = NULL;
	Pessoa* fimLista = NULL;
	Pessoa* aux = NULL;

	int opcao = 0;
	while (opcao != 4)
	{
		cout<<  "_________";
		cout << "\n|1-Próximo atendimento    |";
		cout << "\n|2-Exibir cadastros       |";
		cout << "\n|3-Apagar cadastros       |";
		cout << "\n|4-Sair                   |" << endl;
		cout<<  "|_________|" <<endl;
		cin >> opcao;

		switch (opcao)
		{
			case 1:
			{
				Pessoa* novo = new Pessoa;
				novo->idade = lerInteiro("idade");
				novo->cpf = lerString("cpf");
				novo->sexo = lerInteiro("sexo (1-Feminino/2-Masculino)");
				if (novo->sexo == 1)
				{
					int gravida;
					cout << "\nVocê esta gravida? (1-Sim/2-Não): ";
					cin >> gravida;
					if (gravida == 1)
					{
						novo->esta_gravida = true;
					}
					else
					{
						novo->esta_gravida = false;
					}
				}

				if (novo->idade > 65 || novo->esta_gravida == true)
				{
					if (inicioLista == NULL)
					{
						inicioLista = novo;
						fimLista = novo;
						novo->proximo = NULL;
						novo->anterior = NULL;
					}
					else
					{
						novo->proximo = inicioLista;
						inicioLista->anterior = novo;
						novo->anterior = NULL;
						inicioLista = novo;
					}
				}
				else
				{
					if (inicioLista == NULL)
					{
						inicioLista = novo;
						fimLista = novo;
						novo->proximo = NULL;
						novo->anterior = NULL;
					}
					else
					{
						fimLista->proximo = novo;
						novo->anterior = fimLista;
						novo->proximo = NULL;
						fimLista = novo;
					}
				}
			} break;

			case 2:
			{
				if (inicioLista == NULL)
				{
					cout << "\nLista Vazia" << endl;
				}
				else
				{
					aux = inicioLista;
					while (aux != NULL)
					{
						printPessoa(*aux);
						aux = aux->proximo;
					}
				}
			} break;

			case 3:
			{
				if (inicioLista == NULL)
				{
					cout << "\nLista Vazia" << endl;
				}
				else
				{
					aux = inicioLista;

					printPessoa(*aux);

					aux = aux->proximo;

					aux = inicioLista;

					inicioLista = inicioLista->proximo;
					delete(aux);
					aux = inicioLista;
				}
			} break;
		}
	}

	return 0;
}

int lerInteiro(string campo)
{
	int valor;
	cout << "\nDigite " << campo << ": ";
	cin >> valor;

	return valor;
}

string lerString(string campo)
{
	string valor;
	cout << "\nDigite " << campo << ": ";
	cin >> valor;

	return valor;
}

void printPessoa(Pessoa pessoa)
{
	cout << "\nIdade = " << pessoa.idade << endl;
	cout << "CPF = " << pessoa.cpf << endl;
	if (pessoa.sexo == 1)
	{
		cout << "Pessoa do sexo feminino!\n";
		if (pessoa.esta_gravida == true)
		{
			cout << "Está grávida!\n";
		}
		else
		{
			cout << "Não está grávida!\n";
		}
	}
	else
	{
		cout << "Pessoa do sexo masculino!\n";
	}
}
