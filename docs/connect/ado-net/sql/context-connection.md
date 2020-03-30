---
title: Connessione di contesto
description: Viene descritta la connessione di contesto.
ms.date: 08/15/2019
ms.assetid: e443ca86-9243-4234-a822-ed10a53a9de0
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 6dd4260fa15b737ce6b1411056b82bac93f33fa6
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "78897015"
---
# <a name="the-context-connection"></a>Connessione di contesto

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Il problema dell'accesso ai dati interni rappresenta uno scenario comune. Si tratta della situazione in cui si desidera accedere allo stesso server su cui viene eseguita la funzione o la stored procedure CLR (Common Language Runtime). Una delle possibilità consiste nel creare una connessione utilizzando <xref:Microsoft.Data.SqlClient.SqlConnection>, specificare una stringa di connessione che punta al server locale e aprire la connessione. Questa procedura richiede la specifica di credenziali per l'accesso. La connessione si trova in una sessione di database diversa dalla funzione o dalla stored procedure, può presentare opzioni `SET` diverse, si trova in una transazione separata, non vede le tabelle temporanee e così via. Se il codice di funzione o la stored procedure gestita sono in esecuzione nel processo di SQL Server, è perché qualcuno si è collegato a quel server e ha eseguito un'istruzione SQL per richiamarli. È probabile che si voglia eseguire la stored procedure o la funzione nel contesto di quella connessione, insieme alla rispettiva transazione, alle opzioni `SET` e così via. In questo caso si parla di connessione di contesto.  
  
La connessione di contesto consente di eseguire istruzioni Transact-SQL nello stesso contesto nel quale è stato richiamato il codice. Per informazioni più dettagliate, vedere [Connessione di contesto](https://go.microsoft.com/fwlink/?LinkId=115395) nella documentazione online di SQL Server.
