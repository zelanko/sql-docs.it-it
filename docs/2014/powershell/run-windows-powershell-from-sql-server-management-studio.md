---
title: Eseguire Windows PowerShell da SQL Server Management Studio| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: 1f841825-da1f-4062-9a81-3cdbab03845b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c6d71f1158ef73b84e5b04dcc9a1970bfd7dce35
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "72783099"
---
# <a name="run-windows-powershell-from-sql-server-management-studio"></a>Esecuzione di Windows PowerShell da SQL Server Management Studio
  È possibile avviare sessioni di Windows PowerShell da **Esplora oggetti** in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]avvia Windows PowerShell, carica il `sqlps` modulo e imposta il contesto del percorso sul nodo associato nell'albero **Esplora oggetti** .  
  
## <a name="before-you-begin"></a>Prima di iniziare  
 Quando si specifica l'esecuzione di PowerShell per un oggetto in **Esplora oggetti**, [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] inizia una sessione di Windows PowerShell in cui sono stati caricati e registrati gli snap-in PowerShell di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Il percorso della sessione è preimpostato sulla posizione dell'oggetto su cui si è fatto clic con il pulsante destro del mouse in Esplora oggetti. Ad esempio, facendo clic con il pulsante destro del mouse sull'oggetto del database [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] in Esplora oggetti e selezionando **Avvia PowerShell**, il percorso di PowerShell viene impostato come segue:  
  
```
SQLSERVER:\SQL\MyComputer\MyInstance\Databases\AdventureWorks2012>  
```  
  
## <a name="to-run-powershell-from-sql-server-management-studio"></a>Per eseguire PowerShell da SQL Server Management Studio 
  
1.  Aprire **Esplora oggetti**.  
  
2.  Passare al nodo corrispondente all'oggetto desiderato.  
  
3.  Fare clic con il pulsante destro del mouse sull'oggetto e selezionare **Avvia PowerShell**.  
  
## <a name="permissions"></a>Autorizzazioni  
 In caso di apertura da [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], PowerShell non viene eseguito con privilegi di amministratore che possono impedire alcune attività quali chiamate a WMI.  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server PowerShell](sql-server-powershell.md)  
