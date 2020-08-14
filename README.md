# Configuracion-sql-server
 Configuracion necesaria para poder trabajar con un cliente externo como dbeaver o para poder conectar a aplicaciones externas.

# Requisitos
- Dbeaver version 7.0.1
- Sql server 2019

# Links de descarga
- [Dbeaver ultima version](https://dbeaver.io/category/releases/)
- [Otras versiones dbeaver](https://dbeaver.io/category/releases/)
- [Sql server 2019](https://www.microsoft.com/es-es/sql-server/sql-server-2019) 

Muchas veces necesitamos conectar nuestro motor de base de datos a una aplicacion o poder visualizar la informacion mediante otro cliente diferente como lo es dbeaver.

Cuando tratamos de conectar nos mostrara un error similar al siguiente:
 
>No se pudo realizar la conexión con el host DESKTOP-61FDA97, instancia con nombre DEV. Error: "java.net.SocketTimeoutException: Receive timed out". Verifique los nombres del servidor y de instancia, compruebe que no hay ningún firewall bloqueando el tráfico UDP al puerto 1434. Para SQL Server 2005 o posterior, verifique que el servicio SQL Server Browser se está ejecutando en el host.

![error dbeaver](https://github.com/cristian-lara/configuracion-sql-server/blob/master/imagenes/error-dbeaver.PNG?raw=true)

Para esto necesitamos verificar que el sql server tenga las configuraciones necesarias las cuales se detallan a continuacion.

## Paso 1
Ingresamos a la configuracion de sql server podemos ingresar escribiendo SQL server en el menu de inicio de wiindows

![imagen inicio sql](https://github.com/cristian-lara/configuracion-sql-server/blob/master/imagenes/Captura.PNG?raw=true)

## Paso 2
En el panel lateral izquierdo vamos a encontrar diferentes opciones, entre ellas **SQL server services**

![sql services](https://github.com/cristian-lara/configuracion-sql-server/blob/master/imagenes/servicios.PNG?raw=true)

Procedemos a habilitarlos siguientes servicios 
* **SQL server**: Si se encuentra deshabilitado damos doble click en el servicio y se mostrara la siguiente pantalla

![img propiedades sql server](https://github.com/cristian-lara/configuracion-sql-server/blob/master/imagenes/sql-server-propiedades.PNG?raw=true)

Nos dirigimos a la pestaña de **service** y en la parte de **start mode** habilitamos a manual o automatico dependiendo de como queremos que se inicie el servicio de preferencia ponerlo automatico.

Regresamos a la pestaña de **logon** y le damos click en start, de esta manera nuestro servicio estara levantado.

Repetimos el mismo procedimiento para el servicio **SQL browser**

## Paso 3
Vamos a habilitar los protocolos tcp ip para esto en el panel izquierdo seleccionamos **SQL server network configuration**. Desplegamos las opciones y seleccionamos **Protocols for MSSSQL SERVER** 

![protocols](https://github.com/cristian-lara/configuracion-sql-server/blob/master/imagenes/network-sql.PNG?raw=true)

Verificamos que el protocolo TCP/IP se encuentre habilitado, si se encuentra deshabilitado damos doble click y se nos presentara la siguiente pantalla 

![tcp-enabled](https://github.com/cristian-lara/configuracion-sql-server/blob/master/imagenes/tcp-ip-enabled.PNG?raw=true)

Cambiamos la opcion a enabled YES.

Posterior a esto tambien es necesario activar las direcciones ipv4 e ipv6(no obligatorio)
se presentara la siguiente pantalla

![img ip adress](https://github.com/cristian-lara/configuracion-sql-server/blob/master/imagenes/ip-enabled.PNG?raw=true)

Verificamos que la ip Adress 127.0.0.1 este habilitada en mi caso es la ip10 para la ipv4 y la ip11 para la ipv6

 Finalmente reiniciamos los servicios configurados en el paso 2 
 
 ## Paso 4
 Abrimos el dbeaver y creamos una nueva conexion
 
 ![img new conecction](https://github.com/cristian-lara/configuracion-sql-server/blob/master/imagenes/new-conection.PNG?raw=true)
 
 Elegimos sql server
 
 Posterior a esto nos aparecera un formulario para ingresar las credenciales y poder acceder a la base de datos
  ![form credentials](https://github.com/cristian-lara/configuracion-sql-server/blob/master/imagenes/config-sql-conection.PNG?raw=true)
  
  Recordar que el host sera el que nosotros le pusimos al momento de la instalacion a nuestro servidor de base de datos. por default es el nombre del equipo 
  
  Lo siguiente es revisar que el dbeaver tenga los drivers adecuados esto se descarga de manera automatica los dirvers
  
  En este ejemplo se instalaron las siguientes versiones de los drivers
  ![drivers](https://github.com/cristian-lara/configuracion-sql-server/blob/master/imagenes/drivers-dbeaver-sql-server.PNG?raw=true)
  
  Listo finalmente damos en test conection y se debe conectar

