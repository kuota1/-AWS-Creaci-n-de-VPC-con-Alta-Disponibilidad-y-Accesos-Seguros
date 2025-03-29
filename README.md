AWS-VPC: Proyecto de Red Privada y Pública en AWS
Este proyecto demuestra cómo crear manualmente una arquitectura de red en AWS usando la consola. Se incluyen subredes públicas y privadas, acceso controlado mediante Bastion Host, NAT Gateway, VPC Endpoint, y acceso a un bucket S3 desde una instancia privada.

Arquitectura General
VPC personalizada con rango CIDR 10.0.0.0/16.

2 Subredes públicas y 2 subredes privadas.

Internet Gateway (usado temporalmente para pruebas).

Bastion Host (EC2 pública) para acceso SSH a instancias privadas.

Instancia EC2 privada sin IP pública.

NAT Gateway (para acceso a internet desde la subred privada).

VPC Endpoint S3 Gateway para acceso directo desde la red privada a S3.

Bucket S3 con imagen de prueba.

IAM Role asociado a la EC2 privada para permitir lectura de objetos en el bucket.

Pasos Realizados
1. Creación de VPC y subredes
VPC: 10.0.0.0/16

Subred pública: 10.0.0.0/20 y 10.0.16.0/20

Subred privada: 10.0.32.0/20 y 10.0.48.0/20

2. Configuración de Internet Gateway
Asociado solo durante pruebas de conectividad pública.

3. Configuración del Bastion Host
EC2 pública con key pair .pem.

Acceso SSH habilitado desde IP pública.

4. Configuración de la instancia privada
EC2 sin IP pública.

Accesible solo a través del Bastion Host.

5. Configuración de NAT Instance (prueba de acceso a internet desde la subred privada)
Configuración de una NAT Instance como acceso a internet para la red privada.

Eliminado para probar NAT Gateway.

6. Configuración de NAT Gateway
Asociado a la subred pública.

Permite acceso a internet desde la EC2 privada (curl exitoso).

7. Configuración de S3 Bucket y VPC Endpoint
Bucket S3 creado con una imagen de prueba.

VPC Endpoint tipo Gateway asociado a la tabla de ruteo privada.

Acceso exitoso desde la EC2 privada usando aws s3 cp.

8. Configuración de IAM Role
Permiso de solo lectura: AmazonS3ReadOnlyAccess.

Asociado a la EC2 privada para acceso mediante Bastion Host.

Requisitos
Cuenta de AWS activa.

Permisos suficientes para crear y eliminar recursos.

Conexión SSH desde una terminal compatible.

Costos
Todos los recursos fueron creados con el objetivo de eliminarse rápidamente para evitar cargos.
Se priorizó el uso de T2.micro dentro del Free Tier, evitando el uso de recursos innecesarios.

Lecciones Aprendidas
La NAT Instance requiere una AMI específica para funcionar correctamente.

Los VPC Endpoints para S3 solo funcionan con tablas de ruteo privadas.

El uso de Bastion Host es esencial para limitar la exposición pública de las instancias.

Autor
Roberto Carlos Rodríguez Guzmán
Proyecto personal realizado como práctica para fortalecer conocimientos en redes y arquitectura AWS.



sub
