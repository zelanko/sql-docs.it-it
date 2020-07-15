---
title: Installare la replica di SQL Server | Microsoft Docs
description: Installare i componenti di replica tramite l'installazione guidata di SQL Server o in una finestra del prompt dei comandi.
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- components [SQL Server replication]
- command line installations [SQL Server replication]
- installing replication
- replication [SQL Server], installing
- command prompt [SQL Server replication]
ms.assetid: c50ad078-060b-4a8d-ad45-9e31a8d85729
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: e5635065e77921b661d5b60e5ebcd0aad850295b
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85883487"
---
# <a name="install-sql-server-replication"></a>Installare la replica di SQL Server

[!INCLUDE [SQL Server -Windows Only](../../includes/applies-to-version/sql-windows-only.md)]

I componenti della replica possono essere installati mediante l'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o dal prompt dei comandi. L'installazione della replica può essere eseguita durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]oppure durante la modifica di un'istanza esistente.  
  
Dopo aver installato i componenti della replica, è necessario configurare il server per poter utilizzare la replica. Per altre informazioni, vedere [Configura distribuzione](../../relational-databases/replication/configure-distribution.md) nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
>[!IMPORTANT]  
>Se si installano componenti di replica quando si modifica un'istanza esistente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario arrestare e riavviare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent al termine dell'installazione, per fare in modo che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent riconosca i sottosistemi dell'agente di replica e sia in grado di chiamare gli agenti di replica dai passaggi di processo.  
  
## <a name="installing-replication-by-using-setup"></a>Installazione della replica mediante il programma di installazione  
**Per installare la replica durante l'installazione di una nuova istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
  
- Per installare i componenti della replica, inclusi gli oggetti RMO (Replication Management Objects), selezionare **Replica di SQL Server** nella pagina **Selezione funzionalità** dell'Installazione guidata.  
  
## <a name="installing-replication-from-the-command-prompt"></a>Installazione della replica dal prompt dei comandi  
 **Per installare la replica durante l'installazione di una nuova istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
  
- Vedere [Installare SQL Server dal prompt dei comandi](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Installare SQL Server](../../database-engine/install-windows/install-sql-server.md)   
 [Installare SQL Server dal prompt dei comandi](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [Funzionalità supportate dalle edizioni di SQL Server](../../sql-server/editions-and-components-of-sql-server-2017.md)  
  
  
