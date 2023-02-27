Quando registramos serviços em um container (framework), precisamos definir o tempo de vida que queremos usar para este serviço. O tempo de vida do serviço controla por quanto tempo um objeto vai existir após ter sido criado pelo container. O tempo de vida pode ser definido usando o método de extensão apropriado no **IServiceCollection** ao registrar o serviço.

## Tipos de registros de serviços

### Transient

Os serviços são criados cada vez que são solicitados. Cada vez que você injetar o serviço em uma classe, será criada uma nova instância do serviço. É indicado para serviços leves e sem estado ( ou quando não temos certeza de que tipo de registro usar). 

São registrados usando o método `AddTransient`.

### Scoped

Os serviços são criados em cada solicitação (uma vez por solicitação do cliente). É indicado para aplicações WEB. Se, durante um request, você usar a mesma injeção de dependência em muitos lugares, você vai usar a mesma instância do objetos, e ele fará referência à mesma alocação de memória.

São registrados usando o método `AddScoped`.

### Singleton

Os serviços são criados uma vez durante a vida útil do aplicativo, que usa a mesma instância para todo o aplicativo. 

São registrados usando o método `AddSingleton`.
