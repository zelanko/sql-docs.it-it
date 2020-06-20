---
title: Abilitare un database per la replica (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server replication]
ms.assetid: 8092faa3-9cff-4f81-926c-6a0070d1ce2c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 307d52e24187e35c1c30f609facd13bfad569216
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85010741"
---
# <a name="enable-a-database-for-replication-sql-server-management-studio"></a>Abilitazione di un database per la replica (SQL Server Management Studio)
  Un database viene implicitamente abilitato per la replica quando un membro del ruolo predefinito del server **sysadmin** crea una pubblicazione mediante la Creazione guidata nuova pubblicazione. Il membro del ruolo predefinito del server **sysadmin** può inoltre abilitare esplicitamente un database per la replica, in modo che un membro del ruolo predefinito del database **db_owner** possa creare una o più pubblicazioni in tale database. Per abilitare un database in modo esplicito, utilizzare la pagina **database di pubblicazione** della finestra di dialogo **Proprietà server \<Publisher> ** di pubblicazione-. Per ulteriori informazioni sull'accesso a questa finestra di dialogo, vedere [Create a Publication](publish/create-a-publication.md).  
  
### <a name="to-enable-a-database-for-replication"></a>Per abilitare un database per la replica  
  
1.  Nella pagina **database di pubblicazione** della finestra di dialogo **proprietà \<Publisher> server** di pubblicazione-selezionare la casella di controllo **transazionale** e/o **merge** per ogni database che si desidera replicare. Selezionare **Transazionale** per abilitare il database per la replica snapshot.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  
