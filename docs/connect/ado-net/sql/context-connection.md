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
ms.openlocfilehash: 40f2c13ddbcdde10b1b406cf23f182e428704242
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75247844"
---
# <a name="the-context-connection"></a>Connessione di contesto

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Il problema dell'accesso ai dati interni rappresenta uno scenario comune. Si tratta della situazione in cui si desidera accedere allo stesso server su cui viene eseguita la funzione o la stored procedure CLR (Common Language Runtime). Una delle possibilità consiste nel creare una connessione utilizzando <xref:Microsoft.Data.SqlClient.SqlConnection>, specificare una stringa di connessione che punta al server locale e aprire la connessione. Questa procedura richiede la specifica di credenziali per l'accesso. La connessione si trova in una sessione di database diversa dalla funzione o dalla stored procedure, può presentare opzioni `SET` diverse, si trova in una transazione separata, non vede le tabelle temporanee e così via. Se il codice di funzione o la stored procedure gestita sono in esecuzione nel processo di SQL Server, è perché qualcuno si è collegato a quel server e ha eseguito un'istruzione SQL per richiamarli. È probabile che si voglia eseguire la stored procedure o la funzione nel contesto di quella connessione, insieme alla rispettiva transazione, alle opzioni `SET` e così via. In questo caso si parla di connessione di contesto.  
  
La connessione di contesto consente di eseguire istruzioni Transact-SQL nello stesso contesto nel quale è stato richiamato il codice. Per informazioni più dettagliate, vedere [Connessione di contesto](https://go.microsoft.com/fwlink/?LinkId=115395) nella documentazione online di SQL Server.
