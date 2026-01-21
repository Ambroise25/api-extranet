# US-API-004 - Upload de fichiers

## User Story

**En tant que** Email Parser  
**Je veux** uploader des pieces jointes liees a une demande  
**Afin de** conserver les documents et photos

---

## Criteres d'acceptation

### Scenario 1: Upload image
**Donne** une image JPG associee a une demande  
**Quand** je fais POST /api/fichiers  
**Alors** l'image est stockee et liee a la demande

### Scenario 2: Upload PDF
**Donne** un PDF (ordre de service)  
**Quand** je fais POST /api/fichiers  
**Alors** le PDF est stocke et lie a la demande

### Scenario 3: Fichier trop gros
**Donne** un fichier de 15 MB  
**Quand** je fais POST /api/fichiers  
**Alors** je recois une erreur 413

### Scenario 4: Type non autorise
**Donne** un fichier .exe  
**Quand** je fais POST /api/fichiers  
**Alors** je recois une erreur 422

---

## Specifications techniques

### Endpoint

```
POST /api/fichiers
```

### Corps de la requete (multipart/form-data)

| Champ | Type | Obligatoire | Description |
|-------|------|-------------|-------------|
| demande_id | integer | Oui | ID de la demande |
| fichier | file | Oui | Fichier a uploader |
| type | string | Non | "image" ou "document" |
| description | string | Non | Description du fichier |

### Types de fichiers autorises

| Type | Extensions | MIME Types |
|------|------------|------------|
| Images | jpg, jpeg, png, gif | image/jpeg, image/png, image/gif |
| Documents | pdf | application/pdf |

### Limites

| Parametre | Valeur |
|-----------|--------|
| Taille max par fichier | 10 MB |
| Nombre max par demande | 20 |

### Reponse (201 Created)

```json
{
  "id": 456,
  "demande_id": 11950,
  "nom": "photo_fuite.jpg",
  "type": "image",
  "taille": 245678,
  "url": "/uploads/demandes/11950/photo_fuite.jpg",
  "created_at": "2026-01-21T10:36:00Z"
}
```

### Reponse erreur (413 Payload Too Large)

```json
{
  "error": {
    "code": 413,
    "message": "Fichier trop volumineux (max 10 MB)"
  }
}
```

### Reponse erreur (422)

```json
{
  "error": {
    "code": 422,
    "message": "Type de fichier non autorise"
  }
}
```

---

## Stockage

Les fichiers sont stockes dans :
```
/var/www/extranet/public/uploads/demandes/{demande_id}/
```

---

## Securite

- Authentification par Bearer Token
- Validation du type MIME
- Scan antivirus (optionnel)

---

## Definition of Done

- [ ] Endpoint POST /api/fichiers fonctionnel
- [ ] Support multipart/form-data
- [ ] Validation de la taille (max 10 MB)
- [ ] Validation du type MIME
- [ ] Stockage sur le serveur
- [ ] Lien avec la demande
- [ ] Reponse avec URL du fichier
- [ ] Tests avec images et PDF
