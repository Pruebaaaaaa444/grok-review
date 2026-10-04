# grok-review

Revisión automática de Pull Requests con la CLI de Grok (xAI), ejecutada en GitHub Actions.

## ¿Qué hace?

Cada vez que se abre o actualiza un Pull Request, el workflow:

1. Descarga el código del repositorio.
2. Instala la CLI de Grok.
3. Pide a Grok que revise el PR en busca de bugs y publica la revisión.

## Configuración

1. Crea una API key en tu cuenta de xAI.
2. En el repositorio ve a **Settings → Secrets and variables → Actions → New repository secret**.
3. Crea el secreto `XAI_API_KEY` con tu clave.
4. Asegúrate de que el archivo `.github/workflows/grok-review.yml` esté en la rama principal.

## Uso

Abre un Pull Request y revisa la pestaña **Actions** para ver la ejecución. La revisión aparecerá como comentario en el PR.

## Personalizar la revisión

Cambia el texto de `-p` en el workflow para ajustar lo que Grok debe revisar. Por ejemplo:

```yaml
- run: grok -p "Review this PR for bugs and security issues" --always-approve
```

## Limitaciones y seguridad

- **PRs desde forks:** GitHub no expone los secretos en estos casos, así que el job fallará.
- **`--always-approve`:** permite que la herramienta actúe sin pedir confirmación. Mantén los `permissions` al mínimo necesario.
- **Costos:** cada ejecución consume créditos de tu API de xAI.
- Verifica el script de instalación y los flags de `grok` en la documentación oficial de xAI.
