# rtf-html-php (Fork)

_An RTF to HTML converter in PHP_

> **Este repositório é um fork de [henck/rtf-html-php](https://github.com/henck/rtf-html-php)**, mantido por [Alexandre Teixeira Mendes](https://github.com/mendesalexandre) com correções de bugs e melhorias de estabilidade.

## Correções aplicadas neste fork

- **Bug critico no parser**: condição duplicada `'{' || '{'` corrigida para `'{' || '}'` no skip de caracteres Unicode
- **Bounds check na color table**: evita fatal error com RTFs malformados
- **Vazamento de state entre documentos**: limpa `fonttbl`/`colortbl` estáticas ao formatar um novo documento
- **Propriedade `$href` declarada explicitamente** na classe `State` (compatibilidade PHP 8+)
- **Check de background color**: adicionado `array_key_exists()` para evitar warnings
- **Imagens binárias**: tratamento de binary data em vez de retorno vazio silencioso
- **Nome de classe no teste**: `FontFamilyTestTest` corrigido para `FontFamilyTest`
- **PHPUnit atualizado**: de `^8` para `^9.0|^10.0` (compatível com PHP 8+)

## Instalação

Para usar este fork via Composer, adicione ao seu `composer.json`:

```json
{
  "repositories": [
    {
      "type": "vcs",
      "url": "https://github.com/mendesalexandre/rtf-html-php"
    }
  ],
  "require": {
    "henck/rtf-html-php": "dev-master"
  }
}
```

Depois rode:

```shell
composer update
```

## Como usar

```php
use RtfHtmlPhp\Document;
use RtfHtmlPhp\Html\HtmlFormatter;

$rtf = file_get_contents("documento.rtf");
$document = new Document($rtf);

$formatter = new HtmlFormatter('UTF-8');
$html = $formatter->Format($document);
```

`Document` lança uma exception se o RTF não puder ser parseado.

Para debug do parse tree:

```php
echo $document;
```

### Encoding

Por padrão o encoding é `HTML-ENTITIES`. Para usar UTF-8:

```php
$formatter = new HtmlFormatter('UTF-8');
```

Qualquer encoding suportado por `mb_list_encodings()` pode ser usado.

## Requisitos

- PHP ^8.0
- Extensão `php-mbstring`

## Testes

```shell
composer test
```

## Licença

Este projeto é licenciado sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para detalhes.

## Créditos

Projeto original por [Alexander van Oostenrijk](https://github.com/henck) - [henck/rtf-html-php](https://github.com/henck/rtf-html-php).
