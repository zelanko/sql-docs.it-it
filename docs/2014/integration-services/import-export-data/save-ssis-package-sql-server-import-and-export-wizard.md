---
title: Salvare il pacchetto SSIS (Importazione/Esportazione guidata SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.savedtspackage.f1
ms.assetid: 7bf8ac6a-5599-43ab-bf5c-e072c11b85a0
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 9f74d9089bf6c2a87edaeaee80c95757982f6c2a
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966211"
---
# <a name="save-ssis-package-sql-server-import-and-export-wizard"></a>Salva pacchetto SSIS (Importazione/Esportazione guidata SQL Server)
  Utilizzare la pagina **Salva pacchetto SSIS** per assegnare un nome, una descrizione e un salvataggio di un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pacchetto Integration Services ( [!INCLUDE[ssIS](../../includes/ssis-md.md)] ) nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `msdb` database o in un file con estensione dtsx.  
  
> [!NOTE]  
>  In [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] l'opzione per salvare il pacchetto creato con la procedura guidata non è disponibile.  
  
 Per ulteriori informazioni su questa procedura guidata, vedere [SQL Server importazione/esportazione guidata](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Per informazioni sulle opzioni per avviare la procedura guidata e sulle autorizzazioni necessarie per eseguire la procedura guidata, vedere [eseguire l'importazione/esportazione guidata SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 Lo scopo di Importazione/Esportazione guidata SQL Server è la copia di dati da un'origine a una destinazione. La procedura guidata può inoltre creare automaticamente un database di destinazione e le tabelle di destinazione. Se tuttavia è necessario copiare più database o tabelle, o altri tipi di oggetti di database, è preferibile utilizzare Copia guidata database. Per altre informazioni, vedere [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="static-options"></a>Opzioni statiche  
 **Nome**  
 Consente di specificare un nome univoco per il pacchetto.  
  
 **Descrizione**  
 Consente di specificare una descrizione per il pacchetto. È consigliabile includere nella descrizione informazioni sugli scopi del pacchetto, in modo da ottenere pacchetti autodocumentati più semplici da gestire.  
  
 **Destinazione**  
 Consente di visualizzare la destinazione ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o file) specificata in precedenza per il file di destinazione.  
  
## <a name="target-dynamic-options"></a>Opzioni dinamiche di Destinazione  
  
### <a name="target--sql-server"></a>Destinazione = SQL Server  
 **Nome server**  
 Se è stata selezionata una destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], digitare o selezionare il nome del server di destinazione.  
  
 **Usa autenticazione di Windows**  
 Se è stata selezionata una destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], specificare se connettersi al server utilizzando l'autenticazione integrata di Windows. Questo è il metodo di autenticazione ottimale.  
  
 **Usa autenticazione SQL Server**  
 Se è stata selezionata una destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], specificare se connettersi al server utilizzando l'autenticazione di SQL Server.  
  
 **Nome utente**  
 Se è stata selezionata una destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ed è stata specificata l'autenticazione di SQL Server, digitare il nome utente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Password**  
 Se è stata selezionata una destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ed è stata specificata l'autenticazione di SQL Server, digitare la password di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="target--file-system"></a>Destinazione = File System  
 **Nome file**  
 Quando è stata selezionata una destinazione file, digitare il percorso del file di destinazione oppure usare il pulsante **Sfoglia** .  
  
 **Sfoglia**  
 Quando è stata selezionata una destinazione file, passare al file di destinazione utilizzando la finestra di dialogo **Salva pacchetto** .  
  
## <a name="see-also"></a>Vedere anche  
 [Salvataggio di pacchetti](../save-packages.md)  
  
  
