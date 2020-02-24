# Trambo-CloudFormation
Febrero 24, 2020. Create VPC using CloudFormation

Ejercicio 5 (Cloudformation):
Este ejercicio consistira en levantar una base de datos de MySQL en RDS y un servidor de Wordpress en una EC2.
Los template se clasifican segun su tipo.
1. [Network](/Network)
    En el archivo  network.yml se creo toda la infraestructura necesaria para la VPC.
2. [Base de Datos](/BaseDatos)
    En el archivo bd.yml se creo la instancia RDS y se configuro para hacer uso de la infraestructura creada en network.
3. [Instancias](/Instancias)
    En el archivo wordpress.yml se creo la instancia EC2 y se le dio las configuraciones necesarias para levantar WordPress

El diagrama completo es el siguiente:
![alt text](/Imagenes/CloudFormation1.png)

El archivo [principal](/principal.yml) es el encargado de mandar a llamar a los demas templates y orquestar los parametros que cada uno necesita, funciona como una especie de puente entre los demas templates. Este archivo esta estructurado de la siguiente manera:

- Descripcion
    Es un string que describe para que sirve el template
- Recursos
    Este bloque es donde se indican que recursos se van a usar o se mandan a llamar a otros templates.
    - NetworkStack
        ```
        NetworkStack: 
            Type: AWS::CloudFormation::Stack
            Properties: 
            TemplateURL: "https://trambo-elmer.s3-us-west-2.amazonaws.com/CloudFormation/Network/network.yml"
        ```
    - BDStack
        ```
        ```
    - WordpressStack
        ```
        ```

At the command prompt, type `nano`.