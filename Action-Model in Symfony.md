---
date: 2021-04-14
title: Action-Model in Symfony 
slug: /coding/symfony/action-model
tags:
---

Controller-Klassen in Symfony verletzen sehr häufig das [[Single Responsibility Principle]]. Um hier Abhilfe zu schaffen, gibt es das Action-Model, in welchem jede Aktion, die auf einer Website denkbar ist (Login, neuen Benutzer anlegen, einen Tag anzeigen...) eine eigene Action-Klasse zugewiesen wird.

## Voraussetzungen

Anpassung der `config/routes/annotations.yaml`:

```yaml
actions:
	resource: ../../src/Action
	type: annotation
```

Anpassung der `config/services.yaml`:

```yaml
App\Action\:
	resource: '../src/Action'
	tags: ['controller.service_arguments']
```

## Anwendung

Anschließend können Action-Klassen folgendermaßen erstellt werden:

```php
# src/Action/Tags/ShowTagAction.php

namespace App\Action\Tags;

use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Routing\Annotation\Route;

final class ShowTagAction {
	
/**
 * @Route("/tags/show/{tag}", methods={"POST"})
 *
 * @return Response
 */
 public function __invoke($tag): Response {
 	// code goes here
}

```	

## Dependency Injection

Dependency Injection kann ganz normal entweder in der Methode `__invoke` übergeben werden, oder — was ich schöner finde — im Constructor.