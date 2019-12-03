# Laravel Nova TinyMCE editor (with images upload capabilities!)

This Nova package allow you to use [TinyMCE editor](https://tiny.cloud) for text areas. You can customize the editor options and... you can **upload images to your server** and put them right there on the text without leaving the text editor!!

## Installation

```shell
composer require emilianotisato/nova-tinymce
```

## Usage

In your Nova resource add the use declaration and use the NovaTinyMCE field:

```php
use Emilianotisato\NovaTinyMCE\NovaTinyMCE;

// ...

    /**
     * Get the fields displayed by the resource.
     *
     * @param  \Illuminate\Http\Request  $request
     * @return array
     */
    public function fields(Request $request)
    {
        return [
            ID::make()->sortable(),

            NovaTinyMCE::make('body'),
        ];
    }
```

By default, the editor comes with default options and the image without the filemanager.
You can use custome options like this:

```php
NovaTinyMCE::make('body')->options([
                'plugins' => [
                    'advlist autolink lists link image charmap print preview hr anchor pagebreak'
                ],
                'toolbar' => 'insertfile undo redo | styleselect | bold italic'
            ]),
```

### Using the upload images feature

#### Warning
In order to use image upload capabilities with TinyMCE 5, see [this issue comment](https://github.com/UniSharp/laravel-filemanager/issues/759#issuecomment-487258426).

Now if you need to upload images from the text editor, we need to install [UniSharp Laravel Filemanager](https://unisharp.github.io/laravel-filemanager/installation), and pass the `use_lfm` key to your options array:

```php
NovaTinyMCE::make('body')->options([
                'plugins' => [
                    'advlist autolink lists link image charmap print preview hr anchor pagebreak',
                    'searchreplace wordcount visualblocks visualchars code fullscreen',
                    'insertdatetime media nonbreaking save table contextmenu directionality',
                    'emoticons template paste textcolor colorpicker textpattern'
                ],
                'toolbar' => 'insertfile undo redo | styleselect | bold italic | alignleft aligncenter alignright alignjustify | bullist numlist outdent indent | link image media',
                'use_lfm' => true
                ]),
```

In case you change the `laravel-filemanager` URL in the package config file, you need to pass that info to this nova field with the `lfm_url` key in the options array.

```php
// ...
    'use_lfm' => true,
    'lfm_url' => 'laravel-filemanager'
// ...
```

### Extra configuration and plugin customization

You can virtually pass any configuration option for the javascript SDK to the array in the `options()` method.

For example, you like to have increased the height of the text area:

```php
            NovaTinyMCE::make('body')->options([
                'height' => '980'
                ]),
```

You can see the full list of parameters in the docs:
[https://www.tiny.cloud/docs/configure/](https://www.tiny.cloud/docs/configure/)
