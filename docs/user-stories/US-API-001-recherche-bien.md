# US-API-001 - Recherche d'un bien

## User Story

**En tant que** Email Parser  
**Je veux** rechercher si un bien existe deja dans le CRM  
**Afin de** eviter les doublons et lier la demande au bon bien

---

## Criteres d'acceptation

### Scenario 1: Bien trouve
**Donne** une adresse existante dans le CRM  
**Quand** je fais GET /api/biens?adresse=...&code_postal=...  
**Alors** je recois le bien correspondant avec son ID

### Scenario 2: Bien non trouve
**Donne** une adresse inconnue  
**Quand** je fais GET /api/biens?adresse=...&code_postal=...  
**Alors** je recois une liste vide

### Scenario 3: Plusieurs resultats
**Donne** une recherche ambigue  
**Quand** je fais GET /api/biens?adresse=rue+de+la+paix  
**Alors** je recois tous les biens correspondants avec un score de pertinence

---

## Specifications techniques

### Endpoint

```
GET /api/biens
```

### Parametres de requete

| Parametre | Type | Obligatoire | Description |
|-----------|------|-------------|-------------|
| adresse | string | Non | Numero et nom de rue |
| code_postal | string | Non | Code postal (5 chiffres) |
| ville | string | Non | Nom de la ville |

### Reponse (200 OK)

```json
{
  "total": 1,
  "biens": [
    {
      "id": 107,
      "adresse": "12 rue de la Paix",
      "complement_adresse": "Batiment A",
      "code_postal": "75002",
      "ville": "Paris",
      "gestionnaire": {
        "id": 1,
        "nom": "Quentin Cunat"
      },
      "client": {
        "id": 1,
        "nom": "Foncia"
      }
    }
  ]
}
```

### Reponse vide (200 OK)

```json
{
  "total": 0,
  "biens": []
}
```

---

## Securite

- Authentification par Bearer Token
- Header: `Authorization: Bearer <token>`

---

## Definition of Done

- [ ] Endpoint GET /api/biens fonctionnel
- [ ] Recherche par adresse (partielle)
- [ ] Recherche par code postal
- [ ] Recherche par ville
- [ ] Reponse JSON conforme au contrat
- [ ] Authentification requise
- [ ] Tests unitaires et integration
