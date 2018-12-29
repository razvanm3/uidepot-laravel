#Uidepot 

![Uidepot](https://i.imgur.com/UYN03jG.png)


<h3>1.What is Uidepot?</h3>


<p>Uidepot is a simple e-commerce platform based on the Laravel MVC framework. This is the pre-alpha version of the project, so don't expect a lot for the moment.</p>
<p>Uidepot offers both the user and the administrator an user friendly interface, easily usable even by those not tech savy.</p>


<h3>2.Frameworks, languages and other tools used:</h3>

<ul>
<li>HTML5</li>
<li>CSS</li>
<li>Laravel 5</li>
<li>Vue.js</li>
<li>MySQL</li>
<li>Bootstrap</li>
<li>Passport</li>
</ul>

<h3>3.How to test locally:</h3>

<h4>I.Requirements:</h4>
<ul>
<li>XAMPP installed on your computer</li>
<li>Git Bash</li>
<li>Composer</li>
<li>Operating System: Windows 7 or above</li>
</ul>

<h4>II. Installation:</h4>


<p>Copy the repository folder to <i>xampp/htdocs/</i>.</p>

<p>Go to <i>http://localhost/phpmyadmin/</i> and create a database called <i>uidepotdb</i>.</p>

<p>Import the <i>uidepotdb.sql</i> file provided in the repository.</p>

<p>Open the <i>.env</i> file from the root folder and add your database credentials:</p>

```shell
    DB_CONNECTION=mysql
    DB_HOST=127.0.0.1
    DB_PORT=3306
    DB_DATABASE=uidepotdb
    DB_USERNAME=root
    DB_PASSWORD=
```
<p>Open Git Bash from the root folder and run the following commands:</p>

```shell
    composer install
```
```shell
    npm install
```
```shell
    npm install vue-router
```
<p>Install passport:</p>

```shell
    composer require laravel/passport
```

<p>Generate a key for the application:</p>

```shell
    php artisan key:generate
```

<p>Now you can access the project at <i>http://localhost/uidepot/</i>.</p>


<h3>4.Creator:</h3>
<h4>Razvan Mihai</h4>