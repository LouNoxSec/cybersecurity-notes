# 🛡️ Write-Up : SOC L1 Alert Triage & Phishing Investigation (TryHackMe)

## 📌 Contexte & Objectif
* **Plateforme / Parcours :** TryHackMe — *SOC Level 1* (*SOC Team Internals* & *Introduction to Phishing* via le *SOC Simulator*)
* **Rôle simulé :** Analyste SOC L1
* **Objectif :** Appliquer une méthodologie structurée de *triage* d'alertes, analyser des signalements de *phishing*, qualifier les incidents (*True Positive* ou *False Positive*) et rédiger un rapport d'escalade clair.

---

## 🔍 Méthodologie de Triage (SOC L1 Workflow)
Avant d'investiguer le contenu technique, chaque alerte passe par un processus systématique :
1. **Prise en charge & Priorisation :** Vérification de la sévérité (*Severity*), du SLA et du contexte de l'alerte.
2. **Enrichissement (Lookups & Workbooks) :** Consultation des *playbooks* internes et vérification de la réputation des indicateurs (*IoCs* : adresses IP, domaines, hashes, expéditeurs).
3. **Qualification :**
   * **True Positive (TP) :** Activité malveillante confirmée nécessitant une action ou une escalade.
   * **False Positive (FP) :** Alerte déclenchée à tort sur une activité légitime.
   * **Benign True Positive :** Activité réelle (ex. : test interne ou outil autorisé) mais non malveillante.

---

## 🧪 Investigation Pratique : SOC Simulator (*Introduction to Phishing*)

### 1. Analyse de l'email suspect
Lors de la simulation, les éléments suivants ont été inspectés pour évaluer la légitimité du message :
* **Expéditeur & En-têtes (*Headers*) :** Vérification de l'adresse du sender, objet du message, lien à cliquer.
* **Contenu & Ingénierie sociale :** Présence d'un sentiment d'urgence, demande d'identifiants ou incitation à ouvrir une pièce jointe ou cliquer sur un lien.
* **Liens & Pièces jointes :** Inspection des URLs sans cliquer directement dessus dans le SIEM et analyse des fichiers joints dans un environnement isolé (*sandbox*).
* **Observations clés :** le premier cas s'est révélé être un FP car en analysant l'adresse du sender, celle du recipient et le contenu de l'email, le sender était bien un third-party pour la RH. Le second cas était un TP avec un lien malveillant, répertorié comme tel dans TryDetectThis. Pas d'escalation needed car le firewall a blocked la connexion et le message n'a pas été reçu par d'autres personnes.Le troisième cas était le log du blocked du firewall pour le deuxième cas, donc TP sans escalation. Et le dernier cas était un TP avec escalation car le recipient a cliqué sur le lien malveillant et le firewall a allowed la connexion donc un vrai risque est encouru.


### 2. Décision & Escalation (*Alert Reporting*)
Une fois l'alerte qualifiée en **True Positive**, un rapport structuré (regroupant les *5 W* : *Who, What, When, Where, Why*) a été rédigé pour l'escalade vers le niveau 2 (SOC L2) / l'équipe *Incident Response* :

---

## 🛡️ Recommandations Défensives & Remédiation
* **Confinement immédiat :** Bloquer l'adresse de l'expéditeur, le domaine et les URLs malveillantes au niveau de la passerelle de messagerie (*Secure Email Gateway*) et du proxy/pare-feu.
* **Vérification d'impact :** Rechercher dans les logs si d'autres collaborateurs ont reçu le même email ou cliqué sur le lien, et réinitialiser les identifiants des comptes potentiellement compromis.
* **Prévention :** Renforcer les règles de filtrage anti-phishing (DMARC en mode `reject`) et sensibiliser les utilisateurs concernés.

---

## 💡 Ce que j'ai appris
* L'importance de suivre un **workbook** rigoureux pour ne sauter aucune étape lors du triage sous pression.
* Un messae qui de prime abord peut paraître suspiscious nécessite une réelle investigation car dans le premier cas, même si le message paraissait suspiscious, après investigation, il s'est avéré legitimate. Toujours bien vérifier les infos contenues pour faire le bon triage.
* La qualité d'un **rapport d'escalade L1** fait gagner un temps précieux à l'équipe L2 : il doit être factuel, concis et contenir tous les IoCs vérifiés.
