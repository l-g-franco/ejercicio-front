# Instrucciones para la inducció de Capa Front-End 


## Antes de iniciar asegurate de cumplir con los siguientes requerimientos:

Para completar el siguiente ejercicio deberás tener en tu ambiente de desarrollo  las siguientes herramientas:

- Git ( comando o GitHub App)
[**Instalar Git.**](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)<br>
- Angular CLI ( última versión 8.x)
[**Instalar Angular CLI.**](https://angular.io/cli)<br>

- Navegador Chrome
[**Chrome.**](https://www.google.com/chrome/?brand=CHBD&gclid=CjwKCAjwlovtBRBrEiwAG3XJ-5Z2vqcJZl3yhHBjmN6lLHh3Pd13wqIKl8ZVoEaoGVethCPFrL20oBoC_IwQAvD_BwE&gclsrc=aw.ds)<br>


- Terminal de Comandos<br>

## Dinámica del ejercicio:

El código del ejercicio se encuentra  en un repositorio Git en donde por cada paso se deberá de realizar un "commit" para poder tomar tu avance.


## Objetivo

El ejercicio se trata de generar una **App en Angular tipo biblioteca musical** con el registro de canciones. Se deberá crear un formulario de registro y sus componentes internos para el manejo y control de la información.



## Listos! Vamos a iniciar

Abre una terminal de comandos y crea una nueva carpeta

```
$ mkdir proyectoEjercicio
$ cd proyectoEjercicio
```

A partir de ahora esta será tu carpeta raíz del ejercicio del examén.

##### Clonar repositorio

a)  Asegurate de clonar el repositorio de la siguiente dirección:

[**Repositorio base .**](https://github.com/l-g-franco/ejercicio-front.git)<br>


b) Clona el repositorio, ejecuta las siguientes instrucciones en la terminal de comandos:
```
git clone https://github.com/l-g-franco/ejercicio-front.git
cd ejercicio-front
```

c) Realiza el checkout de la rama **ejercicio1-base**
```
git checkout ejercicio1-base
cd frontend
```

d) Crea una rama con tus iniciales:

```
git checkout -b ejercicio1-<iniciales>
```

##### Inicia con el ejercicio.


A partir de este momento todos los cambios se deberán ejecutar en la rama que se creo en los pasos anteriores, ponte comodo :beers:.




Sigue las siguientes intrucciones:

## 1. Crea una aplicació Angular nueva.

```
ng new songs-project --style=scss --routing=true
cd songs-project
ng serve

```

- Abre la siguiente URL en tu navegador:

[** App Biblioteca Musical.**](http://localhost:4200)<br>



![Imagen 1.](./assets/step1-final.png?raw=true "Imagen 1")



- Realiza el **commit** de tus cambios del paso #1. Abre otra teminal de comandos y ejecuta los siguientes comandos:

```
git add .
git commit -m "CHANGES - Resultado del paso #1"
git push --set-upstream origin ejercicio1-<iniciales>
```

* Nota: asegurate de modificar `<iniciales>`por tus iniciales. Deben de ser las mismas del paso 1.


###### Felicidades ! Concluiste tu primer paso vamos por más !! :tada:


## 2. Crear Componente de registro de canciones.


- Crea un nuevo **module**  para la biblioteca de canciones:
```
ng g module library --routing=true
```

- Crear el componente de registro de canción **AddCancion**

```
ng g component library/addCancion
```

- Vamos a realizar un **checkin** de avance de código para esto realizamos el proceso de **commit** de código en Git.

```
git add .
git commit -m "CHANGES 2.1- Se crean módulo y componente de registro de canción"
git push
```

  - 2.1 Wired

  El proceso de **wired** se refiere a *enlazar* los componentes creados con la aplicación principal, es decir que sean visibles dentro de la app.


  a) Abre tu IDE y carga la carpeta raíz del examen a tu área de trabajo. Vamos a editar código.



- Abre proyectos con Atom IDE
[**Atom flight manual.**](https://flight-manual.atom.io/getting-started/sections/atom-basics/#opening-directories)<br>

- Agrega lo siguiente en el archivo: `src/app/app.module.ts`

```javascript
...

import { LibraryModule } from './library/library.module'

@NgModule({
...
  imports: [
    BrowserModule,
    LibraryModule,
    AppRoutingModule
  ],
  ...
})

```


* Nota: Los `...` no se deben de copiar, se utiliza para hacer referencia a código que existe en las zonas indicadas.


- Vamos agregar el **Routing** para indicar la URL de nuestro componente nuevo. Modifica el archivo  `/src/app/library/library-routing.module` para agregar las rutas de los componentes:



```javascript
...
import { AddCancionComponent } from './add-cancion/add-cancion.component'

const routes: Routes = [
  { path: 'add',        component: AddCancionComponent },
  { path: '',   redirectTo: '/add', pathMatch: 'full' },
];
...

```




- Agrega las opciones de registro de canción, actualiza todo el contenidos del siguiente archivo: `src/app/app.component.html`


Por:

```html
...
<!-- Seccion de ejemplo -->
  <h2>Biblioteca</h2>
  <p>App de la biblioteca musical:</p>

  <div class="card-container">
    <a routerLink="/add" routerLinkActive="active"
    class="card" target="_blank" rel="noopener" href="https://angular.io/tutorial">
      <svg class="material-icons" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path d="M5 13.18v4L12 21l7-3.82v-4L12 17l-7-3.82zM12 3L1 9l11 6 9-4.91V17h2V9L12 3z"/></svg>
      <span>Agregar canci&oacute;n</span>
      <svg class="material-icons" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path d="M10 6L8.59 7.41 13.17 12l-4.58 4.59L10 18l6-6z"/></svg>    </a>
  </div>
...
```

- Vamos a definir nuestra Entidad de negocio **Cancion**, crea una clase con ayuda de Angular CLI ejecutando el siguiente comando:


```
ng g class library/cancion
```


- Agrega los atributos de una **Cancion**. Modifica la clase Cancion que se acaba de crear. El archivo es: `/src/app/library/cancion.ts`


```javascript
export class Cancion {
  id: number;
  nombre: string;
  artista: string;
  duracion: number;
  genero: string;
}
```


- Regresamos al componente de **AddCancion** `/src/app/library/add-cancion/add-cancion.component.ts` para mostrar los datos a partir de una clase **Cancion**




```javascript
...
import { Cancion } from '../cancion';
...

export class AddCancionComponent implements OnInit ...

cancion: Cancion = {
  id: 1,
  nombre: 'El nombre de la canción',
  artista: 'Artista de la Cancion',
  duracion: 3.33,
  genero: 'Rock',
}

constructor() { }

...



```



- Mostrar los datos. Modifica el archivo HTML `/src/app/library/add-cancion/add-cancion.component.html` para mostrar los datos.



```html
<h2>{{cancion.nombre}} Detalles</h2>
<div><span>Id: </span>{{cancion.id}}</div>
<div><span>Artista: </span>{{cancion.artista}}</div>
<div><span>Duración: </span>{{cancion.duracion}}</div>
<div><span>G&eacute;nero: </span>{{cancion.genero}}</div>

```


- Editamos los datos. Vamos a realizar la edición de los datos a través del uso de un formulario, agregamos al archivo anterior:



```html
...

<h5>Editar datos de la canci&oacute;n:</h5>

<div>
  <label>Nombre de la canci&oacute;n:
    <input [(ngModel)]="cancion.nombre" placeholder="Edita el nombre de la canción"/>
  </label>
</div>

```


- Revisa los cambios. Ve que al agregar `[(ngModel)]` la app  ha dejado de funcionar. En Chrome abre la *consola de javascript* para revisar más detalles del problema.


> La consola de javascript nos ayuda a identificar problemas con los componentes o con temas de redes.




- Crash !!! La App ha dejado de funcionar. (Solución de problemas). Los mensajes de error en Angular nos ayudan a identificar la causa del problema, en este caso la funcionalidad de `[(ngModel)]` depende del módulo **FormModule**.


- Abre el archivo `/src/app/library/library.module.ts`. Importa el módulo de FormModule.




```javascript
...
import { FormsModule } from '@angular/forms';
...
imports: [
  CommonModule,
  LibraryRoutingModule,
  FormsModule
]
...

```

- Revisa que la App ha funcionado de nuevo. Nota que al editar el *campo de nombre* se actualiza el título con el nombre de la canción.


- Realiza el **commit** de tus cambios del paso #2.

```
cd ..
git add .
git commit -m "CHANGES - Resultado del paso #2"
git push
cd songs-project
```



![Imagen 2.](./assets/step2-final.png?raw=true "Imagen 2")


###### Bien  !! :tada: :tada: :tada:


## 3. Agregar formulario de registro de canción.

- Para agregar el registro  a través de formularios vamos a utilizar **ReactForms** para lo cuál hay que modificar al **AppModule** cambiando el módulo de **FormsModule** por el de **ReactiveFormsModule**. Modifica el archivo: `/src/app/library/library.module.ts`:


```javascript
...
import { ReactiveFormsModule  } from '@angular/forms';
...
imports: [
  CommonModule,
  LibraryRoutingModule,
  ReactiveFormsModule
]
...

```

- Modifica el archivo HTML `/src/app/library/add-cancion/add-cancion.component.html` para agregar el formulario de los datos.



```html
<h2>Editar datos de la canci&oacute;n:</h2>

<div>

  <form [formGroup]="cancionForm">

  <label>
    Nombre:
    <input type="text" formControlName="nombre">
  </label>

  <label>
    Artista:
    <input type="text" formControlName="artista">
  </label>

  <label>
    Duraci&oacute;n:
    <input type="number" formControlName="duracion">
  </label>

  <label>
    G&eacute;nero:
    <input type="text" formControlName="genero">
  </label>


</form>


</div>

```


- Agregamos el manejo del formulario. Modifica el archivo: `/src/app/library/add-cancion/add-cancion.component.html` con el código siguiente:



```html
...
<form [formGroup]="cancionForm" (ngSubmit)="onSubmit()">
...

<label>
  G&eacute;nero:
  <input type="text" formControlName="genero">
</label>

<button type="submit">Agregar</button>

</form>
```

- Modifica el archivo: `/src/app/library/add-cancion/add-cancion.component.ts` con el siguiente código:


```javascript
...
ngOnInit() {
}


onSubmit() {
  console.warn(this.cancionForm.value);
}
...
```

- Validación de datos de formulario. Agrega las validaciones de los datos del formulario mostrando los mensajes de ayuda.  *Form validation* se utiliza para validar la información capturada por el usuario. Agrega el módulo de **Validators** en **LibraryModule**. Modifica el archivo `/src/app/library/add-cancion/add-cancion.component.ts` con el siguiente código:


```javascript
...
import { FormBuilder } from '@angular/forms';
import { Validators } from '@angular/forms';
...
cancionForm = this.fb.group({
  nombre: ['', Validators.required],
  artista: ['',Validators.required],
  duracion: ['',Validators.required],
  genero: ['',Validators.required]
});

  constructor(private fb: FormBuilder) { }
...
```

- Modifica el archivo `/src/app/library/add-cancion/add-cancion.component.html` con el siguiente código:



```html
...

  <form [formGroup]="cancionForm" (ngSubmit)="onSubmit()">

  <label>
    Nombre:
    <input type="text" formControlName="nombre" required>
  </label>

  <label>
    Artista:
    <input type="text" formControlName="artista" required>
  </label>

  <label>
    Duraci&oacute;n:
    <input type="number" formControlName="duracion" required>
  </label>

  <label>
    G&eacute;nero:
    <input type="text" formControlName="genero" required>
  </label>

  <button type="submit" [disabled]="!cancionForm.valid">Agregar</button>

</form>
...

```

- Realiza el **commit** de tus cambios del paso #3.

```
cd ..
git add .
git commit -m "CHANGES - Resultado del paso #3"
git push
cd songs-project
```


![Imagen 3.](./assets/step3-final.png?raw=true "Imagen 3")

###### Vamos por buen camino  !! :tada: :tada: :tada:


## 4. Agregar estilos y temas. Angular Material.


- Material Angular es el framework de diseño de plantillas para las Apps. Agrega tema de Material a la App de la siguiente manera:


    a) Instalar Angular Material:
    ```
    ng add @angular/material
    ```

* Se pedirá confirmar los siguientes valores. Da enter en cada opción y listo !.

``` sh
Installed packages for tooling via npm.
? Choose a prebuilt theme name, or "custom" for a custom theme: Indigo
/Pink        [ Preview: https://material.angular.io?theme=indigo-pink
]
? Set up HammerJS for gesture recognition? Yes
? Set up browser animations for Angular Material? Yes
```


* Reiniciar la app. Abre la terminal en donde esta corriendo el comando `ng serve` y reinicia de nuevo el comando para que se tomen los cambios.



- Agregamos los componentes de Material Angular al módulo de **LibraryModule**. Modifica el archivo `/src/app/library/library.module.ts` con el siguiente código:



```javascript
...

import { MatSliderModule,MatCardModule, MatIconModule, MatToolbarModule, MatButtonModule, MatFormFieldModule, MatInputModule, MatSelectModule } from '@angular/material';
...
imports: [
  CommonModule,
  ReactiveFormsModule,
  LibraryRoutingModule,
  MatSliderModule,
  MatCardModule,
  MatIconModule,
  MatToolbarModule,
  MatButtonModule,
  MatFormFieldModule,
  MatInputModule,
  MatSelectModule
]
...
```

- Agregamos mas validaciones al formulario agregando reglas de validación más epsecificas y por tipo de atrinuto. Modifica el archivo `/src/app/library/add-cancion/add-cancion.component.ts` con el siguiente código:



```javascript

...
cancionForm = this.fb.group({
  nombre: [null, [Validators.required, Validators.minLength(5), Validators.maxLength(40)]],
  artista: [null, [Validators.required, Validators.minLength(5), Validators.maxLength(40)]],
  duracion: ['',Validators.required],
  genero: ['',Validators.required]
});
...
```



- Aplicamos el componente de Formulario de Material Angular al formulario del registro de canción. Modifica el archivo `/src/app/library/add-cancion/add-cancion.component.html` con el siguiente código:



```html

<h2>Editar datos de la canci&oacute;n:</h2>

<div class="container">

  <form [formGroup]="cancionForm" (ngSubmit)="onSubmit()" class="form">


  <div class="example-container">


    <mat-form-field>
      <input matInput placeholder="El nombre" formControlName="nombre" required>
      <mat-error *ngIf="!cancionForm.controls['nombre'].valid && cancionForm.controls['nombre'].touched">
              Campo requerido, se permite entre 10 hasta 40 caracteres.
      </mat-error>
    </mat-form-field>


    <mat-form-field>
      <input matInput placeholder="El artista" formControlName="artista" required>
      <mat-error *ngIf="!cancionForm.controls['artista'].valid && cancionForm.controls['artista'].touched">
              Campo requerido, se permite entre 10 hasta 40 caracteres.
      </mat-error>
    </mat-form-field>


    <mat-form-field>
      <input matInput placeholder="La duración (minutos)" formControlName="duracion" required>
      <mat-error *ngIf="!cancionForm.controls['duracion'].valid && cancionForm.controls['duracion'].touched">
              Campo requerido, captura la duración en minutos ej. 2.33
      </mat-error>
    </mat-form-field>

    <mat-form-field>
    <mat-label>G&eacute;nero:</mat-label>
    <mat-select matNativeControl required formControlName="genero" placeholder="Genero">
      <mat-option value="Rock">Rock</mat-option>
      <mat-option value="Pop">Pop</mat-option>
      <mat-option value="Blues">Blues</mat-option>
      <mat-option value="Electro">Electro</mat-option>
      <mat-option value="Metal">Metal</mat-option>
    </mat-select>
    <mat-error *ngIf="cancionForm.controls['genero'].hasError('required')">
      Campo requerido
    </mat-error>
    <mat-hint>Selecciona el género de la canción.</mat-hint>
  </mat-form-field>


  <div class="form-element">
        <button mat-raised-button color="primary" type="submit" class="button" [disabled]="!cancionForm.valid">Agregar</button>
  </div>


  </div>

</form>




</div>


```

- Agregamos los estilos del formulario. Modifica el archivo `/src/app/library/add-cancion/add-cancion.component.scss` con el siguiente código:


```css

.example-container {
  display: flex;
  flex-direction: column;
}

.example-container > * {
  width: 100%;
}

.container {
  padding: 10px;
}

.form {
  min-width: 150px;
  max-width: 500px;
  width: 100%;
}

.form-element {
  padding: 5px 0px 25px 2px;
  width: 100%;
}

.button {
  width: 100%;
}


```

- Realiza el **commit** de tus cambios del paso #4.

```
cd ..
git add .
git commit -m "CHANGES - Resultado del paso #4"
git push
cd songs-project
```

###### Excelente diseño  !! :tada: :tada: :tada:


![Imagen 4.](./assets/step4-final.png?raw=true "Imagen 4")

## 5. Agregar Servicio de registro de canción.



Hasta el momento tenemos una app con un formulario de registro que nos ayuda a validar la información de acuerdo a ciertas reglas de negocio, el siguiente paso nos ayuda al manejo de la información a través de Servicios.



- Crea un nuevo servicio a través de la consola de Angular CLI, ejecuta el siguiente comando:

```
ng g service library/library
```

- Modificamos el servicio para que contenga una lista de canciones. Modifica el archivo `/src/app/library/library.service.ts` con el siguiente código:


```javascript
...
export class LibraryService {


  canciones: any[] = [];

  constructor() { }
}
...

```

- Agregamos las operaciones de soporte de la biblioteca de canciones. Modifica el archivo `/src/app/library/library.service.ts` con el siguiente código:

```javascript
...

constructor() { }


addCancion(cancion) {
  this.canciones.push(cancion);
}

getCanciones() {
  return this.canciones;
}
...

```

- Usamos el servicio. Se debe de importar el Servicio creado en el componente de **AddCancionComponent**.Modifica el archivo `/src/app/library/add-cancion/add-cancion.component.ts` con el siguiente código:

```javascript
...
import { LibraryService } from '../library.service';
...
constructor(private fb: FormBuilder,
private libraryService: LibraryService) { }
...
onSubmit() {
  this.libraryService.addCancion(this.cancionForm.value);
}
...
```

- Cada vez que se agregue una canción se deberá dar aviso del resultado de la operación, vamos agregar un **SnackBar** que indique el resultado del servicio. Modifica el archivo `/src/app/library/library.module.ts` con el siguiente código:



```javascript
...
import { MatSliderModule,MatCardModule, MatIconModule, MatToolbarModule, MatButtonModule, MatFormFieldModule, MatInputModule, MatSelectModule,MatSnackBarModule } from '@angular/material';

...
imports: [
  CommonModule,
  ReactiveFormsModule,
  LibraryRoutingModule,
  MatSliderModule,
  MatCardModule,
  MatIconModule,
  MatToolbarModule,
  MatButtonModule,
  MatFormFieldModule,
  MatInputModule,
  MatSelectModule,
  MatSnackBarModule
]
...
```


- Agregamos el componente de SnackBar en el formulario. Modifica el archivo `/src/app/library/add-cancion/add-cancion.component.ts` con el siguiente código:



```javascript
...
import { MatSnackBar } from '@angular/material/snack-bar';
...
constructor(private fb: FormBuilder,
private libraryService: LibraryService,
private _snackBar: MatSnackBar) { }
...
onSubmit() {
  console.debug(this.cancionForm.value);
  this.libraryService.addCancion(this.cancionForm.value);
  console.debug(this.libraryService.getCanciones());
  this.openSnackBar('Se agrego el registro OK', "Registro");
  this.cancionForm.reset();
}

openSnackBar(message: string, action: string) {
 this._snackBar.open(message, action, {
   duration: 2000,
 });
}
...
```


- Realiza el **commit** de tus cambios del paso #5.

```
cd ..
git add .
git commit -m "CHANGES - Resultado del paso #5"
git push
cd songs-project
```

###### Mejorando la experiencia de usuario !! :tada: :tada: :tada:

![Imagen 5.](./assets/step5-final.png?raw=true "Imagen 5")


6. Agregar Route para mostrar resultado de operación.
