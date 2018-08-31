to do:

Function resolution without the backslash forces the PHP internals to verify for each function call if function or constant belongs to current namespace or the global namespace. With the backslash PHP does not check the current namespace and therefore execution is faster when using OP Cache.

http://php.net/manual/en/language.namespaces.rules.php
https://veewee.github.io/blog/optimizing-php-performance-by-fq-function-calls/
https://github.com/nilportugues/php-backslasher
