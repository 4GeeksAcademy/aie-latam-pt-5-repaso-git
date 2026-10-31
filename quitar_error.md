# Cómo quitamos el commit problemático sin afectar el resto

El commit problemático fue:

- 97ddf57e90351b71ef84038a7843aa2666f707d0

## ¿Qué hicimos?

Usamos el comando:

```bash
git revert --no-edit 97ddf57e90351b71ef84038a7843aa2666f707d0
```

## ¿Por qué este comando?

`git revert` no elimina el commit del historial ni reescribe la rama. En su lugar, crea un nuevo commit que invierte exactamente los cambios del commit anterior.

Esto es importante porque:

- mantiene intactos los demás commits;
- conserva el historial completo del proyecto;
- evita romper el trabajo realizado en otras ramas o commits;
- es la forma segura de deshacer un cambio cuando ya fue compartido o integrado.

## Qué hizo exactamente Git

Git tomó el contenido del commit 97ddf57e... y generó el cambio inverso:

- si el commit añadió líneas, las eliminó;
- si el commit modificó archivos, los devolvió a su estado previo;
- si el commit había creado archivos, los eliminó del seguimiento.

En este caso, el commit problemático añadía el archivo `auth-frontend-error.md`, así que el commit de reversión lo eliminó del árbol del proyecto.

## Resultado

Se creó un nuevo commit de reversión, en lugar de borrar el commit original. Esto deja intactos todos los demás cambios realizados antes y después, pero deshace el problema introducido por ese commit específico.

## Diferencia entre revert y reset

Es importante entender la diferencia:

- `git revert` = deshace sin destruir historial, ideal para trabajar en repos compartidos.
- `git reset` = reescribe la rama y puede borrar commits de la historia local, por lo que es más agresivo y puede afectar a otros colaboradores.

Como la solicitud pedía dejar el resto intacto, `git revert` fue la opción correcta.

## Evidencia del resultado

La ejecución del comando generó un nuevo commit de reversión:

```bash
[main ea53e53] Revert "fix: add frontend auth error notes"
```

El commit de reversión logra el efecto deseado sin tocar la historia original de los demás cambios.
