# Docker Compose para Odoo
## Instalación
* instalar docker-compose con "pip install docker-compose"
* instalar docker-engine con "sudo curl -sSL https://get.docker.com/ | sh"
* en algun directorio que deseemos, descargamos este repositorio "git clone git@github.com:ingadhoc/docker-compose-odoo.git"
* levantamos odoo entrando al directorio (cd docker-compose-odoo) y corriendo "docker-compose up"

## Agregado de repositorios
La imagen sugerida de odoo ya tiene los repositorios que usamos cargados. Si se quiere trabajar en desarrollo o agregar otros repositorios localmente, entonces:

1. clonar dichos repositorios en la carpeta "sources"
2. editar .env (subl .env) y modificar parámetro "CUSTOM_ADDONS" para que quede de la forma "CUSTOM_ADDONS=/mnt/extra-addons/[nombre_directorio_repositorio]"

## Usando docker compose
* docker-compose up:
    * crea todos los containers y los deja levantados. Crea tambien volumes para la data si no existen ya
    * se puede usar -d para que quede en segundo plano
* docker-compose rm: borra todos los containers pero no los volumes (la data queda persistente)
* docker-compose down -v: borra todos los containers y los volumes (la data no queda persistente)
* docker-compose ps: lista todos los contenedores
* docker-compose pull: pull a imagenes de contenedores
* docker-compose run: permite correr un comando sobre un servicio.
    * Por defecto no expone ningun puerto, para hacerlo agregar "--service-ports"
    * Puede ser recomendable agregar --rm cuando queremos tirar un comando y queremos que luego el container se borre
    * ejemplo de uso:
        * crear bd "demo" e instalar "notes" "docker-compose run --rm odoo -d demo -i base"
        * tirar un update de un modulo "docker-compose run --rm odoo -d demo -u base"
* docker-compose config: permite ver la configuracion con la que se esta levantando
* export atributo=valor: permite definir atributos de contexto que el compose toma y se puede ver con el config 
