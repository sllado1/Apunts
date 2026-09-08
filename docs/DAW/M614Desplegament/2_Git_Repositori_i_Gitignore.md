# Bloc 2. Crear un repositori i decidir què versionem

**Pregunta clau:** com començo i quins fitxers han d'entrar a l'historial?

Configura la identitat que apareixerà als commits una vegada per ordinador. Aquesta configuració no inicia sessió a cap plataforma:

```bash
git config --global user.name "Nom Cognom"
git config --global user.email "alumne@example.com"
```

Per començar un projecte nou, executa dins de la seva carpeta:

```bash
git init -b main
git status
```

Si el projecte ja existeix en un remot, utilitza `git clone URL_DEL_REPOSITORI` i entra a la carpeta creada. **Tria `init` o `clone` segons el cas**; no cal inicialitzar un repositori que acabes de clonar.

Abans del primer commit, crea un fitxer `.gitignore`. Exemple per a un projecte web, que cal adaptar a la tecnologia utilitzada:

```gitignore
.env
node_modules/
vendor/
*.log
```

Versionem el codi, la documentació, els fitxers de dependències i els fitxers de bloqueig de versions. Excloem secrets, dependències instal·lades i fitxers temporals. Podem compartir un `.env.example` amb valors ficticis.

**Atenció:** `.gitignore` no deixa de seguir fitxers ja versionats ni esborra secrets de l'historial. Si publiques una credencial, cal revocar-la o substituir-la; eliminar el fitxer no és suficient.

**Pràctica:** crea un repositori amb `index.html` i `.gitignore`. Comprova amb `git status` que un fitxer `.env` nou queda exclòs.
