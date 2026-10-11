NTELLIGENT ACCESS VERIFICATION SYSTEM (TREES)
==============================================
 
A browser-based simulation of an access control system for a high-security
biomedical research laboratory. Researchers request entry to a laboratory, and
the system decides whether to grant or deny access by running a series of
security checks. All of the logic is built on tree data structures.
 
Data Structures micro-project, Alliance School of Advanced Computing,
Alliance University.
 
Live demo: https://<your-username>.github.io/Lab-Access-Verification-System/
(replace with your GitHub Pages link after you enable it)
 
 
FEATURES
--------
- Researcher portal: enter a researcher ID and choose a laboratory to request
  access. Each check shows Passed, Failed or Skipped, followed by the final
  decision.
- Security officer dashboard:
    * live statistics (researchers, requests, granted, denied, BST height)
    * add a researcher, remove a researcher
    * revoke or restore access, activate or deactivate permission
    * emergency lockdown switch that denies every request
    * security activity log (newest first)
- Tree view: live drawings of the researcher BST and the facility zone tree,
  with pre-order, in-order and post-order traversals. A researcher whose
  access is revoked is outlined in red.
- Works fully offline in the browser. No installation, no backend.
 
 
DATA STRUCTURES USED
--------------------
1. Binary search tree (key = researcher ID)
   Stores researcher records.
   Operations: search (authentication), insert (add researcher),
   delete (remove researcher), in-order walk (sorted list).
 
2. General tree (first-child / next-sibling links)
   Stores the facility zones: Facility -> Wings -> Laboratories.
   Operation: depth-first search to check whether a lab lies under the
   researcher's authorized zone.
 
3. Binary search tree (key = request number)
   Stores the access log.
   Operations: insert each decision, reverse in-order walk to list the
   newest first.
 
 
FACILITY ZONE TREE
------------------
FAC (Research Facility)
  |-- RW (Research Wing)
  |     |-- LAB1 (Biomedical Research)
  |     |-- LAB2 (Chemical Analysis)
  |-- SW (Storage Wing)
        |-- LAB3 (Cold Storage)
 
A researcher authorized for a wing can enter every laboratory below it.
 
 
HOW A REQUEST IS VERIFIED
-------------------------
The checks run in this order. The first failure denies access and the
remaining checks are skipped.
 
1. Authentication  - search the researcher BST for the ID.
2. Authorization   - is the requested lab inside the subtree of the
                     researcher's authorized zone?
3. Permission      - is the researcher's permission active?
4. Revocation      - has the researcher's access been revoked?
5. Emergency lockdown - is the lockdown switch off?
 
 
SAMPLE DATA
-----------
ID     Name            Authorized zone       Status
R101   Dr. Anika Rao   Research Wing (RW)    Active
R102   Meera Nair      LAB2                  Active
R103   Arjun Das       LAB3                  Active
R104   Kiran Shah      LAB1                  Revoked
 
Test cases to try:
- R101 -> LAB1 : Granted (LAB1 is under RW)
- R101 -> LAB3 : Denied, laboratory outside authorized zone
- R102 -> LAB1 : Denied, laboratory outside authorized zone
- R104 -> LAB1 : Denied, access revoked
- R999 -> any lab : Denied, unknown researcher ID
- Any valid request with lockdown on : Denied, emergency lockdown
 
 
PROJECT STRUCTURE
-----------------
Lab-Access-Verification-System/
  index.html   (the whole application: HTML, CSS and JavaScript in one file)
  README.txt
 
 

 
 
