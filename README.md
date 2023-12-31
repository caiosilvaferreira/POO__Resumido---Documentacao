# POO

---

# O que é POO ?

Orientação a objetos é composto propriedades, métodos e eventos.

propriedades são as caracteristicas.

metodos é as ações do objeto

eventos são gatilhos iniciais e que influencia tbm nas ações dependendo dos eventos

---

# classe e objeto diferenças

![Untitled](POO%20a4b31c7554974d1ba7e69cc8630b8e42/Untitled.png)

---

# ENCAPSULAMENTO

ele esconde a classe e encapsula tudo oq estiver dentro

```csharp
class Pagamento
{
// propriedades 
DateTime Vencimento;      // TODO CONTEXTO É ENCAPSULAMENTO

//Métodos
void Pagar() {}

}
```

---

# ABSTRAÇÃO

ele esconde os detalhes para o cliente e deixa em método privado, deixa somente o necessario

```csharp
class Pagamento
{
// propriedades 
DateTime Vencimento;

//Métodos
void Pagar() {}
}

private void ConsultarSaldoDoCartao(){    //ABSTRAÇÃO

}

```

---

# HERANÇA

ele tras para outra classe toda propriedade e metodos sendo publica ou privada

```csharp
class Pagamento      //CLASSE BASE OU PAI
{
// propriedades 
public DateTime Vencimento;

//Métodos
public void Pagar() {}
}

class PagamentoBoleto : Pagamento        //HERANÇA, CLASSE FILHA
{
public DateTime Vencimento;

public void Pagar() {}

}

```

---

# POLIMORFISMO

ele e criado para ter varias formas e dentro da classe

```csharp
class Pagamento      
{
// propriedades 
public DateTime Vencimento;

//Métodos
public virtual void Pagar() {}
}

class PagamentoBoleto : Pagamento        
{
public DateTime Vencimento;

pulic overrride void pagar(){           //POLIMORFISMO
//regra de pagamento
}

}
class PagamentoCartao 
{
public string Numero;

pulic overrride void pagar(){           //POLIMORFISMO
//regra de pagamento
}

}
```

---

# MODIFICADORES DE ACESSO

exemplos de modificadores de acessos

```csharp
// private, protected, internal e public 

class Pagamento      
{
// propriedades 
private DateTime Vencimento;   // não vamos conseguir acessar essas propriedades em outras classes, esta privada

//Métodos
private void Pagar() {}
}

----------------------------------------------------------------------------------------------------------------------------------------------

class Pagamento      
{
// propriedades 
protected DateTime Vencimento;            // esta em modo protegido, somente a classe filho tem acesso

//Métodos
private void Pagar() {}
}

class PagamentoBoleto : Pagamento        
{
			void Test() {
							base.vencimento          // essa é a forma de acessar a propriedade da classe protegida
				}

}

-------------------------------------------------------------------------------------------------------------------------------------------------

internal class Pagamento {  // internal fica disponivel para todo o namespace 

        protected DateTime Vencimento;

        private void pagar() { }
    }

    public class PagamentoBoleto : Pagamento {

        void Test() {

            base.Vencimento;
            
        }
    }

-------------------------------------------------------------------------------------------------------------------------------------------------

internal class Pagamento {

        protected DateTime Vencimento;

        private void pagar() { }
    }

    public class PagamentoBoleto : Pagamento {      // public fica disponivel para todos

        void Test() {

            base.Vencimento;
            
        }
    }

```

---

# TIPOS COMPLEXOS

quando criado uma classe ela vira um tipo, mas diferentemente do tipo primitivo, ela é um tipo complexo. structs, datetime e class, sao tipos complexos.

---

# PROPRIEDADES

prop+tab+tab = cria uma propriedade padrao :

```csharp
public int teste { get; set; }

```

propfull+ tab = cria uma propriedade com disponibilidade de interação, esse e o metodo de propriedade menos usado.

```csharp
private int myVar;

	public DateTime DataPagamento{
		get { return _dataPagamento;
				console.writeLine("Lendo valor");

 }  // aqui ele permite que antes de obter ou ler o valor a gente possa interagir com a variavel ou propriedades
		set { _dataPagamento= value; } // value é uma palavra reservada que é transmitido todo valor para essa variavel
console.writeLine("atribuindo valor");
	}

```

a diferença de uma propriedade para uma variavel, é que a variavel ela depende do desenvolvedor setar um valor, ja a propriedade ele tem o get e set para leitura e modificação da propriedade.

propG + tab = propriedade somente para leitura, modificação fica privada, usado muito em dominios ricos

```csharp
public int MyProperty { get; private set; }

```

```csharp
public int teste { get; set; }  // get e set são os acessores, voce pode atribuir ou receber valores

```

---

# Métodos

ele disse um pouco sobre sobrecarg, que os nomes dos metodos sao iguals (Pagar) mas as assinaturas são diferentes

```csharp
public void Pagar(string numero) { }

public void Pagar(string numero, DateTime vencimento) { }

```

metodo construtor é usado normalmente quando instanciamos um objeto, outros detalhes tem la no curso do nelio que fiz as anotações

---

# Using e dispose

o que foi realizado nesse codigo é o processo de pagamento e depois a exclusão do processo, normalmente esse metodo é usado quando uma classe conecta no banco de dados e depois do uso, ele excluir a conexão quando o usuario sai do app ou site

codigo principal

```csharp
namespace testecurso_balta {
    internal class Program {
        static void Main(string[] args) {
            Console.WriteLine("Hello, World!");

            var pagamento = new Pagamento();
            pagamento.Dispose();
        }

    }

}

OU
namespace testecurso_balta {
    internal class Program {
        static void Main(string[] args) {
            Console.WriteLine("Hello, World!");

            using (var pagamento = new Pagamento()) {
                Console.WriteLine("processando pagamento");  // ESSE METODO É MAIS USADO E NÃO NECESSITA DO DESENVOLVEDOR CHAMAR O ATRIBUTO PARA SER DELETADO

            }
        }

    }

}

```

classe pagamento

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace testecurso_balta {
    public class Pagamento : IDisposable {   // quando usamos o Ctrl + . , ele gera a implementação para ser exluida

            public Pagamento() {
                Console.WriteLine("iniciando pagamento");
            }
            public void Dispose() {
                Console.WriteLine("finalizando pagamento");
            }
        }
    }

```

---

# CLASSES ESTATICAS

quando colocamos uma classe estatica, nao conseguirmos fazer uma instanciação do jeito normal

igual este : var pagamento = new Pagamento(). este seria o jeito certo de instanciar.

quando transformamos uma classe em estatica todo o restante tem que ser estatico tambem, tanto metodos e propriedades, e muda a fora de instanciação

```csharp
namespace testecurso_balta {
    internal class Program {
        static void Main(string[] args) {
            Console.WriteLine("Hello, World!");

            Pagamento.Vencimento = DateTime.Now;    <<<<<<<<<
        }

    }

}

namespace testecurso_balta {
    public static class Pagamento  {  // classe estatica

            public static DateTime Vencimento { get; set; }
    }

        }

```

o estatico é usado quando a aplicação é uma regra que nunca vai mudar dentro da empresa, agora quando for uma classe mais flexivel por exemplo o metodo de pagamento as vezes pode mudar então seria bom nao usar o estatico. esse metodo estatico é usado raramente, so usada quando realmente tem certeza que tem uma regra fixa que geralmente nao muda.

---

# CLASSES SELADAS

normalmente isso é usado pra garantir que aquela classe tenha somente uma forma de funcionar fixa

```csharp
namespace testecurso_balta {
    public sealed class Pagamento  {  // aqui ele sela a classe para nunca ser usada por ninguem

            public static DateTime Vencimento { get; set; }
    }

    public class PagamentoBoleto : Pagamento { // fiz um teste na herança, mas deu erro pra pegar os mesmo atributos

    }

}

```

---

# PARTIAL CLASS

ARQUIVO CLASSE PAYMENT

```csharp
namespace payment {
    public class Payment {
    }
}

```

ARQUIVO CLASSE CREDITCARDPAYMENT

```csharp
namespace payment {
    public partial class Payment {
    }
}

```

o intuito do partial class, é que sua classe caso seja muito grande, ela pode ser partilhada em outro arquivo e somente colocamos o partial para que o sistema indentifique

---

# INTERFACES

a interface é usado normalmente por senior ou pleno, para que seja dirigida a regra de negocio de como funciona uma classe ou aplicação do sistema, é como se fosse um contrato. ela não é usada normalmente igual uma classe para implementar algo, somente em um cenario bem especifico

```csharp
public interface IPagamento {

         DateTime Vencimento { get; set; }     // isso seria uma regra de negocio da interface e das classes

         void Pagar(double valor);

    }

```

usando herança com interface

quando usamos o ctrl + . ele implementa uma interface com os atributos

```csharp

```

![POO%20a4b31c7554974d1ba7e69cc8630b8e42/Untitled%201.png](POO%20a4b31c7554974d1ba7e69cc8630b8e42/Untitled%201.png)

RESULTADO:

```csharp
public class Pagamento : IPagamento {    // ESSA CLASSE ESTA SEGUINDO A REGRA DE NEGOCIO DA INTERFACE, ATRAVES DA HERANÇA
        public DateTime Vencimento { get ; set; }

        public void Pagar(double valor) {

        }
    }
    public interface IPagamento {

         DateTime Vencimento { get; set; }

         void Pagar(double valor);

    }

```

---

# CLASSES ABSTRATAS

```csharp
namespace testecurso_balta {
    public abstract class Pagamento : IPagamento {  // essa classe é abstrata porque o pagamento é algo que nao existe fisicamente
        public DateTime Vencimento { get ; set ; } // outra coisa é que so vamos conseguir herdar ela , nao conseguimos instanciar

        public void Pagar(double valor) {

        }
    }
    public interface IPagamento {

         DateTime Vencimento { get; set; }

         void Pagar(double valor);

    }

    public class PagamentoBoleto {

        DateTime Vencimento { get; set; }
        public int dataNascimento { get; set; }

    }
}

```

---

# UPcast e Downcast

na pratica é um tipo de conversao de pai para filho na herança, o pai fica no lugar do filho ou o filho fica no lugar do pai. upcast faz com que o filho se torne pai e pegue suas propriedades, e downcast o pai se torne filho tbm pegando suas propriedades

OBS: nao tem como fazer casting de filho para filho

```csharp
using System.Security.Cryptography.X509Certificates;

namespace testecurso_balta {
    public class Program {
        public void Main(string[] args) {
            Console.WriteLine("Hello, World!");

            var person = new Person();
            var personal = new Personal();
            var corporate = new Corporate();

            person = new Person();    //  aqui ele faz um upcast
            person = new Corporate();

            personal = (Personal)person;  // aqui ele faz um dowcast

        }

    }

    public class Person {
        public string Name { get; set; }

    }

    public class Personal : Person {
        public string CPF { get; set; }

    }

    public class Corporate : Person {
        public string CNPJ { get; set; }
    }

}

```

---

# COMPARANDO OBJETOS

o equals compara os valores da variavel, se caso eu colocasse igual ==, ele iria comparar o endereço da onde esta armazednado os objetos, ai sempre daria diferentes, mesmo o valores sendo iguais.

```csharp
Console.WriteLine("Hello, World!");

    var pessoaA = new Person(1,"CAIO DA SILVA");
    var pessoaB = new Person(1,"CAIO DA SILVA");
    Console.WriteLine(pessoaA.Equals(pessoaB));

    public class Person : IEquatable<Person>
    {
    public Person(int id,string name) {
        Id=id;
        Name = name;

    }
    public int Id { get; set; }
    public string Name { get; set; }

    public bool Equals(Person person) {
        return Id == person.Id;
    }
}

```

---

# DELEGATES

Em outras palavras, um delegate é uma referência a um método que pode ser atribuído a uma variável, passado como argumento para outro método ou retornado por um método. Isso permite que você escreva código que seja mais flexível e extensível, permitindo que os métodos sejam tratados como objetos de primeira classe.

```csharp
static void RealizarPagamento(double valor) { // tem que ter os mesmos tipos

    Console.WriteLine($"pago o valor de {valor}");
}

var pagar = new Pagamento.Pagar(RealizarPagamento);
pagar(25);

public class Pagamento {

    public delegate void Pagar(double valor); // tem que ter os mesmos tipos
}

```

---

# EVENTS

eventos normalmente são usados em conjuntos com delegates, por isso o balta ensinou delegates primeiro

rodar o codigo para poder entender como é realizado um event no codigo, e tbm se caso quiser verificar no chatgpt

```csharp
using System.Security.Cryptography.X509Certificates;

var room = new Room(3);
room.RoomSoldOutEvent += OnRoomSoldOut;
room.ReserveSeat();
room.ReserveSeat();
room.ReserveSeat();
room.ReserveSeat();
room.ReserveSeat();
room.ReserveSeat();

static void OnRoomSoldOut(object sender, EventArgs e) {

    Console.WriteLine("sala lotada");
}

public class Room {
    public Room(int seats) {
        Seats= seats;
        seatsInUse=0;
    }
    private int seatsInUse = 0;

    public int Seats { get; set; }

    public void ReserveSeat() {

        seatsInUse++;
        if(seatsInUse >= Seats) {

            OnRoomSoldOut(EventArgs.Empty);
        }
        else {
            Console.WriteLine("Assento reservado");

        }

    }
    public event EventHandler RoomSoldOutEvent;

    protected virtual void OnRoomSoldOut(EventArgs e) {

        EventHandler handler = RoomSoldOutEvent;
        handler?.Invoke(this, e);
    }
}

```

---

# Generics

codigo de 3 tipos genericos se caso quiser entender melhor consultar o chatgpt

```csharp
var person = new Person();
var payments = new Payments();
var subscription = new Subscription();
var context = new DataContext<IPerson, Payments, Subscription>(); // aceita interface tbm
context.Save(person); // so vai aceitar desta forma com tipo generico, igual o person la em cima
context.Save(payments);
context.Save(subscription);
public class DataContext<P, PA, S>

    where P : IPerson    // aqui ele mostra aonde o deve ser linkado cada classe em cada tipo generico
    where PA : Payments     // funciona ate com interfaces
    where S: Subscription {  // classe que salva no banco de dados quando nomeado dessa forma
    // quando colocado com esses simbolos <> ele transforma a variavel no tipo generico, ele transformou em 3 tipos genericos nesse caso T,U e V

    public void Save(P entity) { // entity aqui vira um tipo generico

    }
    public void Save(PA entity) { // entity aqui vira um tipo generico

    }

    public void Save(S entity) { // entity aqui vira um tipo generico

    }
}

public interface IPerson {

}

public class Person : IPerson {  // aqui eu tiver que realizar a herança para que nao desse erro nos tipos genericos e person fica pertencente a interface IPerson
                              // como nao tem nenhum contrato na interface nao vai ter nenhuma diferença

}

public class Payments {

}

public class Subscription {

}

```

---

# LIST

criando uma nova lista basica

```csharp

using System.Collections.Generic;
using System.Data.SqlTypes;

var payments = new ICollection<Payment>();
var payments = new IEnumerable<Payment>();
var payments = new List<Payment>();

public class Payment {

}

```

jeito certo de instancia uma interface com lista

```csharp
using System.Collections.Generic;
using System.Data.SqlTypes;

IEnumerable<Payment>  payments = new List<Payment>();

public class Payment {

}

```

usado bastante em list

```csharp
IList<Payment>  payments = new List<Payment>();
payments.Add(new Payment());    // adicionar
payments.Remove(new Payment());  // remover

public class Payment {

}

```
