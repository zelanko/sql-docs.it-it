---
title: Spostare un punto di controllo dell'utilità da un'istanza di SQL Server a un'altra (Utilità SQL Server) | Microsoft Docs
description: Informazioni su come usare SQL Server Management Studio per spostare un punto di controllo dell'utilità da un'istanza di SQL Server a un'altra.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: b402fd9e-0bea-4c38-a371-6ed7fea12e96
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4eef85ed3e12c5ba25d5ba778c83914dfb69c245
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85784073"
---
# <a name="move-a-ucp-from-one-instance-of-sql-server-to-another-sql-server-utility"></a>Spostare un punto di controllo dell'utilità da un'istanza di SQL Server a un'altra (Utilità SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  In questo argomento viene illustrato come spostare un punto di controllo dell'utilità da un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un'altra in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="move-a-ucp-from-one-instance-of-sql-server-to-another"></a>Spostare un punto di controllo dell'utilità da un'istanza di SQL Server a un'altra.  
  
1.  Creare un nuovo punto di controllo dell'utilità nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che sarà la nuova istanza host del punto di controllo dell'utilità. Per altre informazioni, vedere [Creare un punto di controllo dell'Utilità SQL Server &#40;Utilità SQL Server&#41;](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md).  
  
2.  Se sono state configurate impostazioni dei criteri non predefinite per un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , prendere nota delle soglie dei criteri in modo da poterli reimpostare sul nuovo punto di controllo dell'utilità. Quando al nuovo punto di controllo dell'utilità vengono aggiunte istanze, vengono applicati i criteri predefiniti. Se vengono applicati i criteri predefiniti, nella visualizzazione elenco di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verrà visualizzato il valore **Globale** nella colonna **Tipo criteri** .  
  
3.  Rimuovere tutte le istanze gestite dal vecchio punto di controllo dell'utilità. Per altre informazioni, vedere [Rimuovere un'istanza di SQL Server da Utilità SQL Server](../../relational-databases/manage/remove-an-instance-of-sql-server-from-the-sql-server-utility.md).  
  
4.  Eseguire il backup del data warehouse di gestione dell'utilità dal vecchio punto di controllo dell'utilità. Il nome del file è Sysutility_mdw_\<GUID>_DATA e il percorso predefinito del database è \<System drive>:\Programmi\Microsoft SQL Server\MSSQL10_50.<Nome_punto di controllo utilità>\MSSQL\Data\\, dove \<System drive> è in genere l'unità C:\. Per altre informazioni, vedere [Copiare database tramite backup e ripristino](../../relational-databases/databases/copy-databases-with-backup-and-restore.md).  
  
5.  Ripristinare il backup del data warehouse di gestione dell'utilità nel nuovo punto di controllo dell'utilità. Per altre informazioni, vedere [Copiare database tramite backup e ripristino](../../relational-databases/databases/copy-databases-with-backup-and-restore.md).  
  
6.  Registrare le istanze nel nuovo punto di controllo dell'utilità per consentirne la gestione da parte di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [Registrare un'istanza di SQL Server &#40;Utilità SQL Server&#41;](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md).  
  
7.  Implementare le definizioni dei criteri personalizzati per le istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se necessario.  
  
8.  Attendere circa 1 ora per il completamento delle operazioni di raccolta e di aggregazione dei dati.  
  
9. Per aggiornare i dati, fare clic con il pulsante destro del mouse sul nodo **Istanze gestite** in **Esplora utilità**e scegliere **Aggiorna**. I dati della visualizzazione elenco vengono visualizzati nel riquadro del contenuto di **Esplora utilità** . Per altre informazioni, vedere [View Resource Health Policy Results &#40;SQL Server Utility&#41;](../../relational-databases/manage/view-resource-health-policy-results-sql-server-utility.md) (Visualizzare i risultati dei criteri di integrità delle risorse - Utilità SQL Server).  
  
## <a name="see-also"></a>Vedere anche  
 [Attività e funzionalità di Utilità SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Registrare un'istanza di SQL Server &#40;Utilità SQL Server&#41;](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)  
  
  
