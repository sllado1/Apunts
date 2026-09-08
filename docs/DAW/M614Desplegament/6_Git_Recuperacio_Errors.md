# Bloc 6. Corregir errors i recuperar-se amb criteri

**Pregunta clau:** com desfaig una acció sense perdre canvis que vull conservar?

Abans d'actuar, consulta `git status` i revisa les diferències. Les ordres següents resolen problemes diferents:

| Situació | Ordre | Efecte |
| --- | --- | --- |
| He preparat un fitxer per error, en un repositori que ja té commits. | `git restore --staged FITXER` | El treu de la preparació i conserva les modificacions al disc. |
| Vull descartar modificacions no preparades d'un fitxer seguit. | `git restore FITXER` | Recupera el contingut de la zona de preparació; **es perden les modificacions no preparades del fitxer**. |
| Vull desfer un commit ordinari que ja he compartit. | `git revert ID_DEL_COMMIT` | Crea un nou commit que inverteix aquell canvi i conserva l'historial. Pot requerir resoldre conflictes. |

Utilitza `git log --oneline` per localitzar l'identificador del commit que vols revertir. Executa `revert` amb el directori de treball net. Per a aquest flux bàsic no necessitem `reset --hard`, reescriptura de l'historial ni enviaments forçats.


