# Renovar Atlassian

El acceso operativo a Atlassian utiliza la cuenta y token configurados para
`acli` en la VM. Tras un fallo de autorización, comprueba su estado.

```sh
acli jira auth status
```

Si requiere renovación, prepara un token con los permisos de la cuenta autorizada,
actualiza el entorno privado de la VM y autentica el CLI pasando el token por
stdin. Usa los valores de sitio y correo de ese entorno. Comprueba después una
consulta al proyecto esperado desde el bot.

Selecciona proyecto, zona e instancia desde el inventario operativo antes de
copiar credenciales o conectar a la VM. Guarda el token fuera de comandos,
historial, logs y Git.
