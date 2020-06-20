---
title: Creare le credenziali - Eseguire l'autenticazione nel servizio di archiviazione Azure | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.backuptourl.createcred.f1
ms.assetid: 0622619d-27c5-4ff0-83e5-cde31648c27a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 5f76a455637e28c06e967b0609cea19a874d7967
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84958591"
---
# <a name="create-credential---authenticate-to-azure-storage"></a>Creare le credenziali - Eseguire l'autenticazione nel servizio di archiviazione Azure
  Usare la finestra di dialogo **Backup su URL - Creazione credenziali** per creare nuove credenziali SQL.  
  
 Quando si usa questa finestra di dialogo per creare le credenziali, è necessario specificare un certificato di gestione di Azure aggiunto all'archivio certificati locale o un profilo di pubblicazione scaricato nel computer per convalidare la sottoscrizione e le informazioni sull'account di archiviazione.  
  
 **Credenziali SQL**  
 Specificare il nome delle credenziali SQL che si desidera creare.  
  
## <a name="azure-credentials"></a>Credenziali Azure  
 **Certificato di gestione**  
 Usare questa opzione per specificare un certificato dall'archivio certificati locale corrispondente al certificato di gestione di Azure. Per altre informazioni sul certificato di gestione di Azure, vedere [Creare e caricare un certificato di gestione per Azure](https://go.microsoft.com/fwlink/?LinkId=320781).  
  
 **Sottoscrizione**  
 Selezionare, digitare o incollare l'ID sottoscrizione di Azure corrispondente al certificato di gestione dall'archivio certificati locale.  
  
 **Profilo di pubblicazione**  
 Utilizzare questa opzione se si dispone di un profilo di pubblicazione scaricato nel computer. Se si utilizza questa opzione, l'ID sottoscrizione e il certificato vengono inseriti automaticamente.  
  
> [!CAUTION]  
>  SQL Server supporta attualmente la versione del profilo di pubblicazione 2.0. Per scaricare la versione supportata del profilo di pubblicazione, vedere [Download del profilo di pubblicazione 2.0](https://go.microsoft.com/fwlink/?LinkId=396421).  
  
## <a name="storage-account"></a>Account di archiviazione  
 Selezionare l'account di archiviazione da utilizzare per archiviare i file di backup.  
  
  
