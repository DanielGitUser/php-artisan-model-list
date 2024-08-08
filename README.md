# laravel-list-models-command

BY DANIEL GUEVARA 

this code allow you to use 
```
php artisan model:list
```
this will show all the models you got in the app


```
<?php

namespace App\Console\Commands;

use Illuminate\Console\Command;
use Illuminate\Support\Facades\File;

class listModelsCommand extends Command
{
    protected $signature = 'model:list';
    protected $description = 'List all models in the application';

    public function handle()
    {
        $modelsPath = app_path('Models');
        $models = File::files($modelsPath);

        $modelNames = array_map(function ($file) {
            return pathinfo($file)['filename'];
        }, $models);

        // Determine the number of columns
        $columns = 3;
        $rows = array_chunk($modelNames, ceil(count($modelNames) / $columns));

        // Print the header
        $this->line(' -- THIS ARE THE MODELS INSIDE THE APP -- ');
        $this->line(str_repeat('-', 15) . '|' . str_repeat('-', 15) . '|' . str_repeat('-', 15));

        // Print the model names in columns
        foreach ($rows as $row) {
            // Adjust each model name to have a fixed width
            $formattedRow = array_map(function ($name) {
                return str_pad($name, 20); // Adjust padding as necessary
            }, $row);

            // Ensure each row has three columns
            while (count($formattedRow) < $columns) {
                $formattedRow[] = ''; // Fill empty columns if necessary
            }

            $this->line(implode(' | ', $formattedRow));
        }

        // Print footer
        $this->line(str_repeat('-', 15) . '|' . str_repeat('-', 15) . '|' . str_repeat('-', 15));
    }
}

```
