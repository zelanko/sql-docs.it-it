---
title: Salvare ed eseguire il pacchetto (importazione/esportazione guidata SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.saveschedule.f1
ms.assetid: b582c462-3d7a-4a4c-a2a2-2c79fedab75a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 517ba30e4565ec05e5fa15a650bb39909d24dd02
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62894765"
---
# <a name="save-and-execute-package-sql-server-import-and-export-wizard"></a>Salvataggio ed esecuzione pacchetto (Importazione/Esportazione guidata SQL Server)
  Utilizzare la finestra di dialogo **Salva ed Esegui pacchetto** per eseguire il pacchetto immediatamente, salvarlo in modo che venga eseguito in un secondo momento o in entrambi.  
  
> [!NOTE]  
>   Se l'esecuzione di un pacchetto viene arrestata prima del completamento, il pacchetto non verrà salvato, anche se si seleziona la casella di controllo **Salva** .  
  
 Per ulteriori informazioni su questa procedura guidata, vedere [SQL Server importazione/esportazione guidata](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Per informazioni sulle opzioni di avvio della procedura guidata, nonché sulle autorizzazioni necessarie per eseguire la procedura guidata, vedere [eseguire l'importazione/esportazione guidata SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 Lo scopo di Importazione/Esportazione guidata SQL Server è la copia di dati da un'origine a una destinazione. La procedura guidata può inoltre creare automaticamente un database di destinazione e le tabelle di destinazione. Se tuttavia è necessario copiare più database o tabelle, o altri tipi di oggetti di database, è preferibile utilizzare Copia guidata database. Per altre informazioni, vedere [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opzioni  
 **Esegui immediatamente**  
 Selezionare questa opzione per eseguire il pacchetto immediatamente.  
  
 **Salva pacchetto SSIS**  
 Consente di salvare il pacchetto per eseguirlo in un momento successivo con l'opzione per l'esecuzione immediata.  
  
> [!NOTE]  
>  In [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] l'opzione per salvare il pacchetto creato con la procedura guidata non è disponibile.  
  
 **SQL Server**  
 Selezionare questa opzione per salvare il pacchetto [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `msdb` nel database.  
  
> [!NOTE]  
>  Questa opzione è disponibile solo se è stata selezionata l'opzione **Salva pacchetto SSIS** .  
  
 **File system**  
 Selezionare questa opzione per salvare il pacchetto come file con estensione dtsx.  
  
> [!NOTE]  
>  Questa opzione è disponibile solo se è stata selezionata l'opzione **Salva pacchetto SSIS** .  
  
 **Livello di protezione pacchetto**  
 Selezionare un livello di protezione dall'elenco.  
  
 Il livello di protezione determina il metodo di protezione, la password o chiave utente e l'ambito di protezione del pacchetto. La protezione può includere tutti i dati o solo i dati sensibili. Per informazioni sui requisiti e le opzioni per la sicurezza dei pacchetti, vedere [Access Control for sensitive data in Packages](../security/access-control-for-sensitive-data-in-packages.md) and [security Overview &#40;Integration Services&#41;](../security/security-overview-integration-services.md).  
  
> [!NOTE]  
>  Questa opzione è disponibile solo se è stata selezionata l'opzione **Salva pacchetto SSIS** .  
  
 **Password**  
 Digitare una password.  
  
> [!NOTE]  
>  Questa opzione è disponibile solo se è stata impostata l'opzione **livello di protezione pacchetto** per **crittografare i dati sensibili con una password** o **crittografare tutti i dati con una password**.  
  
 **Conferma password**  
 Digitare di nuovo la password.  
  
> [!NOTE]  
>  Questa opzione è disponibile solo se è stata impostata l'opzione **livello di protezione pacchetto** per **crittografare i dati sensibili con una password** o **crittografare tutti i dati con una password**.  
  
## <a name="see-also"></a>Vedi anche  
 [Esecuzione di progetti e pacchetti](../packages/run-integration-services-ssis-packages.md)   
 [Salvataggio di pacchetti](../save-packages.md)  
  
  
