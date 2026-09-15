# Práctica de Git y GitHub

**Nombre:** José Luis Guilen González
**Matrícula:** 2630455
**Nombre de la práctica:** Sincronización de un repositorio local con un repositorio remoto en GitHub
**Repositorio:** `practica-git-guilen-jose`

---

## Objetivo de la práctica

El propósito de esta práctica fue comprobar, de manera directa, que Git y GitHub se comunican en ambos sentidos: que los cambios realizados en la computadora se reflejan en GitHub, y que los cambios realizados en GitHub también se reflejan de vuelta en la computadora. Hasta antes de esta práctica había utilizado Git principalmente de forma mecánica, repitiendo comandos sin detenerme a analizar su función; por ello, el objetivo real para mí fue entender qué hace cada paso y por qué es necesario, más allá de solo ejecutarlo correctamente.

---

## Descripción del procedimiento

### Creación del repositorio local

El procedimiento inició con la creación de una carpeta llamada `practica-git-guilen-jose`. Dentro de ella, se abrió PowerShell y se ejecutó `git init`, comando que convierte una carpeta común en un repositorio de Git, es decir, permite que Git comience a llevar un registro de los cambios que ocurren en su interior. Posteriormente se utilizó `git branch -M main` para establecer `main` como nombre de la rama principal, ya que en algunas instalaciones de Git el nombre por defecto es `master`.

Una vez inicializado el repositorio, se crearon dos archivos: este `README.md` y un archivo `datos.txt` con un texto inicial, el cual sirvió posteriormente para observar la sincronización de cambios entre la computadora y GitHub.

### Registro de los primeros cambios

Antes de guardar cualquier cambio se revisó el estado del repositorio con `git status`, el cual mostró ambos archivos como nuevos y sin seguimiento. A continuación, se ejecutó `git add .` para enviarlos al área de preparación (*staging area*), es decir, al espacio intermedio donde se colocan los cambios antes de confirmarlos de forma definitiva. Se verificó nuevamente el estado y, por último, se creó el primer commit mediante `git commit -m "Primer commit"`, lo cual guardó una versión del proyecto en ese momento junto con un mensaje descriptivo.

### Creación del repositorio en GitHub y vinculación con el repositorio local

En GitHub se creó un repositorio con el mismo nombre (`practica-git-guilen-jose`), configurado como público y sin agregar automáticamente README, `.gitignore` ni licencia, con el fin de que quedara vacío y los primeros archivos provinieran del repositorio local.

Se copió la URL proporcionada por GitHub y se vinculó con el repositorio local mediante:

```
git remote add origin https://github.com/usuario/practica-git-guilen-jose.git
```

Este comando indica a Git que existe un repositorio remoto, identificado como `origin`, ubicado en esa dirección. Para confirmar la vinculación se ejecutó `git remote -v`, comando que muestra las URLs configuradas tanto para subir como para descargar información.

### Sincronización del repositorio local hacia GitHub

Con la conexión ya establecida, se subieron por primera vez los archivos mediante:

```
git push -u origin main
```

El parámetro `-u` establece una relación de seguimiento entre la rama local `main` y la rama remota `main`, de modo que en adelante ya no es necesario especificar `origin main` en cada envío, bastando con `git push`. Al revisar el repositorio en GitHub se confirmó que los archivos `README.md` y `datos.txt` ya se encontraban ahí, por lo que esta parte del procedimiento se completó correctamente.

### Sincronización de GitHub hacia el repositorio local

Para comprobar el flujo en sentido contrario, se editó directamente el archivo `datos.txt` desde la interfaz web de GitHub, agregando la línea "Este archivo fue modificado desde GitHub", y se guardó el cambio mediante un commit realizado desde la propia plataforma.

De vuelta en la computadora, se ejecutó:

```
git pull origin main
```

Este comando descarga los cambios existentes en el repositorio remoto y los integra con el contenido local. Al revisar nuevamente `datos.txt` se confirmó que la línea agregada desde GitHub ya estaba presente en la computadora, validando así esta parte del flujo.

### Nueva modificación desde el repositorio local

Para completar el ciclo, se modificó otra vez `datos.txt`, ahora desde la computadora, agregando la línea "Este archivo fue modificado desde el repositorio local". Se repitió la secuencia habitual:

```
git status
git add .
git commit -m "Actualización desde repositorio local"
git push
```

Se revisó el estado del repositorio, se agregó el cambio al área de preparación, se creó un commit con un mensaje descriptivo y, finalmente, se envió a GitHub mediante `git push`, sin necesidad de especificar de nuevo el remoto y la rama, debido a la relación de seguimiento establecida previamente. Al consultar el repositorio en GitHub, la nueva línea aparecía reflejada correctamente.

---

## Comandos de Git utilizados y su función

| Comando | Función |
|---|---|
| `git init` | Inicializa un nuevo repositorio de Git en la carpeta actual. |
| `git branch -M main` | Establece o renombra la rama principal como `main`. |
| `git status` | Muestra el estado de los archivos: modificados, agregados o sin seguimiento. |
| `git add .` | Envía todos los cambios al área de preparación, previo a un commit. |
| `git commit -m "mensaje"` | Guarda una nueva versión de los cambios preparados, junto con un mensaje descriptivo. |
| `git remote add origin URL` | Vincula el repositorio local con un repositorio remoto identificado como `origin`. |
| `git remote -v` | Muestra las URLs de los repositorios remotos configurados. |
| `git push -u origin main` | Envía los commits al repositorio remoto y establece la relación de seguimiento entre ramas. |
| `git pull origin main` | Descarga los cambios del repositorio remoto y los integra con el repositorio local. |
| `git push` | Envía los commits nuevos, utilizando la relación de seguimiento ya configurada. |

---

## Descripción de los archivos del repositorio

- **README.md**: documento que describe el objetivo, el procedimiento realizado y la función de cada comando utilizado.
- **datos.txt**: archivo empleado para comprobar la sincronización bidireccional; contiene el texto inicial y las líneas agregadas tanto desde GitHub como desde el repositorio local.

---

## Conclusión personal

Esta práctica permitió comprender de manera concreta el funcionamiento del flujo de trabajo básico de Git y GitHub, un aspecto que anteriormente conocía solo de forma teórica. Observar cómo un cambio realizado directamente en GitHub se refleja en la computadora después de ejecutar `git pull`, y cómo un cambio realizado en la computadora se refleja en GitHub después de un `git push`, permitió entender con mayor claridad la utilidad de Git para el trabajo colaborativo: distintas personas pueden modificar un mismo proyecto desde ubicaciones diferentes y mantenerlo sincronizado, siempre que se respete el orden de los comandos `add`, `commit`, `push` y `pull`. Asimismo, quedó clara la función del área de preparación, la cual permite decidir con precisión qué cambios se incluirán en cada commit, en lugar de guardar todas las modificaciones de manera automática.
