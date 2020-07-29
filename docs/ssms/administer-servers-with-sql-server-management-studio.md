---
title: Amministrazione di server con SQL Server Management Studio
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], servers
- servers [SQL Server], administering
ms.assetid: 938bb035-e07a-4082-9f93-229d9feb6b06
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 96119c90c8a187830fd5a2264e833bb326593a29
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "86010915"
---
# <a name="administer-servers-with-sql-server-management-studio"></a>Amministrazione di server con SQL Server Management Studio
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
[!INCLUDE[msCoName](../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] è un client di amministrazione completo e integrato progettato per soddisfare i requisiti di gestione del server dell'amministratore del database SQL di Azure e [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. In [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]le attività di amministrazione vengono eseguite utilizzando Esplora oggetti, che consente di connettersi a qualsiasi server del gruppo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e di visualizzarne graficamente il contenuto. Un server può essere un'istanza del [!INCLUDE[ssDE](../includes/ssde_md.md)], [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] o di database SQL di Azure.  
  
I componenti di [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] includono Server registrati, Esplora oggetti, Esplora soluzioni, Esplora modelli, la pagina Dettagli Esplora oggetti e la finestra del documento. Per visualizzare uno strumento, scegliere il nome desiderato dal menu **Visualizza** . Per visualizzare lo strumento Editor di query, fare clic sul pulsante **Nuova query** sulla barra degli strumenti.  
  
> [!IMPORTANT]  
> Per impostazione predefinita, il traffico di rete tra [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] e [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] non è crittografato. In [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] lavorare con dati sensibili (comprese le password) solo dopo aver stabilito una connessione crittografata. Per altre informazioni, vedere [Procedura: Abilitazione di connessioni crittografate al Motore di database (Gestione configurazione SQL Server)](https://msdn.microsoft.com/e1e55519-97ec-4404-81ef-881da3b42006).  
  
Utilizzare [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] per:  
  
-   Registrare server.  
  
-   Connettersi a un'istanza del [!INCLUDE[ssDE](../includes/ssde_md.md)], SSAS, [!INCLUDE[ssRS](../includes/ssrs.md)],  [!INCLUDE[ssIS](../includes/ssis_md.md)] o di database SQL di Azure.  
  
-   Configurare le proprietà del server.  
  
-   Gestire database e oggetti SASS come ad esempio cubi, dimensioni e assembly.  
  
-   Creare oggetti come ad esempio database, tabelle, cubi, utenti di database e account di accesso.  
  
-   Gestire file e filegroup.  
  
-   Collegare o scollegare database.  
  
-   Avviare strumenti di scripting.  
  
-   Gestire la sicurezza.  
  
-   Visualizzare registri di sistema.  
  
-   Monitorare l'attività corrente.  
  
-   Configurare la replica.  
  
-   Gestire indici full-text.  
  
Per avviare e arrestare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent, utilizzare Gestione configurazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Vedere anche  
[Utilizzo di SQL Server Management Studio](../ssms/use-sql-server-management-studio.md)  
[Procedura: Visualizzazione o modifica delle proprietà del server (SQL Server Management Studio)](https://msdn.microsoft.com/55f3ac04-5626-4ad2-96bd-a1f1b079659d)  
  
