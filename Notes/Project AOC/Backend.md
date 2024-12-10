## Handle multilingual data
### Database
Use a Translation Table: 
``` sql
CREATE TABLE translation ( 
id INT AUTO_INCREMENT PRIMARY KEY, 
entity_type VARCHAR(50), -- Type of entity (e.g., 'celebrity', 'event') 
entity_id INT NOT NULL, -- ID of the entity being translated 
language_code VARCHAR(10) NOT NULL, -- Language code (e.g., 'en', 'zh') 
field_name VARCHAR(50), -- Field name being translated (e.g., 'name', 'description') 
field_value TEXT NOT NULL -- Translated content );
```
