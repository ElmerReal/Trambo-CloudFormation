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

            En este caso solamente se crea un objeto del template network porque solo una VPC necesitamos crear.
            ```
            NetworkStack: 
                Type: AWS::CloudFormation::Stack
                Properties: 
                TemplateURL: "https://trambo-elmer.s3-us-west-2.amazonaws.com/CloudFormation/Network/network.yml"
            ```
    - BDStack

        En este bloque se crea un objeto de RDS se le pasa como parametro eun String de las subnets privadas separadas por coma, se envia el security group que solo tiene el puerto 3306 abierto y el security group default de la VPC.
        ```
        BDStack: 
            Type: AWS::CloudFormation::Stack
            Properties: 
            TemplateURL: "https://trambo-elmer.s3-us-west-2.amazonaws.com/CloudFormation/BaseDatos/bd.yml"
            Parameters:
                RefSubnetsPrivadas: !GetAtt NetworkStack.Outputs.RefSubnetsPrivadas
                RefSG : !GetAtt NetworkStack.Outputs.RefSGBD
                RefDefaultSG : !GetAtt NetworkStack.Outputs.RefDefaultSG

        ```
    - WordpressStack
    
        En este bloque se crea un objeto de tipo instancia, se le envia como parametro el id de la subnet publica 1 (donde estara corriendo), el security group con el puerto 80 y 22 abiertos, el endpoint del RDS y el security gruoup default de la VPC
        ```
          WordpressStack: 
            Type: AWS::CloudFormation::Stack
            Properties: 
            TemplateURL: "https://trambo-elmer.s3-us-west-2.amazonaws.com/CloudFormation/Instancias/wordpress.yml"
            Parameters:
                RefSubnetPublica: !GetAtt NetworkStack.Outputs.RefSubnetPublic1
                RefSG : !GetAtt NetworkStack.Outputs.RefSG
                EndpointBD: !GetAtt BDStack.Outputs.EndpointBD
                RefDefaultSG : !GetAtt NetworkStack.Outputs.RefDefaultSG
        ```

At the command prompt, type `nano`.