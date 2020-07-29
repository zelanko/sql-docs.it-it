---
title: Sicurezza di una tabella temporale | Microsoft Docs
ms.custom: ''
ms.date: 10/16/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 60e5d6f6-a26d-4bba-aada-42e382bbcd38
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6f9392a6ef282d1a3201e5edb2a4fa026adc5752
ms.sourcegitcommit: d855def79af642233cbc3c5909bc7dfe04c4aa23
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2020
ms.locfileid: "87122775"
---
# <a name="temporal-table-security"></a>Sicurezza di una tabella temporale

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

Per comprendere il tema della sicurezza in riferimento alle tabelle temporali, è importante conoscere i principi di sicurezza che riguardano le tabelle temporali. Dopo aver compreso questi principi è possibile procedere approfondendo il tema della sicurezza in relazione alle istruzioni **CREATE TABLE**, **ALTER TABLE**e **SELECT** .

## <a name="security-principles"></a>Principi di sicurezza

 La tabella seguente descrive i principi di sicurezza che riguardano le tabelle temporali:

|Principio|Descrizione|
|---------------|-----------------|
|L'abilitazione/disabilitazione del controllo delle versioni di sistema richiede i privilegi più elevati per gli oggetti interessati|L'abilitazione e disabilitazione di SYSTEM_VERSIONING richiede l'autorizzazione CONTROL sia per la tabella corrente che per quella di cronologia|
|I dati di cronologia non possono essere modificati direttamente|Quando SYSTEM_VERSIONING è ON, gli utenti non possono modificare i dati di cronologia indipendentemente dalle autorizzazioni effettive per la tabella corrente o di cronologia. Ciò vale sia per le modifiche dei dati che per quelle dello schema.|
|Per l'esecuzione di query sui dati di cronologia è richiesta l'autorizzazione **SELECT** per la tabella di cronologia|Il fatto che un utente abbia l'autorizzazione **SELECT** per la tabella corrente non significa che abbia l'autorizzazione **SELECT** per la tabella di cronologia.|
|Il controllo espone le operazioni che influiscono sulla tabella di cronologia in modi specifici:|Le impostazioni di controllo della tabella corrente non vengono applicate automaticamente alla tabella di cronologia. Il controllo deve essere abilitato in modo esplicito per la tabella di cronologia.<br /><br /> Dopo l'abilitazione, il controllo sulla tabella di cronologia acquisisce regolarmente tutti i tentativi diretti di accesso ai dati (indipendentemente dal fatto che siano riusciti o meno).<br /><br /> **SELECT** con l'estensione per query temporali mostra che la tabella di cronologia è stata interessata da tale operazione.<br /><br /> Le operazioni**CREATE/ALTER** sulla tabella temporale espongono informazioni che indicano che il controllo delle autorizzazioni viene eseguito anche sulla tabella di cronologia. Il file di controllo conterrà record aggiuntivi per la tabella di cronologia.<br /><br /> Le operazioni DML sulla tabella corrente indicano che la tabella di cronologia è stata interessata, ma additional_info fornisce il contesto necessario (DML risultante da SYSTEM_VERSIONING).|

## <a name="performing-schema-operations"></a>Esecuzione di operazioni sullo schema

Quando SYSTEM_VERSIONING è impostato su ON, le operazioni di modifica dello schema sono limitate.

### <a name="disallowed-alter-schema-operations"></a>Operazioni ALTER sullo schema non consentite

|Operazione|Tabella corrente|Tabella di cronologia|
|---------------|-------------------|-------------------|
|**DROP TABLE**|Non consentita|Non consentita|
|**ALTER TABLE...SWITCH PARTITION**|Solo SWITCH IN (vedere [Partizionamento con le tabelle temporali](../../relational-databases/tables/partitioning-with-temporal-tables.md))|Solo SWITCH OUT (vedere [Partizionamento con le tabelle temporali](../../relational-databases/tables/partitioning-with-temporal-tables.md))|
|**ALTER TABLE...DROP PERIOD**|Non consentita|-|
|**ALTER TABLE...ADD PERIOD**|-|Non consentita|

## <a name="allowed-alter-table-operations"></a>Operazioni ALTER TABLE consentite

|Operazione|Corrente|Cronologia|
|---------------|-------------|-------------|
|**ALTER TABLE...REBUILD**|Consentita (in modo indipendente)|Consentita (in modo indipendente)|
|**CREATE INDEX**|Consentita (in modo indipendente)|Consentita (in modo indipendente)|
|**CREATE STATISTICS**|Consentita (in modo indipendente)|Consentita (in modo indipendente)|

## <a name="security-of-the-create-temporal-table-statement"></a>Sicurezza dell'istruzione CREATE TABLE per le tabelle temporali

| Funzionalità | Creare una nuova tabella di cronologia | Riutilizzare una tabella di cronologia esistente |
| ------- | ------------------------ | ---------------------------- |
|Autorizzazione necessaria|Autorizzazione**CREATE TABLE** nel database<br /><br /> Autorizzazione**ALTER** per gli schemi in cui vengono create le tabelle corrente e di cronologia|Autorizzazione**CREATE TABLE** nel database<br /><br /> Autorizzazione**ALTER** per lo schema in cui verrà creata la tabella corrente.<br /><br /> Autorizzazione**CONTROL** per la tabella di cronologia specificata come parte dell'istruzione **CREATE TABLE** per la creazione della tabella temporale|
|Audit|Dal controllo risulta che gli utenti hanno tentato di creare due oggetti. L'operazione può non riuscire a causa della mancanza di autorizzazioni per creare una tabella nel database o a causa della mancanza di autorizzazioni per la modifica degli schemi per entrambe le tabelle.|Il controllo indica che la tabella temporale è stata creata. L'operazione può non riuscire a causa della mancanza di autorizzazioni per creare una tabella nel database, a causa della mancanza di autorizzazioni per la modifica dello schema per la tabella temporale o a causa della mancanza di autorizzazioni per la tabella di cronologia.|

## <a name="security-of-the-alter-temporal-table-set-system_versioning-onoff-statement"></a>Sicurezza dell'istruzione ALTER TABLE SET (SYSTEM_VERSIONING ON/OFF) per le tabelle temporali

| Funzionalità | Creare una nuova tabella di cronologia | Riutilizzare una tabella di cronologia esistente |
| ------- | ------------------------ | ---------------------------- |
|Autorizzazione necessaria|Autorizzazione**CONTROL** nel database<br /><br /> Autorizzazione**CREATE TABLE** nel database<br /><br /> Autorizzazione**ALTER** per gli schemi in cui viene creata la tabella di cronologia|Autorizzazione**CONTROL** per la tabella originale modificata<br /><br /> Autorizzazione**CONTROL** per la tabella di cronologia specificata come parte dell'istruzione **ALTER TABLE**|
|Audit|Il controllo indica che la tabella temporale è stata modificata e contemporaneamente è stata creata la tabella di cronologia. L'operazione può non riuscire a causa della mancanza di autorizzazioni per creare una tabella nel database, a causa della mancanza di autorizzazioni per la modifica dello schema per la tabella di cronologia o a causa della mancanza di autorizzazioni per la modifica della tabella temporale.|Il controllo indica che la tabella temporale è stata modificata, ma l'operazione ha richiesto l'accesso alla tabella di cronologia. L'operazione potrebbe non riuscire a causa della mancanza di autorizzazioni per la tabella di cronologia o per la tabella corrente.|

## <a name="security-of-select-statement"></a>Sicurezza dell'istruzione SELECT

L'autorizzazione**SELECT** è invariata per le istruzioni **SELECT** senza effetti sulla tabella di cronologia. Per le istruzioni **SELECT** che interessano la tabella di cronologia, l'autorizzazione **SELECT** è richiesta sia per la tabella corrente che per la tabella di cronologia.

## <a name="see-also"></a>Vedere anche

- [Tabelle temporali](../../relational-databases/tables/temporal-tables.md) 
- [Introduzione alle tabelle temporali con controllo delle versioni di sistema](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)
- [Verifiche di coerenza del sistema della tabella temporale](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [Partizionamento con le tabelle temporali](../../relational-databases/tables/partitioning-with-temporal-tables.md)
- [Considerazioni e limitazioni delle tabelle temporali](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)
- [Gestire la conservazione dei dati cronologici nelle tabelle temporali con controllo delle versioni di sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [Tabelle temporali con controllo delle versioni di sistema con tabelle con ottimizzazione per la memoria](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [Funzioni e viste per i metadati delle tabelle temporali](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)
