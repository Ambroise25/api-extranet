# US-API-006 - Liste des clients (syndics)

## User Story

**En tant que** Email Parser  
**Je veux** recuperer la liste des clients/syndics  
**Afin de** identifier le syndic associe a un bien

---

## Criteres d'acceptation

### Scenario 1: Liste complete
**Donne** des syndics enregistres dans le CRM  
**Quand** je fais GET /api/clients  
**Alors** je recois la liste complete des syndics

### Scenario 2: Recherche par nom
**Donne** un nom de syndic "Foncia"  
**Quand** je fais GET /api/clients?nom=Foncia  
**Alors** je recois les syndics correspondants

---

## Specifications techniques

### Endpoint

```
GET /api/clients
```

### Parametres de requete

| Parametre | Type | Obligatoire | Description |
|-----------|------|-------------|-------------|
| nom | string | Non | Recherche par nom |

### Reponse (200 OK)

```json
{
  "clients": [
    {
      "id": 1,
      "nom": "QCC",
      "adresse": "10 rue du Commerce, 75015 Paris"
    },
    {
      "id": 2,
      "nom": "RBH Scholer",
      "adresse": "25 avenue de la Republique, 92000 Nanterre"
    },
    {
      "id": 3,
      "nom": "Foncia Vaucelles",
      "adresse": "5 rue Vaucelles, 14000 Caen"
    }
  ]
}
```

---

## Usage

Permet de verifier si un syndic existe deja dans le CRM avant de l'associer a un bien.

---

## Securite

- Authentification par Bearer Token

---

## Definition of Done

- [ ] Endpoint GET /api/clients fonctionnel
- [ ] Retourne ID, nom, adresse
- [ ] Recherche par nom (optionnel)
- [ ] Authentification requise
- [ ] Tests unitaires
