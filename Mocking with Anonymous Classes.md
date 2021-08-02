---
date: 2021-08-01
title: Mocking with Anonymous Classes 
slug: /coding/unit-testing/mocking-with-anonymous-classes
aliases: []
---

%%
Relates to: [[61.04.11 UnitTesting]]
%%

Most classes that you test have at least some dependencies, no matter how mush you adhere to the [[SOLID Principles]]. If you know what you're doing, you will most likely define those dependencies in the `constructor`, since your class is unable to function without them.

In [[Symfony]], this will also enable auto-wiring of your dependencies.

## Code example

Let's say for the sake of argument that you're writing a `UserAuthenticator` which, given username and password, retrieves a `User` entity from the database and outputs a log message. This class could look like this:

```php
class UserAuthenticator
{
	public function __construct(UserRepository $userRepository, LoggerInterface $logger) {
		$this->userRepository = $userRepository;
		$this->logger = $logger;
	}
	
	public function authenticate($username, $password) {
		$user = $this->userRepository->getByUsernameAndPassword($username, $password);
		$this->logger->info('Authenticated user ' . $username . '.');
	}
}
```

One way to test this is to set up a test database and actually populate it with fixture data, but the other — and quicker (and more elegant) — solution is mocking the repository class.

Symfony gives you access to a `MockBuilder`, which makes this fairly easy, but there's a quicker (and less resource intensive) way: anonymous classes.

### Replace concrete class by interface

First, we replace the concrete implementation (`UserRepository`) by an interface which provides access to the same `public` functions:

```php
interface UserRepositoryInterface {
	public function getByUsernameAndPassword(string $username, string $password): ?User;
}
```

Make the class implement that interface:

```php
class UserRepository implements UserRepositoryInterface {}
```

And replace the type-hinting in the `UserAuthenticator`:

```git
---public function __construct(UserRepository $userRepository, LoggerInterface $logger)
+++public function __construct(UserRepositoryInterface $userRepository, LoggerInterface $logger)
```

## Use anonymous class to mock

Now, when we instantiate our `UserAuthenticator` in a unit test, we can give an anonymous class that implements the same interface and provides us with some mock data:

```php
$logger = new \Psr\Log\NullLogger();
$repository = new class implements UserRepositoryInterface {
	public function getByUsernameAndPassword(string $username, string $password): ?User {
		return (new User())->setUsername($username);
	}
};

$userAuth = new UserAuthenticator($repository, $logger);
```

The added benefit is that we can make our anonymous class act the way we need it for *each individual test*. For example, if we want to test how our `UserAuthenticator` acts when it can't find a `User` object in the database, just return `null` in your anonymous class instead.