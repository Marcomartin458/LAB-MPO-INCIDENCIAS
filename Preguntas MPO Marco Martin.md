**1. ¿Por qué el frontend no necesita conectarse a PostgreSQL?**



Porque el frontend solo espera interacciones del usuario y es el backend el que, según la interacción del usuario, se comunica con la base de datos, entonces no es necesario tener el front conectado a PostgreSQL.



**2. ¿Por qué el backend pertenece a dos redes?**



El backend pertenece a frontend y a datos. Esto es así porque el backend es el encargado de comunicar a frontend con los datos y viceversa. Si el usuario crea una incidencia, el botón lo muestra el front, al clicar, el back recibe ese click y procesa los datos introducidos hacia la db.



**3. ¿Qué servicio necesita publicar un puerto en el anfitrión?**



El que necesita publicar un puerto en el anfitrión (localhost) es el front, ya que backend y db se comunican mediante redes internas de Docker. Es al front al que accedemos mediante el navegador.



**4. ¿Por qué publicar PostgreSQL hacia fuera no es la solución adecuada para un fallo de comunicación interno?**



Principalmente porque es un gran error en cuanto a la seguridad. Al publicar hacia fuera PostreSQL dejas expuesta la db. Además, es muy posible que el fallo venga de la configuración de las redes, ya que, como he visto en esta práctica, hasta una identación mal hecha puede hacer que falle.

**5. ¿Qué ventaja ofrece Docker Compose respecto a ejecutar los tres contenedores manualmente?**



La principal ventaja que ofrece es la compactación de configuraciones en un solo archivo, facilitando el desarrollo. Además, se puede levantar, parar, etc. con un solo comando. Hacerlo por separado se haría bastante más aburrido, largo y sujeto a errores humanos. 



**6. ¿Por qué hemos dividido la arquitectura en dos redes?**



Es una buena práctica dividir los servicios. Que el front esté en una red y back y db en otra, ya que necesitan comunicarse pero no estar dentro de la misma red. Así, además, garantizas un punto extra en seguridad, ya que no interesa que si alguien consigue acceso a la red del front, no tiene acceso a las otras redes.



**7. ¿Por qué el backend utiliza `db` como dirección de PostgreSQL?**



Porque es el nombre interno del servicio PostgreSQL en el compose. Si pusiéramos localhost haría referencia al propio contenedor del backend, no al de PostgreSQL.



**8. ¿Qué diferencia existe entre detener un proyecto y eliminar sus volúmenes?**



Al poner Docker compose stop, paramos los contenedores, pero tanto ellos como sus volúmenes siguen existiendo. Si ponemos Docker compose down eliminaremos los contenedores, pero no sus volúmenes ni sus datos. Para eliminar también los volúmenes, pondremos -v al final.



**9. ¿Qué consecuencias tendría para la empresa perder el volumen de PostgreSQL?**



Pues es probablemente una de las peores cosas que pueden pasar, ya que caerían los datos que la empresa tuviese guardados y, si no hay copias de seguridad, se vería en un problema bastante importante.





