# Checkpoint-3

Violação 1

Single Responsibility Principle
Classe e Método: GerenciadorBiblioteca (em quase todos os métodos, mas especialmente em RealizarEmprestimo e AdicionarUsuario).
Princípio Violado: Single Responsibility Principle.
Justificativa: A classe GerenciadorBiblioteca possui múltiplas responsabilidades: gerenciar livros, gerenciar usuários, gerenciar empréstimos, calcular multas e enviar notificações ( e-mail/SMS ). Isso viola o Single Responsibility Principle, que afirma que uma classe deve ter apenas uma razão para mudar. Se o método de envio de e-mail mudar (por exemplo, para usar um serviço diferente), a classe GerenciadorBiblioteca precisaria ser alterada, mesmo que a lógica de gerenciamento da biblioteca permaneça a mesma. O mesmo se aplica à lógica de cálculo de multa ou ao armazenamento de dados.


Violação 2

Open/Closed Principle 
Classe e Método: GerenciadorBiblioteca.RealizarEmprestimo, GerenciadorBiblioteca.AdicionarUsuario.
Princípio Violado: Open/Closed Principle.
Justificativa: Os métodos RealizarEmprestimo e AdicionarUsuario contêm lógica de notificação ( envio de e-mail e SMS ). Se uma nova forma de notificação for adicionada ( por exemplo, notificação push ), esses métodos precisarão ser modificados. O Open/Closed Principle afirma que entidades de software ( classes, módulos, funções ) devem ser abertas para extensão, mas fechadas para modificação. A inclusão direta de EnviarEmail e EnviarSMS acopla as funcionalidades de negócio com as de notificação, tornando a classe não extensível sem modificação.


Violação 3

Hardcoding e Falta de Injeção de Dependência ( Violação do DIP )
Classe e Método: GerenciadorBiblioteca ( especificamente EnviarEmail e EnviarSMS e como são chamados ).
Princípio Violado: Dependency Inversion Principle (DIP).
Justificativa: A classe GerenciadorBiblioteca depende diretamente das implementações concretas EnviarEmail e EnviarSMS. Isso viola a Dependency Inversion Principle, que afirma que módulos de alto nível não devem depender de módulos de baixo nível, ambos devem depender de abstrações. As abstrações não devem depender de detalhes; os detalhes devem depender de abstrações. Se quisermos mudar a forma como os e-mails ou SMS são enviados ( por exemplo, usar uma API de terceiros ), teríamos que modificar a classe GerenciadorBiblioteca. Idealmente, GerenciadorBiblioteca deveria depender de uma interface de serviço de notificação, e a implementação concreta seria injetada.


Violação 4

Comentários Excessivos e Redundantes (Clean Code)
Classe e Método: Em toda a classe GerenciadorBiblioteca.
Boa Prática Violada: Comentários adequados ( apenas quando necessário ) e nomes significativos.
Justificativa: O código está repleto de comentários como // Método que adiciona um livro, // Método que adiciona um usuário, // Método que realiza empréstimo. Esses comentários são redundantes, pois o nome do método já expressa claramente sua intenção. Comentários devem ser usados para explicar "porquês" complexos ou nuances que o código não pode expressar por si só, não para parafrasear o que o código já diz. Nomes claros e autoexplicativos tornam os comentários desnecessários na maioria dos casos.


Violação 5

Retorno de Valor Mágico (Clean Code)
Classe e Método: GerenciadorBiblioteca.RealizarDevolucao.
Boa Prática Violada: Tratamento adequado de erros e legibilidade.
Justificativa: O método RealizarDevolucao retorna -1 para indicar um erro ( quando o empréstimo não é encontrado ). Isso é um "número mágico" e uma má prática. Retornos de erro devem ser explícitos e significativos. Idealmente, deveria ser lançada uma exceção para indicar que o empréstimo não foi encontrado ou que a operação não pôde ser concluída. O uso de valores mágicos torna o código mais difícil de entender e manter, pois quem o utiliza precisa saber o significado específico de -1.
