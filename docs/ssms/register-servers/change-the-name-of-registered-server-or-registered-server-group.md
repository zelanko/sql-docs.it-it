---
title: Modificare il nome di un server registrato o di un gruppo di server registrati | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- modifying registered server or server group names
- server groups [SQL Server]
- Registered Servers [SQL Server], names
- renaming registered server or server group
- names [SQL Server], registered server or server group
ms.assetid: 10e1546b-9edb-400c-8676-2ea1192d6134
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 4a14982913cad38b290c2c63a86e373e26ef664c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65104343"
---
# <a name="change-the-name-of-registered-server-or-registered-server-group"></a>Modificare il nome di un server registrato o di un gruppo di server registrati
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  In questo argomento viene descritto come modificare il nome di un server registrato o un gruppo di server registrati in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. È possibile modificare il nome in qualunque momento. La modifica del nome di un server nella finestra Server registrati consente solo di modificare il nome visualizzato. Per connettersi a un server diverso, è necessario modificare le proprietà di connessione del server registrato.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
Dal menu passare a **Visualizza\\server registrati** per aprire il riquadro **Server registrati**.  
#### <a name="to-change-the-name-of-a-server"></a>Per modificare il nome di un server  
  
1.  In **Server registrati**espandere **Motore di database** , quindi **Gruppi di server locali**.  

2.  Fare clic con il pulsante destro del mouse su un server e selezionare **Proprietà** per aprire la finestra di dialogo **Modifica proprietà registrazione server** .
  
3.  Nella casella di testo **Nome server registrato** immettere il nuovo nome per la registrazione del server e quindi fare clic su **Salva**.  
  
#### <a name="to-change-the-name-of-a-server-group"></a>Per modificare il nome di un gruppo di server  
  
1.  In **Server registrati**espandere **Motore di database** , quindi **Gruppi di server locali**.  

2.  Fare clic con il pulsante destro del mouse su un gruppo di server e selezionare **Proprietà** per aprire la finestra di dialogo **Modifica proprietà gruppo di server** . 
  
3.  Nella casella di testo **Nome gruppo** immettere il nuovo nome per il gruppo di server e quindi fare clic su **Salva**.  
  
## <a name="see-also"></a>Vedere anche  
 [Modifica della registrazione di un server &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/change-a-server-s-registration-sql-server-management-studio.md)  
  
  
