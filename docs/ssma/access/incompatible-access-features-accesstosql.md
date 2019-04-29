---
title: Le funzionalità di Access non compatibili (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases
- Access databases, features incompatible with SQL Azure
- Access databases, features incompatible with SQL Server
- dates
- default expressions
- foreign keys
- hyperlink columns
- incompatible Access features
- indexes
- indexes, length of
- keywords
- primary keys
- reference, incompatible features
- replication columns
- special characters
- unique indexes
- validation rules
ms.assetid: 99d45b9c-e3b9-4d56-8c25-b594b887ace1
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 29b5225f95c6b2cb04f42c0e67c504ac2cb20e53
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62740901"
---
# <a name="incompatible-access-features-accesstosql"></a>Funzionalità di Access non compatibili (AccessToSQL)
Non tutte le funzionalità di database di Access sono compatibili con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ad esempio, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e accesso avere diversi set di parole chiave riservate. Problemi come questi possono impedire la corretta migrazione alla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Usare la tabella seguente per informazioni sui problemi di migrazione possibili e ciò che è possibile eseguire per risolverli.  
  
## <a name="database-settings-or-features-that-might-affect-migration"></a>Le impostazioni del database o funzionalità che potrebbero influire sulla migrazione  
  
|Impostazione del Database o una funzionalità di accesso|Problema di migrazione|  
|--------------------------------------|-------------------|  
|Accedere alle tabelle privo di indici univoci.|Se viene eseguita la migrazione di una tabella che non dispone di un indice univoco a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], non è possibile modificare la tabella dopo la migrazione. Questo può causare problemi di compatibilità dell'applicazione.<br /><br />Quando si convertono gli oggetti di database di Access, la finestra di Output elencherà tutte le tabelle di accesso che non hanno gli indici univoci.<br /><br />È possibile configurare l'accesso per aggiungere una chiave primaria nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabella durante la conversione. Per altre informazioni, vedere [impostazioni progetto (conversione)](https://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388).|  
|Accedere alle tabelle presenti colonne di replica.|Se una tabella di Access che include le colonne di sistema di replica viene eseguita la migrazione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la funzionalità di replica Jet verranno interrotta dopo la migrazione.<br /><br />Dopo la migrazione, è consigliabile usare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] replica per mantenere copie sincronizzate dei database.|  
|Accedere alle tabelle con indici univoci contengono più valori null.|Accedere alle tabelle con indici univoci con più valori null non possono essere trasferite alla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], in quanto in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], gli indici univoci non consentire più valori null. La migrazione avrà esito negativo per queste tabelle.<br /><br />SSMA Contrassegna questo problema nei report di valutazione. Per creare un report di valutazione, vedere [valutazione accedere agli oggetti di Database per la conversione](assessing-access-database-objects-for-conversion-accesstosql.md).<br /><br />Se questo problema si verifica, è necessario assicurarsi che la chiave primaria non dispone di valori null duplicati. In alternativa, è necessario rimuovere la chiave primaria o indici univoci che contengono più valori null.|  
|Accedere alle tabelle contengono i valori di data che sono fuori il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intervallo.|Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** tipo accetta le date dell'intervallo di 1 gennaio 1753 al 31 dicembre 9999 solo. Accesso accetta le date dell'intervallo pari a 100 1 gennaio al 31 dicembre 9999.<br /><br />SSMA Contrassegna questo problema nei report di valutazione. Per creare un report di valutazione, vedere [valutazione accedere agli oggetti di Database per la conversione](assessing-access-database-objects-for-conversion-accesstosql.md).<br /><br />È possibile configurare come SSMA risolve le date che sono fuori il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intervallo. Per altre informazioni, vedere [impostazioni progetto (migrazione)](https://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d).|  
|Lunghezza di indice nell'accesso superiore a 900 byte.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gli indici hanno un limite di 900 byte per le dimensioni totali delle colonne chiave indice. Se l'accesso alle tabelle usano indici di dimensioni maggiori, SSMA verrà visualizzato un avviso.<br /><br />Se si continua con la migrazione dei dati, la migrazione potrebbe non riuscire.|  
|I nomi degli oggetti di accesso sono [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] parole chiave, o può contenere caratteri speciali.|Accesso e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] avere diversi set di caratteri speciali e parole chiave riservate. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] accetta gli oggetti che vengono denominati usando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] parole chiave o che contengono caratteri speciali, se si usano identificatori inseriti tra parentesi o tra virgolette, ad esempio "select" o [selezionare] p. Per altre informazioni, vedere "Identificatori delimitati (motore di Database)" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online.<br /><br />**NOTA:** Per utilizzare le virgolette per delimitare gli identificatori, le opzioni SET QUOTED_IDENTIFIER deve essere impostata su ON.<br /><br />Ad esempio, `CREATE TABLE [schema](c1 [FOR])` sia un'istruzione valida, anche se **schema** e **per** sono parole chiave riservate. È inoltre `CREATE TABLE [xxx*yyy](c1 x&y)` sia un'istruzione valida, anche se il nome di tabella e colonna di contenere i caratteri speciali  **\&#42;** e **&amp;**.<br /><br />Tutte le query che fanno riferimento a tali oggetti devono usare anche i nomi con parentesi quadre o virgolette. Ad esempio, la query `SELECT * FROM schema` avrà esito negativo. La query corretta è: `SELECT * FROM [schema]`.<br /><br />Quando si convertono gli oggetti di database di Access, il riquadro di Output elencherà tutte le tabelle di Access che utilizzano caratteri speciali o parole chiave. È possibile modificare le tabelle di Access, rimuovere e aggiungere nuovamente il database In alternativa, è possibile modificare le query che fanno riferimento a tali oggetti in modo che le query usano parentesi quadre o virgolette doppie per delimitare gli identificatori. Se non si modificano le query, le applicazioni Access potrebbero restituire errori o di altri problemi.|  
|Le dimensioni dei campi differiscono primarie/chiave relazioni di chiave esterna.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non supporta la funzionalità di Jet di collegamento tra le colonne con tipi di dati o dimensioni con vincoli di chiave esterna.<br /><br />Quando si convertono gli oggetti di database di Access, la finestra di Output elencherà qualsiasi primari/chiave vincoli di chiave esterna che non verranno convertiti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile modificare i tipi di dati e le dimensioni per le colonne di accesso in modo che essi corrispondono, quindi rimuovere e aggiungere nuovamente il database di Access. Oppure, è possibile migrare i dati anche se questi vincoli non verranno creati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|Le tabelle cui viene fatto riferimento nelle relazioni di accesso hanno una chiave primaria né un indice univoco.|Accesso accetta una relazione tra tabelle in cui la tabella di riferimento non dispone di una chiave primaria o un indice univoco. Tuttavia, questo non è supportato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br />Quando si convertono gli oggetti di database di Access, la finestra di Output elencherà tutte le tabelle con relazioni, ma nessuna chiave primaria o indice univoco. È possibile modificare le tabelle per aggiungere le chiavi primarie o indici univoci, quindi rimuovere e aggiungere nuovamente il database di Access. In alternativa, è possibile migrare i dati anche se la relazione tra le tabelle verranno interrotta.|  
|Accedere alle tabelle hanno colonne collegamento ipertestuale.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non supporta **hyperlink** colonne. Al contrario, le colonne vengono considerate come accedere alle colonne di tipo memo. Per impostazione predefinita, queste colonne verranno convertite in **nvarchar (max)** colonne [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile personalizzare il mapping. Per altre informazioni, vedere [Mapping tipi di origine e destinazione dati](mapping-source-and-target-data-types-accesstosql.md).|  
|Le espressioni di regola predefinito o la convalida contenere funzioni di accesso che non possono essere convertite in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.|Espressioni di accesso predefinito o le regole di convalida potrebbero includere funzioni di sistema di accesso o funzioni definite dall'utente che non sono mappati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Uso delle funzioni che non sono mappati al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure impedirà di caricamento predefinito espressioni o delle regole di convalida in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.|  
  
## <a name="see-also"></a>Vedere anche  
[Preparazione dei database di Access per la migrazione](preparing-access-databases-for-migration-accesstosql.md)  
[Migrazione dei database di Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
