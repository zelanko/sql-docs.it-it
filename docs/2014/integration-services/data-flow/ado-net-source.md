---
title: Origine ADO NET | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.adonetsource.f1
helpviewer_keywords:
- ADO.NET source
- sources [Integration Services], ADO.NET
- sources [Integration Services], DataReader
- .NET Framework [Integration Services]
- DataReader source
ms.assetid: 2a2f1750-2cda-4dda-9dca-623a96a6b3c0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1bc6c150f8c8f4f4e6f68b275a901ab8f1f5e8e5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62832483"
---
# <a name="ado-net-source"></a>Origine ADO NET
  L'origine ADO NET utilizza i dati di un provider .NET e li rende disponibili per il flusso di dati.  
  
 È possibile usare l'origine ADO NET per connettersi a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. La connessione a [!INCLUDE[ssSDS](../../includes/sssds-md.md)] tramite OLE DB non è supportata. Per altre informazioni su [!INCLUDE[ssSDS](../../includes/sssds-md.md)], vedere [Limitazioni e linee guida generali per il database SQL di Azure](https://go.microsoft.com/fwlink/?LinkId=248228).  
  
## <a name="data-type-support"></a>Supporto dei tipi di dati  
 Tramite l'origine viene convertito qualsiasi tipo di dati di cui non è stato eseguito il mapping a un tipo di dati specifico di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] nel tipo di dati DT_NTEXT di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . La conversione viene eseguita anche se il tipo di dati è `System.Object`.  
  
 È possibile modificare il tipo di dati DT_NTEXT nel tipo di dati DT_WSTR e vice versa. È possibile modificare i tipi di dati configurando la proprietà **DataType** nella finestra di dialogo **Editor avanzato** dell'origine ADO NET. Per altre informazioni, vedere [Proprietà comuni](../common-properties.md).  
  
 Il tipo di dati DT_NTEXT può anche essere convertito nel tipo di dati DT_BYTES o DT_STR utilizzando una trasformazione Conversione dati sull'origine ADO NET. Per altre informazioni, vedere [Trasformazione Conversione dati](transformations/data-conversion-transformation.md).  
  
 In [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]sui tipi di dati relativi alle date, DT_DBDATE, DT_DBTIME2, DT_DBTIMESTAMP2 e DT_DBTIMESTAMPOFFSET, viene eseguito il mapping a tipi di dati relativi alle date specifici in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile configurare l'origine ADO NET per convertire i tipi di dati relativi alle date usati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nei tipi usati in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Per configurare l'origine ADO NET per convertire questi tipi di dati relativi alle date, impostare la proprietà **Type System Version** della gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] su **Ultima versione**. La proprietà **Type System Version** si trova nella pagina **Tutto** della finestra di dialogo **Gestione connessione** . Per aprire la finestra di dialogo **Gestione connessione** , fare clic con il pulsante destro del mouse sulla gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] e quindi su **Modifica**.  
  
> [!NOTE]  
>  Se la proprietà **Type System Version** della gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] è impostata su **SQL Server 2005**, i tipi di dati per le date di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono convertiti in dati DT_WSTR.  
  
 I tipi di dati definiti dall'utente (UDT, User-Defined Type) vengono convertiti negli oggetti binari di grandi dimensioni (Binary Large Object) di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] quando la gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] specifica il provider come provider di dati .NET per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient). Durante la conversione del tipo di dati definito dall'utente (UDT), vengono applicate le regole seguenti:  
  
-   Se i dati sono di tipo definito dall'utente (UDT) di piccole dimensioni, vengono convertiti nel tipo di dati DT_BYTES.  
  
-   Se i dati sono di tipo definito dall'utente (UDT) non di grandi dimensioni e la proprietà **Length** della colonna nel database è impostata su -1 o su un valore maggiore di 8000 byte, i dati vengono convertiti nel tipo di dati DT_IMAGE.  
  
-   Se i dati sono di tipo definito dall'utente (UDT) di grandi dimensioni, vengono convertiti nel tipo di dati DT_IMAGE.  
  
    > [!NOTE]  
    >  Se l'origine ADO NET non è configurata per l'utilizzo dell'output degli errori, i dati vengono trasmessi alla colonna DT_IMAGE in blocchi da 8.000 byte. Se l'origine ADO NET è configurata per l'utilizzo dell'output degli errori, l'intera matrice di byte viene trasmessa alla colonna DT_IMAGE. Per altre informazioni sulla configurazione dei componenti per l'uso dell'output degli errori, vedere [Gestione degli errori nei dati](error-handling-in-data.md).  
  
 Per altre informazioni sui tipi di dati di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , sulle conversioni dei tipi di dati supportate e sul mapping dei tipi di dati in alcuni database, tra cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Tipi di dati di Integration Services](integration-services-data-types.md).  
  
 Per altre informazioni sul mapping di tipi di dati di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a tipi di dati gestiti, vedere [Utilizzo di tipi di dati nel flusso di dati](../extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md).  
  
## <a name="ado-net-source-troubleshooting"></a>Risoluzione dei problemi relativi all'origine ADO NET  
 È possibile registrare le chiamate eseguite dall'origine ADO NET a provider di dati esterni. Questa funzionalità di registrazione può essere utilizzata per risolvere i problemi relativi al caricamento di dati da origini esterne da parte dell'origine ADO NET. Per registrare le chiamate eseguite dall'origine ADO NET a provider di dati esterni, abilitare la registrazione dei pacchetti e selezionare l'evento **Diagnostic** al livello di pacchetto. Per altre informazioni, vedere [Risoluzione dei problemi relativi agli strumenti per l'esecuzione del pacchetto](../troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="ado-net-source-configuration"></a>Configurazione dell'origine ADO NET  
 Per configurare l'origine ADO NET, è necessario specificare l'istruzione SQL che definisce il set di risultati. Un'origine ADO NET che si connette ad esempio al database [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] e usa l'istruzione SQL `SELECT * FROM Production.Product` estrae tutte le righe della tabella **Production.Product** e fornisce il set di dati a un componente a valle.  
  
> [!NOTE]  
>  Quando si utilizza un'istruzione SQL per richiamare una stored procedure che restituisce risultati da una tabella temporanea, utilizzare l'opzione WITH RESULT SETS per definire metadati per il set di risultati.  
  
> [!NOTE]  
>  Se si utilizza un'istruzione SQL per eseguire una stored procedure e l'esecuzione del pacchetto ha esito negativo con l'errore seguente, è possibile risolvere il problema aggiungendo l'istruzione `SET FMTONLY OFF` prima dell'istruzione exec.  
>   
>  **Impossibile trovare la colonna <nome_colonna> nell'origine dati.**  
  
 Nell'origine ADO NET viene usata una gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] in cui è specificato il provider .NET per connettersi a un'origine dati. Per altre informazioni, vedere [Gestione connessione ADO.NET](../connection-manager/ado-net-connection-manager.md).  
  
 L'origine ADO NET include un output regolare e un output degli errori.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](../common-properties.md)  
  
-   [Proprietà personalizzate ADO NET](ado-net-custom-properties.md)  
  
 Per altre informazioni su come impostare le proprietà, vedere [Impostazione delle proprietà di un componente del flusso di dati](set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Destinazione DataReader](datareader-destination.md)   
 [Destinazione ADO NET](ado-net-destination.md)   
 [Flusso di dati](data-flow.md)  
  
  
