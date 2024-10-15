---
longform:
---

How to make changes in database table?
- Move one column from one table to another
- Delete column

### Step 1: Update Your SQLAlchemy Models 

First, ensure your SQLAlchemy models reflect the new structure. It seems you've already updated the `BasicProperty` model to include the `average_cost` column. Make sure the `Material` model no longer includes this column. Here's an example of how your models might look: 

```python from sqlalchemy import create_engine, Column, Integer, Float, ForeignKey from sqlalchemy.ext.declarative import declarative_base from sqlalchemy.orm import relationship, sessionmaker Base = declarative_base() class Material(Base): __tablename__ = 'materials' id = Column(Integer, primary_key=True) name = Column(String) basic_properties = relationship('BasicProperty', back_populates='material', uselist=False) class BasicProperty(Base): __tablename__ = 'basic_properties' id = Column(Integer, primary_key=True) material_id = Column(Integer, ForeignKey('materials.id'), unique=True) density = Column(Float) # kg/m^3 average_cost = Column(Float) # Dollars per kg material = relationship('Material', back_populates='basic_properties') ``` 

### Step 2: Update the Database Schema To update the database schema, you can use a migration tool like Alembic. Alembic is a lightweight database migration tool for use with SQLAlchemy. Here's how you can use it: 1. **Install Alembic** if you haven't already: 
```bash pip install alembic ``` 

2. **Initialize Alembic** in your project: ```bash alembic init alembic ``` This will create an `alembic` directory with configuration files. 3. **Configure Alembic** by editing `alembic.ini` and `env.py` to point to your database and models. 4. **Create a Migration Script**: Generate a new migration script using Alembic: ```bash alembic revision --autogenerate -m "Move average_cost to BasicProperty" ``` This will create a new script in the `alembic/versions` directory. Open this script and ensure it correctly reflects the changes you want to make. It should include: - Removing the `average_cost` column from the `Material` table. - Adding the `average_cost` column to the `BasicProperty` table. 5. **Apply the Migration**: Run the migration to update your database schema: ```bash alembic upgrade head ``` ### Step 3: Verify the Changes After applying the migration, verify that the database schema has been updated correctly. You can do this by inspecting the database tables or using a database management tool. ### Explanation - **SQLAlchemy Models**: These define the structure of your tables in Python code. By updating the models, you ensure that your application code reflects the desired database schema. - **Alembic**: This tool helps manage database migrations, allowing you to apply changes to the database schema incrementally and safely. By following these steps, you can successfully update your database schema to reflect the changes in your SQLAlchemy models.