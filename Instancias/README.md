First Header  | Second Header
------------- | -------------
Content Cell  | Content Cell
Content Cell  | Content Cell


# BaseDatos/bd.yml
El archivo [bd](/BaseDatos/bd.yml) es el template que que permite crear RDS:
Este archivo esta estructurado de la siguiente manera:

* Descripcion

* Parameters
    * RefSubnetsPrivadas
        * String separado por coma de los ids de las subneets privadas
    * RefSG
        * Security group que solo tiene el puerto 3306 abierto.
    * RefDefaultSG
        * Security group default de la VPC.

* Recursos
    * SubnetGroup
        * Crea un subnet group con los ids de las subnets recibidas como parametro.
    * MyDB
        * Crea la instancia del RDS

* Outputs
    * EndpointBD
        * Devuelve el endpoint de la instancia