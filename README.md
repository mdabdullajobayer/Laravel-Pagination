### 1. Basic Pagination

To paginate results from a database query, you can use the `paginate()` method provided by Eloquent.
```php
use App\Models\Post;

public function index()
{
    // Retrieve 10 posts per page
    $posts = Post::paginate(10);

    return view('posts.index', compact('posts'));
}
```
### 2. Displaying Pagination Links

In your Blade view, you can use the `links()` method to display the pagination controls:
```php
@foreach ($posts as $post)
    <h2>{{ $post->title }}</h2>
    <p>{{ $post->content }}</p>
@endforeach

{{ $posts->links() }}
```
### 3. Handle User Input in Controller or Route

Now, modify your route or controller to handle the `per_page` input from the user.
```php
// routes/web.php
use App\Models\Post;
use Illuminate\Http\Request;

Route::get('/posts', function (Request $request) {
    // Set a default value of 10 if 'per_page' is not provided
    $perPage = $request->input('per_page', 10);
    
    // Retrieve paginated posts based on user input
    $posts = Post::paginate($perPage);

    return view('posts.index', compact('posts'));
});
```
### 4. Append Query Parameters to Pagination Links

To preserve the `per_page` parameter when navigating between pages, append the parameter to the pagination links using `appends()` in the Blade view:
```php
<!-- Preserve the 'per_page' parameter when generating pagination links -->
{{ $posts->appends(['per_page' => request('per_page')])->links() }}
```
