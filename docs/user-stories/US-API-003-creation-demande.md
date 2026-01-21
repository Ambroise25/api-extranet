# US-API-003 - Creation d'une demande

## User Story

**En tant que** Email Parser  
**Je veux** creer une nouvelle demande liee a un bien  
**Afin de** enregistrer les demandes d'intervention

---

## Criteres d'acceptation

### Scenario 1: Creation reussie
**Donne** des donnees de demande valides avec un bien_id existant  
**Quand** je fais POST /api/demandes  
**Alors** la demande est creee et son ID est retourne

### Scenario 2: Bien inexistant
**Donne** un bien_id invalide  
**Quand** je fais POST /api/demandes  
**Alors** je recois une erreur 404

### Scenario 3: Demande urgente
**Donne** une demande avec urgence "Urgent"  
**Quand** la demande est creee  
**Alors** elle apparait en priorite dans le tableau de bord

---

## Specifications techniques

### Endpoint

```
POST /api/demandes
```

### Corps de la requete

```json
{
  "bien_id": 107,
  "date_demande": "2026-01-21",
  "objet": "Infiltration terrasse - fuite importante",
  "metier": "Etancheite",
  "statut": "En attente de traitement",
  "urgence": "Urgent",
  "details": {
    "description": "Fuite d'eau importante au niveau de la terrasse",
    "ref_syndic": "OS-2026-001234",
    "contact_nom": "Mme Martin",
    "contact_telephone": "0698765432",
    "contact_email": "martin@foncia.fr",
    "codes_acces": "Digicode 1234, Interphone Martin"
  },
  "source": {
    "type": "email",
    "email_id": "msg-123456",
    "date_reception": "2026-01-21T08:30:00Z",
    "expediteur": "gestionnaire@foncia.fr"
  }
}
```

### Champs principaux

| Champ | Type | Obligatoire | Description |
|-------|------|-------------|-------------|
| bien_id | integer | Oui | ID du bien concerne |
| date_demande | date | Oui | Date de la demande |
| objet | string | Oui | Description courte |
| metier | string | Oui | Etancheite, Plomberie, Couverture, Autre |
| statut | string | Oui | Statut initial |
| urgence | string | Non | Urgent, Normal, Faible |
| details | object | Non | Informations detaillees |
| source | object | Non | Origine de la demande |

### Metiers possibles

- Etancheite
- Plomberie
- Couverture
- Autre

### Statuts possibles

- En attente de traitement
- A contacter
- A relancer
- Rdv non pris
- Rendez-vous programme

### Urgences possibles

- Urgent
- Normal (defaut)
- Faible

### Reponse (201 Created)

```json
{
  "id": 11950,
  "bien_id": 107,
  "objet": "Infiltration terrasse - fuite importante",
  "metier": "Etancheite",
  "statut": "En attente de traitement",
  "urgence": "Urgent",
  "created_at": "2026-01-21T10:35:00Z"
}
```

---

## Securite

- Authentification par Bearer Token
- Verification que bien_id existe

---

## Definition of Done

- [ ] Endpoint POST /api/demandes fonctionnel
- [ ] Validation du bien_id (doit exister)
- [ ] Validation du metier (valeurs autorisees)
- [ ] Validation du statut (valeurs autorisees)
- [ ] Stockage des details et source en JSON
- [ ] Reponse 201 avec l'ID de la demande
- [ ] Tests unitaires et integration
