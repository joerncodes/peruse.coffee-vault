---
date: 2021-07-16
title: Chain of Responsibility Pattern in Symfony 
aliases: []
slug: /coding/symfony/chain-of-responsibility-pattern
---

Here's how to create classes adhering to the Chain of Responsibility pattern in [[Symfony]].

## Create and tag interface classes

First, create an interface:

```php
interface FiletypeHandlerInterface {
	public function getApplicableFiletypes(): array;
	public function handleFile(File $file);
}
```

Now we also need a implementing class:

```php
class Mp3FiletypeHandler implements FiletypeHandlerInterface {
	public function getApplicableFiletypes() {
		return ['mp3'];
	}
	
	public function handleFile(File $file) {
		// code goes here
	}
	
}
```

These classes now get *tagges* in `services.yaml`:

```yaml
services:
    _instanceof:
		App\FiletypeHandler\FiletypeHandlerInterface:
			tags: ['app.filetypehandler']
```

## Handler class

Now we need a handler class to pass it to:

```php
class FiletypeManager {
	public function __construct(iterable $filetypeHandlers) {
		Assert::allIsInstanceOf($filetypeHandlers, FiletypeHandlerInterface::class);
		$this->filetypeHandlers = $filetypeHandlers;
	}
	
	public function handleFile(File $file) {
		foreach($this->filetypeHandlers as $filetypeHandler) {
			if(in_array($file->getFiletype(), $filetypeHandler->getApplicableFiletypes())) {
				return $filetypeHandler->handleFile($file);
			}
		}
		return null;
	}
}
```

And lastly, pass all interface instances into the constructor in `services.yaml`:

```yaml
services:
	App\FiletypeHandler\FiletypeManager:
		arguments: [!tagged app.filetypehandler]
```