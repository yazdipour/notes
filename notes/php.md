# PHP

`php -S localhost:8000`

## Xampp Docker

https://github.com/fuhrysteve/php-docker-apache-example

## Crawling

```php
Set Conent of Url in $res: $res=file_get_contents('url');

Will paste $res content in new address: file_put_contents('newaddress',$res)

Html Parsing:

$url = 'https://somedomain.com/somesite/';
$content = file_get_contents($url);
$first_step = explode( '<div id="thediv">' , $content );
$second_step = explode("</div>" , $first_step[1] );
echo $second_step[0];
```