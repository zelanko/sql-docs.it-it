---
title: Crea database (Importazione/Esportazione guidata SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.createdatabase.f1
ms.assetid: 56a8a79f-086c-4bdc-8888-0045bb4b0cbf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a80526b0f4a1b9f122ff79bbbb5a5a8ac08a2d07
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62893107"
---
# <a name="create-database-sql-server-import-and-export-wizard"></a>Crea database (Importazione/Esportazione guidata SQL Server)
  Utilizzare la pagina **Crea database** per definire un nuovo database per un file di destinazione.  
  
 Nella pagina è incluso un subset delle opzioni disponibili per la creazione di un nuovo database. Per visualizzare tutte le opzioni, usare [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Per ulteriori informazioni su questa procedura guidata, vedere [SQL Server importazione/esportazione guidata](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Per informazioni sulle opzioni per avviare la procedura guidata e sulle autorizzazioni necessarie per eseguire la procedura guidata, vedere [eseguire l'importazione/esportazione guidata SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 Lo scopo di Importazione/Esportazione guidata SQL Server è la copia di dati da un'origine a una destinazione. La procedura guidata può inoltre creare automaticamente un database di destinazione e le tabelle di destinazione. Se tuttavia è necessario copiare più database o tabelle, o altri tipi di oggetti di database, è preferibile utilizzare Copia guidata database. Per altre informazioni, vedere [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opzioni  
 **Nome**  
 Consente di specificare un nome univoco per il database di SQL Server di destinazione. Accertarsi di rispettare le convenzioni di denominazione dei database di SQL Server.  
  
 **Nome file di dati**  
 Consente di visualizzare il nome del file di dati. Tale nome è tratto dal nome del database specificato precedentemente.  
  
 **Nome file di log**  
 Consente di visualizzare il nome del file di log. Tale nome è tratto dal nome del database specificato precedentemente.  
  
 **Dimensioni iniziali (file di dati)**  
 Consente di specificare il numero di megabyte per le dimensioni iniziali del file di dati.  
  
 **Aumento dimensioni non consentito (file di dati)**  
 Consente di indicare se le dimensioni del file di dati possono eccedere le dimensioni iniziali specificate.  
  
 **Aumento dimensioni in percentuale (file di dati)**  
 Consente di specificare che le dimensioni del file di dati possono aumentare in base a un valore percentuale.  
  
 **Aumento dimensioni (file di dati)**  
 Consente di specificare che le dimensioni del file di dati possono aumentare in base a un numero di megabyte.  
  
 **Dimensioni iniziali (file di log)**  
 Consente di specificare il numero di megabyte per le dimensioni iniziali del file di log.  
  
 **Aumento dimensioni non consentito (file di log)**  
 Consente di indicare se le dimensioni del file di log possono eccedere le dimensioni iniziali specificate.  
  
 **Aumento dimensioni in percentuale (file di log)**  
 Consente di specificare che le dimensioni del file di log possono aumentare in base a un valore percentuale.  
  
 **Aumento dimensioni (file di log)**  
 Consente di specificare che le dimensioni del file di log possono aumentare in base a un numero di megabyte.  
  
  
