# US-API-002 - Creation d'un bien

## User Story

**En tant que** Email Parser  
**Je veux** creer un nouveau bien dans le CRM  
**Afin de** enregistrer les adresses inconnues

---

## Criteres d'acceptation

### Scenario 1: Creation reussie
**Donne** des donnees de bien valides  
**Quand** je fais POST /api/biens  
**Alors** le bien est cree et son ID est retourne

### Scenario 2: Donnees manquantes
**Donne** des donnees incompletes (sans code postal)  
**Quand** je fais POST /api/biens  
**Alors** je recois une erreur 422 avec les champs manquants

### Scenario 3: Gestionnaire inexistant
**Donne** un gestionnaire_id invalide  
**Quand** je fais POST /api/biens  
**Alors** je recois une erreur 422

---

## Specifications techniques

### Endpoint

```
POST /api/biens
```

### Corps de la requete

```json
{
  "adresse": "12 rue de la Paix",
  "complement_adresse": "Batiment A",
  "code_postal": "75002",
  "ville": "Paris",
  "gestionnaire_id": 1,
  "information": "Copropriete Les Jardins - Digicode 1234"
}
```

### Champs

| Champ | Type | Obligatoire | Description |
|-------|------|-------------|-------------|
| adresse | string | Oui | Numero et nom de rue |
| complement_adresse | string | Non | Batiment, escalier |
| code_postal | string | Oui | Code postal (5 chiffres) |
| ville | string | Oui | Ville |
| gestionnaire_id | integer | Oui | ID du gestionnaire interne |
| information | string | Oui | Infos complementaires |

### Reponse (201 Created)

```json
{
  "id": 108,
  "adresse": "12 rue de la Paix",
  "complement_adresse": "Batiment A",
  "code_postal": "75002",
  "ville": "Paris",
  "gestionnaire_id": 1,
  "created_at": "2026-01-21T10:30:00Z"
}
```

### Reponse erreur (422)

```json
{
  "error": {
    "code": 422,
    "message": "Validation failed",
    "details": {
      "code_postal": "Le code postal est obligatoire",
      "gestionnaire_id": "Le gestionnaire n'existe pas"
    }
  }
}
```

---

## Securite

- Authentification par Bearer Token
- Validation des donnees entrantes

---

## Definition of Done

- [ ] Endpoint POST /api/biens fonctionnel
- [ ] Validation des champs obligatoires
- [ ] Verification que gestionnaire_id existe
- [ ] Reponse 201 avec l'ID du bien cree
- [ ] Gestion des erreurs 422
- [ ] Tests unitaires et integration
