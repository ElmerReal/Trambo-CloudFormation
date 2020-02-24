# Instancias/wordpress.yml
El archivo [wordpress](/Instancias/wordpress.yml) es el template que que permite crear EC2.
Este archivo esta estructurado de la siguiente manera:

* Descripcion

* Parameters
    * RefSubnetPublica
        * String del id de la subnet publica
    * RefSG
        * Security group que solo tiene el puerto 80 y 22 abierto.
    * RefDefaultSG
        * Security group default de la VPC.
    * EndpointBD
        * Endpoint del RDS creado

* Recursos
    * MyEC2Instance
        * Instancia EC2 creada con un user data que instala wordpress
