---
title: Specificare la modalità di propagazione delle modifiche per gli articoli transazionali | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, propagation methods
ms.assetid: a10c5001-22cc-4667-8f0b-3d0818dca2e9
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: eb07987bfdca341a01a523c13db3e346ab5085f2
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85016565"
---
# <a name="specify-how-changes-are-propagated-for-transactional-articles"></a>Impostazione della modalità di propagazione delle modifiche per gli articoli transazionali
  La replica transazionale consente di specificare la modalità di propagazione delle modifiche dei dati dal server di pubblicazione ai Sottoscrittori. Per ogni tabella pubblicata è possibile specificare una delle quattro modalità con cui ogni operazione (INSERT, UPDATE o DELETE) dovrebbe propagarsi al Sottoscrittore:  
  
-   Specificare che la replica transazionale deve inserire in uno script e in un secondo momento chiamare una stored procedure per propagare le modifiche ai Sottoscrittori (impostazione predefinita).  
  
-   Specificare la necessità che la modifica si propaghi tramite un'istruzione INSERT, UPDATE o DELETE (impostazione predefinita per i Sottoscrittori in cui non è in esecuzione[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ).  
  
-   Specificare che è necessario utilizzare una stored procedure personalizzata.  
  
-   Specificare che l'azione non deve essere eseguita in alcun Sottoscrittore. In tal caso le transazioni non vengono replicate.  
  
 Per impostazione predefinita, la replica transazionale propaga le modifiche ai Sottoscrittori utilizzando un set di stored procedure installate in ogni Sottoscrittore. Quando in una tabella del server di pubblicazione ha luogo un inserimento, un aggiornamento o un'eliminazione, l'operazione viene convertita in una chiamata a una stored procedure nel Sottoscrittore. La stored procedure accetta parametri che eseguono il mapping alle colonne della tabella, consentendo a tali colonne di essere modificate nel Sottoscrittore.  
  
 Per impostare il metodo di propagazione per la modifica dei dati negli articoli transazionali, vedere [Impostazione del metodo di propagazione per le modifiche ai dati negli articoli transazionali](../publish/set-the-propagation-method-for-data-changes-to-transactional-articles.md).  
  
## <a name="default-and-custom-stored-procedures"></a>Stored procedure predefinite e personalizzate  
 Le tre procedure che la replica crea per impostazione predefinita per ogni articolo di tabella sono:  
  
-   **sp_MSins_ \<** *tablename* **> **, che gestisce gli inserimenti.  
  
-   **sp_MSupd_ \<** *tablename* **> **, che gestisce gli aggiornamenti.  
  
-   **sp_MSdel_ \<** *tablename* **> **, che gestisce le eliminazioni.  
  
 Il **\<***tablename***>** utilizzato nella procedura dipende dalla modalità di aggiunta dell'articolo alla pubblicazione e dal fatto che il database di sottoscrizione contenga una tabella con lo stesso nome con un proprietario diverso.  
  
 Ognuna di queste procedure può essere sostituita da una procedura personalizzata che viene specificata durante l'aggiunta di un articolo a una pubblicazione. Le procedure personalizzate vengono utilizzate se un'applicazione richiede una logica personalizzata, ad esempio l'inserimento di dati in una tabella di controllo quando una riga viene aggiornata in un Sottoscrittore. Per ulteriori informazioni sulla definizione di stored procedure personalizzate, vedere l'elenco delle procedure riportato sopra.  
  
 Se si specificano le procedure di replica predefinite o le procedure personalizzate, verrà anche specificata la sintassi di chiamata per ogni procedura. Se si utilizzano le procedure predefinite, la replica selezionerà i valori predefiniti. La sintassi di chiamata determina la struttura dei parametri forniti alla procedura e la quantità di informazioni inviate al Sottoscrittore a ogni modifica dei dati. Per ulteriori informazioni, vedere la sezione "Sintassi di chiamata per le stored procedure" più avanti in questo argomento.  
  
### <a name="considerations-for-using-custom-stored-procedures"></a>Considerazioni per l'utilizzo di stored procedure personalizzate  
 È bene tenere a mente le seguenti considerazioni quando si utilizzano stored procedure personalizzate:  
  
-   È necessario supportare la logica presente nella stored procedure. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] non fornisce il supporto per la logica personalizzata.  
  
-   Per evitare conflitti con le transazioni utilizzate dalla replica, non utilizzare le transazioni esplicite nelle procedure personalizzate.  
  
-   Lo schema nel Sottoscrittore è in genere identico allo schema nel server di pubblicazione, ma può essere anche un subset dello schema del server di pubblicazione se viene utilizzato il filtro delle colonne. Tuttavia, se è necessario trasformare lo schema mentre i dati vengono spostati in modo che lo schema del Sottoscrittore non sia un subset dello schema nel server di pubblicazione, [!INCLUDE[ssISCurrent](../../../includes/ssiscurrent-md.md)] è la soluzione consigliata. Per altre informazioni, vedere [SQL Server Integration Services](../../../integration-services/sql-server-integration-services.md).  
  
-   Se si apportano modifiche allo schema in una tabella pubblicata, è necessario rigenerare le procedure personalizzate. Per altre informazioni, vedere [Rigenerare procedure transazionali personalizzate per riflettere le modifiche dello schema](transactional-articles-regenerate-to-reflect-schema-changes.md).  
  
-   Se si usa un valore maggiore di 1 per il parametro **-SubscriptionStreams** dell'agente di distribuzione, sarà necessario verificare che vengano completati gli aggiornamenti alle colonne chiave primaria. Ad esempio:  
  
    ```  
    update ... set pk = 2 where pk = 1 -- update 1  
    update ... set pk = 3 where pk = 2 -- update 2  
    ```  
  
     Se l'agente di distribuzione utilizza più di una connessione, questi due aggiornamenti potrebbero essere replicati su diverse connessioni. Se l'aggiornamento 1 viene applicato per primo, non vi sono problemi; se l'aggiornamento 2 viene applicato per primo, restituirà "Righe interessate 0" in quanto l'aggiornamento 1 non ha ancora avuto luogo. Questa situazione viene gestita nelle procedure predefinite con la generazione di un errore se nessuna riga è interessata da un aggiornamento:  
  
    ```  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sys.sp_MSreplraiserror 20598  
    ```  
  
     La generazione di un errore obbliga l'agente di distribuzione a riprovare il processo di aggiornamento su una singola connessione. Il processo verrà eseguito correttamente. È necessario che le stored procedure personalizzate includano una logica simile.  
  
### <a name="call-syntax-for-stored-procedures"></a>Sintassi di chiamata per le stored procedure  
 Sono disponibili cinque opzioni per la sintassi che consente di chiamare le procedure utilizzate dalla replica transazionale:  
  
-   Sintassi CALL. Può essere utilizzata per gli inserimenti, gli aggiornamenti e le eliminazioni. Per impostazione predefinita, la replica utilizza questa sintassi per gli inserimenti e le eliminazioni.  
  
-   Sintassi SCALL. Può essere utilizzata solo per gli aggiornamenti. Per impostazione predefinita, la replica utilizza questa sintassi per gli aggiornamenti.  
  
-   Sintassi MCALL. Può essere utilizzata solo per gli aggiornamenti.  
  
-   Sintassi XCALL. Può essere utilizzata per gli aggiornamenti e le eliminazioni.  
  
-   VCALL. Utilizzata per le sottoscrizioni aggiornabili. Solo per uso interno.  
  
 Questi metodi si differenziano per la quantità di dati propagati al Sottoscrittore. Con la sintassi SCALL, ad esempio, vengono passati esclusivamente i valori delle colonne effettivamente interessate da un aggiornamento. Con la sintassi XCALL vengono invece passate tutte le colonne, interessate o meno da un aggiornamento, e tutti i valori di dati precedenti per ogni colonna. In molti casi la sintassi appropriata per gli aggiornamenti è SCALL, ma se durante un aggiornamento l'applicazione in uso richiede tutti i valori di dati, è la sintassi XCALL a consentire che ciò avvenga.  
  
#### <a name="call-syntax"></a>Sintassi CALL  
 Stored procedure INSERT  
 Alle stored procedure che gestiscono istruzioni INSERT vengono passati i valori inseriti per tutte le colonne:  
  
```  
c1, c2, c3,... cn  
```  
  
 Stored procedure UPDATE  
 Alle stored procedure che gestiscono istruzioni UPDATE vengono passati i valori aggiornati per tutte le colonne definite nell'articolo, seguiti dai valori originali per le colonne chiave primaria. Non viene effettuato alcun tentativo per determinare quali colonne siano state modificate:  
  
```  
c1, c2, c3,... cn, pkc1, pkc2, pkc3,... pkcn  
```  
  
 Stored procedure DELETE  
 Alle stored procedure che gestiscono istruzioni DELETE vengono passati i valori per le colonne chiave primaria:  
  
```  
pkc1, pkc2, pkc3,... pkcn  
```  
  
#### <a name="scall-syntax"></a>Sintassi SCALL  
 Stored procedure UPDATE  
 Alle stored procedure che gestiscono istruzioni UPDATE vengono passati i valori aggiornati solo per le colonne che sono state modificate, seguiti dai valori originali per le colonne di chiavi primarie e da un parametro di maschera di bit (`binary(n)`) che indica le colonne modificate. Nell'esempio seguente la colonna 2 (c2) non è stata modificata:  
  
```  
c1, , c3,... cn, pkc1, pkc2, pkc3,... pkcn, bitmask  
```  
  
#### <a name="mcall-syntax"></a>Sintassi MCALL  
 Stored procedure UPDATE  
 Alle stored procedure che gestiscono istruzioni UPDATE vengono passati i valori aggiornati per tutte le colonne definite nell'articolo, seguiti dai valori originali per le colonne di chiavi primarie e da un parametro di maschera di bit (`binary(n)`) che indica le colonne modificate:  
  
```  
c1, c2, c3,... cn, pkc1, pkc2, pkc3,... pkcn, bitmask  
```  
  
#### <a name="xcall-syntax"></a>Sintassi XCALL  
 Stored procedure UPDATE  
 Alle stored procedure che gestiscono istruzioni UPDATE vengono passati i valori originali, ovvero l'immagine precedente all'aggiornamento, per tutte le colonne definite nell'articolo, seguiti dai valori di aggiornamento, ovvero l'immagine successiva all'aggiornamento, per le stesse colonne:  
  
```  
old-c1, old-c2, old-c3,... old-cn, c1, c2, c3,... cn,  
```  
  
 Stored procedure DELETE  
 Alle stored procedure che gestiscono istruzioni DELETE vengono passati i valori originali, ovvero l'immagine precedente all'eliminazione, per tutte le colonne definite nell'articolo:  
  
```  
old-c1, old-c2, old-c3,... old-cn  
```  
  
> [!NOTE]  
>  Quando si utilizza la sintassi XCALL, i valori dell'immagine precedente per le colonne di tipo **text** e **image** saranno NULL.  
  
## <a name="examples"></a>Esempi  
 Le procedure che seguono sono le procedure predefinite create per la `Vendor Table` nel database di esempio di [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)] .  
  
```  
--INSERT procedure using CALL syntax  
create procedure [sp_MSins_PurchasingVendor]   
  @c1 int,@c2 nvarchar(15),@c3 nvarchar(50),@c4 tinyint,@c5 bit,@c6 bit,@c7 nvarchar(1024),@c8 datetime  
as   
begin   
insert into [Purchasing].[Vendor]([VendorID]  
,[AccountNumber]  
,[Name]  
,[CreditRating]  
,[PreferredVendorStatus]  
,[ActiveFlag]  
,[PurchasingWebServiceURL]  
,[ModifiedDate])  
values (   
 @c1  
,@c2  
,@c3  
,@c4  
,@c5  
,@c6  
,@c7  
,@c8  
 )   
end  
go  
  
--UPDATE procedure using SCALL syntax  
create procedure [sp_MSupd_PurchasingVendor]   
 @c1 int = null,@c2 nvarchar(15) = null,@c3 nvarchar(50) = null,@c4 tinyint = null,@c5 bit = null,@c6 bit = null,@c7 nvarchar(1024) = null,@c8 datetime = null,@pkc1 int  
,@bitmap binary(2)  
as  
begin  
update [Purchasing].[Vendor] set   
 [AccountNumber] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [AccountNumber] end  
,[Name] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [Name] end  
,[CreditRating] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [CreditRating] end  
,[PreferredVendorStatus] = case substring(@bitmap,1,1) & 16 when 16 then @c5 else [PreferredVendorStatus] end  
,[ActiveFlag] = case substring(@bitmap,1,1) & 32 when 32 then @c6 else [ActiveFlag] end  
,[PurchasingWebServiceURL] = case substring(@bitmap,1,1) & 64 when 64 then @c7 else [PurchasingWebServiceURL] end  
,[ModifiedDate] = case substring(@bitmap,1,1) & 128 when 128 then @c8 else [ModifiedDate] end  
where [VendorID] = @pkc1  
if @@rowcount = 0  
    if @@microsoftversion>0x07320000  
        exec sp_MSreplraiserror 20598  
end  
go  
  
--DELETE procedure using CALL syntax  
create procedure [sp_MSdel_PurchasingVendor]   
  @pkc1 int  
as   
begin   
delete [Purchasing].[Vendor]  
where [VendorID] = @pkc1  
if @@rowcount = 0  
    if @@microsoftversion>0x07320000  
        exec sp_MSreplraiserror 20598  
end   
go  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Article Options for Transactional Replication](article-options-for-transactional-replication.md)  
  
  
