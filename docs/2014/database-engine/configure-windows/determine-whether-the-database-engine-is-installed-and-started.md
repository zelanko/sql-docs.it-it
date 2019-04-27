---
title: Verificare l'installazione e l'avvio del motore di database | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server, determining if installed
- verifying Database Engine installation
- viewing Database Engine installation
- installed Database Engine verification [SQL Server]
ms.assetid: babb02e4-3521-4b75-b5df-e09205594375
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: bed1ec3eeb3dffe1ff1174d83050cd2e09af4caf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62782634"
---
# <a name="determine-whether-the-database-engine-is-installed-and-started"></a>Verificare l'installazione e l'avvio del Motore di database
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Un'installazione corretta del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] installa i file nel file system, crea voci nel Registro di sistema e installa numerosi strumenti. In questo argomento viene descritto come determinare se il [!INCLUDE[ssDE](../../includes/ssde-md.md)] viene installato e avviato in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
##  <a name="SSMSProcedure"></a> Utilizzo di Gestione configurazione SQL Server  
  
#### <a name="how-to-view-and-start-the-database-engine-by-using-sql-server-configuration-manager"></a>Visualizzazione e avvio di Motore di database utilizzando Gestione configurazione SQL Server  
  
1.  Fare clic su **Start**, scegliere **Tutti i programmi**, **Microsoft SQL Server**, **Strumenti di configurazione**, quindi **Gestione configurazione SQL Server**.  
  
     Se nel menu **Start** non sono presenti gli elementi indicati, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è installato correttamente. Eseguire il programma di installazione per installare [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
2.  Nel riquadro sinistro di **Gestione configurazione SQL Server**fare clic su **Servizi di SQL Server**. Nel riquadro destro sono elencati numerosi servizi correlati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se [!INCLUDE[ssDE](../../includes/ssde-md.md)] è installato, il servizio [!INCLUDE[ssDE](../../includes/ssde-md.md)] viene elencato come **SQL Server (MSSQLSERVER)** se si tratta dell'istanza predefinita, oppure come **SQL Server (**\<*nome_istanza*>**),** se [!INCLUDE[ssDE](../../includes/ssde-md.md)] è installato come istanza denominata. Salvo il caso in cui il nome dell'istanza sia stato modificato, [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] viene installato come istanza denominata con il nome **SQLEXPRESS**. Un'icona a forma di triangolo di colore verde indica che [!INCLUDE[ssDE](../../includes/ssde-md.md)] è in esecuzione. Un'icona a forma di quadrato di colore rosso indica che [!INCLUDE[ssDE](../../includes/ssde-md.md)] è stato arrestato.  
  
3.  Per avviare [!INCLUDE[ssDE](../../includes/ssde-md.md)], fare clic con il pulsante destro del mouse su [!INCLUDE[ssDE](../../includes/ssde-md.md)]nel riquadro destro e quindi scegliere **Avvia**.  
  
> [!NOTE]  
>  Durante l'installazione, l'utente può selezionare un percorso in cui installare i file di programma e di database. Se l'utente accetta la posizione predefinita, i file vengono installati in [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)] e in C:\Programmi\Microsoft SQL Server\MSSQL.*x*, dove *x* è un numero.  
  
  
