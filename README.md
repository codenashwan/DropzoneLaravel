# DropzoneLaravel
![1](https://user-images.githubusercontent.com/35005761/207071923-bc8f0ca1-f1a1-44e4-8b35-9a9440bd5c4b.jpg)



**Laravel Drag and Drop File/Image Upload using Dropzone JS**
Source: [https://www.tutsmake.com/laravel-8-drag-and-drop-file-upload-using-dropzone-tutorial/](https://www.tutsmake.com/laravel-8-drag-and-drop-file-upload-using-dropzone-tutorial/)

- Step 1 – Download Laravel Application
- Step 2 – Setup Database with App
- Step 3 – Create Model & Migration
- Step 4 – Create Routes
- Step 5 – Generate Controller By Artisan Command
- Step 6 – Create Blade View



**Step 1 – Download Laravel 8 Application**
`composer create-project --prefer-dist laravel/laravel LaravelImage`
**Step 2 – Setup Database with App**
**Step 3 – Create Model & Migration**
`php artisan make:model Photo -m`
**Step 4 – Create Routes**
```
Route::get('dropzone', [DropzoneController::class, 'dropzone']);
Route::post('dropzone/store', [DropzoneController::class, 'dropzoneStore'])->name('dropzone.store');

```
**Step 5 – Generate Controller By Artisan Command**
`php artisan make:controller DropzoneController
`

```
<?php
namespace App\Http\Controllers;
use Illuminate\Http\Request;
    
class DropzoneController extends Controller{
    
    public function dropzone(){
        return view('dropzone-view');
    }     

    public function dropzoneStore(Request $request){
        $image = $request->file('file');
    
        $imageName = time().'.'.$image->extension();
        $image->move(public_path('images'),$imageName);
    
        return response()->json(['success'=>$imageName]);
    }
    
}
```
**Step 6 – Create Blade View**
```
<!DOCTYPE html>
<html>
<head>
    <meta name="csrf-token" content="{{ csrf_token() }}" />
    <script src="https://unpkg.com/dropzone@5/dist/min/dropzone.min.js"></script>
    <link rel="stylesheet" href="https://unpkg.com/dropzone@5/dist/min/dropzone.min.css" type="text/css" />
</head>
<body>
   
<form action="{{ route('dropzone.store') }}" method="post" enctype="multipart/form-data" id="image-upload" class="dropzone">
                @csrf
                <div>
                    <h3>Upload Multiple Image By Click On Box</h3>
                </div>
            </form>
   
<script type="text/javascript">
        Dropzone.autoDiscover = false;
            var dropzone = new Dropzone('#openFolderModal', {
                maxFilesize: 10000000,
                acceptedFiles: ".jpeg,.jpg,.png,.gif,.svg,.webp,.pdf,.mp3,.mp4,application/pdf",
            });
</script>
</body>
</html>
```
