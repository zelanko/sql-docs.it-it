---
title: Sviluppo di database orientato ai progetti utilizzando gli strumenti della riga di comando
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 9a26def9-8fbd-43e4-9e57-414840b73ed8
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 04/26/2017
ms.openlocfilehash: 321c0988603f7c31460d1c95791d57e5945c2b07
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "75243754"
---
# <a name="project-oriented-database-development-using-command-line-tools"></a>Sviluppo di database orientato ai progetti utilizzando gli strumenti della riga di comando

SQL Server Data Tools offre strumenti della riga di comando che consentono numerosi scenari di sviluppo di database orientato ai progetti.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|||  
|-|-|  
|[SqlPackage.exe](../tools/sqlpackage.md)|In questo argomento viene descritta l'utilità SQLPackage.exe che consente di eseguire le attività seguenti:<br /><br />- Estrazione di un file con estensione dacpac da un database di SQL Server attivo.<br />- Pubblicazione di un file con estensione dacpac in un database di SQL Server attivo per aggiornare in modo incrementale lo schema del database attivo affinché corrisponda al file con estensione dacpac.<br />- Confronto di un file con estensione dacpac con un database di SQL Server attivo e generazione di uno script Transact\-SQL di aggiornamento incrementale senza l'aggiornamento del database attivo.<br />- Confronto di due file con estensione dacpac per la generazione di uno script Transact\-SQL di aggiornamento incrementale.<br />- Generazione di un report XML in cui vengono riepilogate le modifiche dell'aggiornamento incrementale che si verificherebbero in caso di aggiornamento incrementale del database.|  
|[Uso di MSDeploy con il provider dbSqlPackage](../ssdt/using-msdeploy-with-dbsqlpackage-provider.md)|Questo argomento descrive il provider dello [Strumento di distribuzione Web](https://go.microsoft.com/fwlink/?LinkId=231798) denominato dbSqlPackage incluso in SSDT, che interagisce con lo Strumento di distribuzione Web (MSDeploy.exe) di Microsoft Internet Information Services (IIS), usato per le attività seguenti:<br /><br />- Estrazione di un file con estensione dacpac da un database di SQL Azure o di SQL Server remoto o locale.<br />- Pubblicazione di un file con estensione dacpac in un database di SQL Azure o di SQL Server remoto o locale per il relativo aggiornamento incrementale.<br />- Pubblicazione da un database di SQL Server locale in un database di SQL Azure o di SQL Server remoto per l'aggiornamento  incrementale del database remoto.<br />- Confronto di un file con estensione dacpac con un database di SQL Azure o di SQL Server remoto o locale per generare uno script Transact\-SQL di aggiornamento incrementale senza l'aggiornamento del database attivo.<br />- Generazione di un report XML in cui vengono riepilogate le modifiche dell'aggiornamento incrementale che si verificherebbero in caso di aggiornamento incrementale del database.|  
  
## <a name="related-sections"></a>Sezioni correlate  
[Sviluppo di database offline orientato ai progetti](../ssdt/project-oriented-offline-database-development.md)  
  
