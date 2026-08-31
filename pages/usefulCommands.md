- ```sql
  CREATE TABLE modules.st_user LIKE demo.st_user;
  
  INSERT INTO modules.st_user
  SELECT * FROM demo.st_user;
  ```