# 5. Intenta realizar operaciones similares de importación y exportación con las herramientas proporcionadas con Postgres desde línea de comandos, documentando el proceso.

Postgresql nos ofrece unas herramienta para este fin llamadas pg_dump y pg_restore.

**Exportar**
Voy a intentar hacer el mismo proceso, lo mas cercano posible al ejercicio 1.

```
pg_dump -U postgres scott \
    --exclude-table=bonus \
    --file=pg_dump.sql
```
![ ](img/501.png)

No hace falta especificar logs, ya que se guardan en `/var/log/postgresql`. Tambien sale el tamaño estimado.

![ ](img/502.png)

**Importar**

La herramienta pg_restore sirve para importar archivos generados con pg_dump siempre que no sean generados en texto plano.

Para importar el nuestro simplemente corremos el script

```
psql -U postgres < pg_dump.sql
```

Si queremos generar un archivo para pg_restore tenemos que usar la opcion --format={ custom | directory | tar }

```
pg_dump -U postgres scott \
    --exclude-table=bonus \
    --format=tar \
    --file=pg_dump.tar
```

```
pg_restore -f pg_dump.tar -F tar
```
