# Awesome Project  

This project demonstrates the use of **SDM (Schema Data Migration)** for managing database schema and data migrations in a reproducible and rollback-safe manner.  

---

## Environment Details  

For this assignment, both **MySQL** and **SDM** were run inside Docker containers.  

- **MySQL Version:** `9.4.0`  
  Retrieved with:  
  ```bash
  docker exec -it sdm-mysql mysql -u root -pXXXX -e "SELECT VERSION();"


- **SDM Version:** `0.6.4`  
  Retrieved with:  
  ```bash
  docker run -v "%cd%:/workspace" -e MYSQL_PWD="XXXX" -it --rm beim/schema-data-migration:latest sdm --version
