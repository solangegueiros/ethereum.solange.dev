
Para hacer deploy de un contrato inteligente con Truffle,
necesitamos un nuevo archivo de migraciones donde Truffle lo encontrará.
Este archivo contiene instrucciones para implementar el contrato inteligente.

La carpeta `migrations` contiene archivos JavaScript que te ayudan a publicar contratos en blockchain.
Estos archivos son los encargados de preparar las tareas de publicación,
y están escritos en base a la suposición de que sus necesidades de implementación pueden cambiar con el tiempo.
Un historial de las publicaciones ejecutadas previamente se guarda en el Blockchain a través de un contrato inteligente especial creado automáticamente por Truffle, llamado Migraciones.
(source: [truffle: running-migrations](https://www.trufflesuite.com/docs/truffle/getting-started/running-migrations))

Normalmente comenzamos el nombre del archivo con un número, 
ya que Truffle hace el deploy de los archivos en orden alfabético 
y de esta forma definimos el orden de publicación de los contratos inteligentes.

