---
title: LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: c178a308-8d99-47fc-8a49-5a480dc592f6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 94439a6981a2cf891a55bcbda7498db83e1fa52e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62990575"
---
# <a name="localdb_error_instance_folder_path_too_long"></a>LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|260|  
|Origine evento|Runtime database locale di SQL Server 12.0|  
|Componente|API di Runtime database locale|  
|Testo del messaggio|La lunghezza del percorso completo della cartella di istanze del database locale è superiore a MAX_PATH. L'istanza deve essere archiviata nella cartella:%% LOCALAPPDATA%% \ Microsoft\Microsoft SQL Server Local\\ DB\Instances<nome\>istanza.|  
  
## <a name="explanation"></a>Spiegazione  
 Percorso di archiviazione richiesto per l'istanza più lungo di MAX_PATH.  
  
## <a name="user-action"></a>Azione dell'utente  
 Creare un nuovo percorso più corto di MAX_PATH.  
  
  
