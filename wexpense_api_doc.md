

Arquivo de documentação da API pública do [Wexpense](http://www.wexpense.com)
Caso tenha dúvidas técnicas, entre em contato por: *jonathan@laivon.com*

**Todos os métodos da API precisam ser chamados via post**


*Parâmetros com * são obrigatórios*



*api_key* é um parâmetro obrigatório para **todas** as chamadas. Você gera sua chave de api através de nosso painel para desenvolvedores

Todas as chamas são feitas para:

```
  www.wexpense.com/ (função desejada)
```

Todos os retornos são em formato JSON, como no exemplo:


```
{
   "success":true,
   "message":"se tiver erro ela virá aqui e o success será falso",
   "retorno1":"r1",
   "retorno2":"r2",
   "retorno3":[
      {
         "array1a":"valor1a",
         "array1b":"valor1b",
         "array1c":"valor1c"
      },
      {
         "array2a":"valor2a",
         "array2b":"valor2b",
         "array2c":"valor2c"
      }
   ]
}

```

Exemplo de requisição em JavaScript (*usando JQuery*)

```
var url = 'http://www.wexpense.com/api/v2/users/list_reports';

$.post(url, {'api_key': 'sua_api_key_para_usar_a_api', 'token': 'token_do_usuario'}, function(data) {
    if (data.success == true) {
        // tudo ocorreu bem
    } else {
        // deu algum erro na sua requisição :(
        alert(data.message);
    }
});

```
Possíveis retornos para a requisição acima

Com sucesso
```
{
    "success": true,
    "message": "",
    "reports": [{
        "id": 153,
        "name": "Agosto15",
        "user_id": 266,
        "created_at": "16 de Ago",
        "situation": 0,
        "situation_name": "Criado",
        "evaluator_id": "",
        "recipient_id": "",
        "value": 43.5,
        "value_approved": 0,
        "user": "Jonathan Silva",
        "quantity": 5
    }, {
        "id": 146,
        "name": "Julho15",
        "user_id": 266,
        "created_at": "27 de Jul",
        "situation": 0,
        "situation_name": "Criado",
        "evaluator_id": 267,
        "evaluator_name": "Heron Júnior",
        "recipient_id": "",
        "value": 29.71,
        "value_approved": 0,
        "user": "Jonathan Silva",
        "quantity": 3
    }]
}

```
Sem sucesso
```
{
    "success": false,
    "message": "Login inválido"
}
```




**Funções para uso do administrador da empresa**




/api/v2/admin/invite_new_user



Função usada para convidar um novo usuário para a empresa. Atenção! Essa função aumenta o custo da empresa dentro do Wexpense.



Parâmetros:

* api_key*

* token*

* email*




/api/v2/admin/update_business



Função usada para alterar dados da empresa



Parâmetros:

* api_key*

* token*

* name*

* site*




/api/v2/admin/remove_user



Função usada para remover um usuário da empresa



Parâmetros:

* api_key*

* token*

* id*




**Funções para controle da empresa do usuário**




/api/v2/business/delete_alert_goal



Função usada para deletar um alerta de valores



Parâmetros:

* api_key*

* token*

* id*




/api/v2/business/new_alert_goal



Função usada para gerar um alerta caso as depesas do mês ultrapassem o valor especificado



Parâmetros:

* api_key*

* token*

* percentage*

* email* (não precisa ser de um usário cadastrado na plataforma)




/api/v2/business/change_alert_goal_value



Função usada para alterar o valor da meta de gastos



Parâmetros:

* api_key*

* token*

* value*




/api/v2/business/rename



Função usada para renomear a empresa



Parâmetros:

* api_key*

* token*

* name*




**Funções para controle das despesas do usuário**




/api/v2/expenditures/count



Função usada para retornar a quantidade de depesas que um usuário possui



Parâmetros:

* api_key*

* token*




/api/v2/expenditures/create



Função usada para criar uma despesa para um usuário



Parâmetros:

* api_key*

* token*

* pricekm

* category_id (este parâmetro OU o 'category' podem ser enviados. Se for o 'category' ele pegará o id buscando pelo nome)

* category

* report_id (este parâmetro OU o 'report' podem ser enviados. Se for o 'report' ele pegará o id buscando pelo nome)

* report

* type_expenditure (0 para despesa comum e 1 para transporte)




/api/v2/expenditures/load_web



Função usada para retornar a lista de despesas do usuário



Parâmetros:

* api_key*

* token*




/api/v2/expenditures/destroy



Função usada para apagar uma depesa



Parâmetros:

* api_key*

* token*

* ids* (pode apagar mais de uma despesa, mandar no formado 'id1,id2,id3,..., idN'. Para apagar uma única, basta mandar 'id')




/api/v2/expenditures/show



Função usada para retornar os dados de uma despesa específica



Parâmetros:

* api_key*

* token*

* id*




/api/v2/expenditures/categories



Função usada para retornar a lista de categorias disponíveis



Parâmetros:

* api_key*

* token*




/api/v2/expenditures/change_status



Função usada para alterar o status de uma despesa. Somente com valor de aprovação.

O status será automático de acordo com o valor aprovado:

Caso 0: Recusado

Caso valor total da despesa ou acima: Aprovado

Caso valor menor que o da despesa: Aprovado parcialmente





Parâmetros:

* api_key*

* token*

* id*

* value_approved*




**Funções para gestão dos relatórios dos usuários**




/api/v2/report/create



Função usada para criar um novo relatório na conta do usuário



Parâmetros:

* api_key*

* token*

* title*




/api/v2/report/list



Lista os relatórios ligados ao usuário



Parâmetros:

* api_key*

* token*




/api/v2/report/approve



Função usada para aprovar uma despesa do usuário



Parâmetros:

* api_key*

* token*

* id*

* value_approved*




/api/v2/report/change_situation



Função usada para alterar a situação de um relatório



Parâmetros:

* api_key*

* token*

* id*

* situation* (0 para 'Criado', 1 para 'Aguardando Análise', 2 para 'Aguardando pagamento' ou 3 para 'Fechado')




/api/v2/report/delete



Função usada para deletar um relatório



Parâmetros:

* api_key*

* token*

* id*




/api/v2/report/rename



Função usada para renomear um relatório



Parâmetros:

* api_key*

* token*

* id*

* name*




/api/v2/report/remove_items



Função usada para remover despesas de um relatório



Parâmetros:

* api_key*

* token*

* id*

* ids* (lista de ids das depesas no formato '1,2,3,etc')




/api/v2/report/approve_all



Função usada para aprovar todas as depesas de um relatório com o valor total



Parâmetros:

* api_key*

* token*

* id*




/api/v2/report/reprove_all



Função usada para reprovar todas as depesas de um relatório com o valor total



Parâmetros:

* api_key*

* token*

* id*




/api/v2/request/create



Função usada para criar uma nova requisição na conta do usuário



Parâmetros:

* api_key*

* token*

* motive*

* value*

* date* (formato brasileiro dd/mm/aaaa)

* recipient (id do usuário gestor que avaliará a requisição. Caso não tenha, a requisição será aberta a todos os gestores)




/api/v2/request/change_situation



Função usada para alterar a situação de uma requisição



Parâmetros:

* api_key*

* token*

* id*

* situation* (0 para 'Criado', 1 para 'Aguardando Análise', 2 para 'Aguardando pagamento' ou 3 para 'Fechado')




**Funções para gestão dos usuários da empresa**




/api/v2/users/create



Função usada para criar um novo usuário.



Parâmetros:

* api_key*

* email*

* password*




/api/v2/users/change_profile



Função usada para alterar um ou mais itens do perfil do usuário



Parâmetros:

* api_key*

* token*

* name

* position

* bank

* agency

* account

* cpf

* bitcoin_wallet

* pricekm




/api/v2/users/categories



Função usada para ler a lista de categorias de despesas que são aceitas.



Parâmetros:

* api_key*




/api/v2/users/list_reports



Função usada para ler a lista de relatórios do usuário



Parâmetros:

* api_key*

* token*




