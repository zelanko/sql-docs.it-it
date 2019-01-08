---
title: Salvataggio ed esecuzione pacchetto (Server importazione / esportazione guidata SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.saveschedule.f1
ms.assetid: b582c462-3d7a-4a4c-a2a2-2c79fedab75a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fc075a50f3b57cf4856dbcd2ee36c13b83d968d4
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52773373"
---
# <a name="save-and-execute-package-sql-server-import-and-export-wizard"></a>Salvataggio ed esecuzione pacchetto (Importazione/Esportazione guidata SQL Server)
  Usare la **salvare ed eseguire il pacchetto** finestra di dialogo per eseguire il pacchetto immediatamente, salvare l'esecuzione in un secondo momento o entrambi.  
  
> [!NOTE]  
>  Se un pacchetto prima di esso viene arrestata al termine dell'esecuzione, il pacchetto non è salvato, anche se si seleziona il **salvare** casella di controllo.  
  
 Per altre informazioni su questa procedura guidata, vedere [SQL Server importazione / esportazione guidata](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Per altre informazioni sulle opzioni per avviare la procedura guidata, nonché le autorizzazioni necessarie per eseguire correttamente la procedura guidata, vedere [esecuzione di SQL Server importazione / esportazione guidata](start-the-sql-server-import-and-export-wizard.md).  
  
 Lo scopo di Importazione/Esportazione guidata SQL Server è la copia di dati da un'origine a una destinazione. La procedura guidata può inoltre creare automaticamente un database di destinazione e le tabelle di destinazione. Se tuttavia è necessario copiare più database o tabelle, o altri tipi di oggetti di database, è preferibile utilizzare Copia guidata database. Per altre informazioni, vedere [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opzioni  
 **Esegui immediatamente**  
 Selezionare questa opzione per eseguire il pacchetto immediatamente.  
  
 **Salva pacchetto SSIS**  
 Consente di salvare il pacchetto per eseguirlo in un momento successivo con l'opzione per l'esecuzione immediata.  
  
> [!NOTE]  
>  In [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] l'opzione per salvare il pacchetto creato con la procedura guidata non è disponibile.  
  
 **SQL Server**  
 Selezionare questa opzione per salvare il pacchetto per il [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `msdb` database.  
  
> [!NOTE]  
>  Questa opzione è disponibile solo se è stata selezionata la **Salva pacchetto SSIS** opzione.  
  
 **File system**  
 Selezionare questa opzione per salvare il pacchetto come file con estensione dtsx.  
  
> [!NOTE]  
>  Questa opzione è disponibile solo se è stata selezionata la **Salva pacchetto SSIS** opzione.  
  
 **Livello di protezione pacchetto**  
 Selezionare un livello di protezione dall'elenco.  
  
 Il livello di protezione determina il metodo di protezione, la password o chiave utente e l'ambito di protezione del pacchetto. La protezione può includere tutti i dati o solo i dati sensibili. Per comprendere i requisiti e opzioni per la sicurezza dei pacchetti, vedere [controllo di accesso per dati sensibili nei pacchetti](../security/access-control-for-sensitive-data-in-packages.md) e [Cenni preliminari sulla sicurezza &#40;Integration Services&#41;](../security/security-overview-integration-services.md).  
  
> [!NOTE]  
>  Questa opzione è disponibile solo se è stata selezionata la **Salva pacchetto SSIS** opzione.  
  
 **Password**  
 Digitare una password.  
  
> [!NOTE]  
>  Questa opzione è disponibile solo se è stato impostato il **livello di protezione pacchetto** possibilità di scegliere tra **crittografare dati sensibili con una password** oppure **Crittografa tutti i dati con una password**.  
  
 **Conferma password**  
 Digitare di nuovo la password.  
  
> [!NOTE]  
>  Questa opzione è disponibile solo se è stato impostato il **livello di protezione pacchetto** possibilità di scegliere tra **crittografare dati sensibili con una password** oppure **Crittografa tutti i dati con una password**.  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione di progetti e pacchetti](../packages/run-integration-services-ssis-packages.md)   
 [Salvare i pacchetti](../save-packages.md)  
  
  
