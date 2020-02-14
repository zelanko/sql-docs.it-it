

### <a name="index-stats-options"></a>Opzioni per le statistiche degli indici

<!--
This includes/paragraph-content/ file was created when processing vsts sqlbuvsts01 2999014 (5589131).  genemi  2017-07-21

Initially used in:
- relational-databases/maintenance-plans/rebuild-index-task-maintenance-plan.md
- relational-databases/maintenance-plans/reorganize-index-task-maintenance-plan.md
-->


Nelle versioni precedenti di Microsoft SQL Server, la riorganizzazione o ricostruzione di un indice di grandi dimensioni poteva causare rallentamenti del sistema. In SQL Server 2016 sono stati implementati miglioramenti significativi delle prestazioni per queste operazioni sugli indici.

Nelle versioni precedenti anche la granularità del controllo era meno precisa. A causa di questo aspetto, il sistema riorganizzava o ricostruiva alcuni indici anche se non erano molto frammentati, con un conseguente spreco di risorse. I controlli più nuovi nell'interfaccia utente per i piani di manutenzione consentono di escludere gli indici che non devono essere aggiornati, in base a criteri correlati alle statistiche degli indici. A questo scopo vengono usate internamente le viste a gestione dinamica (DMV) seguenti di Transact-SQL:


- [sys.dm_db_index_usage_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)
- [sys.dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)


 **Tipo analisi**  
 Il sistema deve usare risorse per raccogliere le statistiche degli indici. È possibile scegliere se usare una quantità relativamente maggiore o minore di risorse a seconda del livello di precisione che si ritiene necessario per le statistiche. L'interfaccia utente offre l'elenco seguente di livelli di precisione tra cui scegliere:


- Veloce
- Campionato
- Dettagliato


 **Ottimizza indice solo se:**  
 L'interfaccia utente offre i seguenti filtri personalizzabili, che è possibile usare per evitare di aggiornare gli indici per i quali non è ancora effettivamente necessario un aggiornamento:


- Frammentazione &gt; *(%)*
- Conteggio pagine &gt;
- Usato negli ultimi *(giorni)*

