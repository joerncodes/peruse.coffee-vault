---
title: Single Responsibility Principle
slug: /coding/solid/single-responsibility-principle
publish: true
---

> **A class should have one and only one reason to change, meaning that a class should have only one job.**

Let's take the example that I have a `Messenger` class:

```php

class Messenger extends SomeBasicMessenger {

	public function sendMessage(Message $message) {
		$result = $this->getBus()->send($message);
		$this->logResult($result);
	}
	
	protected function logResult(Result $result) {
		file_put_content(__DIR__ . md5(time()).'.log', $result->getMessage());
	}
	
}

```

The problem with is, of course, is the fact that the class handles both *sending a message* and *logging the result of the message*. It is far better practice to [[Dependency Injection|dependency inject]] a dedicated `Logger` and delegate the logging to that class.

Let's say the `Logger` class writes into a log file on the server disk, as in the example. If multiple classes use that `Logger` class, I can decide to store the logs in the database instead and have all logging classes implement that behaviour.