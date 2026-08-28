# AZ-104 | Lab 01 : Manage Microsoft Entra ID Identities

## Architecture / Composants
* **Tenant :** Microsoft Entra ID
* **Utilisateurs :** `usr-tech01` (Support), `usr-admin01` (Admin)
* **Groupes :** `Grp-IT-Support` (Security)

---

## Procédure

### Tâche 1 : Créer et configurer des comptes utilisateurs
1. Aller dans **Microsoft Entra ID** > **Users** > **New user** > **Create new user**.
<img width="1284" height="690" alt="Capture d&#39;écran 2026-08-27 145454" src="https://github.com/user-attachments/assets/344c70f8-781f-4b2e-b1a2-8d55513c1f90" />


2. Renseigner les informations de l'utilisateur :
   * **User principal name :** `usr-tech01`
   * **Display name :** `usr-tech01`
<img width="607" height="531" alt="Capture d&#39;écran 2026-08-27 151408" src="https://github.com/user-attachments/assets/1de2d0e1-2a83-40ec-bc02-163f5eb34445" />

3. Définir un mot de passe temporaire et valider la création.
<img width="1035" height="352" alt="Capture d&#39;écran 2026-08-27 152217" src="https://github.com/user-attachments/assets/d34d1a09-b999-4d35-8af7-ea641295acaa" />

4. Répéter l'opération pour `usr-admin01`.
<img width="922" height="849" alt="Capture d&#39;écran 2026-08-27 153701" src="https://github.com/user-attachments/assets/f6cbe6e4-b8b2-4e1c-a999-a0031c0449a3" />

### Tâche 2 : Créer des groupes et ajouter des membres
1. Aller dans **Microsoft Entra ID** > **Groups** > **New group**.
<img width="836" height="649" alt="Capture d&#39;écran 2026-08-27 153916" src="https://github.com/user-attachments/assets/a4b1ae02-d972-484e-9a96-f6081f5b2960" />

3. Configurer le groupe :
   * **Group type :** Security
   * **Group name :** `Grp-IT-Support`
   * **Membership type :** Assigned
<img width="824" height="578" alt="Capture d&#39;écran 2026-08-27 154040" src="https://github.com/user-attachments/assets/08fe1214-5643-498d-ae15-10e2504e91ad" />
     
5. Dans la section **Members**, ajouter l'utilisateur `usr-tech01`.
<img width="824" height="578" alt="Capture d&#39;écran 2026-08-27 154040" src="https://github.com/user-attachments/assets/0db868c7-1f26-4ba9-8823-4e494e620536" />
   
7. Cliquer sur **Create**.
<img width="975" height="666" alt="Capture d&#39;écran 2026-08-27 154139" src="https://github.com/user-attachments/assets/57f28ea9-e9c5-4cec-97f1-cf326646bf91" />
