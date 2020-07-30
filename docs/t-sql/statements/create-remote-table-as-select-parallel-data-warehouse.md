---
title: CREATE REMOTE TABLE AS SELECT (Parallel Data Warehouse)
ms.custom: seo-dt-2019
ms.date: 08/10/2017
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.assetid: 16ef8191-7587-45a3-9ee9-7d99b7088de3
author: ronortloff
ms.author: rortloff
ms.reviewer: jrasnick
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4547fe6ae7282aa95ed2b1e46c47a5a07aa20f11
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2020
ms.locfileid: "87395246"
---
# <a name="create-remote-table-as-select-parallel-data-warehouse"></a>CREATE REMOTE TABLE AS SELECT (Parallel Data Warehouse)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Seleziona i dati da un database [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] e li copia in una nuova tabella in un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SMP in un server remoto. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] usa l'appliance, con tutti i vantaggi dell'elaborazione di query MPP, per selezionare i dati per la copia remota. Usare questa istruzioni per gli scenari che richiedono funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Per configurare il server remoto, vedere la sezione relativa alla copia di tabelle remote nella [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```syntaxsql
  
CREATE REMOTE TABLE { database_name.schema_name.table_name | schema_name.table_name | table_name }  AT ('<connection_string>')  
    [ WITH ( BATCH_SIZE = batch_size ) ]  
    AS <select_statement>  
[;]  
  
<connection_string> ::=   
    Data Source = { IP_address | hostname } [, port ]; User ID = user_name ;Password = password;  
  
<select_statement> ::=  
    [ WITH <common_table_expression> [ ,...n ] ]  
    SELECT <select_criteria>  
```  
  
## <a name="arguments"></a>Argomenti  
 *database_name*  
 Database in cui creare la tabella remota. *database_name* è un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. L'impostazione predefinita corrisponde al database predefinito per l'account di accesso utente nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione.  
  
 *schema_name*  
 Schema della nuova tabella. L'impostazione predefinita corrisponde allo schema predefinito per l'account di accesso utente nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione.  
  
 *table_name*  
 Nome della nuova tabella. Per dettagli sui nomi di tabella consentiti, vedere la sezione relativa alle regole di denominazione degli oggetti nella [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 La tabella remota viene creata come heap. Non ha vincoli check o trigger. Le regole di confronto delle colonne della tabella remota corrispondono alle regole di confronto delle colonne della tabella di origine. Questo vale per le colonne di tipo **char**, **varchar**, **nchar** e **nvarchar**.  
  
 *connection_string*  
 Stringa di caratteri che specifica i parametri `Data Source`, `User ID` e `Password` per la connessione al server remoto e al database.  
  
 La stringa di connessione è un elenco di valori delimitati da punto e virgola di coppie chiave-valore. Le parole chiave non fanno distinzione tra maiuscole e minuscole. Gli spazi tra le coppie chiave-valore vengono ignorati. I valori, tuttavia, possono fare distinzione tra maiuscole e minuscole, a seconda dell'origine dati.  
  
 *Origine dati*  
 Parametro che specifica il nome o l'indirizzo IP e il numero di porta TCP per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dell'SMP remoto.  
  
 *hostname* o *IP_address*  
 Nome o indirizzo IPv4 del server remoto. Gli indirizzi IPv6 non sono supportati. È possibile specificare un'istanza denominata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel formato **Nome_computer\Nome_istanza** o **Indirizzo_IP\Nome_istanza**. Il server deve essere remoto e pertanto non può essere specificato come (local).  
  
 Numero *porta* TCP  
 Numero della porta TCP usata per la connessione. Per un'istanza di SQL Server che non è in ascolto sulla porta predefinita 1433, è possibile specificare un numero di porta TCP compreso tra 0 e 65535. Ad esempio: **ServerA,1450** o **10.192.14.27,1435**  
  
> [!NOTE]  
>  È consigliabile connettersi a un server remoto tramite indirizzo IP. A seconda della configurazione di rete, la connessione tramite nome computer potrebbe richiedere passaggi aggiuntivi perché sia possibile usare il server DNS non appliance per risolvere il nome server in modo corretto. Questo passaggio non è necessario se ci si connette con un indirizzo IP. Per altre informazioni, vedere la sezione relativa all'uso di un server d'inoltro DNS per risolvere i nomi DNS non di appliance (piattaforma di strumenti analitici) nella [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 *user_name*  
 ID di accesso valido per l'autenticazione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il numero massimo di caratteri è 128.  
  
 *password*  
 Password di accesso. Il numero massimo di caratteri è 128.  
  
 *batch_size*  
 Numero massimo di righe per batch. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] invia le righe in batch al server di destinazione. *Batch_size* è un numero intero positivo >= 0. Il valore predefinito è 0.  
  
 WITH *common_table_expression*  
 Indica un set di risultati denominato temporaneo, noto come espressione di tabella comune (CTE). Per altre informazioni, vedere [WITH common_table_expression &#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 SELECT \<select_criteria> Predicato di query che specifica quali dati popoleranno la nuova tabella remota. Per informazioni sull'istruzione SELECT, vedere [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md).  
  
## <a name="permissions"></a>Autorizzazioni  
 Richiede:  
  
-   Autorizzazione SELECT per ogni oggetto nella clausola SELECT.  
  
-   Autorizzazione CREATE TABLE per il database SMP di destinazione.  
  
-   Autorizzazioni ALTER, INSERT e SELECT per lo schema SMP di destinazione.  
  
## <a name="error-handling"></a>Gestione degli errori  
 Se la copia dei dati nel database remoto non riesce, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] interrompe l'operazione, registra un errore e tenta di eliminare la tabella remota. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] non garantisce una pulizia corretta della nuova tabella.  
  
## <a name="limitations-and-restrictions"></a>Limitazioni e restrizioni  
 **Server di destinazione remoto**:  
  
-   TCP è il protocollo predefinito e l'unico protocollo supportato per la connessione a un server remoto.  
  
-   Il server di destinazione deve essere un server non appliance. L'istruzione CREATE REMOTE TABLE non può essere usata per copiare dati da un'appliance a un'altra.  
  
-   L'istruzione CREATE REMOTE TABLE crea solo nuove tabelle. La nuova tabella, quindi, non può essere già esistente. Il database remoto e lo schema devono essere già esistenti.  
  
-   Il server remoto deve avere spazio disponibile per archiviare i dati che vengono trasferiti dall'appliance per il database remoto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Istruzione SELECT**:  
  
-   Le clausole ORDER BY e TOP non sono supportate nei criteri di selezione.  
  
-   L'istruzione CREATE REMOTE TABLE non può essere eseguita all'interno di una transazione attiva o quando l'impostazione AUTOCOMMIT corrisponde a OFF per la sessione.  
  
 [SET ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/statements/set-rowcount-transact-sql.md) non influisce su questa istruzione. Per ottenere un comportamento simile, usare [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md).  
  
## <a name="locking-behavior"></a>Comportamento di blocco  
 Dopo la creazione della tabella remota, la tabella di destinazione viene bloccata solo all'avvio della copia. È pertanto possibile che un altro processo elimini la tabella remota dopo che è stata creata e prima che la copia venga avviata. In questo caso, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] genera un errore e la copia non riesce.  
  
## <a name="metadata"></a>Metadati  
 Usare [sys.dm_pdw_dms_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md) per visualizzare lo stato della copia dei dati selezionati nel server SMP remoto. Queste informazioni sono contenute all'interno di righe di tipo PARALLEL_COPY_READER.  
  
## <a name="security"></a>Sicurezza  
 CREATE REMOTE TABLE usa l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] remota; non usa l'autenticazione di Windows.  
  
 La rete [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] connessa con l'esterno deve essere protetta tramite firewall, ad eccezione delle porte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], delle porte amministrative e delle porte di gestione.  
  
 Per evitare la perdita o il danneggiamento accidentale di dati, l'account utente usato per copiare dall'appliance al database di destinazione deve avere solo le autorizzazioni minime necessarie per il database di destinazione.  
  
 Le impostazioni di connessione consentono di connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SMP proteggendo i dati relativi a nome utente e password tramite SSL, ma inviando i dati effettivi in testo non crittografato. In questo caso, un utente malintenzionato può intercettare il testo dell'istruzione CREATE REMOTE TABLE, che contiene il nome utente e la password per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], per accedere all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SMP. Per evitare questo rischio, usare la crittografia dei dati per la connessione all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SMP.  
  
##  <a name="examples"></a><a name="Examples"></a> Esempi  
  
### <a name="a-creating-a-remote-table"></a>R. Creazione di una tabella remota  
 Questo esempio crea una tabella remota di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SMP `MyOrdersTable` nel database `OrderReporting` e nello schema `Orders`. Il database `OrderReporting` si trova in un server denominato `SQLA` in ascolto sulla porta predefinita 1433. La connessione al server usa le credenziali dell'utente `David`, la cui password è `e4n8@3`.  
  
```  
CREATE REMOTE TABLE OrderReporting.Orders.MyOrdersTable  
AT ( 'Data Source = SQLA, 1433; User ID = David; Password = e4n8@3;' )  
AS SELECT <select_criteria>;  
```  
  
### <a name="b-querying-the-sysdm_pdw_dms_workers-dmv-for-remote-table-copy-status"></a>B. Query del DMV sys.dm_pdw_dms_workers per lo stato della copia di tabelle remote  
 Questa query illustra come visualizzare lo stato della copia di tabelle remote.  
  
```  
SELECT * FROM sys.dm_pdw_dms_workers   
WHERE type = 'PARALLEL_COPY_READER';  
```  
  
### <a name="c-using-a-query-join-hint-with-create-remote-table"></a>C. Uso di un hint di join per la query con CREATE REMOTE TABLE  
 Questa query illustra la sintassi di base per l'uso di un hint di join per la query con CREATE REMOTE TABLE. Dopo l'invio della query al nodo di controllo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], in esecuzione nei nodi di calcolo, genera il piano di query di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] applicando la strategia di hash join. Per altre informazioni sugli hint di join e su come usare la clausola OPTION, vedere [Clausola OPTION &#40;Transact-SQL&#41;](../../t-sql/queries/option-clause-transact-sql.md).  
  
```  
USE ssawPDW;  
CREATE REMOTE TABLE OrderReporting.Orders.MyOrdersTable  
AT ( 'Data Source = SQLA, 1433; User ID = David; Password = e4n8@3;' )  
    AS SELECT T1.* FROM OrderReporting.Orders.MyOrdersTable T1   
    JOIN OrderReporting.Order.Customer T2  
    ON T1.CustomerID=T2.CustomerID OPTION (HASH JOIN);  
```  
  
  

