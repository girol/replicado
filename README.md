## Replicado

Biblioteca PHP que abstrai o acesso aos dados do replicado USP, 
isto é, ao invés de inserir uma consulta SQL diretamente em seu código, 
como por exemplo: 

    SELECT codpes,nompes,... FROM pessoa WHERE codpes='123'

Usa-se uma classe PHP que faz a abstração do acesso e portanto deixa 
seu código muito mais limpo e torna as consultas reutilizáveis:

    Pessoa::dump('123')

## Adicione essa lib em seu projeto PHP:

    composer require uspdev/replicado

## Biblioteca PHP usada para conexão (testado com PHP7.2):

    php-sybase

## Para testar:

```php
    <?php
    namespace Meu\Lindo\App;
    require_once __DIR__ . '/vendor/autoload.php';
    use Uspdev\Replicado\Pessoa;
    
    putenv('REPLICADO_HOST=192.168.100.89');
    putenv('REPLICADO_PORT=1498');
    putenv('REPLICADO_DATABASE=rep_dbc');
    putenv('REPLICADO_USERNAME=dbmaint_read');
    putenv('REPLICADO_PASSWORD=secret');

    $emails = Pessoa::emails('123456');
    print_r($emails);
```

## Informações sobre tabelas:

   [https://uspdigital.usp.br/replunidade](https://uspdigital.usp.br/replunidade)

## Métodos existentes:

### Classe Pessoa 

 - *dump($codpes)*: recebe codpes e retorna todos campos da tabela Pessoa para o codpes em questão
 - *nome($nome)*: recebe uma string nome e retorna os resultados para a tabela Pessoa
 - *cracha($codpes)*: recebe codpes e retorna todos campos da tabela catr_cracha para o codpes em questão 
 - *email($codpes)*: recebe codpes e retorna email de correspondência da pessoa
 - *emails($codpes)*: recebe codpes e retorna todos emails da pessoa
 - *emailusp($codpes)*: recebe codpes e retorna email usp da pessoa
 - *localiza($codpes)*: retorna vínculos ativos da pessoa -- deprecado? issue 72
 - *vinculos($codpes)*: retorna vínculos ativos da pessoa
 - *docentes($unidade)*: retorna *array* de todos os docentes ativos na unidade
 - *servidores($unidade)*: retorna *array* de todos os funcionários ativos na unidade
 - *estagiarios($unidade)*: retorna *array* de todos os estagiários ativos na unidade
 
### Classe Graduacao

 - *verifica($codpes,$unidade)*: verifica se aluno (codpes) tem matrícula ativa na graduação da unidade
 - *ativos($unidade, $strFiltro = '')*: retorna *array* de todos alunos de graduação ativos na unidade ou somente os alunos de graduação ativos que obedeçam o filtro
 - *ativosCsv($unidade)*: retorna *csv* de todos alunos de graduação ativos na unidade
 - *curso($codpes,$unidade)*: retorna os dados acadêmicos do aluno de graduação ativo na unidade
 - *nomeCurso($codcur)*: retorna o nome do curso 
 - *nomeHabilitacao($codhab, $codcur)*: retorna o nome da habilitação
 - *obterCursosHabilitacoes($unidade)*: retorna os cursos e habilitações na unidade
 - *obterDisciplinas($arrCoddis)*: recebe um *array* com o prefixo dos codigos das disciplinas e retorna *array* com todas as disciplinas na unidade
 - *nomeDisciplina($coddis)*: recebe o código da disciplina *string* e retorna *string* com o nome da disciplina
 - *programa($codpes)*: recebe o nº USP do aluno *int* e retorna *int* com o código do programa
 - *disciplinasConcluidas($codpes, $unidade)*: recebe o nº USP do aluno *int* e o código da unidade *int* e retorna *array* com os cógigos, status e créditos de todas as disciplinas concluidas pelo aluno

### Classe Posgraduacao

 - *verifica($codpes,$unidade)*: verifica se aluno (codpes) tem matrícula ativa na pós-graduação da unidade
 - *ativos($unidade)*: retorna *array* de todos alunos de pós-graduação ativos na unicade
 - *ativosCsv($unidade)*: retorna *csv* de todos alunos de pós-graduação ativos na unidade
 
 ### Classe Bempatrimoniado

 - *dump($numpat)*: recebe numpat e retorna todos campos da tabela bempatrimoniado
 
 
