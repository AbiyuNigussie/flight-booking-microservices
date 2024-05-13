<div align="center" style="margin-bottom:20px">
  <img src="assets/logo.png" alt="booking-microservices-nestjs" />
    <div align="center">
                       <a href="https://github.com/AbiyuNigussie/booking-microservices-nestjs/actions/workflows/ci.yml"><img src="https://github.com/AbiyuNigussie/booking-microservices-nestjs/actions/workflows/ci.yml/badge.svg?branch=main&style=flat-square"/></a>
                       <a href="https://github.com/AbiyuNigussie/booking-microservices-nestjs/blob/main/LICENSE"><img src="https://img.shields.io/github/license/AbiyuNigussie/booking-microservices-nestjs?color=%234275f5&style=flat-square"/></a>
    </div>
</div>
           
> **A practical and imaginary microservices for implementing an infrastructure for up and running distributed system with the latest technology and architecture like Vertical Slice Architecture, Event Driven Architecture, CQRS, Postgres, RabbitMq and Nestjs.** 🚀

> 💡 **This project is not business-oriented and most of my focus was in the thechnical part for implement a distributed system with a sample project. In this project I implemented some concept in microservices like Messaging, Tracing, Event Driven Architecture, Vertical Slice Architecture, CQRS.**



Instead of grouping related action methods in one controller, as found in traditional ASP.net controllers, I used the [REPR pattern](https://deviq.com/design-patterns/repr-design-pattern). Each action gets its own small endpoint, consisting of a route, the action, and an `IMediator` instance (see [MediatR](https://github.com/jbogard/MediatR)). The request is passed to the `IMediator` instance, routed through a [`Mediatr pipeline`](https://lostechies.com/jimmybogard/2014/09/09/tackling-cross-cutting-concerns-with-a-mediator-pipeline/) where custom [middleware](https://github.com/jbogard/MediatR/wiki/Behaviors) can log, validate and intercept requests. The request is then handled by a request specific `IRequestHandler` which performs business logic before returning the result.

The use of the [mediator pattern](https://dotnetcoretutorials.com/2019/04/30/the-mediator-pattern-in-net-core-part-1-whats-a-mediator/) in my controllers creates clean and [thin controllers](https://codeopinion.com/thin-controllers-cqrs-mediatr/). By separating action logic into individual handlers we support the [Single Responsibility Principle](https://en.wikipedia.org/wiki/Single_responsibility_principle) and [Don't Repeat Yourself principles](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself), this is because traditional controllers tend to become bloated with large action methods and several injected `Services` only being used by a few methods.

I used CQRS to decompose my features into small parts that makes our application:

- Maximize performance, scalability and simplicity.
- Easy to maintain and add features to. Changes only affect one command or query, avoiding breaking changes or creating side effects.
- It gives us better separation of concerns and cross-cutting concern (with help of mediatr behavior pipelines), instead of bloated service classes doing many things.

Using the CQRS pattern, we cut each business functionality into vertical slices, for each of these slices we group classes (see [technical folders structure](http://www.kamilgrzybek.com/design/feature-folders)) specific to that feature together (command, handlers, infrastructure, repository, controllers, etc). In our CQRS pattern each command/query handler is a separate slice. This is where you can reduce coupling between layers. Each handler can be a separated code unit, even copy/pasted. Thanks to that, we can tune down the specific method to not follow general conventions (e.g. use custom SQL query or even different storage). In a traditional layered architecture, when we change the core generic mechanism in one layer, it can impact all methods.

## How to Use Migrations
> Note: For easy using of migrations commands in typeorm, I add some scripts in `package.json` and base on these scripts we can use below commands to generate and run migrations easily.

For `generating` a new migration use this command in the root of each microservice:

```bash
npm run migration:generate -- src/data/migrations/new-migration-name
```

Also for `running` migration use this command in the root of each microservice:
```bash
npm run migration:run  
```

## How to Run


> ### Docker Compose

Use the command below to run our `infrastructure` with `docker` using the [infrastructure.yaml](./deployments/docker-compose/infrastructure.yaml) file at the `root` of the app:

```bash
docker-compose -f ./deployments/docker-compose/infrastructure.yaml up -d
```
##### Todo
I will add `docker-compsoe` for up and running whole app here in the next...

> ### Build
To `build` each microservice, run this command in the root directory of each microservice where the `package.json` file is located:
```bash
npm run build
```

> ### Run
To `run` each microservice, run this command in the root of the microservice where `package.json` is located:
```bash
npm run dev
```

> ### Test

To `test` each microservice, run this command in the root directory of the microservice where the `package.json` file is located:
```bash
npm test
```

> ### Documentation Apis

Each microservice has a `Swagger OpenAPI`. Browse to `/swagger` for a list of endpoints.

As part of API testing, I created the [booking.rest](./booking.rest) file which can be run with the [REST Client](https://github.com/Huachao/vscode-restclient) `VSCode plugin`.

# Support

If you like my work, feel free to:

- ⭐ this repository. And we will be happy together :)

Thanks a bunch for supporting me!

## Contribution

Thanks to all [contributors](https://github.com/AbiyuNigussie/booking-microservices-nestjs/graphs/contributors), you're awesome and this wouldn't be possible without you! The goal is to build a categorized, community-driven collection of very well-known resources.

Please follow this [contribution guideline](./CONTRIBUTION.md) to submit a pull request or create the issue.

## Project References & Credits

- [https://github.com/jbogard/ContosoUniversityDotNetCore-Pages](https://github.com/jbogard/ContosoUniversityDotNetCore-Pages)
- [https://github.com/nestjs](https://github.com/nestjs)


## License
This project is made available under the MIT license. See [LICENSE](https://github.com/AbiyuNigussie/booking-microservices-nestjs/blob/main/LICENSE) for details.
