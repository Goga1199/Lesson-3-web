## Урок 3. GraphQL и микросервисная архитектура

### Задание

Добавьте отдельный сервис позволяющий хранить информацию о товарах на складе/магазине. Реализуйте к нему доступ посредством API и GraphQL.
Реализуйте API-Gateway для API сервиса склада и API-сервиса из второй лекции.

### Решение

- Решение разделено на 4 проекта:
	- CSharpWebApplication – оригинальный проект, в котором реализован API работы с продуктами и категориями.
	- SharedModels для хранения общих моделей базы данных и её контекста. В этот проект перенесена соответсвующая часть из CSharpWebApplication.
	- ProductStorageAPI – новый проект, в котором реализован API работы с распределением продуктов на складах.
	- Gateway – проект API Gateway.
- Все части решения используют общую БД. Строка подключения настраивается в appsettings.json отдельно для CSharpWebApplication и ProductStorageAPI.
- CSharpWebApplication и ProductStorageAPI запускаются на разных портах. Там и там работает Swagger.
- Gateway объединяет API из разных проектов, запускается через порт 7201.
- Для проекта ProductStorageAPI реализован доступ через GraphQL (). Общий функционал работы с БД через контроллер и GraphQL перенесен в класс ProductStorageRepository.

Пример запроса для GraphQL:

```
{
  storages{
    id,
    name,
    description
  }
}
```

Пример мутации для GraphQL:

```
mutation addStorage{
  addStorage(input: {
    name: "GraphQL склад",
    description : "Склад создан через GraphQL"
  })
  {
    storage{
      id,
      name,
      description
    }
  }
}
```
	
