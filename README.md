# php artisan model:list
## laravel-list-models-command

BY DANIEL GUEVARA 

this code allow you to use 
```
php artisan model:list
```

this will show all the models you got in the app

FIRST -> create the command file with this tag

```
php artisan make:command ListModels
```

THEN COPY PASTE

```PHP
<?php

namespace App\Console\Commands;

use Illuminate\Console\Command;
use Illuminate\Support\Facades\File;

class listModelsCommand extends Command
{
    protected $signature = 'models:list';
    protected $description = 'List all models in the application';

    public function handle()
    {
        $modelsPath = app_path('Models');
        $models = File::files($modelsPath);

        $modelNames = array_map(function ($file) {
            return pathinfo($file)['filename'];
        }, $models);

        $this->line(' -- THESE ARE THE MODELS INSIDE THE APP -- ');
        $this->line(str_repeat('-', 40));

        $number = 1;
        foreach ($modelNames as $modelName) {
            $this->line('     ' . str_pad($number, 2, '0', STR_PAD_LEFT) . ' -> ' . "<fg=yellow>" . $modelName . "</>");
            $number++;
        }

        // Print footer
        $this->line(str_repeat('-', 40));
    }

}

```
