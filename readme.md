# Laravel Starter

1. `composer install` 

2. `cp .env.example .env`

3. `vagrant up`

:boom:* 

*Assuming you have [Vagrant] and [Composer]
** there's a bit more to do

[composer]: https://getcomposer.org/
[Vagrant]: https://vagrantup.com

## What it gets you
- Vagrant box
- Ubuntu-based [LEMP stack](https://lemp.io/)
- `vagrant_dev` database (ready for [SSH access](#connecting-to-the-sql-server))
- Fresh and current Laravel 5 (default app with inspiring quotes and basic auth)
- All the proper permissions


## Reasons
I was tied of spinning up the same environment over and over for developement, I hate Homestead and the hacky way it abuses the power of Vagrant, I wanted to bring some consistancy to [my team](http://redpepperland.com)'s projects, and I didn't like any of the existing solutions out there.

## Using
### Connecting to the SQL Server
Out of the box, you can connect to the Vagrant box's MySQL server with the following credentials:

- MySQL Host: 127.0.0.1
- Username: root
- Password: root
- Port: 3306
- SSH Host: localhost
- SSH Username: vagrant
- SSH Key: ~/.vagrant.d/insecure_private_key
- SSH Port: 2222

**On the command line:**  
`ssh -f vagrant@localhost -p 2222 -i ~/.vagrant.d/insecure_private_key -L 33060:localhost:3306 -N`

`mysql -h 127.0.0.1 -P33060 -u root -proot`

**To stop**  
`ps aux | grep 33060`

Look for the pid

`kill <pid>`


## Future
laravel-starter is intended to become the foundation for a Yeoman generator, possible serve as the first of many "starter pack" style generators.

The Vagrant box will eventually become a bit more specialized (killing off apache, etc), making the provisioning script a little less lengthy.
