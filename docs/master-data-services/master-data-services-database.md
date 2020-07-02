---
title: Database Master Data Services
description: Il database Master Data Services contiene tutte le informazioni per il sistema di Master Data Services ed è fondamentale per una distribuzione di Master Data Services.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- database [Master Data Services], about the database
- database [Master Data Services]
ms.assetid: 5f590cc1-6ec2-4b8c-a598-03de0f6051a0
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 2c7e24a7d519d787882ec587fc33f624f1eb6472
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85811486"
---
# <a name="master-data-services-database"></a>Database Master Data Services

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  Nel database sono contenute tutte le informazioni per il sistema [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . È l'elemento centrale di una distribuzione di [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Il database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] :  
  
-   Archivia le impostazioni, gli oggetti di database e i dati necessari per il sistema [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
-   Contiene le tabelle di staging utilizzate per elaborare i dati provenienti dai sistemi di origine.  
  
-   Fornisce oggetti dello schema e di database per l'archiviazione dei dati master provenienti dai sistemi di origine.  
  
-   Supporta le funzionalità di controllo delle versioni, incluse la convalida delle regole business e le notifiche tramite posta elettronica.  
  
-   Fornisce le viste per i sistemi di sottoscrizione per il quali è necessario il recupero di dati dal database.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Tabella di gestione temporanea dei membri foglia &#40;Master Data Services&#41;](../master-data-services/leaf-member-staging-table-master-data-services.md)  
  
-   [Tabella di gestione temporanea di membri consolidati &#40;Master Data Services&#41;](../master-data-services/consolidated-member-staging-table-master-data-services.md)  
  
-   [Tabella di gestione temporanea delle relazioni &#40;Master Data Services&#41;](../master-data-services/relationship-staging-table-master-data-services.md)  
  
-   [Errori del processo di gestione temporanea &#40;Master Data Services&#41;](../master-data-services/staging-process-errors-master-data-services.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un database di Master Data Services](../master-data-services/install-windows/create-a-master-data-services-database.md)   
 [&#40;di sicurezza degli oggetti di database Master Data Services&#41;](../master-data-services/database-object-security-master-data-services.md)   
 [Account di accesso, utenti e ruoli di database &#40;Master Data Services&#41;](../master-data-services/database-logins-users-and-roles-master-data-services.md)  
  
  
