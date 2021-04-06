# Install-Laravel-Passport.

# Hello Dears,

Laravel Passport provides a full OAuth2 server implementation for your Laravel application in a matter of minutes. Passport is built on top of the League OAuth2 server that is maintained by Andy Millington and Simon Hamp.

If your application absolutely needs to support OAuth2, then you should use Laravel Passport.

Thats See How is way to implement Laravel passport.


# To get started, install Passport via the Composer package manager:
     
     composer require laravel/passport
     
# Passport's service provider registers its own database migration directory, so you should migrate your database after installing the package. 
      
     php artisan migrate

# Next, you should execute the passport:install Artisan command.
This command will create the encryption keys needed to generate secure access tokens.
      
      php artisan passport:install 
      
After running the passport:install command, add the Laravel\Passport\HasApiTokens trait to your App\Models\User model. This trait will provide a few helper methods to your model which allow you to inspect the authenticated user's token and scopes:

        <?php

        namespace App\Models;

        use Illuminate\Database\Eloquent\Factories\HasFactory;
        use Illuminate\Foundation\Auth\User as Authenticatable;
        use Illuminate\Notifications\Notifiable;
        use Laravel\Passport\HasApiTokens;

        class User extends Authenticatable
        {
            use HasApiTokens, HasFactory, Notifiable;
        }

Next, you should call the Passport::routes method within the boot method of your App\Providers\AuthServiceProvider. This method will register the routes necessary to issue access tokens and revoke access tokens, clients, and personal access tokens.

Finally, in your application's config/auth.php configuration file, you should set the driver option of the api authentication guard to passport. This will instruct your application to use Passport's TokenGuard when authenticating incoming API requests:

    'guards' => [
        'web' => [
            'driver' => 'session',
            'provider' => 'users',
        ],

      'api' => [
          'driver' => 'passport',
          'provider' => 'users',
      ],
    ],
