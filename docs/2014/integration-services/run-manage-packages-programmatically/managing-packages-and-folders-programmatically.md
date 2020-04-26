---
title: Gestione di pacchetti e cartelle a livello di programmazione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- enumerators [Integration Services]
- packages [Integration Services], managing
- custom enumerators [Integration Services]
ms.assetid: ec59b75d-ba09-44ac-9039-9d593bb462d9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a6ede05e340cbd2822cd72ceee514f6ce31a2755
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/25/2020
ms.locfileid: "62766853"
---
# <a name="managing-packages-and-folders-programmatically"></a>Gestione di pacchetti e cartelle a livello di programmazione
  Quando si utilizzano i pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a livello di programmazione, può essere necessario determinare se un singolo pacchetto o cartella esiste oppure gestire le cartelle in cui i pacchetti sono archiviati. La classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> dello spazio dei nomi <xref:Microsoft.SqlServer.Dts.Runtime> fornisce un'ampia varietà di metodi e classi per soddisfare questi requisiti.  
  
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
  

  
##  <a name="managing-packages-and-folders"></a><a name="managing"></a> Gestione di pacchetti e cartelle  
 La classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> dello spazio dei nomi <xref:Microsoft.SqlServer.Dts.Runtime> fornisce metodi aggiuntivi per la gestione dei pacchetti e delle cartelle in cui sono archiviati.  
  
###  <a name="removing-a-package"></a><a name="managing_rempkg"></a> Rimozione di un pacchetto  
 Per rimuovere un pacchetto salvato a livello di programmazione, chiamare uno dei metodi seguenti:  
  
|Posizione di archiviazione|Metodo da chiamare|  
|----------------------|--------------------|  
|Archivio pacchetti SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromSqlServer%2A>|  
  

  
###  <a name="creating-a-folder"></a><a name="managing_create"></a> Creazione di una cartella  
 Per creare una cartella di archiviazione a livello di programmazione, chiamare uno dei metodi seguenti:  
  
|Posizione di archiviazione|Metodo da chiamare|  
|----------------------|--------------------|  
|Archivio pacchetti SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnSqlServer%2A>|  
  

  
###  <a name="removing-a-folder"></a><a name="managing_remfldr"></a> Rimozione di una cartella  
 Per rimuovere una cartella di archiviazione a livello di programmazione, chiamare uno dei metodi seguenti:  
  
|Posizione di archiviazione|Metodo da chiamare|  
|----------------------|--------------------|  
|Archivio pacchetti SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromSqlServer%2A>|  
  
  
  
###  <a name="renaming-a-folder"></a><a name="managing_rename"></a> Ridenominazione di una cartella  
 Per rinominare una cartella di archiviazione a livello di programmazione, chiamare uno dei metodi seguenti:  
  
|Posizione di archiviazione|Metodo da chiamare|  
|----------------------|--------------------|  
|Archivio pacchetti SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnSqlServer%2A>|  
  

  
![Integration Services icona (piccola)](../media/dts-16.gif "Icona di Integration Services (piccola)")  **rimane aggiornata con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visitare la pagina relativa a Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
## <a name="see-also"></a>Vedi anche  
 [Gestione pacchetti &#40;servizio SSIS&#41;](../service/package-management-ssis-service.md)   
 [Enumerazione dei pacchetti disponibili a livello di codice](../run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)  
  
  
