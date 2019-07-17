---
title: sp_tableoption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_tableoption_TSQL
- sp_tableoption
dev_langs:
- TSQL
helpviewer_keywords:
- sp_tableoption
ms.assetid: 0a57462c-1057-4c7d-bce3-852cc898341d
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 15c3c9716adefbb95d24c9528dce8607678998c8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096064"
---
# <a name="sptableoption-transact-sql"></a>sp_tableoption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Imposta i valori delle opzioni per le tabelle definite dall'utente. Per controllare il comportamento all'interno delle righe di tabelle in cui è possibile utilizzare sp_tableoption **varchar (max)** , **nvarchar (max)** , **varbinary (max)** , **xml**, **testo**, **ntext**, **immagine**, o le colonne di tipo definito dall'utente di grandi dimensioni.  
  
> [!IMPORTANT]  
>  La caratteristica text in row verrà rimossa nelle versioni future di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per archiviare dati per valori di grandi dimensioni, si consiglia di usare la **varchar (max)** , **nvarchar (max)** e **varbinary (max)** i tipi di dati.  
  

 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_tableoption [ @TableNamePattern = ] 'table'   
     , [ @OptionName = ] 'option_name'   
     ,[ @OptionValue =] 'value'  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @TableNamePattern =] '*tabella*'  
 Nome completo o non qualificato di una tabella di database definita dall'utente. Nel caso di un nome qualificato di tabella, ovvero contenente un nome di database, il nome del database deve corrispondere a quello del database corrente. Non è possibile configurare le opzioni tabella per più tabelle contemporaneamente. *Nella tabella* viene **nvarchar(776)** , non prevede alcun valore predefinito.  
  
 [ @OptionName =] '*option_name*'  
 Nome di un'opzione di tabella. *option_name* viene **varchar(35**, non prevede alcun valore predefinito null. *option_name* può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|table lock on bulk load|Quando questa opzione è disabilitata (impostazione predefinita), durante il processo di caricamento bulk nelle tabelle definite dall'utente vengono acquisiti blocchi di riga. Se abilitata, viene acquisito un blocco di tipo aggiornamento bulk.|  
|insert row lock|Non più supportata.<br /><br /> Questa opzione non influisce sulla funzionalità di blocco di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ed è disponibile solo per compatibilità con script e procedure esistenti.|  
|text in row|Quando questa opzione è disabilitata, ovvero impostata su OFF o 0 (impostazione predefinita), il funzionamento corrente rimane invariato e la riga non contiene valori BLOB.<br /><br /> Quando specificato e @OptionValue è impostata su ON (abilitata) oppure un valore intero compreso tra 24 e 7000, le nuove **testo**, **ntext**, oppure **immagine** le stringhe vengono archiviate direttamente nella riga di dati. Tutti i valori esistenti BLOB (oggetto binario di grandi dimensioni: **testo**, **ntext**, o **immagine** dati) verrà modificato in formato text in row quando viene aggiornato il valore BLOB. Per altre informazioni, vedere la sezione Osservazioni.|  
|large value types out of row|1 = **varchar (max)** , **nvarchar (max)** , **varbinary (max)** , **xml** e colonne di grandi dimensioni tipo definito dall'utente (UDT) nella tabella vengono archiviate all'esterno delle righe, con un puntatore di 16 byte all'elemento radice.<br /><br /> 0 = **varchar (max)** , **nvarchar (max)** , **varbinary (max)** , **xml** e valori UDT di grandi dimensioni vengono archiviati direttamente nella riga di dati, con un limite massimo di 8000 byte e a condizione che il valore può essere contenuti nel record. Se le dimensioni del record non sono sufficienti per il valore, all'interno della riga viene archiviato un puntatore e i dati restanti vengono archiviati all'esterno della riga nello spazio di archiviazione LOB. Il valore predefinito è 0.<br /><br /> Il tipo definito dall'utente (UDT) di grandi dimensioni si applica a: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] - [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. <br /><br /> Utilizzare l'opzione TEXTIMAGE_ON del [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) per specificare un percorso per l'archiviazione dei tipi di dati di grandi dimensioni. |  
|formato di archiviazione vardecimal|**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Se TRUE, ON o 1, la tabella designata è abilitata per il formato di archiviazione vardecimal. Se FALSE, OFF o 0, il formato di archiviazione vardecimal non è abilitato per la tabella. Formato di archiviazione vardecimal può essere abilitato solo quando il database abilitato per il formato di archiviazione vardecimal utilizzando [sp_db_vardecimal_storage_format](../../relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql.md). Nelle [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive **vardecimal** il formato di archiviazione è deprecato. ed è necessario usare il tipo di compressione ROW. Per altre informazioni, vedere [Data Compression](../../relational-databases/data-compression/data-compression.md). Il valore predefinito è 0.|  
  
 [ @OptionValue =] '*valore*'  
 È se il *option_name* è abilitata (TRUE, ON o 1) oppure disabilitata (FALSE, OFF o 0). *valore* viene **varchar(12)** , non prevede alcun valore predefinito. *valore* viene operata la distinzione.  
  
 Per l'opzione text in row, i valori dell'opzione validi sono 0, ON, OFF o un numero intero compreso tra 24 e 7000. Quando *valore* è impostata su ON, le impostazioni predefinite di limite di 256 byte.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o numero di errore (esito negativo)  
  
## <a name="remarks"></a>Note  
 La stored procedure sp_tableoption può essere utilizzata solo per impostare i valori delle opzioni per le tabelle definite dall'utente. Per visualizzare le proprietà della tabella, usare OBJECTPROPERTY.  
  
 In sp_tableoption è possibile abilitare o disabilitare l'opzione text in row solo in tabelle contenenti colonne di testo. Nel caso di tabelle prive di colonne di questo tipo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genera un errore.  
  
 Quando l'opzione text in row è abilitata, il @OptionValue parametro consente agli utenti di specificare le dimensioni massime devono essere archiviati in una riga per un BLOB. I possibili valori sono compresi tra 24 e 7000 byte. Il valore predefinito è 256 byte.  
  
 **testo**, **ntext**, o **immagine** le stringhe vengono archiviate nella riga di dati se si verificano le condizioni seguenti:  
  
-   L'opzione text in row è abilitata.  
  
-   La lunghezza della stringa è più breve rispetto al limite specificato in @OptionValue  
  
-   Nella riga di dati lo spazio disponibile è sufficiente.  
  
 Quando si archiviano stringhe BLOB nella riga di dati, la lettura e scrittura i **testo**, **ntext**, o **immagine** stringhe possono essere il più veloce la lettura o scrittura di stringhe di caratteri e binarie. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non accede a pagine separate per la lettura o scrittura di stringhe BLOB.  
  
 Se un **testo**, **ntext**, o **immagine** stringa è maggiore del limite specificato o lo spazio disponibile nella riga, i puntatori vengono archiviati nella riga invece. Le condizioni per l'archiviazione delle stringhe BLOB nella riga devono comunque essere soddisfatte: Deve esserci spazio sufficiente nella riga di dati per includervi i puntatori.  
  
 Le stringhe e i puntatori BLOB archiviati nella riga di una tabella vengono gestiti in modo analogo alle stringhe a lunghezza variabile, ovvero [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizza solo il numero di byte necessari per l'archiviazione della stringa o del puntatore.  
  
 Quando si abilita l'opzione text in row per la prima volta, le stringhe BLOB esistenti non vengono convertite immediatamente, ma solo in fase di aggiornamento. Analogamente, quando il testo nel limite dell'opzione riga viene aumentato, il **testo**, **ntext**, o **immagine** stringhe già nella riga di dati non verranno convertite al fine di rispettare il limite fino al successivo aggiornamento.  
  
> [!NOTE]  
>  Per disabilitare l'opzione text in row o ridurne il valore limite, è necessario convertire tutti i valori BLOB. L'operazione può pertanto richiedere tempi lunghi, a seconda del numero di stringhe BLOB da convertire. Durante il processo di conversione la tabella viene bloccata.  
  
 Per una variabile di tabella, così come per una funzione che restituisce una variabile di tabella, l'opzione text in row viene abilitata automaticamente con il valore predefinito 256 per il parametro inline limit. Questa opzione non può essere modificata.  
  
 L'opzione text in row supporta le funzioni TEXTPTR, WRITETEXT, UPDATETEXT e READTEXT. Gli utenti possono leggere parti di un valore BLOB tramite la funzione SUBSTRING(). È importante sottolineare, tuttavia, che i limiti massimi relativi a durata e numero per i puntatori di testo all'interno di righe sono diversi da quelli degli altri puntatori di testo.  
  
 Per modificare di nuovo il formato di archiviazione di una tabella da vardecimal a decimal, è necessario che per il database sia impostata la modalità di recupero SIMPLE. La modifica della modalità di recupero causa l'interruzione della catena di log per il backup. Dopo la rimozione del formato di archiviazione vardecimal da una tabella è pertanto necessario creare un backup completo del database.  
  
 Se si sta convertendo un'esistente LOB colonna tipo di dati (text, ntext o image) in tipi di valori di grandi dimensioni piccoli a medi (varchar (max), nvarchar (max), o varbinary e la maggior parte delle istruzioni non fanno riferimento le colonne di tipo di valori di grandi dimensioni nell'ambiente in uso, prendere in considerazione modificando **large_value_types_out_of_row** al **1** per ottenere prestazioni ottimali. Quando la **large_value_types_out_of_row** opzione valore viene modificato, esistenti varchar (max), nvarchar (max), varbinary (max), e i valori xml non vengono convertiti immediatamente. L'archiviazione delle stringhe viene modificata nel corso del successivo aggiornamento. Qualsiasi nuovo valore inserito in una tabella viene archiviato in base all'opzione di tabella attiva. Per risultati immediati, creare una copia dei dati e quindi ripopolare la tabella dopo aver modificato il **large_value_types_out_of_row** impostazione o aggiornare ciascuna colonna di tipi di valori di grandi dimensioni piccole e medie a se stesso in modo che lo spazio di archiviazione del le stringhe viene modificato con l'opzione di tabella in vigore. Provare a ricompilare gli indici nella tabella dopo l'aggiornamento o il ripopolamento per ridurre la tabella. 
    
  
## <a name="permissions"></a>Permissions  
 Per l'esecuzione di sp_tableoption è richiesta l'autorizzazione ALTER per la tabella.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-storing-xml-data-out-of-the-row"></a>R. Archiviazione di dati xml all'esterno delle righe  
 Nell'esempio seguente specifica che il **xml** i dati nel `HumanResources.JobCandidate` tabella archiviati all'esterno delle righe.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_tableoption 'HumanResources.JobCandidate', 'large value types out of row', 1;  
```  
  
### <a name="b-enabling-vardecimal-storage-format-on-a-table"></a>B. Abilitazione del formato di archiviazione vardecimal in una tabella  
 Nell'esempio seguente viene modificato il `Production.WorkOrderRouting` tabella per archiviare il `decimal` tipo di dati di `vardecimal` il formato di archiviazione.  

```sql  
USE master;  
GO  
-- The database must be enabled for vardecimal storage format  
-- before a table can be enabled for vardecimal storage format  
EXEC sp_db_vardecimal_storage_format 'AdventureWorks2012', 'ON';  
GO  
USE AdventureWorks2012;  
GO  
EXEC sp_tableoption 'Production.WorkOrderRouting',   
   'vardecimal storage format', 'ON';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Motore di database le Stored procedure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
