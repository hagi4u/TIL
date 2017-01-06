Laravel Migration Error

```
[06-Dec-2016 06:50:31 UTC] PHP Fatal error:  Uncaught exception 'UnexpectedValueException' with message 'The stream or file "/Applications/XAMPP/xamppfiles/htdocs/App/storage/logs/laravel.log" could not be opened: failed to open stream: Permission denied' in /Applications/XAMPP/xamppfiles/htdocs/App/vendor/monolog/monolog/src/Monolog/Handler/StreamHandler.php:107
Stack trace:
#0 /Applications/XAMPP/xamppfiles/htdocs/App/vendor/monolog/monolog/src/Monolog/Handler/AbstractProcessingHandler.php(37): Monolog\Handler\StreamHandler->write(Array)
#1 /Applications/XAMPP/xamppfiles/htdocs/App/vendor/monolog/monolog/src/Monolog/Logger.php(336): Monolog\Handler\AbstractProcessingHandler->handle(Array)
#2 /Applications/XAMPP/xamppfiles/htdocs/App/vendor/monolog/monolog/src/Monolog/Logger.php(615): Monolog\Logger->addRecord(400, Object(UnexpectedValueException), Array)
#3 /Applications/XAMPP/xamppfiles/htdocs/App/vendor/laravel/framework/src/Illuminate/Log/Writer.php(202): Monolog\Logger->error(Object(UnexpectedValueException), Array)
#4 /Applications/XAMPP/xamppfil in /Applications/XAMPP/xamppfiles/htdocs/App/vendor/monolog/monolog/src/Monolog/Handler/StreamHandler.php on line 107
[06-Dec-2016 06:50:31 UTC] PHP Fatal error:  Uncaught exception 'UnexpectedValueException' with message 'The stream or file "/Applications/XAMPP/xamppfiles/htdocs/App/storage/logs/laravel.log" could not be opened: failed to open stream: Permission denied' in /Applications/XAMPP/xamppfiles/htdocs/App/vendor/monolog/monolog/src/Monolog/Handler/StreamHandler.php:107
Stack trace:
#0 /Applications/XAMPP/xamppfiles/htdocs/App/vendor/monolog/monolog/src/Monolog/Handler/AbstractProcessingHandler.php(37): Monolog\Handler\StreamHandler->write(Array)
#1 /Applications/XAMPP/xamppfiles/htdocs/App/vendor/monolog/monolog/src/Monolog/Logger.php(336): Monolog\Handler\AbstractProcessingHandler->handle(Array)
#2 /Applications/XAMPP/xamppfiles/htdocs/App/vendor/monolog/monolog/src/Monolog/Logger.php(615): Monolog\Logger->addRecord(400, Object(Symfony\Component\Debug\Exception\FatalErrorException), Array)
#3 /Applications/XAMPP/xamppfiles/htdocs/App/vendor/laravel/framework/src/Illuminate/Log/Writer.php(202): Monolog\Logger->error(Object(Symfony\Component\Debug\Exception\Fa in /Applications/XAMPP/xamppfiles/htdocs/App/vendor/monolog/monolog/src/Monolog/Handler/StreamHandler.php on line 107
```

아래와 같은 오류 발생 시에는

```
chmod -R 777 storage
chmod -R 777 vendor
```

storage, vendor 폴더의 mod를 777로 지정