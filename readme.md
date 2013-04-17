# Laravel 4 Vagrant

This is a quick configuration base for setting up [Vagrant](http://www.vagrantup.com/) to support a site that uses [Laravel 4](http://laravel.com/) as it's base.

## Prerequisites

First you need to [install Vagrant](http://docs.vagrantup.com/v2/installation/) and [VirtualBox](https://www.virtualbox.org/wiki/Downloads)

Once both Vagrand and VirtualBox are installed, just add the `Vagrant` and `bootstrap.php` files from this repository into the root folder of your project.

## Laravel development environment

Keen observers will note that the artisan migrate and db seeding are being done with the flag `--env=development`. This lets laravel know that you want to use the development version of configuration files etc. To support this, you'll need to make a folder inside your `app/config` folder called `development` and add a copy of your `database.php` file in there (at least, you can add any other config files in there, and Laravel will use these instead of config files of the same name in the base config folder)

You'll also need to make one more change to make sure that when you're using the app via the browser, Laravel knows to use the development configs. In your /bootstrap/start.php, modify the $env variable to include a new element in the array like this:

```
'development'   => array('precise32'),
```

This tells Laravel to use the development configuration when the machine with name `precise32` is being used, which is what we named the box in the Vagrant file.

## Firing it up

Once you've installed everything and setup your Laravel app to support the development configs, simply run `vagrant up` from your command line... give it a few minutes and you should be able to point your browser to localhost:8080 and see your project up and running.

### Important
Be sure to read the [Vagrant docs](http://docs.vagrantup.com/v2/) on maintaining, rebooting, and destroying your environment.

## Unit testing

The bootstrap.sh template installs PHPUnit, so you can ssh into the vagrant box and run phpunit like this

```
vagrant ssh
phpunit
```
