# Slim Twig Translation

This repository provides a twig extension class for the twig view parser. 
The class adds a translate helper function  for the use in twig templates.
The translator function tries to call the trans() function of an 
Illuminate\Translation\Translator object in the slim DI container. 

## How to install

#### using [Composer](http://getcomposer.org/)

Create a composer.json file in your project root:
    
```json
{
    "require": {
        "abedmaatalla/slim-twig-translation": "v0.1.0"
    }
}
```

Then run the following composer command:

```bash
$ php composer.phar install
```

## How to use

Create new folder for langauges 

+
-- lang
  + -- en
      + -- file.php
  + -- fr
      + -- file.php

### Tanslator 

Set up your Tansloator 

```php
$container['translator'] = function ($c)
{
  // Register the English translator 'en'
  $translator = new Illuminate\Translation\Translator(new Illuminate\Translation\FileLoader(new Illuminate\Filesystem\Filesystem(), __DIR__ . '/lang'), 'en');
    // setLocal for new location 
    $translator->setLocale('fr');
    return $translator;
};
```

### Slim

Set up your twig views as described in the [SlimViews Repository](https://github.com/codeguy/Slim-Views).
Add the extension to your parser extensions.

```php
$container['view'] = function ($c)
{
  $view = new \Slim\Views\Twig('../resources/views');

  // add translator functions to Twig
  $view->addExtension(new \abedmaatalla\Slim\Twig\Extension\TranslationExtension($c->translator));

}
```

### Twig template

In your twig template you would write:

```
  {{ translate('male') }}
```
  
You can also use the shorthand:

```
  {{ tans('male') }}
```  

You can also use the shorthand:

```
  {{ _('male') }}
```
