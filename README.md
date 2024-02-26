# Ficha de Programação e Sistemas de Informação - Módulo 11

Cria um repositório **privado** no GitHub com o nome **"PSI_Ficha_M11"** e com um ficheiro **README**. Faz ***clone*** do mesmo para o teu computador.

Preenche o **README** localmente com as respostas dos exercícios, e seguidamente, faz ***push*** das atualizações.

Para entregar a ficha, acede a [este link](https://docs.google.com/spreadsheets/d/1DrdGnICVAA8q9bs9_LAURFKoReAO7jJGB8qqvUWacL0/edit?usp=sharing) (separador **Ficha Módulo 11**), e mete o **URL** do teu repositório ao lado do teu nome.
No teu repositório, acede a "Settings -> Collaborators" e adiciona o utilizador "Manuel Geraldes" para ter acesso.

## Exercício 1 - Para cada afirmação sobre tratamento de erros em C#, indica se é **Verdadeira** ou **Falsa**. Justifica a tua resposta. (3v)

1. Exceções são usadas para lidar com situações inesperadas que podem ocorrer durante a execução de um programa.
  Verdadeira. As exceções permitem que um programa lide com erros de forma estruturada e evite que o programa pare abruptamente.
2. O bloco 'try' é usado para prevenir uma exceção.
  Falsa. Na verdade, o bloco 'try' é usado para envolver o código que pode lançar uma exceção, permitindo que o programa capture e lide com essa exceção de forma apropriada
3. Um bloco 'catch' tem de ser sempre usado imediatamente depois de um bloco 'try'.
  Falsa. Pode haver um bloco 'finally' entre o 'try' e o 'catch', ou pode não haver um bloco 'catch' se não for necessário lidar com a exceção.
4. O bloco 'finally' é sempre executado antes do bloco 'catch', mesmo que uma exceção não seja lançada ou apanhada.
  Verdadeira. O bloco 'finally' é usado para garantir a execução de um código, independentemente de uma exceção ser lançada ou não.
5. É possível criar exceções customizadas.
  Verdadeira. Isso permite que os programadores criem exceções específicas para o seu código e forneçam informações personalizadas sobre o erro que ocorreu.
6. O *statement* 'using' é usado para gerir recursos apropriadamente.
  Verdadeira. O 'using' é geralmente usado para garantir que os recursos sejam libertados de forma correta, mesmo em casos de exceção.

## Exercício 2 - Para cada afirmação sobre manipulação de *streams* em C#, indica se é **Verdadeira** ou **Falsa**. Justifica a tua resposta. (4v)

1. *Streams* são unidirecionais.
Verdadeira. Streams são unidirecionais, ou seja, podemos ler ou escrever em uma stream, mas não ambas simultaneamente.
2. As classes StreamReader/StreamWriter são usadas para ler/escrever caracteres de/para uma *stream* em qualquer formato.
Verdadeira. As classes StreamReader/StreamWriter são usadas para ler/escrever caracteres de/para uma stream em qualquer formato de codificação de caracteres.
3. Uma stream pode ser fechada de forma explícita ou implícita.
Verdadeira. Uma stream pode ser fechada de forma explícita, chamando o método Close, ou de forma implícita, utilizando um bloco using para garantir que a stream seja fechada automaticamente ao sair do bloco.
4. A classe 'GZipStream' é usada tanto para comprimir como descomprimir *streams* de dados.
Verdadeira. A classe 'GZipStream' é utilizada para comprimir e descomprimir streams de dados, permitindo a compressão dos dados antes de serem escritos em uma stream ou a descompressão dos dados lidos de uma stream.

## Exercício 3 - Escreve o código necessário para criar um programa em C# de acordo com as seguintes instruções: (7v)

- O programa deve aceitar como único argumento da linha de comandos um nome de ficheiro de texto e imprimir os conteúdos desse ficheiro no ecrã.
- O programa deve tratar separadamente todas as exceções que podem ocorrer quando o ficheiro é aberto para leitura, apresentando uma mensagem de erro adequada em cada caso.

using System;

namespace LeitorDeArquivo
{
    class Program
    {
        static void Main(string[] args)
        {
            if (args.Length != 1)
            {
                Console.WriteLine("Incorreto. Insira o nome do arquivo de texto como argumento da linha de comandos.");
  try{
  String Arquiv = args[0];
               
  using (StreamReader sr = new StreamReader(Arquiv))
                {
                    string linha;
                    while (linha = sr.ReadLine() != null)
                    {
                        Console.WriteLine(linha);
                    }
                }
            }
            catch (InvalidOperationException)
            {
                Console.WriteLine($"O ficheiro '{Arquiv}' não foi encontrado.");
            }
            catch (NullReferenceException)
            {
                Console.WriteLine($"Acesso negado ao ficheiro '{Arquiv}'. Verifique as permissões.");
            }
            catch (Exception e)
            {
                Console.WriteLine($"Erro ao ler o ficheiro: {e.Message}");
            }
        }
    }
}

