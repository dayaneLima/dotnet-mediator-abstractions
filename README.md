# D.Mediator.Abstractions

| Package | Version | Downloads |
| ------- | ------- | ------- |
| `Mediator.Abstractions` | [![Nuget](https://img.shields.io/nuget/v/D.Mediator.Abstractions.svg)](https://nuget.org/packages/D.Mediator.Abstractions) | [![Nuget](https://img.shields.io/nuget/dt/D.Mediator.Abstractions.svg)](https://nuget.org/packages/D.Mediator.Abstractions) |



Este projeto define os contratos e interfaces essenciais para implementação do padrão Mediator de forma leve e extensível.

## Objetivo

O `Mediator.Abstractions` contém apenas as abstrações que permitem desacoplar os componentes da aplicação, permitindo que diferentes implementações de Mediator possam ser utilizadas sem dependência direta de uma biblioteca específica.

## Interfaces Disponíveis

### `IMediator`

```csharp
public interface IMediator
{
    Task<TResponse> SendAsync<TResponse>(IRequest<TResponse> request, CancellationToken cancellationToken = default);
    Task PublishAsync<TNotification>(TNotification notification, CancellationToken cancellationToken = default)
        where TNotification : INotification;
}
```

### `IRequest<TResponse>`

Representa uma solicitação que retorna uma resposta.

```csharp
public interface IRequest<TResponse> { }
```

### `IRequestHandler<TRequest, TResponse>`

Manipula solicitações do tipo `IRequest<TResponse>`.

```csharp
public interface IRequestHandler<in TRequest, TResponse>
    where TRequest : IRequest<TResponse>
{
    Task<TResponse> HandleAsync(TRequest request, CancellationToken cancellation = default);
}
```

### `INotification`

Representa uma notificação (sem resposta).

```csharp
public interface INotification { }
```

### `INotificationHandler<TNotification>`

Manipula notificações publicadas.

```csharp
public interface INotificationHandler<TNotification>
    where TNotification : INotification
{
    Task HandleAsync(TNotification notification, CancellationToken cancellationToken = default);
}
```

## Uso

Este pacote é geralmente referenciado por bibliotecas ou aplicações que implementam ou consomem um Mediator customizado. Ele pode ser compartilhado entre múltiplos projetos para garantir consistência e reuso de contratos.

## 📜 Licença

Este projeto está licenciado sob a [MIT License](LICENSE).
