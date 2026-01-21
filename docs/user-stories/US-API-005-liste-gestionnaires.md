# US-API-005 - Liste des gestionnaires

## User Story

**En tant que** Email Parser  
**Je veux** recuperer la liste des gestionnaires internes  
**Afin de** associer un gestionnaire par defaut aux nouveaux biens

---

## Criteres d'acceptation

### Scenario 1: Liste complete
**Donne** des gestionnaires enregistres dans le CRM  
**Quand** je fais GET /api/gestionnaires  
**Alors** je recois la liste complete des gestionnaires

### Scenario 2: Aucun gestionnaire
**Donne** aucun gestionnaire enregistre  
**Quand** je fais GET /api/gestionnaires  
**Alors** je recois une liste vide

---

## Specifications techniques

### Endpoint

```
GET /api/gestionnaires
```

### Reponse (200 OK)

```json
{
  "gestionnaires": [
    {
      "id": 1,
      "nom": "Quentin Cunat",
      "email": "quentin@enerpur.fr"
    },
    {
      "id": 2,
      "nom": "Guillaume Oyer",
      "email": "guillaume@enerpur.fr"
    },
    {
      "id": 3,
      "nom": "Rbh Scholer",
      "email": "rbh@enerpur.fr"
    }
  ]
}
```

---

## Usage

Le gestionnaire_id est utilise lors de la creation d'un bien.
Si le gestionnaire n'est pas specifie dans l'email, utiliser un gestionnaire par defaut.

---

## Securite

- Authentification par Bearer Token

---

## Definition of Done

- [ ] Endpoint GET /api/gestionnaires fonctionnel
- [ ] Retourne ID, nom, email
- [ ] Authentification requise
- [ ] Tests unitaires
