---
title: Installazione di SQL Server Migration Assistant per Access (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- installing SSMA
- instructions, installation
- instructions, upgrade
- licensing SSMA
- prerequisites for installing SSMA
- procedure, installation
- procedure, licensing
- procedure, upgrading
- removing SSMA
- Setup
- uninstalling SSMA
- upgrading SSMA
ms.assetid: dd50eebd-75df-4e0d-8c4d-88b511aae4c7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 128c83e0fd63b2724311aec046bdb9683c569a03
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62740944"
---
# <a name="installing-sql-server-migration-assistant-for-access-accesstosql"></a>Installazione di SQL Server Migration Assistant per Access (AccessToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) per l'accesso viene installato usando una procedura guidata basata su Windows Installer. Questo argomento vengono fornite informazioni sui prerequisiti di installazione, un collegamento alla versione più recente di SSMA e istruzioni per l'installazione, gestione delle licenze, la disinstallazione e l'aggiornamento di SSMA.  
  
## <a name="prerequisites"></a>Prerequisiti  
Prima di installare SSMA, assicurarsi che il sistema soddisfi i requisiti seguenti:  
  
-   Windows 7 o versione successiva, o Windows Server 2008 o versione successiva.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 o versione successiva.  
  
-   Il [!INCLUDE[msCoName](../../includes/msconame_md.md)] .NET Framework versione 4.0 o versione successiva. È disponibile in .NET Framework versione 4.0 il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disco del prodotto e con le informazioni nel [Guida di Microsoft .NET](https://docs.microsoft.com/dotnet/framework/).
  
-   Accesso a e autorizzazioni sufficienti nel computer che ospita l'istanza di destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DB di SQL Azure a cui si eseguirà la migrazione dei dati e oggetti di database.  
  
-   Microsoft oggetto DAO (Data Access) versione del provider 12.0 o 14.0. È possibile installare il provider DAO dal prodotto Microsoft Office 2010 o 2007 o scaricarlo dal sito web Microsoft.  
  
-   SQL Server Native Access Client (SNAC) versione 10.5 e versioni successive per la migrazione a SQL Azure. È possibile ottenere la versione più recente di SNAC da [Microsoft® SQL Server® 2008 R2 Feature Pack](https://go.microsoft.com/fwlink/?LinkId=196940)  
  
-   4 GB di RAM (consigliato).  
  
## <a name="installing-ssma"></a>Installazione di SSMA  
SSMA è un download Web. Per scaricare la versione più recente, vedere la [pagina di download di SQL Server Migration Assistant](https://aka.ms/ssmaforaccess).  
  
Dopo aver scaricato la versione più recente, è necessario estrarre i file di installazione prima di poter installare SSMA.

> [!IMPORTANT]  
> -   Prima di installare la nuova versione, disinstallare tutte le versioni precedenti di SSMA per Access.  
  
**Installare SSMA**  
  
1.  Fare doppio clic su SSMA for Access *n*file con estensione msi, dove *n* è il numero di build.  
  
2.  Nella pagina di benvenuto, fare clic su **successivo**.  
  
    Se non hai installati i prerequisiti, viene visualizzato un messaggio che indica che è necessario innanzitutto installare i componenti necessari. Assicurarsi che si sono installati tutti i prerequisiti e quindi eseguire nuovamente il programma di installazione.  
  
3.  Leggere il contratto di licenza dell'utente finale. Se si accetta, selezionare **accetto il contratto**, quindi fare clic su **successivo**.  
  
4.  Nella pagina Selezione tipo di installazione, fare clic su **tipica**.  
  
5.  Fare clic su **Installa**.  
  
Il percorso di installazione predefinito è C:\Program Files\Microsoft SQL Server Migration Assistant per Access.  
  
## <a name="uninstalling-ssma-for-access"></a>Disinstallazione di SSMA per Access  
Disinstallare con SSMA **Aggiungi / Rimuovi programmi** nel Pannello di controllo. Tenere presente che il programma di disinstallazione non elimina i file di progetto SSMA né i file di log.  
  
**Per disinstallare SSMA**  
  
1.  Fare clic su **avviare**, fare clic su **Pannello di controllo**, quindi fare clic su **Aggiungi / Rimuovi programmi**.  
  
2.  Selezionare **Microsoft SQL Server Migration Assistant per Access**, quindi fare clic su **rimuovere**.  
  
## <a name="upgrading-to-a-later-version"></a>L'aggiornamento a una versione successiva  
Se si desidera eseguire l'aggiornamento a una versione successiva di SSMA per Access, è necessario innanzitutto disinstallare SSMA per Access e quindi installare la versione più recente. Seguire le istruzioni nella disinstallazione di SSMA per la sezione accesso per completare questo processo.  
  
Se si apre un progetto creato in una versione precedente di SSMA per Access, SSMA chiede se si vuole convertire il progetto alla versione più recente. Fare clic su **Sì** per lavorare con il progetto alla versione più recente di SSMA.  
  
## <a name="see-also"></a>Vedere anche  
[Preparazione dei database di Access per la migrazione](preparing-access-databases-for-migration-accesstosql.md)  
[Migrazione dei database di Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Collegamento delle applicazioni di accesso a SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)  
  
