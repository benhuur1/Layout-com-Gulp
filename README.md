# Layout com Gulp
 Layout de WebSite com SASS, Browser-Sinc, Bootsratp 4 & GULP

### Requisitos para montar um layout de site bootstrap, sass e gulp para criar novas paletas de cores no bootstrap e compilar tudo em tempo real

1. node.js
1. npm 
1. abrir o `CMD`
1. instalar o gulp com o comando `npm install --global gulp-cli `
1. criar 1 pasta com o nome do projeto
1. abrir a pasta no prompt de comando
1. `npm init -y` para dar os nomes padrão ´para os pacotes
1. Em seguida o comando: `npm install gulp browser-sync gulp-sass --save-dev`
1. npm install bootstrap jquery popper.js --save-dev
1. abre a pasta do projeto no editor de código
1. cria uma pasta chamada `src`
1. dentro dessa pasta cria 1 pasta `css`, 1 pasta `js`, 1 pasta `scss`, e 1 pasta `img`
1. Cria um arquivo `index.html` e coloca o código a seguir:
```
<!doctype html>
<html lang="pt-br">
<head>
	<!-- Required meta tags -->
	<meta charset="utf-8">
	<meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

	<!-- Bootstrap CSS -->
	<link rel="stylesheet" href="css/bootstrap.css">
	<link rel="stylesheet" href="css/style.css">
	<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.2/css/all.min.css"/>

	<title>`Template de Site com Bootstrap</title>
</head>
<body>


<!-- Optional JavaScript; choose one of the two! -->
<!-- Option 2: jQuery, Popper.js, and Bootstrap JS -->
<script src="js/jquery.js"></script>
<script src="js/popper.js"></script>
<script src="js/bootstrap.js"></script>	
</body>
</html>

1. Em seguida você volta a pasta raiz do projeto e cria o arquivo `gulpfile.js` e coloca o código a seguir:

```
var gulp = require('gulp');
var browsersync = require('browser-sync').create();
var sass = require('gulp-sass');

//Compilar o Sass
gulp.task('sass',gulp.series( function() {
    return gulp.src(['node_modules/bootstrap/scss/bootstrap.scss', 'src/scss/*.scss'])
        .pipe(sass())
        .pipe(gulp.dest("src/css"))
        .pipe(browsersync.stream());
    }));

//mover js para src.js
gulp.task('js',gulp.series( function() {
    return gulp.src(['node_modules/bootstrap/dist/js/bootstrap.js', 'node_modules/jquery/dist/jquery.js', 'node_modules/popper.js/dist/umd/popper.js'])
        .pipe(gulp.dest("src/js"))
        .pipe(browsersync.stream());

}));


//servidor para olhar os Html /scss
gulp.task('server', gulp.series( ['sass'], function() {
    browsersync.init({
        server: "./src"

    });

    gulp.watch(['node_modules/bootstrap/scss/*.scss', 'src/scss/*.scss'], gulp.parallel( ['sass']));
    gulp.watch("src/*.html").on('change',gulp.parallel( browsersync.reload));

}));

gulp.task('default', gulp.series( ['js', 'server']));
```