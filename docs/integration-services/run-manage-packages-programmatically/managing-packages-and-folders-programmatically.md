---
title: Gestione di pacchetti e cartelle a livello di programmazione | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- enumerators [Integration Services]
- packages [Integration Services], managing
- custom enumerators [Integration Services]
ms.assetid: ec59b75d-ba09-44ac-9039-9d593bb462d9
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5c45f6a5b59a65046a0e48fd930fd27d689c0a0a
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86913310"
---
# <a name="managing-packages-and-folders-programmatically"></a>Gestione di pacchetti e cartelle a livello di programmazione

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


<a name="top"></a> Quando si usano i pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a livello di programmazione, può essere necessario determinare se un singolo pacchetto o cartella esiste oppure gestire le cartelle in cui i pacchetti sono archiviati. La classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> dello spazio dei nomi <xref:Microsoft.SqlServer.Dts.Runtime> fornisce un'ampia varietà di metodi e classi per soddisfare questi requisiti.    
    
##  <a name="determining-whether-a-package-or-folder-exists"></a><a name="exists"></a> Verifica dell'esistenza di un pacchetto o di una cartella    
 Per determinare a livello di programmazione se un pacchetto salvato esiste, chiamare uno dei metodi seguenti prima di tentare di caricarlo ed eseguirlo:    
    
|Posizione di archiviazione|Metodo da chiamare|    
|----------------------|--------------------|    
|Archivio pacchetti SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.ExistsOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.ExistsOnSqlServer%2A>|    
    
 Per determinare a livello di programmazione se una cartella esiste, chiamare uno dei metodi seguenti prima di tentare di elencare i pacchetti archiviati al suo interno:    
    
|Posizione di archiviazione|Metodo da chiamare|    
|----------------------|--------------------|    
|Archivio pacchetti SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.FolderExistsOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.FolderExistsOnSqlServer%2A>|    
    
 [Torna all'inizio](#top)    
    
##  <a name="managing-packages-and-folders"></a><a name="managing"></a> Gestione di pacchetti e cartelle    
 La classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> dello spazio dei nomi <xref:Microsoft.SqlServer.Dts.Runtime> fornisce metodi aggiuntivi per la gestione dei pacchetti e delle cartelle in cui sono archiviati.    
    
###  <a name="removing-a-package"></a><a name="managing_rempkg"></a> Rimozione di un pacchetto    
 Per rimuovere un pacchetto salvato a livello di programmazione, chiamare uno dei metodi seguenti:    
    
|Posizione di archiviazione|Metodo da chiamare|    
|----------------------|--------------------|    
|Archivio pacchetti SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromSqlServer%2A>|    
    
 [Torna all'inizio](#top)    
    
###  <a name="creating-a-folder"></a><a name="managing_create"></a> Creazione di una cartella    
 Per creare una cartella di archiviazione a livello di programmazione, chiamare uno dei metodi seguenti:    
    
|Posizione di archiviazione|Metodo da chiamare|    
|----------------------|--------------------|    
|Archivio pacchetti SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnSqlServer%2A>|    
    
 [Torna all'inizio](#top)    
    
###  <a name="removing-a-folder"></a><a name="managing_remfldr"></a> Rimozione di una cartella    
 Per rimuovere una cartella di archiviazione a livello di programmazione, chiamare uno dei metodi seguenti:    
    
|Posizione di archiviazione|Metodo da chiamare|    
|----------------------|--------------------|    
|Archivio pacchetti SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromSqlServer%2A>|    
    
 [Torna all'inizio](#top)    
    
###  <a name="renaming-a-folder"></a><a name="managing_rename"></a> Ridenominazione di una cartella    
 Per rinominare una cartella di archiviazione a livello di programmazione, chiamare uno dei metodi seguenti:    
    
|Posizione di archiviazione|Metodo da chiamare|    
|----------------------|--------------------|    
|Archivio pacchetti SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnSqlServer%2A>|    
    
 [Torna all'inizio](#top)    
    
## <a name="see-also"></a>Vedere anche    
 [Gestione dei pacchetti &#40;servizio SSIS&#41;](../../integration-services/service/package-management-ssis-service.md)     
 [Enumerazione dei pacchetti disponibili a livello di programmazione](../../integration-services/run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)    
    
  
