---
title: Caricamento bulk dei dati tramite la destinazione SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server destination
- loading data
- destinations [Integration Services], SQL Server
- inserting data
- bulk load [Integration Services]
ms.assetid: 8f982f85-a82e-4e2d-9cd8-cd2f85402d8e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: bf8e8c7bafb72b90edfe108c5702ad330bc3e700
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293473"
---
# <a name="bulk-load-data-by-using-the-sql-server-destination"></a>Caricamento bulk dei dati tramite la destinazione SQL Server

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  È possibile aggiungere e configurare una destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo se il pacchetto include già almeno un'attività Flusso di dati e un'origine dati.  
  
### <a name="to-load-data-using-a-sql-server-destination"></a>Per caricare dati tramite una destinazione SQL Server  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di dati** e quindi trascinare la destinazione **dalla**casella degli strumenti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] all'area di progettazione.  
  
4.  Connettere la destinazione a un'origine o una trasformazione precedente nel flusso di dati trascinando un connettore fino alla destinazione.  
  
5.  Fare doppio clic sulla destinazione.  
  
6.  Nella pagina **Gestione connessione**della finestra di dialogo **Editor destinazione SQL Server** selezionare una gestione connessione OLE DB esistente oppure fare clic su **Nuova** per creare una nuova gestione connessione. Per altre informazioni, vedere [Gestione connessione OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
7.  Per specificare la tabella o vista in cui caricare i dati, eseguire una delle operazioni seguenti:  
  
    -   Selezionare una tabella o vista esistente.  
  
    -   Fare clic su **Nuovo**e quindi nella finestra di dialogo **Crea tabella** scrivere un'istruzione SQL che crea una tabella o una vista.  
  
        > [!NOTE]  
        >  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] genera un'istruzione CREATE TABLE predefinita basata sull'origine dati connessa. Questa istruzione CREATE TABLE predefinita non includerà l'attributo FILESTREAM anche se la tabella di origine include una colonna con l'attributo FILESTREAM dichiarato. Per eseguire un componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con l'attributo FILESTREAM, implementare innanzitutto l'archiviazione di FILESTREAM nel database di destinazione. Aggiungere quindi l'attributo FILESTREAM all'istruzione CREATE TABLE nella finestra di dialogo **Crea tabella**. Per altre informazioni, vedere [Dati BLOB &#40;Binary Large Object&#41; &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
8.  Fare clic su **Mapping** ed eseguire il mapping delle colonne nell'elenco **Colonne di input disponibili** alle colonne nell'elenco **Colonne di destinazione disponibili**, trascinando le colonne da un elenco all'altro.  
  
    > [!NOTE]  
    >  La destinazione esegue automaticamente il mapping delle colonne con lo stesso nome.  
  
9. Fare clic su **Avanzate** e impostare le opzioni di caricamento bulk: **Mantieni valori Identity**, **Mantieni valori Null**, **Blocco di tabella**, **Verifica vincoli**e **Attiva trigger**.  
  
     Facoltativamente, specificare la prima e l'ultima riga di input da inserire, il numero massimo di errori che possono verificarsi prima che l'operazione di inserimento venga arrestata e le colonne in base alle quali viene ordinato l'inserimento.  
  
    > [!NOTE]  
    >  Il tipo di ordinamento è determinato dall'ordine in cui sono elencate le colonne.  
  
10. Fare clic su **OK**.  
  
11. Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Destination](../../integration-services/data-flow/sql-server-destination.md)   
 [Trasformazioni di Integration Services](../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Percorsi in Integration Services](../../integration-services/data-flow/integration-services-paths.md)   
 [Attività Flusso di dati](../../integration-services/control-flow/data-flow-task.md)  
  
  
