Historia Clínica Distribuida con PostgreSQL + Citus
Este laboratorio implementa una base de datos distribuida real usando PostgreSQL con la extensión Citus, permitiendo fragmentar automáticamente los datos y distribuir las consultas de forma transparente.

Arquitectura
1 Coordinator (puerto 5432)
2 Workers
Todas las tablas distribuidas por documento_id, excepto profesional_salud, que es replicada.
Requisitos
Docker
Docker Compose
psql (cliente PostgreSQL)
Instrucciones
Clona este repositorio y entra en el directorio:
git clone https://github.com/TU_USUARIO/historia-clinica-distribuida-citus.git
cd historia-clinica-distribuida-citus
Levanta los servicios:
docker-compose -f docker-compose-citus.yml up -d
Accede al coordinador y ejecuta el script de esquema:
docker exec -it citus_coordinator psql -U admin -d historia_clinica -c "CREATE EXTENSION IF NOT EXISTS citus;"
docker exec -i citus_coordinator psql -U admin -d historia_clinica < /mnt/schema_citus.sql
Inserta datos de ejemplo:
docker exec -i citus_coordinator psql -U admin -d historia_clinica < /mnt/insert_datos.sql
Validación
Puedes hacer consultas distribuidas directamente desde el coordinador:

SELECT * FROM usuario WHERE documento_id > 0;
Aqui se hace la validacion de la consulta anterior Diagrama ER
Archivos
.
├── docker-compose-citus.yml
├── schema_citus.sql
├── insert_datos.sql
├── README_CITUS.md
Aqui se puede apreciar el modelo entidad relacion Diagrama ER

Autor
Jaider reyes Herazo Ingeniero Experto SRE
