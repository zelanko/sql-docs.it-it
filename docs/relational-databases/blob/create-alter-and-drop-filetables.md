---
title: Creare, modificare ed eliminare FileTable | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], altering
- FileTables [SQL Server], dropping
- FileTables [SQL Server], creating
ms.assetid: 47d69e37-8778-4630-809b-2261b5c41c2c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cfe7ea1c88a6d7118be63314824a479bd108f070
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65094358"
---
# <a name="create-alter-and-drop-filetables"></a>Creare, modificare e rilasciare FileTables
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Viene descritto come creare una nuova tabella FileTable o modificarne o eliminarne una esistente.  
  
##  <a name="BasicsCreate"></a> Creazione di una tabella FileTable  
 Una tabella FileTable è una tabella utente specializzata con uno schema predefinito e fisso. In questo schema sono archiviati dati FILESTREAM, informazioni su file e directory e attributi dei file. Per informazioni sullo schema FileTable, vedere [FileTable Schema](../../relational-databases/blob/filetable-schema.md).  
  
 È possibile creare una nuova tabella FileTable tramite Transact-SQL o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Poiché una tabella FileTable ha uno schema fisso, non è necessario specificare un elenco di colonne. La sintassi semplice per la creazione di una tabella FileTable consente di specificare gli elementi seguenti:  
  
-   Nome di directory. Nella gerarchia di cartelle FileTable questa directory a livello di tabella diventa il figlio della directory dei database specificata a livello di database e il padre delle directory o dei file archiviati nella tabella.  
  
-   Nome delle regole di confronto da utilizzare per i nomi di file nella colonna **Name** della tabella FileTable.  
  
-   Nomi da utilizzare per i 3 vincoli di chiave primaria e univoci creati automaticamente.  
  
###  <a name="HowToCreate"></a> Procedura: Creare una tabella FileTable  
 **Creare una tabella FileTable tramite Transact-SQL**  
 Creare una tabella FileTable chiamando l'istruzione [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md) con l'opzione **AS FileTable**. Poiché una tabella FileTable ha uno schema fisso, non è necessario specificare un elenco di colonne. È invece possibile specificare le impostazioni seguenti per la nuova tabella FileTable:  
  
1.  **FILETABLE_DIRECTORY**. Specifica la directory che serve come directory radice per tutti i file e le directory archiviata in FileTable. Questo nome deve essere univoco tra tutti i nomi di directory FileTable nel database. Nel confronto dell'univocità non viene applicata la distinzione tra maiuscole e minuscole, indipendentemente dalle impostazioni delle regole di confronto correnti.  
  
    -   Questo valore è di tipo **nvarchar(255)** e usa regole di confronto fisse **Latin1_General_CI_AS_KS_WS**.  
  
    -   Il nome di directory specificato deve essere conforme ai requisiti del file system relativi ai nomi di directory validi.  
  
    -   Questo nome deve essere univoco tra tutti i nomi di directory FileTable nel database. Nel confronto dell'univocità non viene applicata la distinzione tra maiuscole e minuscole, indipendentemente dalle impostazioni delle regole di confronto correnti.  
  
    -   Se non si fornisce un nome di directory quando si crea la tabella FileTable, allora il suo nome viene utilizzato come nome di directory.  
  
2.  **FILETABLE_COLLATE_FILENAME**. Specifica il nome delle regole di confronto da applicare alla colonna **Name** della tabella FileTable.  
  
    1.  Nelle regole di confronto specificate deve essere fatta una **distinzione tra maiuscole e minuscole** affinché siano conformi alla semantica di denominazione file di Windows.  
  
    2.  Se non si specifica un valore per **FILETABLE_COLLATE_FILENAME**o si specifica **database_default**, la colonna eredita le regole di confronto del database corrente. Se nelle regole di confronto del database corrente viene applicata la distinzione tra maiuscole e minuscole, viene generato un errore e l'operazione **CREATE TABLE** non viene completata.  
  
3.  È inoltre possibile specificare i nomi da utilizzare per i 3 vincoli di chiave primaria e univoci creati automaticamente. Se non si forniscono nomi, vengono generati dal sistema come descritto più avanti in questo argomento.  
  
    -   **FILETABLE_PRIMARY_KEY_CONSTRAINT_NAME**  
  
    -   **FILETABLE_STREAMID_UNIQUE_CONSTRAINT_NAME**  
  
    -   **FILETABLE_FULLPATH_UNIQUE_CONSTRAINT_NAME**  
  
 **Esempi**  
  
 Nell'esempio seguente viene creata una nuova tabella FileTable e vengono specificati valori definiti dall'utente sia per **FILETABLE_DIRECTORY** che per **FILETABLE_COLLATE_FILENAME**.  
  
```sql  
CREATE TABLE DocumentStore AS FileTable  
    WITH (   
          FileTable_Directory = 'DocumentTable',  
          FileTable_Collate_Filename = database_default  
         );  
GO  
```  
  
 Nell'esempio seguente viene inoltre creata una nuova tabella FileTable. Poiché non sono specificati valori definiti dall'utente, il valore di **FILETABLE_DIRECTORY** diventa il nome della tabella FileTable, il valore di **FILETABLE_COLLATE_FILENAME** diventa database_default e tramite i vincoli di chiave primaria e univoci si ricevono i nomi generati dal sistema.  
  
```sql  
CREATE TABLE DocumentStore AS FileTable;  
GO  
```  
  
 **Creare una tabella FileTable tramite SQL Server Management Studio**  
 In Esplora oggetti espandere gli oggetti inclusi nel database selezionato, fare clic con il pulsante destro del mouse sulla cartella **Tabelle** , quindi scegliere **Nuova FileTable**.  
  
 Verrà visualizzata una nuova finestra di script contenente un modello di script Transact-SQL, che è possibile personalizzare ed eseguire per creare una tabella FileTable. Per personalizzare facilmente lo script, utilizzare l'opzione **Imposta valori per parametri modello** dal menu **Query** .  
  
###  <a name="ReqCreate"></a> Requisiti e restrizioni per la creazione di una tabella FileTable  
  
-   Non è possibile modificare una tabella esistente per convertirla in tabella FileTable.  
  
-   La directory padre specificata precedentemente a livello di database deve includere un valore diverso da Null. Per informazioni sulla specifica della directory a livello di database, vedere [Abilitazione dei prerequisiti per la tabella FileTable](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md).  
  
-   Poiché una tabella FileTable contiene una colonna FILESTREAM, tale tabella richiede un filegroup FILESTREAM valido. È eventualmente possibile specificare un filegroup FILESTREAM valido come parte del comando **CREATE TABLE** per la creazione di una tabella FileTable. Se non si specifica un filegroup, la tabella FileTable utilizza il filegroup FILESTREAM predefinito per il database. Se il database non include un filegroup FILESTREAM, viene generato un errore.  
  
-   Non è possibile creare un vincolo di tabella come parte di un'istruzione **CREATE TABLE...AS FILETABLE**. Sarà tuttavia possibile aggiungere il vincolo in seguito utilizzando un'istruzione **ALTER TABLE** .  
  
-   Non è possibile creare una tabella FileTable nel database **tempdb** o in qualsiasi altro database di sistema.  
  
-   Non è possibile creare una tabella FileTable come tabella temporanea.  
  
##  <a name="BasicsAlter"></a> Modifica di una tabella FileTable  
 Poiché una tabella FileTable ha uno schema predefinito e fisso, non è possibile aggiungere colonne o modificarle. È invece possibile aggiungere indici, trigger, vincoli e altri elementi personalizzati a una tabella FileTable.  
  
 Per informazioni sull'uso dell'istruzione ALTER TABLE per abilitare o disabilitare lo spazio dei nomi FileTable, inclusi i vincoli definiti dal sistema, vedere [Gestione di tabelle FileTable](../../relational-databases/blob/manage-filetables.md).  
  
###  <a name="HowToChange"></a> Procedura: Modificare la directory per una tabella FileTable  
 **Modificare la directory per una tabella FileTable tramite Transact-SQL**  
 Chiamare l'istruzione ALTER TABLE e specificare un nuovo valore valido per l'opzione SET di **FILETABLE_DIRECTORY** .  
  
 **Esempio**  
  
```sql  
ALTER TABLE filetable_name  
    SET ( FILETABLE_DIRECTORY = N'directory_name' );  
GO  
```  
  
 **Modificare la directory per una tabella FileTable tramite SQL Server Management Studio**  
 In Esplora oggetti fare clic con il pulsante destro del mouse sulla tabella FileTable e selezionare **Proprietà** per aprire la finestra di dialogo **Proprietà tabella** . Nella pagina **FileTable** immettere un nuovo valore per **Nome di directory FileTable**.  
  
###  <a name="ReqAlter"></a> Requisiti e restrizioni per la modifica di una tabella FileTable  
  
-   Non è possibile modificare il valore di **FILETABLE_COLLATE_FILENAME**.  
  
-   Non è possibile modificare, eliminare o disabilitare le colonne definite dal sistema di una tabella FileTable.  
  
-   Non è possibile aggiungere nuove colonne utente, colonne calcolate o colonne calcolate persistenti a una tabella FileTable.  
  
##  <a name="BasicsDrop"></a> Eliminazione di una tabella FileTable  
 È possibile eliminare una tabella FileTable tramite la sintassi ordinaria dell'istruzione [DROP TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md).  
  
 Quando si elimina una tabella FileTable, anche i seguenti oggetti vengono eliminati:  
  
-   Vengono inoltre rilasciate tutte le colonne della tabella FileTable e tutti gli oggetti a essa associati, come gli indici, i vincoli e i trigger.  
  
-   La directory FileTable e le sottodirectory in essa contenute scompaiono dal file FILESTREAM e dalla gerarchia di directory del database.  
  
 Il comando DROP TABLE ha esito negativo se nello spazio dei nomi dei file della tabella FileTable sono presenti handle di file aperti. Per informazioni sulla chiusura di handle aperti, vedere [Gestione di tabelle FileTable](../../relational-databases/blob/manage-filetables.md).  
  
##  <a name="BasicsOtherObjects"></a> Quando si crea una tabella FileTable, vengono creati altri oggetti di database  
 Quando si crea una nuova tabella FileTable, vengono creati anche alcuni indici e vincoli definiti dal sistema. Non è possibile modificare o eliminare questi oggetti, che verranno eliminato solo all'eliminazione della tabella FileTable stessa. Per visualizzare l'elenco di questi oggetti, eseguire una query sulla vista del catalogo [sys.filetable_system_defined_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql.md).  
  
```sql  
--View all objects for all filetables, unsorted  
SELECT * FROM sys.filetable_system_defined_objects;  
GO  
  
--View sorted list with friendly names  
SELECT OBJECT_NAME(parent_object_id) AS 'FileTable', OBJECT_NAME(object_id) AS 'System-defined Object'  
    FROM sys.filetable_system_defined_objects  
    ORDER BY FileTable, 'System-defined Object';  
GO  
```  
  
 **Indici creati durante la creazione di una nuova tabella FileTable**  
 Quando si crea una nuova tabella FileTable, vengono creati anche gli indici definiti dal sistema seguenti:  
  
|||  
|-|-|  
|**Colonne**|**Tipo di indice**|  
|[path_locator] ASC|Chiave primaria, non cluster|  
|[parent_path_locator] ASC,<br /><br /> [name] ASC|Univoco, non cluster|  
|[stream_id] ASC|Univoco, non cluster|  
  
 **Vincoli creati durante la creazione di una nuova tabella FileTable**  
 Quando si crea una nuova tabella FileTable, vengono creati anche i vincoli definiti dal sistema seguenti:  
  
|Vincoli|Imposizioni|  
|-----------------|--------------|  
|Vincoli predefiniti sulle seguenti colonne:<br /><br /> creation_time<br /><br /> is_archive<br /><br /> is_directory<br /><br /> is_hidden<br /><br /> is_offline<br /><br /> is_readonly<br /><br /> is_system<br /><br /> is_temporary<br /><br /> last_access_time<br /><br /> last_write_time<br /><br /> path_locator<br /><br /> stream_id|I vincoli predefiniti definiti dal sistema applicano valori predefiniti per le colonne specificate.|  
|Vincoli CHECK|I vincoli CHECK definiti dal sistema applicano i requisiti seguenti:<br /><br /> Nomi file validi.<br /><br /> Attributi di file validi.<br /><br /> L'oggetto padre deve essere una directory.<br /><br /> La gerarchia dello spazio dei nomi è bloccata durante la modifica dei file.|  
  
 **Convenzione di denominazione per i vincoli definiti dal sistema**  
 I vincoli definiti dal sistema descritti in precedenza vengono denominati usando il formato **\<tipovincolo>_\<nometabella>[\_\<nomecolonna>]\_\<identificatoreunivoco>**, dove:  
  
-   *<tipovincolo>* è CK (vincolo CHECK), DF (vincolo DEFAULT), FK (chiave esterna), PK (chiave primaria) o UQ (vincolo UNIQUE).  
  
-   *\<identificatoreunivoco* è una stringa generata dal sistema per specificare un nome univoco. È possibile che questa stringa contenga il nome della tabella FileTable e un identificatore univoco.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestire tabelle FileTable](../../relational-databases/blob/manage-filetables.md)  
  
  
