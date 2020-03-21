# FileSqlLoggerBundle
This bundle provides service witch implements SQLLogger interface. With this service you can log all mutating queries (Insert, Update and Delete) of Doctine.

## Installation
```
composer require php-programmist/file-sql-logger-bundle
```

## Usage
```
//src/Controller/SomeController.php
namespace App\Controller;

use PhpProgrammist\FileSqlLoggerBundle\FileSqlLogger;
use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;

class SomeController extends AbstractController
{
    public function index(FileSqlLogger $sql_logger)
    {
        $connection = $this->getDoctrine()->getConnection();
        $connection->getConfiguration()->setSQLLogger($sql_logger);
        $em = $this->getDoctrine()->getManager();
        //make queries for some entities and change it
        $em->flush();
        ...
    }
}
```
## Configuration
By default log will be written to folder /sql/. You can change folder via configuration.

Create file config/packages/file_sql_logger.yaml:
```
file_sql_logger:
    path_to_logs: '%kernel.project_dir%/sql/'
```